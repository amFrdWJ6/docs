# Queues (FIFO)
Usage: BFS algorithm, requests in ws, yarn queue  
**Be aware** of thread safety in multithreaded envs

## Implementation

### with arrays
```TypeScript
class Queue<T> {
  private queue: Array<T>;

  constructor() {
    this.queue = [];
  }

  public enqueue(data: T): void {
    this.queue.push(data);
  }

  public dequeue(): T | undefined {
    return this.queue.shift();
  }

  public peek(): T | never {
    if (this.isEmpty()) {
      throw new Error();
    }
    return this.queue[0];
  }

  public getSize(): number {
    return this.queue.length;
  }

  private isEmpty(): boolean {
    return this.queue.length === 0;
  }
}

const q = new Queue<string>();
console.log(q.getSize());
q.enqueue("first");
q.enqueue("second");
q.enqueue("third");
q.enqueue("forth");
q.enqueue("fifth");
console.log(q.peek());
console.log(q.getSize());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
```

### with linked lists
```TypeScript
class QueueNode<T> {
  public data: T;
  public next: QueueNode<T> | null;

  constructor(data: T) {
    this.data = data;
    this.next = null;
  }
}

class Queue<T> {
  private first: QueueNode<T> | null;
  private last: QueueNode<T> | null;
  private size: number;

  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  public enqueue(data: T): void {
    const newNode = new QueueNode<T>(data);
    if (this.first) {
      this.last && (this.last.next = newNode);
    } else {
      this.first = newNode;
    }
    this.last = newNode;
    this.size = this.size + 1;
  }

  public dequeue(): T | undefined {
    if (!this.first) return undefined;

    const removedNode = this.first;
    this.first = this.first.next;
    this.first ?? (this.last = null);
    this.size = this.size - 1;
    return removedNode.data;
  }

  public peek(): T | undefined {
    return this.first ? this.first.data : undefined;
  }

  public getSize(): number {
    return this.size;
  }

  private isEmpty(): boolean {
    return this.first === null;
  }
}

const q = new Queue<string>();
console.log(q.getSize());
q.enqueue("first");
q.enqueue("second");
q.enqueue("third");
q.enqueue("forth");
q.enqueue("fifth");
console.log(q.peek());
console.log(q.getSize());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
console.log(q.dequeue());
```