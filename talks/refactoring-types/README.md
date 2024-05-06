# Talk \#9 Refactoring Types

* [Playground](https://www.typescriptlang.org/play/?#code/JYWwDg9gTgLgBAJQKYEMDGMA0cDecAKUEYAzgOrAwAWAwlcADYAmUSAdtsujAHIRNI4AXzgAzIiDgByVtykBuAFCLgbGEiij0ggLIBPACr02Ac1yK4luAGtVTAFzSUUuAB9pAIykWrHxyRgoVTN3NgBXEA8NH0s0f0DgtzhwyOihZVEwtgxgCDYxCAgACgAPR30jYIBKcys4YFE4UoA6WzYmOABebqcpGpwYqzQ8kggGJGaGCBMWj2bWMFQYIoBmKqr5OAB6LbgAUSgoAEJB9PSVNQ0tNF09amCAQVqrNodewb84AKDTQbivhK-c6qdSabRwfT3UwAIWellejikXg+jhSUSgf1REXRinOMD0iwhemhSBgoMqpi6RKhJie7khxhM0IyWRyeQKEAATKVysTSeTGf1Bg0miVWnYuj0pM4hXVYiMxhMpjMxXMFktVutNjs4Hx9ocTqdccp8YTCMRyJQqHw2DwwgwGHRGCx2AAefBUnBCAB8VI9ADJcHA0PRmKw2I49iU0AwwgJXVwMHwBNhwg6klkBKJVEgmL7zkA)

## It's Not Really Any Different

Refactoring types is a lot like refactoring code, so don't get intimidated. That being said, some people seem to have a
sort of mental block on this topic so also don't feel bad if you *do* feel intimidated. Lets walk through some examples
so this doesn't seem so scary.

## Ex 1 Better Discriminating

We have a thing!

```typescript
interface MyThing {
    kind: 'a' | 'b'
    b: string | number
    c: string | number
}

function foo(x: MyThing) {
    if (x.kind === 'a') {
      console.log(x.b.repeat(3)); // Err!
    }
}
```

...but our thing is hard to use :(. Lets make it easier to use:

```typescript
interface MythingA {
    kind: 'a'
    b: string
    c: string
}

interface MythingB {
    kind: 'b'
    b: number
    c: number
}

type MyThing = MythingA | MythingB

function foo(x: MyThing) {
    if (x.kind === 'a') {
      console.log(x.b.repeat(3)); // No Err!
    }
}
```

Here we pulled `MyThing` apart and put it back together in a way that more clearly specifies intent. I've renamed stuff
so there's no syntax error in the playground but in the example code and IRL you'd want to actually *change* the
interface `MyThing` and the signature of `foo`. But what about types you *can't* change?


## Ex 2 Lets Type Children Moar Stricterer

We don't like the React type `PropsWithChildren` because it's too loose for our current use case: we expect the
component we're defining to *require* `children`. So lets make a PR to the React types on GitHub and they'll merge it
and we'll be fine right?

When working with 3rd party types it is often necessary to make a *new* type theat modifies the old:

```typescript
import React, { PropsWithChildren, ReactNode } from 'react';

type PropsWithNonNullChildren<P = {}> = P & { children: Exclude<ReactNode, null | undefined> }
```

## Use Your Best Judgement

So when should you change the types and when should you use `Exculde`, `Omit`, `Pick` and friends instead? Condsider:

1. Clarity. `Exclude<ReactNode, null | undefined>` is clearer than `string | number | boolean | ReactElement | Iterable<ReactNode> | ReactPortal` even though they mean the same thing.
2. Reuse. If I pull `{ a: string, b: string }` apart into `{ a: string }` and `{ b: string }` because I just want `a` can I reuse the pieces? Or just use `Pick`?
3. Flexibility vs Control. In example #1 I gave two ways of defining the idea of a `ReactNode` without `null` or
   `undefined`. One of them changes as the underlying union adds or removes types with future versions of React, the
   other does not.
4. Breakage. If somebody other than you is using the existing type *think carefully* before breaking its contract. It
   may be enough that you update the usage site for them in your PR, or it may not. If you have even the slightest shred
   of doubt here, just make a new type.

## Case Study: KAP Web Client
