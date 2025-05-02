# Your Friendly Neighborhood Compiler

## _The compiler is your friend._

When writing code in Typescript it can often be the case that the compiler yells at you for what seems like no good reason. Consider the following:

```typescript
function getThing(): HTMLElement {
  const thing = document.querySelector("some thing");
  return thing; // <- err
}

function doSomethingWithThing(el: HTMLElement) {
  console.log(el.textContent.replace(/some regex/, "")); // <- err
}

try {
  doSomethingWithThing(getThing());
} catch (_e: unknown) {
  // don't care
}
```

We know the code can't fail at runtime, because if the element isn't found or doesn't have textContent the error will be caught. Right? The compiler is just being a useless bureaucratic jerk here right? Right? Since we definitely know better, lets just assert the fact to the compiler:

```typescript
function getThing(): HTMLElement {
  const thing = document.querySelector("some thing");
  return thing as HTMLElement; // <- cast
}

function doSomethingWithThing(el: HTMLElement) {
  console.log(el.textContent!.replace(/some regex/, "")); // <- non-null assertion
}

try {
  doSomethingWithThing(getThing());
} catch (_e: unknown) {
  // still don't care
}
```

Now the code compiles, we're just as safe at runtime, and everybody's happy! I honestly don't know why they tell us to use Typescript in the first place... right?

## Wrong

A month later someone gets the bright idea that `getThing` should be moved to a different file and just imported in this one. No big deal. Three months after that, somebody else decides the call `doSomethingWithThing(getThing)` needs to happen elsewhere also so they move it to yet another file in a different part of the codebase. These functions start to see more use in different places. Maybe somebody sees the try/catch, looks at the intellisense tooltip, and decides it's superfluous. But whether the original use-case stays safe or not the new ones look at the types and use the functions as their _supposed_ to work according to the information they have:

```typescript
// some other file
import { getThing } from "wherever/it/is";
import { doSomethingWithThing } from "wherever/that/lives";

function newUseCase() {
  const thing = getThing();
  // 100 LoC
  doSomethingWithThing(thing); // no try/catch! Compiler is silent! Kaboom: time for a P1!
}
```

The problem is that the original context and assumptions about usage have _evaporated_. There's nothing about these functions that suggest they can fail at runtime and there's even documentation (in the form of the type signatures) that says _conclusively_ that it _can't_ happen! Types are supposed to represent a partial proof of correctness, types that lie are worse than no types.

## You Know What Happens When You Assume...

Here the author(s) of the original code made an unfortunate assumption that wasn't a problem at the time they made it but aged like fine milk. The code was _fine_ as written. When it was written. But it was written in a way that left a time bomb ticking. How many of you are maintaining code today that neither you nor anyone on your team wrote? People move on to other teams/roles/companies, institutional knowledge decays, requirements change.

**When you tell the compiler you know better than it does you are taking responsibility for that choice not just _now_, not just for your current build, not just for the current version, not just for your _current_ team's code, but _forever_.** I'm not saying that it's _never_ the right call to do that, but you should be appropriately reluctant.

Since many of us have various career aspirations, and none of us are immortal as far as I know, that strikes me as a dangerous proposition: you probably aren't in a position to actually be responsible for that choice. You have left a landmine for somebody else to step on later, which may or may not be you. Now there are some obvious exceptions. Short scripts where there's only a single file of reasonable length that isn't realistically expected to grow in size. _Maaaaybe_ a solo project that you don't anticipate turning into the next big thing. But if you do that in Esperanto or some other production codebase at Kroger, you're probably just being a jerk.

## How NOT to Solve This

There is absolutely a wrong way to do this in Typescript-land (several actually). This code is a "solution" in the sense
that it works:

```typescript
function getThing2(): Element | null {
  const thing = document.querySelector("some thing");
  return thing;
}

function doSomethingWithThing2(el: Element | null) {
  console.log(el && el.textContent && el.textContent.replace(/some regex/, ""));
}

doSomethingWithThing2(getThing2());
```

