# Stack (LIFO)
Usage: DFS algorithm, Undo functionality, functino calls

## Implementation

### with arrays
```TypeScript
class Stack<T> {
  private stack: Array<T>;

  constructor() {
    this.stack = [];
  }

  public peek(): T | undefined | never {
    if (this.isEmpty()) {
      throw new EmptyStack("");
    }
    return this.stack[this.stack.length - 1];
  }

  public pop(): T | undefined | never {
    if (this.isEmpty()) {
      throw new EmptyStack("");
    }
    return this.stack.pop();
  }

  public push(data: T): void {
    this.stack.push(data);
  }

  private isEmpty() {
    return this.stack.length === 0;
  }
}

const stack = new Stack<string>();
stack.push("first");
stack.push("second");
stack.push("third");
console.log(stack.peek());
console.log(stack.pop());
console.log(stack.pop());
console.log(stack.pop());
```

### with linked list
```TypeScript
class StackNode<T> {
  data: T;
  next: StackNode<T> | null;

  constructor(data: T) {
    this.data = data;
    this.next = null;
  }
}

class Stack<T> {
  private top: StackNode<T> | null;

  constructor() {
    this.top = null;
  }

  public peek(): T | null {
    if (this.isEmpty()) {
      return null;
    } else {
      if (this.top != null) {
        return this.top.data;
      }
      return null;
    }
  }

  public pop(): T | null {
    if (this.isEmpty()) {
      return null;
    } else {
      if (this.top != null) {
        const poppedData = this.top.data;
        this.top = this.top.next;
        return poppedData;
      }
      return null;
    }
  }

  public push(data: T): void {
    const newNode = new StackNode<T>(data);
    if (this.isEmpty()) {
      this.top = newNode;
    } else {
      newNode.next = this.top;
      this.top = newNode;
    }
  }

  private isEmpty(): boolean {
    return this.top == null;
  }
}

const stack = new Stack<string>();
stack.push("first");
stack.push("second");
stack.push("third");
console.log(stack.peek());
console.log(stack.pop());
console.log(stack.pop());
console.log(stack.pop());
```