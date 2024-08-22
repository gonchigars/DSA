

```java
// Day 2: Linked Lists in Java

// 1. Singly Linked List
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class SinglyLinkedList {
    Node head;

    // Insertion at the beginning
    void insertAtBeginning(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    // Deletion of a node
    void deleteNode(int key) {
        Node temp = head, prev = null;

        if (temp != null && temp.data == key) {
            head = temp.next;
            return;
        }

        while (temp != null && temp.data != key) {
            prev = temp;
            temp = temp.next;
        }

        if (temp == null) return;

        prev.next = temp.next;
    }

    // Traversal
    void printList() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("NULL");
    }

    // Reversal
    void reverse() {
        Node prev = null;
        Node current = head;
        Node next = null;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }
}

// 2. Doubly Linked List
class DoublyNode {
    int data;
    DoublyNode prev;
    DoublyNode next;

    DoublyNode(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {
    DoublyNode head;

    // Insertion at the end
    void insertAtEnd(int data) {
        DoublyNode newNode = new DoublyNode(data);
        if (head == null) {
            head = newNode;
            return;
        }
        DoublyNode last = head;
        while (last.next != null) {
            last = last.next;
        }
        last.next = newNode;
        newNode.prev = last;
    }

    // Traversal (forward)
    void printListForward() {
        DoublyNode current = head;
        System.out.print("NULL <-> ");
        while (current != null) {
            System.out.print(current.data + " <-> ");
            current = current.next;
        }
        System.out.println("NULL");
    }
}

// 3. Circular Linked List
class CircularLinkedList {
    Node head;

    // Insertion at the end
    void insertAtEnd(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            newNode.next = head;
            return;
        }
        Node last = head;
        while (last.next != head) {
            last = last.next;
        }
        last.next = newNode;
        newNode.next = head;
    }

    // Traversal
    void printList() {
        if (head == null) return;
        Node temp = head;
        do {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        } while (temp != head);
        System.out.println("(back to start)");
    }
}

// Main class to demonstrate usage
public class LinkedListDemo {
    public static void main(String[] args) {
        // Singly Linked List demonstration
        SinglyLinkedList sll = new SinglyLinkedList();
        sll.insertAtBeginning(3);
        sll.insertAtBeginning(2);
        sll.insertAtBeginning(1);
        System.out.println("Singly Linked List:");
        sll.printList();
        sll.deleteNode(2);
        sll.printList();
        sll.reverse();
        sll.printList();

        // Doubly Linked List demonstration
        DoublyLinkedList dll = new DoublyLinkedList();
        dll.insertAtEnd(1);
        dll.insertAtEnd(2);
        dll.insertAtEnd(3);
        System.out.println("\nDoubly Linked List:");
        dll.printListForward();

        // Circular Linked List demonstration
        CircularLinkedList cll = new CircularLinkedList();
        cll.insertAtEnd(1);
        cll.insertAtEnd(2);
        cll.insertAtEnd(3);
        System.out.println("\nCircular Linked List:");
        cll.printList();
    }
}

```



1. What is a Linked List?

Imagine you have a treasure hunt where each clue leads to the next. That's basically what a linked list is in programming! Instead of clues, we have "nodes," and instead of leading to physical locations, each node points to the next node in the list.

2. Types of Linked Lists:

a) Singly Linked List:
   It's like a conga line where each person only knows who's in front of them.
   
   ```
   [Data|Next] -> [Data|Next] -> [Data|Next] -> NULL
   ```

b) Doubly Linked List:
   Now imagine the conga line where each person knows who's in front and behind them.
   
   ```
   NULL <-> [Prev|Data|Next] <-> [Prev|Data|Next] <-> [Prev|Data|Next] <-> NULL
   ```

c) Circular Linked List:
   The conga line forms a circle, with the last person holding the first person's shoulders.
   
   ```
   [Data|Next] -> [Data|Next] -> [Data|Next] -|
         ^                                    |
         |-----------------------------------|
   ```

3. Basic Operations:

a) Insertion:
   - It's like adding a new person to our conga line.
   - In a singly linked list, we need to update the 'next' of the previous node.
   - In a doubly linked list, we update both 'next' of the previous and 'prev' of the next node.

b) Deletion:
   - Removing someone from the conga line.
   - We need to "bridge" the gap by connecting the previous node to the next node.

c) Traversal:
   - Going through the entire conga line, one person at a time.

d) Reversal (for singly linked list):
   - Making the conga line go backwards - the last person becomes the first, and so on.

4. Why Use Linked Lists?

- Dynamic size: Unlike arrays, linked lists can grow or shrink easily.
- Efficient insertion/deletion: No need to shift elements like in arrays.

5. Drawbacks:

- Random access is not allowed: To find the 10th element, you must start from the beginning and count.
- Extra memory for storing the 'next' (and 'prev' in doubly linked lists) pointers.

Now, let's practice! Try these exercises:

1. Implement a function to find the middle element of a singly linked list in one pass.
2. Detect if a singly linked list has a cycle (the last node points back to a previous node).
3. Implement a function to reverse a doubly linked list.

Remember, the key to understanding linked lists is visualizing them as a chain of connected elements. Practice creating and manipulating these structures, and you'll soon become proficient!

Would you like me to explain any part of this in more detail or provide solutions to the practice exercises?
