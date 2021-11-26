# Talk \#3: Types vs Values, Enums

* [Playground](https://www.typescriptlang.org/play?#code/PTAEBUEMBsGtQDoGIDMAuCBPADgUwM6gBuhAajAK4EA0oAogHYUC2+AUGyFnoUaOdCr4MAEUgB3BqAD2AM1ABhaQ1kV8AS2UcuASXmZpFUONwAnXMdPqALuoYBzUJFABjac2zroZ0LOmnQAClIIkh8Fytsa1oAC2lxY0NoABNQAyNrc0hrUGsY9XwAfg5vHPx3XDy7RwBeUBQ2dXkACnLmSvyHAEpQAG82UEHQLmTpUDaO6rYAX20wACVcduYAIx90p3NQbFNpFwINB1yY7KdCACprXAAPa3PaSAZUjZOiC2sx2XV7Ci3DHPEJxyH1Ao2onDAGxcjwA5DkAFZqHLQ6DQUAAA1woWg6IAdKAABLxRIUFJpQygcwRXDZd4xd6mCh5TDAWQwfC4TCgdouE4MdQuQhyCFBEJhCLqKKgOzjCoyPI+aCPH6Qey4QqgADKY3pWxMoFedIsbgY+ylcicoBW0mk3keoHOJqut3uIsBZiNxEoFhOhAm4zwLnUMHG335X2hposKzCuFSyml1guzusFBD2GkGlsCZlCtlv3251xc1AACEmdKpOAcAQJVL9YbQNAbGYQ9Ya-haOUHXn8JB2tLkrgGLYvmZCI3kk1ZB6R9yafyHOwuDGOfGpO6FQEFZgYVtTs5sEr9pXju8bgDdRZnO28NykaB7GNHqk80fICf3eYRdIt9tIKYSYyPIeZKg4aZqo+0hFhA+SEJGVoWOc+AUHgpjnK4yiqIcjhNOSRijAwcLHHY8CQNaFY2CKzawNemEeF4PjiFYVymMWbC3hYACCoB1DCkAwkMgxcHm-GCQUlqXDW5xsCa+A5JAGA8XxAnDGAomqRJzjnNiVAyRxNagAAYuoby8aAACsBl3gAqk8uDyHUFD2V8DBxtZFgAHJeOZTCoh5ECMhYdSZFQHCcYSYQmWZdT9EJfjSBgVmzCKnm4qW+L6pGxFhBo9hSFUhAghMVRHHkpy+rkhkElFpm4LQuIJQ6zBIhhayWbJyjyaA1zmXFQwJRgABsMwlgSHrHIY9gxImMKEAwv5OC4qYwNAXLlTkJymK+YxXKiZ6gtOs77LQNiPpUE4AUOphuvSG4WPJAE5HYzaLo48kULIshoBwqimtmUiyM0-VNXUFngoMMYBHx+QwhDVqQAAXuC0wYAACk9wbQAAPCDNpJfDUMYDCsOE0jGChfVMwAHx9dMPQYCD6jqATAygAAjhQ1zE-SqLSIJAA+oAwuI-gpHDMx9Gzck5F86jmU1ACENROS5dhxqAGpNUl0tdTknO9XUUO8SroDOUOrkawAZFbCOI5rwu89A-OgMToumOLbPmKmphSP1gxy-DgwG2z0ygKNIrgEC3KQFyzCQLR+HGI8wJjNgzm8sYcRYkxLEELK7SlY4NF0hJMo7NIyQUMtmgMCKbhDrQKyUdYc3bGYM7LWtXrNqkL7SqiSKmLSE7EvgmAjh+tguNsmY2LXMfWKx+DFlwADq+TM8zmcrFYS5m4QMYuPAILopxcjor4uzME2YTAuo7Q-Z1DDdUXfVs5DAEYA0KURVH1RR1wNWO8gwQo1gtG-NSsEkKcQwr0BGphv6gFmDLWCAD6QCCoOZc+IFOiOCgYAh08k972AwjCaQKx4S4GWjCEsSgVBqAXtIN4ARNy6gLpMI4Wkqp3n8JaXSFgJLKAsBA+kJF946HGLgXAP4WFOCeDIORCZNTWA-PAAA8iw2QztxD4gAJoUnjlyRsHJhxng5PRZgCZgG1kiDkMwuxTDLkhIYJxuBoDyBlOkAI8QpAN1wE-LgMIjI2kEsobu5gZxONyM+Hh9UrSUUPrgaoB8NZhH4d6A0HoRTBNCZSBy44YkZMEPE5uz0kkpLUGkwgN5DJXnYlwcswIxFWL-BaVacTiArx7lgk02EF4STzOiFwSp8D4HRE3ahkAqmuFGRyZxTgmTuFVAKVaXINAtWgKotyhh8DdwturS0EUNrSiKmIiKoiRGUOoUBb2vw3LJBFCsLkdhHojmDLYMqYiRm5Sfj8sZxkbRS0GOnFYzYZ7c1AEwVYZgOCDBloyZafDmgMAwNCtYpgej+xIivQ2ULQ4R1QYNQFYw6huQSCE6QzQLJdACqWAC2DwHyCalweBkL0U+FmBFel9s6iUqEkJVlPU0UsAxcg5+3VKWAM8v2OMCg5l0GuDsA4C8+VAuEmAf5hBcn8xLDZaa+JCHhK5HJW02QF6SIQnIKJpzjinEKra9JMY+6EDOmqJMDwFF5nIl4GwmARQghmc2ViIYBE1KKh2W15xhz+CsWobuGYTCmFUGifuVSU1FkjtHNYKS+zqGSLQc45xCLEVGDiotT8IoiHUWvcyMJNTm1joLYWmpsi-GSE20AQsYQAFllAdt3FA-u3YtCRw7HWTa6TnD4EDFjTCL9QrLV8Hwh1WY0wA1AM0Kx3VfzsLAiqNUhAy0fGkD0FE3hHlcHtJiaF6In7DhYKANe0jYADuBVqRtmB4atp9gO+Gfanix3hlehRI664pS4AAGXUInLV+csr2hmTelg6Jw1Wl3Ucwy-dnACIeFsuIFBppmwYCXWZuV842DbpAaiNhrDeFmTScwARcxiPKAWCwgIBQzTOgUJ+f0a45nwM+3AtEnjNAHRgYTr7Y5dAwNaW0C4+hQJsmuM4mG7wsYsPxjdeUGBtu-Bqp9d0D4pPtA+m+U6ekWHSDCfayql5x2rjNGA4hY5JKWvsMZpn5wwsQV7So9yyw2jtAwcTscTZ1CkwO3EP723hYFkLN9KtIsvuiw2wDmBaUQbAFxfDU1uMFTgv+QCApSQMuhBYvC06KArA5DkdpUhzMGkszO6hc72iPBSZRwgFcYxgv9SuSorEinx0To8XdPhzP3uhU+l9w5Uj9XS0l2bIm0ufu-fp5bUXY4xc20BiOXBtRNkqG3VRcAnAUWaQeLz+V2hzk06AJrBz+QA3xFxQgkiH5HnUGk60bxaDIeYKhzYMiuDmCaD9vuORGTvPaLQKE9oPyebOUsNTwRQjhDsVZ7ppYuQW2mVs2gTXlgYpqVsewdU64iTEQI4CUjObDlsCGOwVw1TRMeiVo4px0QAAY70cCa1xUwuxxCEH6jZbAtAhhcB5-DEQvipdcAAIzw0gw5aIhmABM8N5jfBiBrrgP8SwGKMAhdkYwOfNONIYd5XOFKHS+rOHIHK-NsCawBvIYu2bBCYABLkdQVdsyMrgZufvFdgE12zHtAFeRS8Mw0QzuIk-DrGFobLoB1EBAWgwAAtByBn7yQwu8IM0GUnHM4VesxSRsII7DzxgOoRGRoLP7W8RyDxPQ+E5z8e4dOVxL1gDDdNx9aN4jjnUbIcAot30AC0zAYYD-DEyTich1G12zTU1D+3mQACzw3-ttcymuHQYRQEv1xeQj8n9AHvtmXBKguGLOnzP4xMjVBXkngXM35gAHFSw8X6nmDrXMGSAlkGB-zrXsHMGHDALLDrTBSoFgOUmFhgGwBOAlnTyT1xC7zeCkGcGYHUFuF+BEVwXeFFnxEkVI2IRSUB3GXbicWUDWTUx3BjkTisS2A5Bfg42M1wFxHsHxGdnsDVAHyKTzFNXoz4SqRdRkGuSXVokwE7ASRyD0R7R7VIENTES+38G2WaRSRBHMBJx8EGWjndDcjkV7EqB-FwXf1tVgAWkkCcHpEgHjBAgfniWVRtWvXM0vhBGcGciYXkGDVbDRDDWLCAA)

## Types v Values: Dawn of Confusion

One thing I mentioned last time when discussing `typeof` was that it has a different meaning when syntactically in a 'type' position. That got some confused looks methinks, so lets explore what I mean by that.

Let's imagine that you are tasked with embedding Javascript as a scripting language in some other system, like a game engine or a new terminal emulator or whatever (the way it's currently embedded in your favorite C++ web browser). And for the sake of this example, no current embedding solution works, you're going to have to write your own compiler for Javascript.

