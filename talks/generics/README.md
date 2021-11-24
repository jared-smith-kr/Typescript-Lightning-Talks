# Talk \# 4 Generics and Overloads

* [Playgound]()

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
            this.head = n
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
            this.head = n
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

        return false // Just to appease the compiler, we shouldn't actually be able to reach this
    }
}
```

Note that every place we reference our List and Node types we have to pass the type parameter.
