# Talk #11 Recursive Types and Mixins

[Playground](https://www.typescriptlang.org/play/?#code/C4TwDgpgBAUgygeQHIAUBOBLAth4GBu0AvFAM7CYB2A5lAD5SUCuWARhGvVKwPY8A2EAIaUuzfvwBQoSLERIAgmjRCQUEkpUgAPPGTpsuAtAZ7Fy1VzMARDAGM8PSkLQgAfNPDQb9x89fqUADeklBhUADaANYAXGQUGDQAunFmmpam8gY4eIRW8rYOGE4uIJIAvpKesgDCTqQ1EBLaACpugSFh+EL8TBBxLaGMEAAewHF1lA1N-K3tDOJSlZIAZkyURU5QdvVzABTdvf1QLQA0UPykE-WNzW0AlNdTt7NtwUNoEMBMaKJBUIc+udKKNxhdSFBygBuCpVNYbPzbFz7OwzJ7TO5uR4nd5hT7fX7bGYAOkBEBhy3hm1EdgAJmgUWioJMMa8seiXnMxEwJLioPifjSSSCxhSqjspsAoDgRoFtDUoKCIJRaRCQQB3KB7e7qdoiEDnACyirGytVwXKbj2NUuE3OMrihuxGq1xLdLmoV2Z9QoTAcPDQKBcQiwXw4pHlWN1UAAkpKRKiWl5I1AAGRQY1EdqdcIIVgAKwgDmJQlIpAw1Eo1suxLAaB4wAbXntGBG9xh4X5X0FzMuYskEvI0tbiQ6QzCpFUcW10YA5AALDCz2ED-iliEAMT4FvFPozrYgtK3PECMr2x5bI0S7YHe5W25ILsNB6PfG1qz4xMnIHfUL2LuPe4v1Ud9VnWalhxGAAhIQ7Ciah63WWk6n4AN5UuE1gDNNUIE1PY3RLNBPTifUIiSHUsygfUrRtL1aJ1HM8W7Qk7DXMtMOw3sIUYztth9NA-UbTh8PdIivVI8i+V43jSCYSA0BEwjPRvaSwmWVSoAAfR2VDOBIWcAGIN2Mkzlw06gvj43TtTicgqFoHiNIFQlgEXUhiW0gQA3HXj1NU0hLJ0gM9iCtBbISGgGJ8jSMBWLVXIwdzDgwWkhCwlDgtC+4oo0jSEvczzdMCULotU8pFUuaBHNysJXPrTUXQAUWUYKAAM42S2krIDeJ7KgAASIJQvKVqVJqyFSrUqoNIAehmqAkAbY47BESgG24aA6wINLoB6uslocQ8oHvTgZVHVj10mgEehSnaMoU0Lwvs7FeAEYQ-iuzs5qgABHJh7CiKiVSgWkMDQUBzhjAAlAAZbZ5yLQGTv5EQLM+8JnNEKC+EEEQQq8tBiSwNK7HnPYZoMiIhAAWgALwUamAC0kiCAA2coZuyq7Kk7SplkHKV7sPY9T1bGC4IQngkPu88+HuW9JW6z5XxPR9cO9XThbfeXQq1nhiVCwJDIABlNs3l0kIA)

## Recursion: Now I'm My Own Grandpa

So lets say that you wanted to write out the Typescript definition for something like the subset of Javascript that can be serialized to JSON. Think about what JSON consists of:

1. Primitive string, bools, numbers, and null
2. Arrays of 1, 2, & 3
3. Key/value dictionaries of 1, 2, & 3

Uh-Oh. Two of those things reference themselves in their own definition. Also each other. Fortunately, Typescript lets us do this:

```typescript
type JSONPrimitive = string | number | boolean | null
type JSONArray = Array<JSONPrimitive | JSONArray | JSONDictionary>
type JSONDictionary = {
    [k: string]: JSONArray | JSONPrimitive | JSONDictionary
}
```

And now we start to see how deep the Rabbit Hole goes: we can define containers that can contain themselves. Types can be recursive. Types can be mutually recursive. And types can be both recursive and mutually recursive at the same time. Magic. 

There are some limitations, you can't pass a recursive definition as a type parameter, for instance you can't replace the index type for `JSONDictionary` with `Record<string, JSONArray | JSONPrimitive | JSONDictionary>`: you'll get a circular reference error.

We all should be familiar with basic utility types like `Partial`, `Pick`, `Omit`, etc, but checkout this definition of `DeepPartial` from the [a-team-gaia repo](https://github.com/krogertechnology/a-team-gaia/blob/25e6472e72eba35aacaee57568b3dc40ab9ee798/packages/%40a-team/models/utils/src/module/data-manipulation/types.ts#L69)

```typescript
export type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends (infer U)[]
    ? DeepPartial<U>[]
    : T[P] extends ReadonlyArray<infer U>
      ? ReadonlyArray<DeepPartial<U>>
      : T[P] extends string | number | boolean
        ? T[P]
        : unknown extends T[P]
          ? unknown
          : DeepPartial<T[P]>
```

Note the recursive nature of the type to make it "Deep". You generally need a recursive type whenever you are typing
something that can contain more if itself (i.e. it is a conceptually recursive data type). The canonical example is the
cons cell that defines a linked list\*:

```typescript
type ConsCell<T> = {
  value: T
  next: ConsCell<T> | null
}
```

Now if you'll recall from [Talk \#4](https://github.com/jared-smith-kr/Typescript-Lightning-Talks/tree/main/talks/generics) that's maybe not how you'd actually *implement* a Linked List in Typescript for practical reasons (most JS data structures have an OO API), but you certainly *could* define it in terms of the cons cell above: walking the list is just chasing `next` until you hit the terminating null:

```typescript
// I've used the traditional LISP names here, but "add", "first", and "rest" worb too
function cons<T>(value: T, ls: ConsCell<T>): ConsCell<T> {
  return { value, next: ls };
}

function car<T>(cell: ConsCell<T>): T {
  return cell.value;
}

function cdr<T>(cell: ConsCell<T>): ConsCell<T> | null {
  return cell.next;
}
```

You can even define the natural numbers this way:

```typescript
// Peano numbers
type Zero = "Zero";
type Succ<N> = { succ: N; };

// Aliases for convenience
type One = Succ<Zero>;
type Two = Succ<One>;

// Addition
type Add<N, M> = N extends Succ<infer Nminus1>
    ? Succ<Add<Nminus1, M>>
    : M;

function proveExtends<T1, T2 extends T1>() {}

// Example: Only type-checks if 1 + 1 = 2
proveExtends<Add<One, One>, Two>();
```

[Source](https://github.com/fwcd/tylude), see also the [wikipedia article on Peano arithmetic](https://en.wikipedia.org/wiki/Peano_axioms)

## Mixins

If you've been in the Javascript game for any length of time you've probably come across mixins, a pattern where you can extend multiple objects with an abstracted out set of behaviors. Unfortunately, many of the common mixin patterns don't play well with Typescript. But you can absolutely make it work:

```typescript
const mix = <C extends new () => any, M extends {}>(Cls: C, mix: M): new (...args: ConstructorParameters<C>) => InstanceType<C> & M => {
    Object.assign(Cls.prototype, mix);
    return Cls;
}

const mixin = {
    say: () => 'hi'
}

class Foo {}

const MixedFoo = mix(Foo, mixin);
const foo = new MixedFoo()
foo.say()
```

It just makes the signature kinda gnarly. You also need to use the return value of `mix` rather than the original class, `(new Foo).say()` will fail to compile even though there's no runtime issue since we modified `Foo`'s prototype. The official mixin pattern from the [Typescript handbook](https://www.typescriptlang.org/docs/handbook/mixins.html) looks something like this (I used my own example):

```typescript
function mixBackgroundColor<Cls extends new (...args: any[]) => any>(Cls: Cls) {
    return class extends Cls {
        constructor (...args: any[]) {
            super(...args);
        }

        _color = '#FFFFFF'
        get color(): string {
            return this._color
        }

        set color(color: string) {
            if (this.validateColor(color)) {
                this._color = color
            } else {
                throw new Error(`Invalid color string ${color}`);
            }
        }

        // Note: cannot be private or protected for mixin class
        validateColor(color: string): boolean {
            // quick and dirty, IRL check for range
            return Boolean(color.match(/#[a-zA-Z]{6}/))
        }
    }
}

const ColoredFoo = mixBackgroundColor(Foo)
const coloredFoo = new ColoredFoo()
coloredFoo.color = '#000000'
```

This is less flexible than the above traditional mixin pattern. You can't type the constructor args (it *must* be a single rest param of type `any[]`), you can't have private or protected methods, and you have to make your mixin a class. But it does have one important advantage over the older pattern: you don't mutate the argument class. This can make [debugging problems significantly easier](https://legacy.reactjs.org/blog/2016/07/13/mixins-considered-harmful.html) than a chain of mixins that all modify a class and all the other advantages of immutability.

Mixins as you can see if you follow the link in the preceding sentence are extremely useful but also can be tricky to get right. Use them judiciously but when you need them they're extremly nice to have. I generally prefer the "official" second pattern when writing them but be aware of the tradeoffs with the more traditional pre-Typescript mixin pattern.

\* You can also use cons cells to build trees and other more complicated structures, but that's out of scope here.
