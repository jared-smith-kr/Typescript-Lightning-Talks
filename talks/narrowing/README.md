# Talk #10 Narrowing Types

## Why can Typescript not just figure this out?

Frequently when writing Typescript one will want to check if an object is a particular type by looking at it's
properties. Something like this:

```typescript
type Foo = {
  a: string
}

type Bar = {
  b: number
}

type Baz = Foo | Bar;

function f(x: Baz): number {
  if (x.a) { // property 'a' does not exist on type Bar!
    return 0;
  }

  if (x.b) { // property 'b' does not exist on type Foo!
    return 1;
  }

  return -1;
}
```

I often see people use examples like this of why they don't like Typescript.

> *Those people are wrong.*

I mean, in a sense they're not, I can't tell them they don't know their own preferences, but rather that the compiler
(as compilers do) **must** consider edge cases for general use that the people making this point don't think of. For
example, lets say we're writing a browser game engine. So we make the following interfaces for vectors:

```typescript
interface Vec2 {
  x: number
  y: number
}

interface Vec3 {
  x: number
  y: number
  z: number
}

const m = { x: 0, y: 0, z: "hello world" };
const n: Vec2 = m; // N.B. structurally m qualifies as Vec2!
function f(x: Vec2 | Vec3) {
  if (x.z) return x.z.toFixed(2); // This fails if z is not a number!
}
f(n); // compiler must allow this call
```

Here the author of the code makes an unfortunate assumption that just because a property is present and truthy that it
is a certain type. But this is doubly wrong: you could have a falsey value of the correct type (zero or NaN in this
case) or a truthy value of a different type. But there are subtler gotchas.

Lets say our game engine doesn't take off so we need to get a boring day job as a sinecure until we make the next
Fortnite. So we start working at a bank, and we write this:

```typescript
type Message =
  { kind: "close" } |
  { kind: "data", payload: object }

function handle(m: Message) {
  switch (m.kind) {
    case "close":
      console.log("closing!");
      // forgot 'break;' here
    case "data":
      updateBankAccount(m.payload);
  }
}
```

This is a scenario where you'd want the compiler to complain about an unintended property access, not just silently propagate undefined. Catching this sort of thing is a big part of why we use static analysis in the first place.

To sum it up, the thing that people think that Typescript should do, i.e. specially interpret the dot access in a conditional check to narrow the type in the following block of code, is actually fraught with peril. There are safer ways to narrow the type of something that could be more than one thing. Let's look at a few.

## The Tightrope Walk

The Typescript compiler is already a marvelous feat of engineering layering a static type system on top of not just a dynamic language but an ultra-dynamic language. What you're looking for here is called [type narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html), where you take a value that could possibly be more than one type and then narrow it down to a specific type. The TS compiler supports (at least) five different idioms to achieve this:

* The instanceof operator.
* The typeof operator.
* The in operator.
* A user-defined type guard.
* A discriminated union.

Let's look at each in turn:

## instanceof

This one works well for user-defined classes:

```typescript
class A {
  public a: number
  constructor () {
    this.a = 4;
  }
}

class B {
  public b: number
  constructor () {
    this.b = 5;
  }
}

type AB = A | B;
function abba(x: AB): number {
  if (x instanceof A) return x.a;
  if (x instanceof B) return x.b;
  return 0;
}
```

## typeof

This one works well for JS primitives (undefined, numbers, strings, booleans, etc).

```typescript
type snumber = string | number;

function f(x: snumber): string {
  if (typeof x === 'number') {
    return x.toFixed(2); // strings don't have toFixed
  } else {
    return x.repeat(2);  // numbers don't have repeat
  }
}
```

## `in` operator

This one works well for structurally typed objects:

```typescript
type A = {
  a: number
}

type B = {
  b: string
}

type AB = A | B;

function f(x: AB): number {
  if ('a' in x) return x.a;
  if ('b' in x) return 5;
  return 0;
}
```

If you're paying close attention you might notice that this has the same problems as the first motivating example above, namely that the existence of a property on an object does not in any way guarantee the type. This was a pragmatic decision on the part of the TS team to allow an uncommon behavior for a simple opt-in idiom of wanting to get either the value or undefined, and much like a cast is an implicit promise that the programmer is taking responsibility for the possible outcome.

## User-defined type guards

This works well for just about anything, but is more verbose than the earlier options. This one is straight from the [TS Handbook](https://www.typescriptlang.org/docs/handbook/advanced-types.html#user-defined-type-guards):

```typescript
function isFish(pet: Fish | Bird): pet is Fish { // note the 'is'
  return (pet as Fish).swim !== undefined;
}

let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

## Discriminated union

This works best when you have a bunch of very similar objects that differ only in the (statically knowable!) value of a single property (I've used `kind` here):

```typescript
type A = {
  a: string
  kind: 'is-an-a'
}

type B = {
  b: number
  kind: 'is-a-b'
}

type AB = A | B;

function f(x: AB): string {
  switch (x.kind) {
    case 'is-an-a': return x.a;
    case 'is-a-b':  return '' + x.b;
  }
}
```

Note that you will as I said need to make the discriminant (the `kind ` property in this case) a statically knowable value, usually a string literal or a member of an enum. You can't use variables, because their values aren't known at compile-time.

So in summary the Typescript compiler can figure it out, you just have to use an idiom it can statically verify instead of one that it can't, and it gives you a fair number of options.
