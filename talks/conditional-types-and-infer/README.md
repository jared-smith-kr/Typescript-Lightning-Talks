# Talk \#8 Conditional Types and Infer

* [Playground](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAogjgVwIYBsDOAeAggGigIQD4oBeKLKCAD2AgDsATNAqAfhetseYvYoC4odCADcIAJyiDhY8QG4AUKEhQAKhDTBSsRKkx0EAWwBGEvAZMTCcqAHpbQo6fFLw0AGJIAlim3xk6BgWznia4l50AObWdg4yEgoKAGYIdADGwF4A9nRQSVlZGKp4AKqEABRUgsVQIIIleEjG1ZQ09Ew6AZg1ZWxQYRGRUo6W4gCUgiJZXgxQAN4AvskF5QDMeABMeADkSNtjNlBH9lBgSGhoy1nl2wAWXtt4AKx4AIwHR7Gn55f51+tQLZQd6HT5fJLeFBXG73R5QF5QXb7GwnCE+RLUMBZcRaZTQACySDAAHkklgUCgsIxiXQUCAANIQECYBRHVStLgdAByOS5CApTRQEAwqQA1nQsgB3OiEHCsqD0gDKHPazAGUSgAB8Rs4tf0QCYslDiGRRUyskk1CruArlexyuzOKqoAAlCBpbEMDBKxp0EDEdjs6SiCRjYbxFyuFQANVQM0ZzO0SL122M2yjHgK2jm8qQ0icCSOzX6wHCUQUSwzag0wA22kJJLJFKpDBpdITmHcBTwsZQ8aZaGIJy7WSrnh8dbIDdJ5Mp1NpDIHGAACl40qKMCOdntZVBe-3mUO4iGXHioOOUKt60SZ835+2lyOoAAyeZpQRIP0LHtxhgdo9CCeiRngAIlkGiKlkhgQAAMlkkRrhgDRWk6NolHqy7iFBXhoMKZQmihbQ2ph2G4UhAaInswyptsihnhQZBgRBUGwfBiHBGYUAkYYOHChx4iENYwFuFAADiEDANxvGqG4RQEY6REdFJZEREkEhQL07DocGsh0SJfKGNo4mSVhPG4TJkArqZvFBAWAkxCc-HCSoxlYOI4hICAFnCqo8nWh0bkeSAGCqepmkaeGJ56S5EmKhJ3lydoCmcswcXACFdBqZI4XaYBunOdAACSmUSOJwjhGkCW+Ul-nMOUoXZWMGVZXuFHRpF+VnsVWVlRIa7eRsRSlH5qEdCUzXqdGbUdepJwwC6LrEi69RQDhQhZFokT0H1aQKEAA)

## Because types aren't confusing enough as it is...

Sometimes we will want to perform conditional logic at the *type* level. This will usually take the form similar to the [Javascript ternary expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) that looks like `T extends Something ? A : B`. Remember from our earlier talks that `extends` means "is assignable to" and it's the easiest way to get a type-level boolean to branch on.

