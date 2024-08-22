
```java
// Day 4: Queues in Java

// 1. Queue implementation using an array
class ArrayQueue {
    private int maxSize;
    private int[] queueArray;
    private int front;
    private int rear;
    private int nItems;

    public ArrayQueue(int size) {
        maxSize = size;
        queueArray = new int[maxSize];
        front = 0;
        rear = -1;
        nItems = 0;
    }

    public void enqueue(int value) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue " + value);
            return;
        }
        rear = (rear + 1) % maxSize;
        queueArray[rear] = value;
        nItems++;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return -1;
        }
        int temp = queueArray[front];
        front = (front + 1) % maxSize;
        nItems--;
        return temp;
    }

    public int front() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No front element.");
            return -1;
        }
        return queueArray[front];
    }

    public int rear() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No rear element.");
            return -1;
        }
        return queueArray[rear];
    }

    public boolean isEmpty() {
        return (nItems == 0);
    }

    public boolean isFull() {
        return (nItems == maxSize);
    }
}

// 2. Queue implementation using a linked list
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedListQueue {
    private Node front;
    private Node rear;

    public LinkedListQueue() {
        this.front = this.rear = null;
    }

    public void enqueue(int value) {
        Node newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
            return;
        }
        rear.next = newNode;
        rear = newNode;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return -1;
        }
        int value = front.data;
        front = front.next;
        if (front == null) {
            rear = null;
        }
        return value;
    }

    public int front() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No front element.");
            return -1;
        }
        return front.data;
    }

    public int rear() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No rear element.");
            return -1;
        }
        return rear.data;
    }

    public boolean isEmpty() {
        return (front == null && rear == null);
    }
}

// 3. Circular Queue implementation
class CircularQueue {
    private int maxSize;
    private int[] queueArray;
    private int front;
    private int rear;
    private int nItems;

    public CircularQueue(int size) {
        maxSize = size;
        queueArray = new int[maxSize];
        front = -1;
        rear = -1;
        nItems = 0;
    }

    public void enqueue(int value) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue " + value);
            return;
        }
        if (isEmpty()) {
            front = 0;
        }
        rear = (rear + 1) % maxSize;
        queueArray[rear] = value;
        nItems++;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return -1;
        }
        int temp = queueArray[front];
        if (front == rear) {
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % maxSize;
        }
        nItems--;
        return temp;
    }

    public boolean isEmpty() {
        return (nItems == 0);
    }

    public boolean isFull() {
        return (nItems == maxSize);
    }
}

// Main class to demonstrate usage
public class QueueDemo {
    public static void main(String[] args) {
        // Array Queue demonstration
        ArrayQueue arrayQueue = new ArrayQueue(3);
        arrayQueue.enqueue(1);
        arrayQueue.enqueue(2);
        arrayQueue.enqueue(3);
        System.out.println("Dequeued from array queue: " + arrayQueue.dequeue());
        System.out.println("Front of array queue: " + arrayQueue.front());
        System.out.println("Rear of array queue: " + arrayQueue.rear());

        // Linked List Queue demonstration
        LinkedListQueue linkedListQueue = new LinkedListQueue();
        linkedListQueue.enqueue(1);
        linkedListQueue.enqueue(2);
        linkedListQueue.enqueue(3);
        System.out.println("Dequeued from linked list queue: " + linkedListQueue.dequeue());
        System.out.println("Front of linked list queue: " + linkedListQueue.front());
        System.out.println("Rear of linked list queue: " + linkedListQueue.rear());

        // Circular Queue demonstration
        CircularQueue circularQueue = new CircularQueue(3);
        circularQueue.enqueue(1);
        circularQueue.enqueue(2);
        circularQueue.enqueue(3);
        System.out.println("Dequeued from circular queue: " + circularQueue.dequeue());
        circularQueue.enqueue(4);  // This should work in a circular queue
    }
}

```


1. What is a Queue?

Imagine you're waiting in line at a movie theater. The first person who arrived gets to buy their ticket first, and new people join at the end of the line. This is exactly how a queue works in programming! It's a "first come, first served" system.

2. FIFO Structure:

FIFO stands for "First In, First Out". It means the first item you put in is the first one you'll take out. Think of it like this:

```
Front                 Rear
  |                     |
  v                     v
[ 1 ][ 2 ][ 3 ][ 4 ][ 5 ]
  ^
  |
 This leaves first
```

3. Basic Operations:

a) Enqueue: Adding an element to the rear of the queue.
   ```
   [ 1 ][ 2 ][ 3 ] -> [ 1 ][ 2 ][ 3 ][ 4 ]
                                         ^
                                    Enqueued
   ```

b) Dequeue: Removing the front element from the queue.
   ```
   [ 1 ][ 2 ][ 3 ] -> [ 2 ][ 3 ]
     ^
 Dequeued
   ```

c) Front: Looking at the front element without removing it.
   ```
   [ 1 ][ 2 ][ 3 ]
     ^
   Front
   ```

d) Rear: Looking at the rear element without removing it.
   ```
   [ 1 ][ 2 ][ 3 ]
               ^
              Rear
   ```

4. Implementations:

a) Using an Array:
   - We use a fixed-size array and 'front' and 'rear' variables to keep track of the ends.
   - Enqueue: Add at 'rear' and increment 'rear'.
   - Dequeue: Remove from 'front' and increment 'front'.
   - Pros: Fixed memory usage.
   - Cons: Size limitation, may waste space after dequeueing.

b) Using a Linked List:
   - Each node points to the next node.
   - Enqueue: Add a new node at the rear.
   - Dequeue: Remove the front node.
   - Pros: Dynamic size.
   - Cons: Extra memory for node pointers.

5. Circular Queue:

A circular queue is like a regular queue, but it reuses the empty spaces created by dequeued elements. Imagine a circular table where people can sit:

```
    [ 1 ][ 2 ]
   /         \
[ 6 ]        [ 3 ]
   \         /
    [ 5 ][ 4 ]
```

When we reach the end of the array, we wrap around to the beginning if there's space.

6. Real-world Applications:

- Printer queue (managing print jobs)
- Breadth-First Search in graphs
- Handling of requests on a single shared resource like CPU
- Buffering for data streams

Now, let's practice! Try these exercises:

1. Implement a queue using two stacks.
2. Create a priority queue where elements with higher priority are dequeued first.
3. Implement a sliding window maximum using a deque (double-ended queue).

Remember, the key to understanding queues is to always think about the FIFO principle. Whenever you're dealing with a problem that involves processing items in the order they arrived or managing a sequence of elements where the oldest ones are processed first, consider using a queue!
###################

Why not use DB instead of que ?


Imagine you're running a small coffee shop. Let's compare using a queue vs. using a database (like writing orders in a book):

1. Speed and Efficiency:

Queue (Line of customers):
- When a customer reaches the front, you immediately know who to serve.
- You can quickly add new customers to the end of the line.

Database (Order book):
- For each new order, you'd have to write it down in the book.
- To find the next order to prepare, you'd have to scan through the entire book each time.

In programming, queues are designed for rapid adding and removing of items, which is much faster than reading and writing to a database for each operation.

2. Memory Usage:

Queue:
- Only the current orders are in the line.
- Once an order is completed, the customer leaves the line.

Database:
- All orders, including completed ones, stay in the book unless manually removed.
- Over time, the book gets fuller and takes longer to search through.

In computing, queues use memory more efficiently for temporary, sequential tasks.

3. Order Preservation:

Queue:
- The line naturally preserves the order of arrival.
- It's clear who came first and should be served first.

Database:
- You'd need to add timestamps and sort orders to maintain the correct sequence.
- This adds complexity and slows down the process.

Queues in programming inherently maintain the order of elements, which is crucial for many applications.

4. Simplicity for Specific Tasks:

Queue:
- Simple "next please" system.
- Easy to understand and manage for sequential tasks.

Database:
- More complex to set up and manage for simple sequential tasks.
- Overkill for basic "first come, first served" operations.

In programming, queues offer a straightforward solution for many common problems without the overhead of a full database system.

5. Real-time Processing:

Queue:
- You're continuously serving customers as they reach the front.

Database:
- You'd need to constantly check the book to see if new orders are added.

Queues in computing allow for efficient real-time processing of data or tasks as they arrive.

6. Practical Examples:

- Printer Queue: Manages the order of print jobs without needing a complex database.
- Call Center: Organizes incoming calls in the order they're received.
- Task Scheduling: In operating systems, for managing which program runs next.

While databases are powerful tools for storing and managing large amounts of persistent data, queues are specialized tools designed for efficient, ordered processing of temporary data or tasks. They're like the express lane in a supermarket – designed for quick, efficient handling of a specific type of task.

In many real-world applications, both queues and databases are used together. The queue handles the immediate, ordered processing, while the database stores the long-term records.