How would you treat this?

```javascript
let foo = 3
if (foo) {
    // do something
}
```

Remember you are processing that as *text*, and you have to figure out what to do, you can't just call `eval`. How would you recreate the truthy/falsey mechanics of Javascript in some other language? Lets say that you're writing the compiler in Scheme in which boolean false `#f` is the *only* value that is false in a conditional, *every* other value (including `'()`!) is truthy, so you can't just piggy-back onto the host language's truthy/falsey semantics. You'd probably create an associative data structure with a mapping between the values that map to `false` in this context and then when evaluating the code you'll have to check if you're in a conditional in the parse tree and look up the appropriate mapping from the value of the node. 

So here we have the concept of a boolean *context*, where the value has some special significance based on its *textual position in the source*. But if you've never worked in a statically-typed language before there is another context you now have to remember.

In statically-typed languages there are actually *two* languages, the *type* language and the *value* or expression language. You can't use one where the other would go syntactically, just like you can't use a value where an identifier would go:

```javascript
var 3=foo; // how many times have you seen something like this by a beginner on Stack Overflow?
```

So we can't say this either

```typescript
const foo = 3 : number
```

But it gets waaay more complicated. In Typescript we have literal types, so *the same identifiers have different meanings based on whether they're at a place in the text where a type must go and the place where other parts of the language go*. This can be *super* confusing if you don't think about it like a compiler writer.