No try/catch is needed anymore, this won't blow up at runtime no matter where you put the code. But it's kinda ugly and
the behavior has changed slightly: now if we don't find the element or find one with no `textContent` we log `undefined`. Huh. We'll Typescript might prevent an outage here, but at the cost of making the code worse. Lets try to clean this up by hoisting the check out of `doSomethingWithThing`:

```typescript
function getThing3(): Element | null {
  const thing = document.querySelector("some thing");
  return thing;
}

function doSomethingWithThing3(el: Element) {
  console.log(el.textContent && el.textContent.replace(/some regex/, ""));
}

const thing3 = getThing3();
if (thing3) doSomethingWithThing3(thing3);
```

Maybe we're mixing different concerns? Lets pull out the validation logic entirely:

```typescript
function isValidThing(x: unknown): boolean {
  return Boolean(x instanceof Element && "textContent" in x);
}

function doSomethingWithThing4(el: Element) {
  console.log(el.textContent && el.textContent.replace(/some regex/, ""));
}

const thing4 = document.querySelector("some thing");
if (isValidThing(thing4)) doSomethingWithThing4(thing4); // <- Error!
```

Oops! Now we're back where we started: _we_ know that we're safe at runtime but only in this case and if the context changes the compiler can't help us. We also still have way too much conditional checking here... this API sucks! Why are we doing this to ourselves.

I'm going to cut to the chase:

```typescript
// note the 'is'
function isTrulyValidThing(x: unknown): x is Node {
  return x instanceof Node;
}

function actuallyDoTheThing(el: Node) {
  console.log(el.textContent);
}

const actualThing = document.querySelector("some thing");
if (isTrulyValidThing(actualThing)) actuallyDoTheThing(actualThing); // no error?
```

Wait huh? What's different than the previous one? First, we did our check in a type-preserving way. The boolean in the previous validation function is opaque to the compiler. But `isTrulyValidThing` is a [type predicate](https://www.typescriptlang.org/docs/handbook/advanced-types.html#using-type-predicates) that the compiler understands _narrows the type_ of the thing you call it on. We've also tuned up the type of the HTML: a `Node` has `textContent` as part of it's definition in a way that `Element` does not. This code is even shorter and simpler than the original code. It's also safer. True, it took more effort to write, and it often takes more effort to write something simple but effective. But _this_ is why it's worth putting in the effort. This is why the platform teams occasionally give you grief about types in your PRs. Which code would you rather work with? The original code which is readable but not amenable to change or reuse? The safe but unwieldy version in `doSomethingWithThing2`? Or the version above that is shorter, simpler, and at least as safe as either?

Also note that in many cases throwing an error also has the effect of narrowing the type for a given scope:

```typescript
const el = document.querySelector("some thing");
if (!(el instanceof Node)) throw new Error("not a node!");

console.log(el.textContent); // fine
```

Note that in _both_ these cases if you modify the code in a way that invalidates the assumptions of the programmer _the compiler will catch it_, which is demonstrably not true of the motivating example code. Note that the True Way is narrow: it's easy to pre-empt the compiler in a way that leaves an explosive present for an unsuspecting future victim. And it's easy to type your code in a way that makes your eyes bleed to accomplish simple tasks. But when you can leverage the tool appropriately, it can be a thing of beauty.

## Further Reading

This talk came out of some conversations I've had with people lately that lead me to believe some of y'all still don't get why this stuff matters. It was also inspired by [an old blog post](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/) I really like that I stumbled back across recently. It's written in Haskell, but it should be accessible enough. Also see [this 2016 paper](https://langsec.org/papers/langsec-cwes-secdev2016.pdf) on what it calls "shotgun parsing", i.e. mixing input validating and normalization code throughout the business logic. Last but not least, see the talk [Simple Made Easy](https://www.youtube.com/watch?v=SxdOUGdseq4) by Rich Hickey about the difference between ease and simplicity and why it matters.
