```java
// Day 3: Stacks in Java

// 1. Stack implementation using an array
class ArrayStack {
    private int maxSize;
    private int[] stackArray;
    private int top;

    public ArrayStack(int size) {
        maxSize = size;
        stackArray = new int[maxSize];
        top = -1;
    }

    public void push(int value) {
        if (isFull()) {
            System.out.println("Stack is full. Cannot push " + value);
            return;
        }
        stackArray[++top] = value;
    }

    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack is empty. Cannot pop.");
            return -1;
        }
        return stackArray[top--];
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Stack is empty. Cannot peek.");
            return -1;
        }
        return stackArray[top];
    }

    public boolean isEmpty() {
        return (top == -1);
    }

    public boolean isFull() {
        return (top == maxSize - 1);
    }
}

// 2. Stack implementation using a linked list
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedListStack {
    private Node top;

    public LinkedListStack() {
        this.top = null;
    }

    public void push(int value) {
        Node newNode = new Node(value);
        newNode.next = top;
        top = newNode;
    }

    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack is empty. Cannot pop.");
            return -1;
        }
        int value = top.data;
        top = top.next;
        return value;
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Stack is empty. Cannot peek.");
            return -1;
        }
        return top.data;
    }

    public boolean isEmpty() {
        return (top == null);
    }
}

// 3. Balancing Parentheses Problem
class ParenthesesChecker {
    public static boolean areParenthesesBalanced(String expr) {
        java.util.Stack<Character> stack = new java.util.Stack<>();

        for (int i = 0; i < expr.length(); i++) {
            char current = expr.charAt(i);

            if (current == '(' || current == '[' || current == '{') {
                stack.push(current);
                continue;
            }

            if (stack.isEmpty())
                return false;

            char check;
            switch (current) {
                case ')':
                    check = stack.pop();
                    if (check == '{' || check == '[')
                        return false;
                    break;

                case '}':
                    check = stack.pop();
                    if (check == '(' || check == '[')
                        return false;
                    break;

                case ']':
                    check = stack.pop();
                    if (check == '(' || check == '{')
                        return false;
                    break;
            }
        }

        return (stack.isEmpty());
    }
}

// Main class to demonstrate usage
public class StackDemo {
    public static void main(String[] args) {
        // Array Stack demonstration
        ArrayStack arrayStack = new ArrayStack(3);
        arrayStack.push(1);
        arrayStack.push(2);
        arrayStack.push(3);
        System.out.println("Popped from array stack: " + arrayStack.pop());
        System.out.println("Peeked from array stack: " + arrayStack.peek());

        // Linked List Stack demonstration
        LinkedListStack linkedListStack = new LinkedListStack();
        linkedListStack.push(1);
        linkedListStack.push(2);
        linkedListStack.push(3);
        System.out.println("Popped from linked list stack: " + linkedListStack.pop());
        System.out.println("Peeked from linked list stack: " + linkedListStack.peek());

        // Parentheses Balancing demonstration
        String expr1 = "{()}[]";
        String expr2 = "({)}";
        System.out.println("Are parentheses balanced in " + expr1 + "? " + 
                           ParenthesesChecker.areParenthesesBalanced(expr1));
        System.out.println("Are parentheses balanced in " + expr2 + "? " + 
                           ParenthesesChecker.areParenthesesBalanced(expr2));
    }
}

```

1. What is a Stack?

Imagine you have a stack of plates. You can only add a new plate to the top of the stack or remove the topmost plate. You can't take a plate from the middle or bottom without removing all the plates above it first. This is exactly how a stack works in programming!

2. LIFO Structure:

LIFO stands for "Last In, First Out". It means the last item you put in is the first one you'll take out. Think of it like this:

```
   | 3 | <-- Top (Last In)
   | 2 |
   | 1 | <-- Bottom (First In)
  -----
```

3. Basic Operations:

a) Push: Adding an element to the top of the stack.
   ```
   | 3 |    | 4 |
   | 2 | -> | 3 |
   | 1 |    | 2 |
   -----    | 1 |
            -----
   ```

b) Pop: Removing the top element from the stack.
   ```
   | 3 |    | 2 |
   | 2 | -> | 1 |
   | 1 |    -----
   -----
   ```

c) Peek: Looking at the top element without removing it.
   ```
   | 3 | <-- Peek (3)
   | 2 |
   | 1 |
   -----
   ```

4. Implementations:

a) Using an Array:
   - We use a fixed-size array and a 'top' variable to keep track of the topmost element.
   - Push: Increment 'top' and add the element.
   - Pop: Return the element at 'top' and decrement 'top'.
   - Pros: Fixed memory usage.
   - Cons: Size limitation.

b) Using a Linked List:
   - Each node points to the next node below it.
   - Push: Add a new node at the head.
   - Pop: Remove the head node.
   - Pros: Dynamic size.
   - Cons: Extra memory for node pointers.

5. Real-world Applications:

- Undo mechanism in text editors
- Browser history (back button)
- Function call stack in programming languages

6. Solving the Parentheses Balancing Problem:

This is a classic problem solved using a stack. Here's how it works:

1. Scan the expression from left to right.
2. If you encounter an opening bracket ('(', '{', '['), push it onto the stack.
3. If you encounter a closing bracket (')', '}', ']'):
   - If the stack is empty, the expression is unbalanced.
   - If the top of the stack doesn't match the closing bracket, it's unbalanced.
   - If it matches, pop the top element from the stack.
4. After scanning all characters, if the stack is empty, the expression is balanced.

Visualization:
```
Expression: { ( ) [ ] }
Stack:
| { |  | { |  | { |  |   |  |   |  |   |
-----  | ( |  -----  -----  -----  -----
       -----

Result: Balanced
```

Now, let's practice! Try these exercises:

1. Implement a function to reverse a string using a stack.
2. Create a stack that keeps track of its minimum element.
3. Implement a queue using two stacks.

Remember, the key to understanding stacks is to always think about the LIFO principle. Whenever you're dealing with a problem that involves processing items in a reverse order or keeping track of previous states, consider using a stack!

