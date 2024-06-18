# Talk \#9 Refactoring Types

* [Playground](https://www.typescriptlang.org/play/?#code/JYWwDg9gTgLgBAJQKYEMDGMA0cDecAKUEYAzgOrAwAWAwlcADYAmUSAdtsujAHIRNI4AXzgAzIiDgByVtykBuAFCLgbGEiij0ggLIBPACr02Ac1yK4luAGtVTAFzSUUuAB9pAIykWrHxyRgoVTN3NgBXEA8NH0s0f0DgtzhwyOihZVEwtgxgCDYxCAgACgAPR30jYIBKcys4YFE4UoA6WzYmOABebqcpGpwYqzQ8kggGJGaGCBMWj2bWMFQYIoBmKqr5OAB6LbgAUSgoAEJB9PSVNQ0tNF09amCAQVqrNodewb84AKDTQbivhK-c6qdSabRwfT3UwAIWellejikXg+jhSUSgf1REXRinOMD0iwhemhSBgoMqpi6RKhJie7khxhM0IyWRyeQKEAATKVysTSeTGf1Bg0miVWnYuj0pM4hXVYiMxhMpjMxXMFktVutNjs4Hx9ocTqdccp8YTCMRyJQqHw2DwwgwGHRGCx2AAefBUnBCAB8VI9ADJcHA0PRmKw2I49iU0AwwgJXVwMHwBNhwg6klkBKJVEgmL7zjrgCY2NBBNQkCQkNhy3oZIIAFZhAJwKgaMsQOAgFDWMutuBIEoocDjYMQcCMJCKU2CADSKDADzAYAYwDQKBguTYOhQbAaFfgnUQSGGUCYru+wWwF9M3qnBMEAEkaPPt2AqcgT2fryYr4CTLfpzgRcwB0fh7SQV932PaAvz-X8fn-O9CWAlc1w3PJQKYcCdFJFAmHXFBPTgAA3DQSE3eIEOEJDBGfMAUA8RhKD0HCYDwgjIMPD8YPPOCg1IqByLySjEh9Gi4AAESQKg9BYdckAAZTY9QqQAbW-VNsQ0eDggAXSUQCEDw+i0GsJT5LU5orKkmS5PUcz1E01IoH08S6IYpj8R4IdBEPb9xPwBh11EaAQAAMSWMJWDCoKTBIGg8mzMxDzwAB3Kh5IErFnOoxQdTXSsATjPQ4GnEh7HE5MkDnMAAHEpg8FAGE9Hwu13UR90cGqUNXddN23dr9x8Nd6MYlcNwrAB+RwnxfecfHnECwPGEhpqApdMOw+bLEWzbxlYlBXzW7jT14hDsB6tD+uWiDcPwtjb0sZdgtChK2CStb3LG5iDvuw7tuDFd2BgBykDWmzZKgeTQeGoG1AeEhKxgVaRNMVTdNh4BgeQExgACDQAFUoAYFGj0-M7EncL7PL0byQCrAEEMe0c1CIB0NDWnc9GNcToSIVLKygGr6ogRrmpS1qdz3AIuvnS6+owqWOoCYb5w88asdJ80QDxpBXVmkD52Z3abq1iRdddYC9ogo2Fo2m6DtfRwTtg871uXXr0K3B27oI5nnpgEKoBAN6kscanxpY322NfHwA6D8LIui2L4sSotHECl7g4i9coqQGKUDi0Oi0x4HQccCG7MU5TBHcIymBMsya9L+HEdJcrGeCdGW5gHG8dBImSed6DTo0zubx5kErnBAAJFASAG6X4AGOo2qX2WFyXVCFa3JWhvOAdIFgepLjBG44BFsWaoigQofUDoV+DNXvomjuDdjnb7awlbHCth35oPiUI+8BAKXyatfXMGh5JMARnobILVLCqWsCfGwSA9AQEaGAhgEDb7QN0mtbWFssE4KgffJBulbyAOASfUE1xBDEPnOaRYsBNbPBNt-W6Md5zD3JmPeWXtra-T9nHIKgdXppxMOHZ+NMhFcLAD3cuklpKQ2hjXJI9dG4w1iHDGACMkYd2-N3bRWM1B93xlAQeHcXYU0pFTaRkc6YM2-JQ5Qh9oDwCnmfQQJIyQaD5hAAWGgsH9hKOodoJA4BzwXnvAI2AGFgBvqQ3MsDshxIauAxhRBmGv2ePHUKOcYB5wLkXCRGdREJwKUUlOxcTA8zccfTxdC4A+NBApDQAlgkDjCUwCJUTF7KywAQFALCmquniYku+uZvTYHwMMjcoz4lMI0K-X0j9hiszGOMKAnM2DcyEEAA)
* [Refactor commit from KWC](https://github.com/krogertechnology/kap-web-client/pull/1404)

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

So when should you take the additive compositional approach and change the types and when should you use the subtractive approach of `Exculde`, `Omit`, `Pick` and friends instead? Condsider:

1. Clarity. `Exclude<ReactNode, null | undefined>` is clearer than `string | number | boolean | ReactElement | Iterable<ReactNode> | ReactPortal` even though they mean the same thing.
2. Reuse. If I pull `{ a: string, b: string }` apart into `{ a: string }` and `{ b: string }` because I just want `a` can I reuse the pieces? Or just use `Pick`?
3. Flexibility vs Control. In example #1 I gave two ways of defining the idea of a `ReactNode` without `null` or
   `undefined`. One of them changes as the underlying union adds or removes types with future versions of React, the
   other does not.
4. Breakage. If somebody other than you is using the existing type *think carefully* before breaking its contract. It
   may be enough that you update the usage site for them in your PR, or it may not. If you have even the slightest shred
   of doubt here, just make a new type.

## Case Study: KAP Web Client

We have two main state objects, one for the browser and one for node.js. They began life at different points in the
SDLC, they had different motivating use cases, and different properties. But over time they have undergone convergent
evolution to be very very similar:

```typescript
type NodeKapGlobal = {
  manifest: KapApplicationManifest
  capabilities?: ICapMap
  appModules?: AppModuleMap
  appModuleMetaMap?: Record<string, ApplicationModuleMetadata>
  platformConfig?: CapabilityMetadataMap
  clientState?: DehydrateState
  clientAssets?: string[]
  clientRegisterUrls?: Record<string | CapabilityName, string>
  controller?: any
}

type BrowserKapGlobal = {
  manifest: KapApplicationManifest
  capabilities?: Promise<ICapMap>
  appModules?: Promise<AppModuleMap>
  appModuleMetaMap: Record<string, ApplicationModuleMetadata>
  platformConfig: CapabilityMetadataMap
  platformFeatureFlagsConfig: PlatformFeatureFlagsConfig
  clientState: DehydrateState | RadpackState
  clientAssets: string[]
  clientRegisterUrls: Record<string, string>
}
```

Don't worry about the names. The point is, it's clear even at a glance there's a lot of overlap, it would be nice to be
able to extract out the common bits to DRY up the types. But there are a few stumbling blocks:

1. Some properties are required in one but optional in the other.
2. Some are `Thing` but in the other it's `Promise<Thing>`
3. Some properties have slightly different types.

## Pick the low-hanging fruit first.

The easiest is `manifest`: it's the same type and required in both:

```typescript
interface HasManifest {
    manifest: KapApplicationManifest
}
```

After that we've got `appModuleMetaMap`, `platformConfig`, `clientAssets`, and `clientRegisterUrls` which are required in the browser but optional in node. However, now there's a decision point: do we group these by their requiredness in this interface or by their semantic association? I vote for the latter. So we're going to shift gears and look at the domain: both `capabilities` and `appModules` are federated modules if you caught our presentation on that a few weeks back. So let's split *those* out:

```typescript
export interface GlobalKapFederated {
  capabilities: ICapMap
  appModules: AppModuleMap
}
```

Okay, but those need to be Promises on the client:

```typescript
export type GlobalKapFederatedAsync = {
  [k in keyof GlobalKapFederated]?: Promise<GlobalKapFederated[k]>
}
```

and now we just need to add the rest of the building blocks:

```typescript
export interface GlobalKapProperties {
  appModuleMetaMap: Record<string, ApplicationModuleMetadata>
  platformConfig: CapabilityMetadataMap
  clientState: DehydrateState | RadpackState
  clientAssets: string[]
  clientRegisterUrls: Record<string | CapabilityName, string>
}
```

...and we can finally start building our types back up to replace the originals:

```typescript
export interface BetterBrowserGlobal extends HasManifest, GlobalKapFederatedAsync, GlobalKapProperties {
  platformFeatureFlagsConfig: PlatformFeatureFlagsConfig
}

export interface BetterServerGlobal extends HasManifest, Partial<GlobalKapFederated>, Partial<GlobalKapProperties> {
  controller?: any
}
```

## Closing Thoughts:

I want to stress that we did this over the course of 30 minutes with a well-understood an unlikely to change pair of types with lots of overlap. We split them up in a way that makes sense for the *domain*, not just where it was most convenient for how Typescript works. But generally, the same principles apply as refactoring code: you break a complicated thing apart into simpler pieces and then recombine them to make a better version of the original thing. I don't want to name-and-shame, but I've seen a Typescript codebase at Kroger where the types were... not constructed with these ideas in mind. At the risk of stereotyping some of our peers over in service-land, the code was apparently written by at least one dev with a Java-esque "there's no such thing as *over*engineered" mentality, it was extremely difficult to follow how the types were split up and why. 

Use the same restraint you would in refactoring code: follow [the rule of three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)) and [prefer duplication to premature abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction).
