# Talk \#∞ Functors and Monads Oh My!

## Before We Get Started, Does Anyone Want to Get Out?

<img src="../../resources/cap-elevator.jpeg" />

Everything I've talked about in this series up to this point has had *immediate* practical application: you can find literally everything I've mentioned so far in Kroger codebases like KAP Web Client, a-team-gaia, and Esperanto. But today, I'm going *deep*. Buckle up buttercup. No promises except you might find you can speak a few words of hyper-nerd by the end of this.

If you've ever heard an argument about the big M-word in Typescript you may have stumbled across mention of this concept: expressing Monads in full generality requires these HKTs. But a Monad is just an interface that follows some rules. Despite that simple fact Monads for some reason are big and scary to people so lets start with something simpler: Functors! Functors are just "something that has a 'map' method". Technically Monads must also be Functors, so if we can't get to a Functor interface then we can't have a Monad interface. Arrays have a map method, so lets test a Functor interface on Arrays:

```typescript
interface Functor<T> {
  map<U>(f: (x: T) => U): Functor<U>
}

class MyArray<T> extends Array<T> implements Functor<T> {} // Ok!
```

So do Promises! An astute reader might notice that `Functor.map` has the exact same shape as `Promise.prototype.then`: we take a function that transforms a `T` into a `U` and return a new `Container<U>`. So lets make a `Promise` that implements this:

```typescript
class MyPromise<T> extends Promise<T> implements Functor<T> {
  map<U>(f: (x: T) => U): MyPromise<U> {
    return this.then(f); // Oops!
  }
}
```

and here we see the limitations: Promises and Arrays aren't fully polymorphic for subtypes. Promises have actually been a thing in JS since before the official ES6 implementation, and so Typescript provides an interface `PromiseLike` for any `then`able type. Think about the signature for `PromiseLike.then` that exists in `lib.d.ts` built in to Typescript. How could we type this so that we didn't need to cast the return value in `MyPromise.map`?

```typescript
interface PromiseLike<T> {
  then<U>(f: (x: T) => U): PromiseLike<U>
}
```

And again we see the problem: we could reasonably want to assert that `PromiseLike.then` returns a new `PromiseLike` that's the same *kind* of `PromiseLike`, but we have no way to express this! A `Q` Promise isn't the same as a `Bluebird` Promise isn't the same as a `jQuery` deferred isn't the same as a native Promise, but the limitations on the interface means we can't express this constraint in the interface.  The array example suffers from the same problem: we could override the `map` method to return a Functor other than an Array, which would be... unexpected behavior to say the least. We *want* to be able to express that `Functor.map` returns the same "kind" of thing as the *specific* Functor instance.


```typescript
// This doesn't actually work...
interface DesiredPromiseLike<T> {
  then<U, (infer SpecificPromiseLike)<T>>(f: (x: T) => U): SpecificPromiseLike<U>
}
```

Because unlike Promises where it's kinda sorta inconvenient not to be able to express this pattern, it's part of the *definition* of a `Functor`. We can't do that, so we can't have a true `Functor` interface. And no `Functor` means nothing based on it either: no Monad!

## Lets Be Crystal Clear

You can *absolutely* define *a* Functor in Typescript. Javascript arrays are Functors. Promises are Functors. You can define *instances* of `Functor` all day long. But what you *can't* do is pull out the abstract pattern of `Functor` into its own thing: Typecript's type system isn't powerful enough, as we've seen. So when people say stuff about not having Functors and Monads in Typescript, they mean *that* rather than that you can't express them at all (or they just don't know what they're talking about, not uncommon especially on the internet).

## The "Monad Tutorial Fallacy" Strikes Back

Ok, so we've seen we can't have Functors and by extension, Monads. We're going to ignore that for a moment and pretend we can so we can talk about Monads. In case you're actually reading this, hello! You're about to read an Elder Scroll, and unfortunately you are **not** the Dragonborn. Just kidding, Monads aren't scary they're just an type required to obey certain rules. The main one is that a Monad should have a `bind` method (which we'll call `mbind` for "monadic bind" to not get it confused with `Function.prototype.bind`). To wit, lets look at an example:

