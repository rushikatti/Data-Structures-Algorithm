# LeetCode 707: Design Linked List

## Problem

Design a singly linked list that supports the following operations:

1. `get(index)` – Get the value of the node at the given index. If the index is invalid, return `-1`.
2. `addAtHead(val)` – Add a node with value `val` at the beginning.
3. `addAtTail(val)` – Add a node with value `val` at the end.
4. `addAtIndex(index, val)` – Insert a node at the given index.
   - If index equals the length of the list, insert at the tail.
   - If index is greater than the length, do nothing.
   - If index is less than zero, insert at the head.
5. `deleteAtIndex(index)` – Delete the node at the given index if it exists.

---

## Approach 1: ArrayList

### Idea

Use an ArrayList to store the linked list values.

ArrayList provides direct index access, so getting and inserting elements at a particular index is straightforward.

### Algorithm

1. Create an ArrayList to store values.
2. For `get(index)`, return the value if the index is valid; otherwise, return `-1`.
3. For `addAtHead(val)`, insert the value at index `0`.
4. For `addAtTail(val)`, append the value.
5. For `addAtIndex(index, val)`, insert the value if the index is valid.
6. For `deleteAtIndex(index)`, remove the value if the index is valid.

### Code (Java)

    class MyLinkedList {

        ArrayList<Integer> list;

        public MyLinkedList() {
            list = new ArrayList<>();
        }

        public int get(int index) {

            if (index < 0 || index >= list.size()) {
                return -1;
            }

            return list.get(index);
        }

        public void addAtHead(int val) {
            list.add(0, val);
        }

        public void addAtTail(int val) {
            list.add(val);
        }

        public void addAtIndex(int index, int val) {

            if (index < 0) {
                index = 0;
            }

            if (index > list.size()) {
                return;
            }

            list.add(index, val);
        }

        public void deleteAtIndex(int index) {

            if (index < 0 || index >= list.size()) {
                return;
            }

            list.remove(index);
        }
    }

### Complexity

| Operation | Time |
|---|---|
| get(index) | O(1) |
| addAtHead(val) | O(n) |
| addAtTail(val) | O(1) amortized |
| addAtIndex(index, val) | O(n) |
| deleteAtIndex(index) | O(n) |

- **Space:** O(n) — storing all values.

---

## Approach 2: Optimal — Singly Linked List with Dummy Node

### Idea

Implement the linked list using nodes instead of an ArrayList.

Each node contains:
- `val` – stores the value.
- `next` – points to the next node.

Use a dummy node before the actual head. This simplifies insertion and deletion at index `0`.

Maintain a `size` variable to track the number of nodes.

### Algorithm

**1. Constructor**

- Create a dummy node.
- Initialize `size = 0`.

**2. get(index)**

- Check whether the index is valid.
- Start from `dummy.next`.
- Traverse until the required index.
- Return the node's value.

**3. addAtHead(val)**

- Create a new node.
- Connect it to the current head.
- Update `dummy.next`.
- Increase size.

**4. addAtTail(val)**

- Use `addAtIndex(size, val)`.

**5. addAtIndex(index, val)**

- If index is less than zero, set it to zero.
- If index is greater than size, do nothing.
- Traverse to the node immediately before the insertion position.
- Connect the new node.
- Increase size.

**6. deleteAtIndex(index)**

- If index is invalid, do nothing.
- Traverse to the node immediately before the target.
- Skip the target node.
- Decrease size.

### Code (Java)

    class MyLinkedList {

        class Node {
            int val;
            Node next;

            Node(int val) {
                this.val = val;
            }
        }

        Node dummy;
        int size;

        public MyLinkedList() {
            dummy = new Node(0);
            size = 0;
        }

        public int get(int index) {

            if (index < 0 || index >= size) {
                return -1;
            }

            Node cur = dummy.next;

            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }

            return cur.val;
        }

        public void addAtHead(int val) {

            Node newNode = new Node(val);

            newNode.next = dummy.next;
            dummy.next = newNode;

            size++;
        }

        public void addAtTail(int val) {
            addAtIndex(size, val);
        }

        public void addAtIndex(int index, int val) {

            if (index < 0) {
                index = 0;
            }

            if (index > size) {
                return;
            }

            Node cur = dummy;

            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }

            Node newNode = new Node(val);

            newNode.next = cur.next;
            cur.next = newNode;

            size++;
        }

        public void deleteAtIndex(int index) {

            if (index < 0 || index >= size) {
                return;
            }

            Node cur = dummy;

            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }

            cur.next = cur.next.next;

            size--;
        }
    }

### Complexity

| Operation | Time | Space |
|---|---|---|
| get(index) | O(n) | O(1) |
| addAtHead(val) | O(1) | O(1) |
| addAtTail(val) | O(n) | O(1) |
| addAtIndex(index, val) | O(n) | O(1) |
| deleteAtIndex(index) | O(n) | O(1) |

- **Space:** O(n) overall for storing the linked list nodes.
- **Auxiliary space per operation:** O(1).

---

## Comparison

| Operation | ArrayList | Singly Linked List |
|---|---|---|
| get(index) | O(1) | O(n) |
| addAtHead | O(n) | O(1) |
| addAtTail | O(1) amortized | O(n) |
| addAtIndex | O(n) | O(n) |
| deleteAtIndex | O(n) | O(n) |

## Key Takeaways

1. A linked list consists of nodes connected through `next` pointers.
2. A dummy node simplifies insertion and deletion at the head.
3. Maintain a `size` variable to validate indices.
4. `addAtIndex()` requires reaching the node before the insertion position.
5. `deleteAtIndex()` requires reaching the node before the target.
6. A singly linked list does not provide O(1) random access.

## Interview Recommendation

Use the **Singly Linked List with Dummy Node** approach.

LeetCode expects you to implement the actual linked list rather than use an ArrayList. Focus on pointer manipulation, index validation, and maintaining the size correctly.
