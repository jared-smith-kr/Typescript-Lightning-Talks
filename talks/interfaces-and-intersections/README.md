# Talk \#2 Interfaces and Intersection Types

* [Recording](https://kproductivity-my.sharepoint.com/:v:/g/personal/jared_smith_kroger_com/ESWS8p5_PnhAjJR_csHhchsBUbhZbdMvQRJghgXw0QEHRQ) \[Starts at 38:34\]
* [Playground](https://www.typescriptlang.org/play?#code/PTAECUFEGEEEAUBQiSgJIDsAuBTATgM44DGWAlgPYahYCeADjgaAIYYAmoZ2+AZi8SbI6jUADEKFUAF5QAb0ShQvSQC5QBLHm4BzRAF9hDHKABCLPDPmLQAIwvqMAVwC2t-AaOiJFc5dk+oABkZhbIxFSaypL2eOo+flYKSioU6gDkABZk6QA0NrHqAKz5hojcuHj8guiBydFpGlq6nuU8VQImaIn1haDObh5lFXydtZKJOAAeuBzMaD656D3Iw+3VXQDqOGR4nNOz7MyLoZYKrSImsAA2BBTbu5yyC5LBy2EoYADyANJLd1xmFhMvgTGxaKB2GReLxQRhBAB+UAATSYAEIvCYAMoUFw4YG6JI2dgUAAqIPJunUAAoLDp1OCAJQyAB8NGyBFaIw6NQAEiwCNAqLxrmRSNYlCx1JptBg9GtKhtQEKMCKxVhmAccHNQPzBcLReL6lL+q53HgLsZQF8KPRmLJjdLmnLLaIAKqZL6ZKw2u1vR2mwYWsoRDBRfhka7qD1epKsdQAZlAZVQNwB7hUeBMpKxoAALAA6ABMSORFCcoEyLAAbiYCcx6HgKLZrjgXAWO6BqUQTBRgfgaCxbIzkKgAOJ94hV5i0csaTLl66cDAUADudjBLbrUhrFDI7FUiFDUTwbBJVgAsixgQWm04ONSrzfTxxcdTGSPEK2sKwksNeF2L4ksyxpEkoKRqKAWQ5DYhj-l2LAFqkIGrKOYBiKSYjIsg352Oo9SpAiTqyvKf7INCgFnhQKFKLYYHgakGTZOksFcgB1K2Ehkg0aAx4UK2BbXBQOgcVx1GtKgXx4B2HbhJEP6pHGJoJksthMTkyZfvidgWFY6QsCxqQANqxAAunJYY-vYABe6gANY4LOAGXBQAGKbI+mGZIJksNZ5kCrQ8LKPepCUNQ74Srx8mgFmBD0FYLCriwZAKfiU7Uukdx4m64AADLpCOSjHj+ABWdzULIiXJT+sX0AWZVUO+NjFaADm0AQ9mOa5NDGN1DUVdatglSQWAFm1BDUv1I6GJcoCklYLlua8qByPGgbmpps0-FYbXdfN4GoJ5yC8CF5BUBuWCVKSvW8NSUwMhgtA8VmWBOHg1BfENI0Fo2fZ9sYBZYBQWLOjoBbECw1zXHd03IO4l34NdjCudSzhQ8yqBGc2w3igAck4UPmfDV03dSRmmcySiY9jI2gLAeCnrQRP4iTyO3QAUliXy4xjYBY194qc9zzMI3gSM4CjT6ZLzoD8zjP5S+ZiBAA)
* [Bug Illustration from Bloomberg](https://www.typescriptlang.org/dev/bug-workbench/?ts=4.1.0-dev.20200917#code/PTAEAEBMFMGMBsCGAnRAXAlgewHYCg8QIAzDeaHRAW2gC5QAHZDAN3WgDo0BnPDHNNGTFEsaKACSoAN55Q80Ino4ArlQBGQgNx4AvgTQBPBuIAqoALwy5CpaFUahegtAAeDLMjShiKnLExcHxxQAAoASlB6KVkFUGRoNBVkEOlFWgBGUF0dfTw3Dy8fPwDsEIBzMMj6c1iFBKSUmXSs-TyicFJyShp6BhV1eAxYLl4MKkLvaWIcABpy3R9kLCpQACIOYCZWdg4AK241giIhZeRQUwBlABYABgAmAGZ6AFF3T0FIUDZmREHxADkLABoAAFohuKBPKAMJCVNx+JUeoCJCDiMtVm5BClEPBQFQsJAVOR1ohRmtQOoVN5YIgcDgsN5NPZqNBIBx8u8irBcNxvCxLMEIjpCGBTMZxLDQAjumh4IYYTghjg2QBCTmTUA8nB80AqQXlYV4IA)
* [Advice on Interfaces vs Intersection Types from Microsoft](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections)

## Intersection types and interfaces

### Intersections

Intersections are the type system's 'and', instead of the Union from last time where a type could be an 'A' or a 'B', with Intersections the type is *both* an 'A' *and* a 'B':

```typescript
type Foo = {
  foo: string
}

type Bar = {
  bar: number
}

type FooBar = Foo & Bar

const foobar: FooBar = {
  foo: 'hi',
  bar: 5,
}
```

### Interfaces

Interfaces are the publicly visible parts of an object's type definition:

```typescript
interface IFoo {
  foo: string
}

interface IBar {
  bar: number
}
```

They are implemented by classes, and you'll get an error if the class does not properly implement the interface:

```
class BadFoo implements IFoo {} // Error: no foo string property!

class Foo implements IFoo {
    public foo: string

    constructor (s: string) {
        this.foo = s
    }
}
```

Just like we can glom types together using intersections, interfaces can be extended, even with multiple parents:

```typescript
interface IFooBar extends IFoo, IBar {

}
```

But we can also extend types...

```typescript
interface IWeird extends Foo, Bar {

}
```

...or take the intersection of interfaces:

```typescript
type AlsoWeird = IFoo & IBar
```

### OK, so is there any difference?

Yes! Consider the following cases:

```typescript
type Something = {
  doTheThing: (arg: any) => this // Error! Can only use 'this' in classes and interfaces
}

interface HasConflict {
  a: string
}

interface Conflicts extends HasConflict {
  a: number // Here you get an error immediately
}

type Oops = {
  a: string
}

type UhOh = Oops & {
  a: number // Silent!
}

const fail: UhOh = { a: 3 } // a is type never? Huh?
```

When there's a property conflict in an intersection type the compiler can and in this case does silently change it to `never`, and you don't find out until you try to assign to it.

## Also before TS 4.2? You have this problem...

```typescript
// @declaration

// @filename: private.ts
interface I {
    a: number;
}

type T = {
    a: number
}

export function fn () : I {
    return { a:1 };
}

export function g () : T {
    return { a:1 }
}

// @filename: public.ts
import {fn,g} from "./private.js"

// error TS4023: Exported variable 'v' has or is using name 'I' from external module "a.ts" but cannot be named.
export const v = fn();

// Type is silently inlined!
export const u = g();
```

Bloomberg had an issue where a declaration file went from *700Kb* to 7kb when they changed an unexported type to an interface.

## Gotchas you should now be able to avoid:

```typescript
const rando = Math.round(Math.random()) // 0 or 1, could be truthy or falsy, don't know

let a = {}

if (rando) {
  a = {
    foo: 'hi'
  }
}

if (a.foo) {

}

// FTFY

let b: {
  foo?: string
} = {}

if (rando) {
  b = {
    foo: 'hi'
  }
}

if (b.foo) {
  console.log(b.foo)
}
```

Or from last time:

```typescript
const works = 'a'

// Remember type narrowing from last time with the Stack Overflow answer?
if (works in foo) {
  foo[works]
}
```

Or....

```typescript
const foo = { a: 3, b: 'hi' }
let bar = 'a'
foo[bar]

const baz: keyof typeof foo = 'a'
foo[baz]
```

So let's break that down...

```typescript
type T = typeof foo // { a: number, b: string }
type K = keyof T    // 'a' | 'b'
```

When we have a compile-time known value and we need to get its type we can use `typeof` to grab it. We can then use `keyof` to get the union of the keys of the object or interface or type:

```typescript
type A = {
    a: string
}

interface AA {
    a: string
}

const a = {
    a: 'hi'
}

// All are the same thing, remember TS is structurally typed:
type K1 = keyof A
type K2 = keyof AA
type K3 = keyof typeof a
```

We can only do this with values known at compile time:

```typescript
async function () {
  const resp = await fetch('someURL')
  const json = await resp.json()
  const keys: keyof typeof json = Object.keys(json) // Error!
}
```

Here since `json`'s shape isn't known at compile-time, the compiler infers `string | symbol | number` because those are the types that can be used to index into arbitrary Javascript objects.