```typescript
class Maybe<T> {
  constructor (public readonly value: T | null) {}
  map<U>(f: (x: T) => U): Maybe<U> {
    const val = this.value === null ? null : f(this.value);
    return new Maybe(val);
  }

  mbind<U>(f: (x: T) => Maybe<U>): Maybe<U> {
    const val = this.map(f).value;
    if (val === null) {
      return new Maybe<U>(null);
    } else {
      return val;
    }
  }
}
```

Maybe is a type that could represent a value or nothing. Per the conversation about Functors above, we can do the same thing to Promises:

```typescript
class MonadicPromise<T> extends Promise<T>  {
  map<U>(f: (x: T) => U): MonadicPromise<U> {
    // map is just an alias for then
    return this.then(f) as MonadicPromise<U>;
  }

  mbind<U>(f: (x: T) => MonadicPromise<U>): MonadicPromise<U> {
    // because Promises auto-flatten mbind is just map
    return this.then(f) as MonadicPromise<U>;
  }
}
```

In the same way that `Maybe` represents a value that may or may not be there, a `Promise` represents a value that may or may not be there *yet*. We can see that the method definitions for `Maybe` and `Promise` are *really* similiar, to the point where I actually copy/pasted them in my editor and did a little regex find-and-replace. So `Maybe` *is* a Monad\* and `MonadicPromise` *is* a Monad \*\* and we can see the similiarities in the code. Can we abstract this out as an `interface Monad` that these classes can implement? No! It's the exact same problem we ran into before: we can't have an interface that takes a generic type parameter that is itself generic! We can easily show this:

```typescript
interface Monad<T> {
  mbind<U>(f: (x: T) => Monad<U>): Monad<U>
}

class MaybeMonad<T> extends Maybe<T> implements Monad<T> {}
class MP<T> extends MonadicPromise<T> implements Monad<T> {}
```

Wait, um, actually, that seems to work. We did need those fancy pantsed HKTs after all! Well, actually just like with Functors we *do*:

```typescript
class Broken<T> implements Monad<T> {
  constructor (public readonly value: T) {}

  mbind<U>(f: (x: T) => MonadicPromise<U>): Maybe<U> {
    const val = f(this.value);
    return new Maybe<U>(null);
  }
}
```

Here the compiler doesn't have any problem. But we do *have* a problem, part of the definition of a Monad that I glossed over before when talking about the rules is that `mbind` needs to return the same *kind* of Monad: `Maybe.mbind` should return a `Maybe`, `Promise.mbind` should return a `Promise`. Our `Broken` class' `mbind` takes a function that returns a `MonadicPromise` but then returns a `Maybe`!. When we wrote them to do the right thing everything worked ok, but we can't actually define an `interface` that actually enforces the rules. As stated previously, Typescript interfaces just aren't powerful enough to express this concept of a function that's generic over a generic container that returns the same type of generic container but with a different parameter. Something something subtype polymorphism. The Aristocrats!

## Now Back To Your Regularly Scheduled Programming: Why Does Any of this Matter?

Ok, I hear you, like Jared, bruh, I'm sure that's really cool if you're a Math PhD but I build React Components yo, do I really need any of this? And the answer is... probably not? A lot of this matters a lot more to library authors than to application developers. But that distinction is a false dichotomy: if you ever extract some code into it's own thing in order to use it in multiple places you are, in the relevant sense, a "library author". You have the same problem: can I extract this bit of code for reuse? Remember back in talk \#8 with the utilities to extract Promise/Set/Array types?

```typescript
type GetPromiseType<T> = T extends Promise<infer U> ? U : never;
type GetArrayType<T> = T extends Array<infer U> ? U : never;
type GetSetType<T> = T extends Set<infer U> ? U : never;
```
There's an obvious pattern and duplication here, but we cannot abstract it away, the type system won't let us. It would
sure be helpful if you could...

