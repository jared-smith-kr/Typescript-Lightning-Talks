# Talk \# 4 Generics and Utility Types

* [Playgound](https://www.typescriptlang.org/play?#code/PTAEBUEMBsGtQMSgCygOIFMB2GBOBLAYwGdRIsATUAVQBd9p9aBPCZgBw2IChuRQAogDc8zAEYB7CswDkpAGKQhEgrQygAkljW4h+DAHcIE9kQBcoADL4ssDFWvFaxAIS9C0SMVKPaAOSl1AG9uUDDQdgBXMUZCUBwAD1oLXwCKdQAfeMjoaFDwqJiiUCEYSIwLLEiAWzE8XnDQQgksJ1xIwloVUAAKUuhyypq63AAaeIwklPwnNMzs3NAAXgXoAEpQEMbG2gALGYA6fvLlkrKMfO3QPcPE2lO7y9AAX25X7g8vUgBlGwBzaDMay2ey+TZPQqxUC7DCQCjTWaBUBZKqLFaovJPZqtWjtTrdHoHIlYQLEBH+QIAbQAuhstlcmi0nKBKQAzfC4JzjIkHXBcWjUh6k3kYEScjA9NZPRr4Vm9dmc2h06UMm7EA4wuGnBVOFVXPlOA6slQCSCEXY9EnpZYAPmu+3VcIolsCaylDJeT2eoAa4QAVJTvsxahJoAcmHhIF1cILJeCPdAMPdNfCrDMKdaUTloKc1RrYRQ9aADPtE70U8qPY1mPpoFQU0XGinTimDo8Pa8PTWMHXVl7fWE-knrpAGL01hZflgAUCbHYKGCs4t6VdZb08ymAPxtyZK+NVsJ82iRXBYCZGKcz4Hz3w9DcFndJd0M94eo8ns84C--QHX0HpyV+yeJ1eitCo00RdIJwgjNgiLMDH3uFZ7zhABuIsUKodFAnQt8kw-eIcKAxp0kTNRQPJOZoOUfAqBXbYyIiPkhAebMi2NXBekYsDQAkOU1UrA9QDXF1rSWcTVg2MQ+UgWBG3CESePE9FBKEhS5R6dhmNUtTti00VEKFdJENw3Swm9HtiDgsyrkwoyMEQ+Srk7GzpNhOS1Jcg99JY7D0iLLzPSxFpaFHVoKJgqiLEkUNYTPejGg4rjhx4vj7RmHSPUUpFlMk0B31PUBWRgKynOEjSlIkrBMqEgqz1xcoysCxpXwZOqipK9R+AAKUiZkujIdhOC8dQ9nUZpqlMRMxmLdRiF2CQcgoLAZHuM1jxgQFQDqMgYlGiR8thc10p4Fq3l4fgAHl4AMDAZBEUA-gke4qlqPB1VAb4DpJIwyNIAxVHUTb7SjXjIjWv4wqK7o2n+YhRj4MAYsTch4dAJNCAOUAACV8D+XZaE3GhqnGAIsa0UBuqULxCAIdh7hLUHbvuoHoBk6Ri1UNQsER4tFt7HbsEW-HxjGvk5EIm5p12xaXuGd7hPqmFQD9Zp0j9cYWi2mx7Qufg-RYThiD9UAACFwfKzRoSUIGYN4uVYenNGNGLch7jGxlJoYPBrgOgxIEK6p1FlXmXZAyBsje3AsfkFRjywKMe2YUWYXF0gI+IUNwfwFoLCHHACBIUB5HAAB1dxPG8M2kx0OYAB5wDtIJQH4PxLvAARdYgOQIWiKE7gsU2a7wevG+RPtGkhYpjnA8AB0ZHE8WjXoZ4scBxgH6vaFrwIG7tJcc3RbMarCPMZ9OGeMIdQz0V3ft3lb57Rt2UGAANwFf4sGBzHa-nwEQzzYlpkmUaHB1AtFAH1DA4xyBUHAN8Jo5B0YAMVqyH2TAzDuCZPcYgSlzxbx3ukHoMh9gyA2C3MAjs-gfGwfEPBX4CEj0CD0AArOQ8I-BXojAumAAAgpQQiRhbqILPHyAGEYwacV8DyCuXxGG4D-AudMe99xhCnnEFMg9h64FHvvVYrFcjz2xG0Doy9CTElJFo7eTD0h7xpCfBezI2Qci5KAHkBoBT2XVMxd6Epnyrg0jqPcCVVTX2bCsIJZUPFGhNGaC0Sk7R5idKJDAboApeh9E8AMQYQxhgjLgKMKhYwOMYpo+Rujx4YlzGEgsRYSze3LAWBx1Zaz1lqWpcJ0IHzthfEWbsvYMTEXCEOd2o4cySisToRRvgVEH1UdsESmFtx3GaeEdqDCh7WIUXOf8Tg953hqXCRC-jtitX1PhQqGztHTOUY3QCZ1gIUCoCkyZNiMB72gpswh7yx4hLCAhO41TDgplMrZQ5WFCLpFBdsdZREHkkR7CAiKXy3kfIsDROiRZGI+QMXkD0SUejcSRGlAS8ysoVRylVY+20ZIeSEtlMSVVVkBN6D5ZlVYfI30hQ5O40LPLo2gFZMlNk7J+R5XfGynpJVuVkk1MqOKxXpPheEbEoUbCkEtK8nRu9G7QWRnFYVYQCVEutCSh07KGXqFyhiDY7ViqCouGpS1ywmWGqrO1BqjqhLNXCGcmFFyzz2tKmdB+YAAjkT2KDUUogIieEIOoYRfI0F8iwPGyRdtYGgDmNcMB-11AvwegNdgciPaG3UMWgpQcdAHF5qXcaSCSoHVVtggpNgTb5zwEQNGmcQbuxhKwaofV7g7QmsW+ge0v57DIKAYgnBCCymKGWzB3AbA6GKmmjQAA1DA+JOL0QSEMKOTxmCHu4e8VdeB13qC3TugAzOjJI2AKCkBvbu+ZAAvU99R3iskiKm+gEDQp2GINuwgDcH3c2fZoUD0Y7R9B3WvaiEhaKbFDaAOtIiyCCoOhQA6EdoDPXtl3YgkAg7pSdrNUAuHJ27DOAMLgy7f3-pzmeEQhBrB2EurgGDKhwO7ifS+njnEVivtg-BwgiH0XIbomhywSZSC4lYANMt060G0GOnyAAjuUQ0RJeBeGYKmoqf7OgscekmL6Vb9jTn2SeaAFgqHQQAAq4AkNUGYPym7BRxIdWdpxID+yYEVDGFo7MnJEgadgBwnBRj6qAO0t6ACciXkRZEi9F0Kx5SB11AAAJgAAz5Yce1dLagkj3N9QKoVfzHH3AoFGCOKwAujnuOlgAVpnLAFXznHkKvV0K98eGgEuiYVwEAHTWyGtgf6MIzzMEWtcXASmDrtQjkAo8oDOBFVc9UVTJmANK1BnVHg-AI4dsLljDDhAkHsgSCdGd+BJpbTEKwGwHhIgUH+F3dbSKVM6w9sQPGCdesVH08QQzcQmOmYgSMyzSZrN-Fy7Z3A9mZ24n+M5nbHnwNZCoV5xoxjWtcHYP5wL9w1Pmh6GFp4EXicZdi6QBLyXUu+aizFrLoAcsFaK26krdOyu0G6y8Kr1kGSE6ow10nLXWcHA6y0IXjR2r9cgIN3m11ICsGaKGLGAQjCRoZvmm2M63PB3SBHNK52u3jD+qAAjEh4Cg0zlZr7+uv6LAWpwX9uRWAkZELzOLwN8OEbSsWmwKd1BiEiAwe4Ots6MBYDmo2LgrDyZnRr3tlH-baF9qAaoslbZQ4OxnoDXBeZrcrmjTNTugZDVc1pfAicyC4D+DUbAzgYECMJ0vMgZ51WhVTeA-iytPjeCxnDm4uxpaMDsCdMvnRIibU16R9QkQSc6wELOyM2gJBYwABISCMNR4R1H9ebl4CpgAwsvW+RhzEHADn8MkPfmD2NtM-2RVdeH7i76Ygk6jQAHqRwjA6R5h3YrAJD5CvA-r7ZmaR4MAUBaAxYD58aPqUCkBX4qA2g9BPAX5rwIyNA8gP5P4X4tq-64BOYBzL46DEAqL8B1wAC09BWa7cAgFgx+tEK0VGGA7IOAoAJBi8ZBFBlaICnI3A0EiB-e8a4AYCKizcFCnOjBbiRI3QEh5AUhYCTw6yhgfBd+RBUo7w4ujW20UedYqhA+PQvC4wt6Uo4uYgpwcBphOIahEolhoAJC+AZCNCrQsUBwBGfwPQkABwCQUota9aZ4jatWra4RkRZBxuGeQWL8CmB0P+nQPevEYgbWO69waUEcFa9AhAOQAcM6L8nAmCl+LaYU9gGBuA4GKwQQzwdoN+vQhBzeT+5AL+tIb+c8QAA)

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
type Ctor = new (...args: any[]) => any

class A {
  constructor (public x: number) {
    this.x = x
  }
}

function buildInstance<T extends Ctor>(
    Clazz: T,
    ...args: ConstructorParameters<T> // <-- NOTE: we didn' define ConstructorParameters
): InstanceType<T> {  // <-- ...or InstanceType
    return new Clazz(...args)
}

const a = buildInstance(A, 3)
const b = buildInstance(A, 'hi')
console.log(a.x)

// We can also constrain a constructor so that it has to construct an object of a particular shape:
type ConstrainedCtor<T = {}> = new (...args: any[]) => T
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