Note that the need to do this is fairly rare: generally you will only be using conditional types to create utility types like the [built-in ones](https://www.typescriptlang.org/docs/handbook/utility-types.html). So lets do that now: we're going to make a utility type that checks if two types are equal. We don't have an equality operator for types but if you can assign B to A and assign A to B then A and B are equal enough for our purposees:

```typescript
type Equals<A, B> = A extends B ? B extends A ? A : never : never;
type Test = Equals<number, number>; // number
type Fail = Equals<number, string>; // never
```

Ok, that works, but that's kinda boring, so lets use it to actually do something:

```typescript
function foo<T, U>(x: T, y: U, ab: T extends Equals<T, U> ? string : number): void {}
foo(3, 2, 'a');    // pass
foo('hi', 5, 1);   // pass
foo(3, 2, 1);      // fail
foo('hi', 5, 'a'); // fail
```

Here we've made it very clear to the callers of `foo` that if the types of the first two arguments are the same they should pass a string otherwise they should pass a number. **NOTE:** avoid use conditionals in the return type of a function, for that you should generally use [function overloading](https://github.com/jared-smith-kr/Typescript-Lightning-Talks/blob/main/talks/overloads/README.md).

Alright, so we now have two new tools in our toolbox: we can use `extends` to do a boolean comparison and we can branch on that comparison at the type-level using a ternary. Lets see another example:

```typescript
export type MapOfAllAndOnlyKeys<
  T extends NonNullable<unknown>,
  KS extends string | number | symbol
> = keyof T extends KS 
  ? (
    T extends Record<KS, any> 
      ? T 
      : never
    ) 
  : never
```

Given an object type and a union of keys, this will ensure that the object uses only and all of the given keys.

```typescript
type ValidKeys = 'a' | 'b'
type Foo = {
  a: number
  b: string
}

type Test2 = MapOfAllAndOnlyKeys<Foo, ValidKeys> // Foo
type Fail2 = MapOfAllAndOnlyKeys<Pick<Foo, 'a'>, ValidKeys> // never
type Fail3 = MapOfAllAndOnlyKeys<Foo & {c: any}, ValidKeys> // never
```

To break that down, we take as type arguments a type `T` that cannot be null and a type `KS` that must be compatible with the type of Javascript object keys (`string | number | Symbol`). If the union of the keys of type `T` are assignable to the type `KS` and type `T` qualifies as an object type of those keys then we get `T`, otherwise `never`. You can see that when we omit the `b` property we get `never`, and when we add the `c` property we get `never`.

A utility like this is useful if you have an enumerated set of things that get used as keys in one or more objects and you want to ensure that if you add a new thing to the set the compiler forces you to go update all the objects. In Kap Web Client we have various capabilities like logging and analytics and when we add a new capability name this utility helps us find all the spots we need to update like the object that maps the capability names to the relevant configs, the object that maps the names to the class constructors that do the concrete implementations, etc.

## The `infer` Keyword

When we write a conditional type for a generic we frequently wind up in a situation where the utility we're writing
would require the user of the utility to pass superfluous information. For example, lets say that we want to use a type
that could either be a type `T` or a `Promise<T>` and do some type logic depending on which it is:

```typescript
type DoesSomeLogic<U, T extends U | Promise<U>> = T extends Promise<U> ? 'a' : 'b';
type A = DoesSomeLogic<number, Promise<number>>;
```

Here the using the utility makes the duplication obvious: we're passing `number` as a type parameter *twice*. We *should* just be able to extract it from the Promise type. It turns out that's exactly what the `infer` keyword is for: getting the parameter to a generic type! So lets write a utility that extracts the type of a Promise:

```typescript
type GetPromiseType<T> = T extends Promise<infer U> ? U : never;
type Num = GetPromiseType<Promise<number>>; // number
```

In fact we can use the same pattern from `GetPromiseType` to extract any generic type:

```typescript
type GetArrayType<T> = T extends Array<infer U> ? U : never;
type GetSetType<T> = T extends Set<infer U> ? U : never;
```

Wow, these look awfully similar both to `GetPromiseType` and each other. Can we abstract out this pattern?

## HKTs

The short answer actually turns out to be no, or at least not in Typescript. Lets take a look at what that might look like:

```typescript
type InferGenericType<T> = T extends (infer U)<infer V> ? V : never;
```

This isn't actually syntactically valid. Ok lets try to simplify, lets have the caller explicitly pass `U`:

```typescript
type InferGenericType2<T, U> = T extends U<infer V> ? V : never // ERROR: U is not generic
```

## I am Fake Smart, And So Can You!

Can we constrain `U` to be generic? Turns out we cannot. In order to express the concept that we are trying to express here we actually need a type that is a higher kind of type than a generic type, i.e. a generic that is generic and Typescript's type system isn't powerful enough to express those. These are called [Higher Kinded Types (HKTs)](https://en.wikipedia.org/wiki/Kind_(type_theory)). Modern languages like Swift and Rust can express some of these higher level type concepts (through Protocols and Traits respectively), and Functional languages like Scala and Haskell have full support for Higher Kinded Types.

If you've ever heard some big-brain nerd-speak about HKTs, now you hopefully have some idea of what they're talking about and just like me you can effectively pretend to be smarter than you actually are!

