# Talk \# 4 Generics and Utility Types

* [Playgound](https://www.typescriptlang.org/play?#code/PTAEBUEMBsGtQMSgCygOIFMB2GBOBLAYwGdRIsATUAeQDc9oB7SC4gKDZFAFF7cBPAEaMK-AOSkAYpFqMCAFwygAklkW5a+DAHcIjAA5EAXKAAy+LLAxVzxecQCEHQtEjFSt+QDkRSgN5soEGg+gCugtBEoDgAHvImnj4USgA+0aHQ0IHBYRFRtDChGCZYoQC2gngcwaCEjFh2uKGE8nKgABQF0EUl5ZW4ADTRGHEJ+HZJqemZoAC809AAlKABNTXyABbjAHRdRXOgexjZa6CbO7HyB5cnoAC+bA9sLm6kAMoWAObQ-OaW1p4VrdcpFCKANhgWGMJr5QGlSjN5gisrc6g15E0Wm12ttcVhfMRod5fABtAC6y1Wp1q9TsoBJADN8Lg7ENcdtcBg7GTrgSORg+MQMO1FrcavgGR0mSz5JSxdTzsRthCWAdpXZ5adOXZtgy5NxIIQNu18ck5gA+M5bJUsCgm3yLUXU+63O6garBABUJLe-AqjGg23w6kgrVwPJFQOd0AwVxVFCJkzhCwOiuVkIomtA2i2MY68blzpq-C00Co8azNXjB3j2xuzoezpLGDLC1dHqCn1jZ0g+GgHUWJg+WG+vwsVgogPhGX7VNOEo6afjAH46yNZVGi0FOfJQrgsMNdMPR38J552kuM2u4k7qU9nTu9wecEevj9TwDxvIRe3braOqaxRmF+kyDsBMJmnOayAdeVzzJeLAANxZghVBIr4yEPrGT7RBhv41MkMaKABiYOiYsj4FQUE1ERIScrQ1wzlmeq4B0tGAaAjCSoqhZbqAC72maszCQsyyCJykCwJWwQCRxwlIrxfEyZK7T6PRilKWsakCrBvLJLBmGaUEbotkKm5Ges1rpqq6H6fWFmNhZ4mQlJSmOVu2kMbZxwNvhwRovIvYNCR4HEskYHCAGkIHtRwQsWx3YcVxVrjBpzqybC8miaAj77qADIwEK0lBBlQkiVgaV8blB4YkUxUur5WbVflhVKFwABSoR0q0ZD6PokJmZsSh1GUhgxoM2ZKMQGyMBkFBYGIVyGruMA-KAlRkBESg9RJRopewNQPE8XDUPA2gYGI9CgJ8jBXKUFR4EqoBvIwuG6ERpDaAoSirVaoacaES2fEF+VtI0XzEAMnBgJFMbkJDoCxoQ2ygAASvgnwbPIy6gAAqmUQw+CjqigO1MhuIQBD6FcOb-edl0-dAEmiNmCiKFg0PZrNrYbdgs2Y0MQ2chIuHnCOm2zXdfSPfxNUQqAnp1MknpDPUa0WFaxxcJ68j8P1xCeqAABCgP8ZKyjgjIP2hZxkrgyOCMW9o5BXENNKjX2eBnK9zt5WUSgSpzFv-pA6QPbgKOSHIu5YKGLb8ILELC6QofEAGgP4PUJhdjgBAkKAkjgAA6s4rjuMbsbqJMAA84CWn4oBcF41DgNwmsQBIwLhKCwyjBX8hV74teWtOmRd3kYJHCY4AdjS6KYmGHRTxAQyXCYRuV3gNd18myKMZklVBGmRwHEcKFWZc1zru2x1gD4xGbP9AAG4BP9mfb9htnz4PQB5opTsZtp6yUPUUAXUMBDHIFQcAbxajkERr-WWDIvbBiMM4WkVxiByUPP3QeyR2hiC2GIZYjcwD20+M8DB0RsEvlwVvXw7QACsJDghcHuv0DgXAACClA3qTTgQeTkX1gwgL3KFdkpdXh0NwB+ScX5h7mRCN3KI8Z16b1wNvEeKYkRMVRBghe2J2SAUJNIzR5JD5zzpIyZkrJQDsm1PIHk3klT0UesKW884VLqg3LFU4qE1Q2PkPVBxup9SGmNHJS0aZbSCQwI6LM7l7juluN6X0-pAwiNwKGOQEYLG0VUaYoeO9R79nglZCszocye3zBmCxxZSzlgzPVas8xaz2VOIk+pLYqDIj8p2bsgU+wDjUQPPAsjPAKJKYo8UKlUKrkuHU4IzVaEb1GTI8cn47DDwvOUq8CyEmzxqMsnQ0jxnyLrj+Q6s9-yxJGXgjAw8wKrPuQo3xuE7LrlTLspC58dgtPeRgQyWpsJ5UAkCl0txCKAJCs8+hyRHnkUYJRaZwRaKeX3lkZ08V2jsVhMlHiKLPEAUyuVGcYkJKuT4qVJQWUKqEqLAJTyiyPL0V0t5Ay9VDqI2gGZN5Sl-HsvaZpTpfFnKSXqiK046LvIHKuXotQQVSAmjuXCh5dcIqMCivAt52LcVmnxdaZlZtiVlR0QfHKIKDwFR5T5KlKk5LlSNUcy1Zwmi2q3JKiFWFdx5WtUVK5t9QD322hsf6Ao8D8BCK4QgShzoWuQZyLAMaAasUBFAoNsJdb634aGq6PV9BSLdlmpQBasn+3UNsDgFh1AFWTcoIuobFB8FecCXABhp6PHQeibMjbw24BMPW3tzb2F4EtPMBual22gAAMwQuLaABtcd6DEAUeO1tU6Z5PDRHSWmTauQmEXXuldI7cBjpWHRKds6ngMlCEm+QmcDyUWwPe3W2yYjTzAuARRzUYidsod20NxBwDAMkD-Gl-FkhqGDPwJhopt1xjcMB-qXhpasXmE+qDr6T3mlg12ukalq08IoKjF18xa4DBw++iAn6LSKO3VFbYTBPjtBiB4i1PqDy-sDUXYa8DCqvUVvooKhsc54CIAjNOf1XYQkjWULqVwNojQLfera79NhkFAMQfqhAJRRGLWgtg1a8C1qUMoAAahgLErEoJUZPbcfgvRw5-qM7gEzKgLOEFneubArB3OWcXlBAAXo5jh17b0tAfT2KwxAPO10RnEHzpBzP+bkJaTolmP2IuRX4bjvGDz8dABQV6ocmBXANVNSA-sUoO34UVtTGxDiFH3RwG9d7Iv0EIOYKw1BcAebDHF7zlAkt9baPMZLVmcMdcy4cJFVF5V0gbjEIYka3TzA67cASYhAtiFlocSzcob6cLAKYWMpAMSRp6vO0OyD5B7U5AARyKDqXEHA3D8CTflcL97QFdnkC9ctWwRzbL3NAEw5CwIAAU21lHGGq+u82rjan0AcSAztgz5SRsaEHbGBJI+2HYUMXVQCWmnQATlJ3CNIeOCe7lINXUAAAmAADEzixzU8eKDiJc4IJkbX0vg4V0Mod5io97Ijrk+htgACs05YG58CjjgvAqHc5tQAwjgIDWktn1bAn0IQHn4LNV1F3XrNVDv-HcQD+r5Whxp1rEXQGP3Fxx9gXBQ6ibzijHjAj8r4BiPtTT+BRprUEJGiwLhQgUC+O3C30L50azdsQDGscfXFFe8Qd7YJ7ffYPL9-7sZAefAZ8D3AoPNMYi+JD6HsO4tpHIfDmoAukco7R1cG7Rp2jY42ypangVafE5neTynFqtP4770T+nzPWf0vZxL7YnPvxsd57yrMAuKBC5b2LkfkuZf1Hl2sZq6-lcBqOzQWAkBI11ADCjHwugnc5qtppxgVWn2h2Sh78TQwPqgCYIweA-004Ado979tAP5wQDAMAb1MhI1iArZOYidfoStbpbYQggpE4lBBBQg+wrgNYM5IhdYzhgENcTt7BNML8pN+FnY1BvZQAyhJJrZs9It79ApotOZzcy4EZ01ACfo+o20CM44yBcBPhyhn1ODeF4MF4yBH10RyBk1ytagOCUZ89zgNhxZIgrB9o2CWhQhVpL9KslBQhkcNZuAtM8AXZGAUYAAJRgXQOrONOrJ3ZcDgedAAYUXiRBORxFxEgCEJMXIH4HMVoxyzYFcKEwsGsDcLkDi3HTuDPVoS8O2B8M+D8KwACIpFoxnjYEYNAToOi1UAJyTTVXi3Zl8xyxw2yBcNcEC2C1ABcLCJwAoEiNwGHihiCHZCSJMTqPnmaDDAhx8P0PUBXS6MaCCgiP6zrnNDYDAnyMCkKKQweWGIxFGMaPGPNAb3YxwloUqMgGqISI6NFC3Q4NAC4U3AkJ6OxBBCiFs1Qw0jTH93mF-WMj-QFz1FenmFyK5BmNkOFC4SGGnTg1pAYyY3aFeO2FYzYCAA)

## Everybody's Favorite Interview Topic: Linked Lists!

![donate](https://imgs.xkcd.com/comics/linked_list_interview_problem.png)

```typescript
class Node {
    public next: Node | null
    public value: number

    constructor (value: number, next: Node | null = null) {
        this.value = value
        this.next = next
    }
}

class SinglyLinkedList {
    public head: Node | null = null

    constructor (...nodes: Node[]) {
        const [first, ...rest] = nodes.reverse()
        if (first) {
            this.head = first
            rest.forEach(node => this.add(node))
        }
    } 

    // If this confuses you, see e.g.
    // https://stackoverflow.com/a/46218959/3757232
    *[Symbol.iterator] () {
        let head: Node | null = this.head
        while (head) {
            yield head
            head = head.next
        }
        yield null
    }

    get tail (): SinglyLinkedList | null {
        if (this.head?.next) {
            return new SinglyLinkedList(this.head.next)
        }

        return new SinglyLinkedList()
    }

    add (node: Node): Node {
        node.next = this.head;
        this.head = node;
        return node;
    }

    delete (n: Node): void {
        let prev = null
        for (let node of this) {
            if (node === null) break
            if (node === n) {
                if (prev) {
                    prev.next = node.next;
                } else {
                    this.head = node.next
                }
                break
            }
            prev = node
        }
    }

    contains (n: Node): boolean {
        for (let node of this) {
            if (node === null) return false
            if (node === n) {
                return true
            }
        }

        return false // Just to appease the compiler, we shouldn't actually be able to reach this
    }
}
```

### Bonus exercise:
Write a implementation of `reverse` that allocates no new `Node`s and runs in `O(n)` time!

Ok we've got numbers. So now lets write all that out again for strings, booleans, etc. Right?

No.

In Javascript what we've already written would be enough, there's nothing about numbers in the *code*, only in the *types* (remember last time where we discussed the difference at length). But we're not in Javascript. We could "fix" this by changing the type of `node.value` to be `any`, but then we lose type-safety. If I have a List of strings, I want the compiler to warn me if I add a number. Fortunately, there's a solution:

## Generics FTW

The Typescript type language (like a lot of others) has a notion of a *type variable* where we don't know the exact type. We call these generics, because reasons. **NOTE:** common point of confusion about generics: when we say we don't know the exact type, we mean at the time of *declaration*, we still have to be able to resolve the type at compile time (remember types don't exist at runtime). Generics a.k.a. type parameters look like this:

```typescript

class BetterNode<T> { // NOTE the T's
    public next: BetterNode<T> | null
    public value: T

    constructor (value: T, next: BetterNode<T> | null = null) {
        this.value = value
        this.next = next
    }
}
```

Note that `T` will be given concrete type on use:

```typescript
const snode = new Node('hi')  // string
const nnode = new Node(5)     // number
```

And now we can rewrite our List...

```typescript
class BetterLinkedList<T> {
    public head: BetterNode<T> | null = null

    constructor (...nodes: BetterNode<T>[]) {
        const [first, ...rest] = nodes.reverse()
        if (first) {
            this.head = first
            rest.forEach(node => this.add(node))
        }
    } 

    *[Symbol.iterator] () {
        let head: BetterNode<T> | null = this.head
        while (head) {
            yield head
            head = head.next
        }
        yield null
    }

    get tail (): BetterLinkedList<T> | null {
        if (this.head?.next) {
            return new BetterLinkedList<T>(this.head.next)
        }

        return new BetterLinkedList<T>()
    }

    add (node: BetterNode<T>): BetterNode<T> {
        node.next = this.head;
        this.head = node;
        return node;
    }

    delete (n: BetterNode<T>): void {
        let prev = null
        for (let node of this) {
            if (node === null) break
            if (node === n) {
                if (prev) {
                    prev.next = node.next;
                } else {
                    this.head = node.next
                }
                break
            }
            prev = node
        }
    }

    contains (n: BetterNode<T>): boolean {
        for (let node of this) {
            if (node === null) return false
            if (node === n) {
                return true
            }
        }

        return false
    }
}
```

Note that every place we reference our List and Node types we have to pass the type parameter. 

## Syntax

Type parameters are defined and passed the same whether we're talking about functions, arrow functions, interfaces, types, or classes:

```typescript
interface IWhatever<T> {
    prop: T
}

const whatever: IWhatever<number> = { prop: 3 }

type Whateves<T> = {
    prop: T
}

const whateves: Whateves<number> = { prop: 3 }

function identity<T>(x: T): T {
    return x
}

const hasTypeFive = identity(5)
const hasTypeNumber = identity<number>(5)

const printAndReturn = <T>(x: T): T => {
    console.log(x)
    return x
}
```

## Constraints

We can also *constrain* generics, so that they must be compatible with a specific type:

```typescript
interface IVector {
    x: number
    y: number
}

interface IVec3 extends IVector {
    z: number
}

function takesVec<T extends IVector> (vec: T): void {}

// We can also do a lot of the same things we do with value arguments, like assign defaults:

function vecLikeOrVector<T extends IVector = IVector>(vec: T): void {}
```

## Error!

Lets try to type the response from a fetch request...

```typescript
async function getSomething<T>(url: string): Promise<T> {
    const resp = await fetch(url)
    if (resp.status > 399 || resp.status < 200) {
        // Error! Type 'string' is not assignable to type 'T'.
        // 'T' could be instantiated with an arbitrary type which
        // could be unrelated to 'string'.(2322)
        return resp.text()
    } else {
        const data = await resp.json()
        return data
    }
}
```

Oops! This happens when you try to return a concrete type from a function that returns a generic. We can fix this simply by including the concrete type in the signature:

```typescript
async function getSomething2<T>(url: string): Promise<T | string> {
    const resp = await fetch(url)
    if (resp.status > 399 || resp.status < 200) {
        return resp.text()
    } else {
        const data = await resp.json()
        return data
    }
}
```

## Quick Digression on Parameter Names

We've all been told with very few exceptions like loop indicies to never give variables single-letter names like `x`, but to instead give longer descriptive ones relevant to the domain. You've probably seen me use short variable and function names in these talks, and probably thought "he's just keeping it short and vague because they're just general examples". And for the most part you'd be right. But in the case of generics, authors *frequently* use single letter variables to name type parameters. 

It's actually for the same reason we use foo/bar/baz for general examples: we don't want to get too hung up on the specific details of something that is supposed to have broad generality. The type variable `T` could stand in for a large number of different types, and any details about what the limitations on `T` might be are easily (YMMV) gleaned from the constraints on the generic, e.g. `<T extends DomainSpecificTypeName>` will have at least the required properties of `DomainSpecificTypeName` and *that* name is the one that matters.

Okay cool. Now that we have some idea of generics, lets look at something that will hopefully save us all a lot of pain, the [built in utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html)! Lets say that we want to make a function that takes a class, and some appropriate arguments, and construct an instance of the class. Something like this actually came up in Esperanto. How do we do that?

```typescript
type Ctor = new (...args: any[]) => {} // NOTE: Object *type*, not a function body!
type ConstrainedCtor<T = {}> = new (...args: any[]) => T

function makesInstance<T extends {}>(
  Clazz: ConstrainedCtor<T>,
  ...args: ConstructorParameters<ConstrainedCtor<T>> // <-- NOTE: We didn't define this!
): InstanceType<ConstrainedCtor<T>> { // <-- or this!
  return new Clazz(...args)
}

class A {
  constructor (public x: number) {
    this.x = x
  }
}

const foo = makesInstance(A, 3)
console.log(foo.x)
```

I won't cover these, but here's an (incompletel) list with descriptions:

* `Partial<Type>` makes all fields of `Type` optional
* `Required<Type>` makes all fields of `Type` required
* `Readonly<Type>` makes all fields of `Type` readonly
* `Record<Keys, Type>` maps `Keys` to values of `Type`, use in place of interface if all values share type
* `Pick<Type, Keys>` creates the subset of the properties of `Type` defined by `Keys`
* `Omit<Type, Keys>` creates the subset of the properties of `Type` with all the properties *except* `Keys`
* `Exclude<Type, ExcludedUnion>` removes `Type` from the union type `ExcludedUnion`
* `Extract<Type, Union>` creates the subset of assignment compatible members of two unions
* `NonNullable<Type>` equivalent to `Exclude<null | undefined, Type>`
* `Parameters<Type>` extracts the parameters from a function as a Tuple
* `ConstructorParameters<Type>` same but for classes
* `ReturnType<Type>` extracts the return type of a function,
* `InstanceType<Type>` extracts the instance type of a class
* `ThisParameterType<Type>` extracts the type of `this` for a function, useful with e.g. `Function.prototype.call`
* `OmitThisParameter<Type>` removes `this` type from function, useful with `Function.prototype.bind`
