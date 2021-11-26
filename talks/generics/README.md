# Talk \# 4 Generics and Utility Types

* [Playgound](https://www.typescriptlang.org/play?#code/PTAEBUEMBsGtQMSgCygOIFMB2GBOBLAYwGdRIsATUAeQDc9oB7SC4gKDZFAFF7cBPAEaMK-AOSkAYpFqMCAFwygAklkW5a+DAHcIjAA5EAXKAAy+LLAxVzxecQCEHQtEjFSt+QDkRSgN5soEGg+gCugtBEoDgAHvImnj4USgA+0aHQ0IHBYRFRtDChGCZYoQC2gngcwaCEjFh2uKGE8nKgABQF0EUl5ZW4ADTRGHEJ+HZJqemZoAC809AAlKABNTXyABbjAHRdRXOgexjZa6CbO7HyB5cnoAC+bA9sLm6kAMoWAObQ-OaW1p4VrdcpFCKANhgWGMJr5QGlSjN5gisrc6g15E0Wm12ttcVhfMRod5fABtAC6y1Wp1q9TsoBJADN8Lg7ENcdtcBg7GTrgTbjV8AyOkyWfJKfzqediNsISwDiK7BLTpy7NsGXJuJBCBt2vjknMAHxnLbSlgUXW+RaLJX3W53UDVYIAKhJb34FUY0G2+HUkFauB57XF1NA0AwV1lFCJkzhCwOUplkIoNu0WzDHUjwZDwX4WmgVEjNpqkYOke2NxDDxDuYw+YWdsdQU+4bOkHw0A6ixMHyw31+FisFEB8IyHapp0FHQTkYA-OWRmKgdngpz5KFcFhhroe32-oPPO1p0n53FrZXG2tV+vN8iG7czR09cUzONickuy+Yfrx2tJ+0HEeLBZsugFUEivg2vatbEP4RbBE+J5XPMoGQReNRXhu0QQTUTw1MkYaKI+0aWiYsj4FQP41ARIScrQ1yjja6q4B01FPqAjBClKwHZn+bGzPxCzLIInKQLAcFBLxsL8Ui3HLhJQrtPotHLEpGC0IhvLJIh4lrMJkJiXJtqGapdHgckqE4ReaLyG2DREZ+b4YB+wiepCm6UcETEsS2bEcca4yydSkn6tJgmgBhm4MjAME6cFSihVggXLhFZxNMchlVtSuHUilUXQDBoBcAAUqEdKtGQ+j6JCBWbEodRlIYYaDKA2hKMQGyMBkFBYGIVxamuMA-KAlRkBESjlSJ2r+ewllPFw1DwK1Yj0KAnyMFcpQVHg0qgG8jBYboBGkNoChKINxp+uxoR9Z8tmgF5jRfMQAycGALlhuQz2gOGhDbKAABK+CfBs8gzqAACqZRDD4f2qKARUyG4hAEPoVyppdS0rTAImiC1CiKFgr0tZ1dYjdgnXA0MtWchIWHnL2o2dRtfTbaAFjGkoTp1MkTpDPUQ3s7VRNOvI-BVcQTqgAAQtdbNCso4IyGdDnsUKj29l9CvaOQVy1TSDXtngZz7drmFlEogpEwrD6QOkW24H9khyGuWB+rW-BUxCNOkLbxCetd+D1CYzY4AQJCgJI4AAOrOK47jS+G6iTAAPOARp+IVYBeNQ4DcBzEASMC4SgsMowJ-ISe+KnRojpkRd5GCRwmOAVm0hizT+h0TcQEMlwmFLid4Cnaexsi9GZEl027IU8WHDPNoJpc1wLg2c1Z+t40bJdAAG4Dby17YdiNnz4PQm5osj4bjWLSj1KApUYEM5BUOAby1OQ31n2zWAMkbPpGM4NuoBiB8S3OXSuyR2hiC2GIZYmdgEYi+M8IBWBQE4F0APCuQ9fDtAAKxwOCFwTa-QOBcAAIKUAOi1OqH9OQnR9LfdcDl2Sx1eOAvAe4ASvmrkuHIxcoiRn7oPXAw8a5xiRAxVEbdMSdxxHiAkQisEiKrmnckk80R0kZMyVkoB2QqnkDyMyXIbR-gVIuDypxQLym0fIHS+i1Qai1DqPiRoExmgtO+M8WU7QOluC6N0HovQMNwH6OQgZJ7UUEew5RyQeG1w7MhE0iYWApjTEodomZeHLhrHWQshkSzzDLBWbx1Y8xUFvJZW4zZdZtg7EGRR6hOFDm4SPeJWTfwKVAnOS4k90LhmvGAzBjSBxcLsNXQ8SSikLi8acbKyp+mYQqcEOZZAKBUA8c+IZ2DYlpw-FsmJGAeEWLlh0ACkyky9OCFYoxkFvr5VgoZBCS9Ek7Dyd4m0KUnx3jwrWK+9l9miI-GRCiNpqImXHlkEMXl2isVhH5Li7SQxxTmAJZEQkRIGTksihKlyJwKRMri6kJkNJGO0oZSy5Lgh6VEjpTKy5wU3PPJUmo1lbKkF1A07ZhzdkmHem5RFnlsSwv1PCk0hLsWotHMsXK0V0pYoUnxVFhK+lrkwu3OVy46VrBWSqgZeUCrFVKrrfakBKrVU3nVRgBsmpDFasAjqXUep9RaKEQa-BhpnTGsbcKkIppSlXqQ9ehFNiXTUngd1+hXCECUHazkv9ORYGjVdZigJn6gBjKLcW1DFYrXKvoNhetM1KHzSE826hthEyjjQzc0V9pc2kbZSWIc8BEC+n7C6usITurKEaj1+t83yHwF67QPoNhkGAVVQggoohFoAWwCw6gopJuUAANQwFiZiP4Yi9HtrcfgO6SFPAXXgJdShV3roAMzfTiNgVgKg10bvaQALwPVUJ4DJQiJsHXfGyVhiAPtTtegmd7z0bqNJ0ddzcgWMHIisNeoAq3vxrflfaFATWhnWqrfOxBIDm38hrbNaGD6bDnt0Lkc6P1fsDpuapD7-QAGErX6HqNgeQgGFy3tIKB-0QwADSQHOOgCsPwPyad2jCZMLxoY9BCBQebiSXjPIfwpRkySYTZJHgcEoy0ajhx13mCsNQXAdG5DsZvZQLjJnmLzG43IA0EHZMQGg7Bvw8HTDhlIBid15Ui3jt-vIKanIACORRVS4g4G4fgib7qfp03fape0y1bF7OM9c0ATDq0+B+AACrgK14xuXpykeiH1xB9AHEgNrH090fo6jSzMk57QVT6G2HYP0pVQBGgvQATm63CNIzXWs2TXKQZOoAABMAAGSbk8UqDcUHEIMPjoIPOpBoq4FA-S23mJVtsVxBsACs-ZYCWyGFKm2bIBqJtQAwjgIAmkVmauyqZsCgBE6EVK3n9opVthfVc18qr3Ty2UPzsXv2bhDfthZDQia22bWHP6iHCAfyZDEaawD8ANSGoId1FgXChAoF8fOf2-m+cFhCDHnxXaquKBF4gUWwTafB6tcMiXwzJc+ON1LuB0sIIIL2HLwOCuAbSJlorLKgHNYq1Vq4-ntTtHq7cP8g22sjc66AHrfWUgDa5C11XHWxtTZmwKoIc3dfbAW-IU7yy7kFWOet0AF3ttkBl6VlrR36jW-maqzcTurvzVgJAd1dRPR-R8LoSH2at4rT9nh8ikIsPw9bUMI6GHGDwEurH9nRPI8jpmB1KqH7Mjupw-QImHXzq2yYFcPy+aLCeyUIIUI7YrjswDpEUWZwb53fc-YYBQeO3Zu1mob1ZRRLKyZ7pyPv7jFcF+3HL6aas8VSUgYAgbsyC4E+OUVji-KHrZkWQTcFg2uJtvpxCnLx3B-TZ+cDYDNIhWGmrDl1br354dCOV9m3Ayt4B1owP6AACUYF0CIztSI0hxnA4F83o07iRB0A6HZEgC30JCP34DUUNDgzYBgIbQsGsFgNM3AAOFcyNHgN0DkW2GQM+FQPIHQIpEwJbjYEnzvjHz-VUFP2jTM2A1IBIPaGyHo1cCfRfVAEY3RBCTwIoAINwGrheiCCQJQJMFEMaA7jkGy2QNwyvhZGTiUIxFsnwP9GrgNDYA-HYJsjP3ABvm0NwJwEkIMLTnFx9R9zAQEMgCEIoKoOIGtCeCv1IDIV4QPxUOYkUn4TBG3Ttn6G4gTDR3mBiGyAeG8KAXVH2nmFYK5FMPIGjXaDISGAvWtA0Vcm2CYE+HaCSO2BiGtCAA)
* [Documentation on utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

## Everybody's Favorite Interview Topic: Linked Lists!

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
        const [first, ...rest] = nodes
        if (first) {
            this.head = first
            rest.forEach(node => this.add(node))
        }
    } 

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

        return null
    }

    add (node: Node): Node {
        if (!this.head) {
            this.head = node
        } else {
            node.next = this.head
        }

        return node
    }

    delete (n: Node): void {
        let prev = null
        for (let node of this) {
            if (node === null) break
            if (node === n) {
                if (prev) prev.next = node.next
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
    public head: BetterNode<T> | null

    constructor (...nodes: BetterNode<T>[]) {
        const [first, ...rest] = nodes
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

        return null
    }

    add (node: BetterNode<T>): BetterNode<T> {
        if (!this.head) {
            this.head = node
        } else {
            node.next = this.head
        }

        return node
    }

    delete (n: BetterNode<T>): void {
        let prev = null
        for (let node of this) {
            if (node === null) break
            if (node === n) {
                if (prev) prev.next = node.next
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

Note that every place we reference our List and Node types we have to pass the type parameter. We can also *constrain* generics, so that they must be compatible with a specific type:

```typescript
interface IVector {
    x: number
    y: number
}

interface IVec3 extends IVector {
    z: number
}

function takesVec<T extends IVector> (vec: T): void {}

// We can also do a lot of the same things we do with values:

function getVectorComponent<T extends IVector, K extends keyof T>(key: K, vec: T): T[K] {
    return vec[key]
}

function vecLikeOrVector<T extends IVector = IVector>(vec: T): void {}
```

Lets try to type the response from a fetch request...

```typescript
async function getSomething<T>(url: string): Promise<T> {
    const resp = await fetch(url)
    if (resp.status > 399 || resp.status < 200) {
        // Error! Type 'string' is not assignable to type 'T'.
        // 'T' could be instantiated with an arbitrary type which
        // could be unrelated to 'string'.(2322)
        return resp.text()
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

Okay cool. Now that we have some idea of generics, lets look at something that will hopefully save us all a lot of pain, the [built in utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html)! Lets say that we want to make a function that takes a class, and some appropriate arguments, and construct an instance of the class. Somethihng like this actually came up in Esperanto. How do we do that?

```typescript
type Ctor = new (...args: any[]) => {} // NOTE: not a function body!
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
