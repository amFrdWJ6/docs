# Linked Lists

sequence of nodes, where each node contains both data and a reference to the next node in the sequence (and previous in bidirectional LL)

## Code example
- simple implementation of Linked List

```TypeScript
class LLNode<T> {
    public data: T;
    public prev: LLNode<T> | null = null;
    public next: LLNode<T> | null = null;

    constructor(data: T) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class LinkedList<T> {
    private head: LLNode<T> | null = null;
    private tail: LLNode<T> | null = null;

    constructor() {
        this.head = null;
        this.tail = null;
    }

    public prepend(data: T): void {
        if (this.head) {
            const newNode = new LLNode(data);
            newNode.next = this.head;
            this.head.prev = newNode;
            this.head = newNode;
        } else {
            this.head = new LLNode(data);
        }
    }

    public append(data: T): void {
        if (this.tail) {
            const newNode = new LLNode(data);
            newNode.prev = this.tail;
            this.tail.next = newNode;
            this.tail = newNode;
        } else {
            if (this.head) {
                const newNode = new LLNode(data);
                newNode.prev = this.head;
                this.head.next = newNode;
                this.tail = newNode;
            } else {
                this.head = new LLNode(data);
            }
        }
    }

    public insertAfter(search: T, data: T): boolean {
        let previousNode = this.searchNode(search);
        if (previousNode != null) {
            const newNode = new LLNode(data);
            newNode.prev = previousNode;
            newNode.next = previousNode.next;

            if (previousNode.next) {
                previousNode.next.prev = newNode;
            } else {
                this.tail = newNode;
            }
            previousNode.next = newNode;
            return true
        }
        return false
    }

    public delete(search: T): boolean {
        let deleteNode = this.searchNode(search);
        if (deleteNode != null) {
            if (deleteNode.prev) {
                deleteNode.prev.next = deleteNode.next;
            } else {
                this.head = deleteNode.next;
            }

            if (deleteNode.next) {
                deleteNode.next.prev = deleteNode.prev;
            } else {
                this.tail = deleteNode.prev;
            }
            deleteNode = null;

            return true;
        }
        return false;
    }

    public has(search: T) {
        let hasNode = this.searchNode(search);
        return hasNode ? true : false;
    }

    public traverse() {
        let current = this.head;
        while (current != null) {
            console.log(current.data);
            current = current.next;
        }
    }

    private searchNode(data: T) {
        let current = this.head;
        while (current != null) {
            if (current.data === data) {
                return current;
            }
            current = current.next;
        }
        return null;
    }
}

const ll = new LinkedList();

ll.append("first");
ll.append("second");
ll.append("fourth");
ll.prepend("zero");
ll.prepend("negative");
ll.insertAfter("second", "third");
ll.insertAfter("fourth", "fifth");
ll.delete("negative");
ll.traverse();
// Output: zero, first, second, third, fourth, fifth
```