```typescript
type A = 'a'     // the 'a' is a *type*
const a: A = 'a' // the 'a' is a *value*
```

How does the compiler know whether we're talking about the literal string *value* `'a'` or the literal string *type* `'a'`? By what position it occupies in the source, so you have to understand the difference, which I label as a *type context* (similar to the boolean context above).

Strings, numbers, booleans, undefined, and null can all be used this way:

```typescript
type Five = 5
type Undef = undefined
type Nil = null
type True = true
```

and of course so can object literals:

```typescript
type HasFive = {
    foo: 5
}

const x = {
    foo: 6
}
```

In a place in the langauge where a type has to go (type context) they have different meaning than a place where syntactically an expression or statement is expected. N.B. that we can't assign `x` to a `HasFive`, the type of `HasFive.foo` is *literally* `5`. Here though it's not actually that hard to tell what context we're in, it gets harder when we start inlining stuff:

```typescript
function f({
  foo = 5,
  bar = 'hi',
  baz,
}: Partial<{
  foo: 5,
  bar: 'hi',
  baz: true,
}> = {}) : {
  fii: 5,
  qux: 'hello' | 'world',
} {
  const fii = foo !== undefined ? foo : 5
  const qux = bar === undefined && baz ? 'hello' : 'world'
  return {
    fii,
    qux
  } 
}
```