More importantly, if you have a shared interface for things, then you can write a suite of functions to work on the *interface*. This means they're open and extensible: if somebody makes a new thing that implements that interface your function will work on it *without you needing to do anything to the functions*. Consider the `Symbol.iterator` protocol in Javascript! Or consider HOCs in React: their possible because every React component conforms to the `(props) => JSX.Element` signature!

**Most** importantly, it gives developers a shared language to talk in. Once upon a time there was a fad calling these things "Design Patterns" and people even asked interview questions about them. Code that obeys rules is easier to reason about, easier to use, and easier to compose with other things that follow the same rules. The rules of functional design patterns like Monad and Functor are specifically designed to facilitate that composition and use.

But there is one more really important thing even if none of that speaks to you: you need to recognize when the type problem that you are struggling with requires something that Typescript just isn't powerful enough to express so you can stop tilting with windmills and just kludge it the best you can.

## TakeAways:

* If you can write `type GetPromiseType<T> = T extends Promise<infer U> ? U : never;` and it's not goobledegak to you then you understood enough of this talk to matter.
* If you understand that you can't have a generic generic without plugging in a concrete type, hopefully you won't try.
* If you think this is all kinda high-falutin... well, you're not wrong but remember that `if` statements and garbage collection and a bunch of other stuff we take for granted was considered "academic" at one point!

Anyway, hopefully all this stuff seems a little less scary now. Please feel free to do some reading up and look over this code (it's on github), play around with it in the TS Playground, etc.

## Useful Resources:

* [Monads, Applicatives, and Functors in Pictures](https://www.adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html)
* [fp-ts](https://gcanti.github.io/fp-ts/) Even though TS doesn't have HKTs this library (ab)uses interface extension to fake them pretty convincingly!
* [Legendary Stack Overflow answer](https://stackoverflow.com/a/2704795/3757232) by compiler guru Eric Lippert about Monads for someone with no FP background

## Notes For Pedants:

\* Yes, I realize my `Maybe` implementation is not an Applicative and therefor not really a Monad by the Category Theory
definition.
\*\* Yes I realize that Promises auto-flatten and therefor are not a Monad regardless of anything else I do to them.

FOR THE PLAYGROUND:

```typescript
interface Functor<T> {
  map<U>(f: (x: T) => U): Functor<U>
}

class MyArray<T> extends Array<T> implements Functor<T> {} // Ok!

class MyPromise<T> extends Promise<T> implements Functor<T> {
  map<U>(f: (x: T) => U): MyPromise<U> {
    return this.then(f); // Oops!
  }
}

interface DesiredPromiseLike<T> {
  // Doesn't work!
  then<U, (infer SpecificPromiseLike)<T>>(f: (x: T) => U): SpecificPromiseLike<U>
}

class Maybe<T> {
  constructor (public readonly value: T | null) {}
  map<U>(f: (x: T) => U): Maybe<U> {
    const val = this.value === null ? null : f(this.value);
    return new Maybe(val);
  }

  mbind<U>(f: (x: T) => Maybe<U>): Maybe<U> {
    const val = this.map(f).value;
    if (val === null) {
      return new Maybe<U>(null);
    } else {
      return val;
    }
  }
}

class MonadicPromise<T> extends Promise<T>  {
  map<U>(f: (x: T) => U): MonadicPromise<U> {
    // map is just an alias for then
    return this.then(f) as MonadicPromise<U>;
  }

  mbind<U>(f: (x: T) => MonadicPromise<U>): MonadicPromise<U> {
    // because Promises auto-flatten mbind is just map
    return this.then(f) as MonadicPromise<U>;
  }
}

interface Monad<T> {
  mbind<U>(f: (x: T) => Monad<U>): Monad<U>
}

class MaybeMonad<T> extends Maybe<T> implements Monad<T> {}
class MP<T> extends MonadicPromise<T> implements Monad<T> {}

class Broken<T> implements Monad<T> {
  constructor (public readonly value: T) {}

  mbind<U>(f: (x: T) => MonadicPromise<U>): Maybe<U> {
    const _val = f(this.value);
    return new Maybe<U>(null);
  }
}
```