That may make you want to punch whoever writes something like this in production code, but it's perfectly valid and illustrates how syntactic position matters. Whiiiiich brings us back to `typeof` from last time:

```typescript
const foo = {
    bar: 3
}

type FooTheType   = typeof foo  // The *type* { bar: 3 }
const fooTheValue = typeof foo  // The *string* 'object'
```

Confusion over whether something is a type or a value is one of the things I see over and over on Stack Overflow. You may have seen this common Typescript error yourself in your own code:

> 'Foo' only refers to a type, but is being used as a value here

or it's twin companion:

> 'Foo' refers to a value, but is being used as a type here.

## Classes

But the mother of all type vs. value confusion is the `class`, because classes automagically simultaneously define a type that is the type of the objects returned by instantiating the class:

```typescript
class Foo {
  public x: number

  constructor (n: number) {
    this.x = n
  }
}

const foo: Foo = new Foo(5)
type Bar = typeof foo // { x: number }
type Baz = Foo        // { x: number }
const FooTheNamedClassExpression = Foo   // class 'Foo'
```

Ugh.

The only consolation I can offer is that this is as bad as it gets, and the ability to use literal values as types is *enormously powerful and useful*.

So at this point I'm going to drizzle a little opinion sauce on this otherwise fact-oriented talk: be very judicious in your use of inline types in function definitions. It's not the end of the world, but as you can see above in the degenerate case it goes ugly early. Speaking of things you probably shouldn't do in Typescript, even though I was just praising the power and usefulness of literal values as types, **don't do this**:

```typescript
type DOW = 'Sunday' | 'Saturday' | 'Monday' // and so on
```

The are two main reasons why. One, it slows down the compiler compared to the alternative I'll show you in a minute. Two, and more importantly, types have no runtime reification. Instead, when you have a enumerated set of values like days of the week or months of the year or reducer actions or states of a FSM you should use...

## Enums

Typescript has a special construct for this situation (most other languages do too) called an `enum`:

```typescript
enum Weekday {
  Sunday,
  Saturday,
  Monday,
  // and so on
}
```

Like classes we can use `enum`s as both a type and a value, although unlike classes it's a little clearer in the source which it is:

```typescript
function isWeekend(day: Weekday): boolean { // Used as a type in the function signature
  // When using an enum as a value you'll pretty much always be accessing a member:
  return Boolean(day === Weekday.Saturday || day === Weekday.Sunday)
}
```

Although in this particular case if a subset of an enum has a special meaning it's probably better to make another enum:

```typescript
enum Weekend {
  Sunday = Weekday.Sunday,
  Saturday = Weekday.Saturday,
}
```

So let's talk about that assignment in the enum definition. As I implied above, `enum`s are reified at runtime, you can access them as Javascript values. By default, enum members are given the value of sequential integers starting at `0`:

```typescript
enum Weekday {
  Sunday,   // 0,
  Saturday, // 1,
  Monday,   // 2,
  // and so on
}
```

You can also start the counting at a different number:

```typescript
enum Months {
  January = 1,
  Febuary,  // 2
  March,    // 3
  // ...and so on
}
```

Or non-sequential numbers (in which case you have to initialize them all yourself) or even computed values:

```typescript
enum PowersOfTwo {
  Zeroth = 1,
  First = 2,
  Second = 4,
  Third = 2 ** 3,
  Fourth = 2 ** 4,
  // etc.
}
```

Or strings...

```typescript
enum RGBA {
  R = 'red',
  G = 'green',
  B = 'blue',
  A = 'alpha',
}
```

...or even a mixture of the two. I like string `enums` personally as they make more sense when e.g. logged to the console or used as object keys, but YMMV. The important thing to remember is that whenever the set of things is known ahead of time, prefer an `enum` to a union of literal values.
