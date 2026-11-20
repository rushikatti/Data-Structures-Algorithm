# Insertion in a Singly Linked List

Insertion in a linked list can be performed at three common positions:

1. Insert at Head
2. Insert at Tail
3. Insert at a Given Position (N)

---

## 1. Insert at Head

### Idea

Create a new node and make its `next` point to the current head.

Then update the head to the new node.

### Algorithm

1. Create a new node with the given value.
2. Set `newNode.next = head`.
3. Update `head = newNode`.
4. Return the updated head.

### Code (Java)

    class Solution {
        public ListNode insertAtHead(ListNode head, int val) {

            ListNode newNode = new ListNode(val);

            newNode.next = head;

            head = newNode;

            return head;
        }
    }

### Complexity

- **Time:** O(1)
- **Space:** O(1)

---

## 2. Insert at Tail

### Idea

Traverse the linked list until the last node and connect the new node to it.

If the list is empty, the new node becomes the head.

### Algorithm

1. Create a new node with the given value.
2. If `head == null`, return the new node.
3. Traverse until `cur.next == null`.
4. Set `cur.next = newNode`.
5. Return the head.

### Code (Java)

    class Solution {
        public ListNode insertAtTail(ListNode head, int val) {

            ListNode newNode = new ListNode(val);

            if (head == null) {
                return newNode;
            }

            ListNode cur = head;

            while (cur.next != null) {
                cur = cur.next;
            }

            cur.next = newNode;

            return head;
        }
    }

### Complexity

- **Time:** O(n) — traversal to the last node.
- **Space:** O(1)

---

## 3. Insert at a Given Position (N)

### Idea

Traverse to the node immediately before the required position and insert the new node.

Assume positions are **1-based**:

- Position 1 means insert at head.
- Position 2 means insert after the first node.
- Position `n + 1` means insert at tail.

### Algorithm

1. Create a new node with the given value.
2. If position is 1, insert at head.
3. Otherwise, initialize `cur` at head.
4. Traverse until the node at position `pos - 1`.
5. If the position is invalid, return the original head.
6. Set `newNode.next = cur.next`.
7. Set `cur.next = newNode`.
8. Return the head.

### Code (Java)

    class Solution {
        public ListNode insertAtPosition(ListNode head, int val, int pos) {

            if (pos <= 0) {
                return head;
            }

            ListNode newNode = new ListNode(val);

            // Insert at head
            if (pos == 1) {
                newNode.next = head;
                return newNode;
            }

            ListNode cur = head;

            // Reach the node before the required position
            for (int i = 1; i < pos - 1 && cur != null; i++) {
                cur = cur.next;
            }

            // Invalid position
            if (cur == null) {
                return head;
            }

            newNode.next = cur.next;
            cur.next = newNode;

            return head;
        }
    }

### Complexity

- **Time:** O(n) — traversal to the required position.
- **Space:** O(1)

---

## Comparison

| Operation | Time | Space |
|---|---|---|
| Insert at Head | O(1) | O(1) |
| Insert at Tail | O(n) | O(1) |
| Insert at Position N | O(n) | O(1) |

## Key Takeaways

1. Insertion at head takes O(1) because no traversal is required.
2. Insertion at tail takes O(n) in a singly linked list when only the head is given.
3. Insertion at a given position requires reaching the previous node.
4. Always connect `newNode.next` before updating `cur.next`.
5. Handle an empty list and invalid positions carefully.

## Interview Recommendation

Remember these two pointer operations:

**Insert at Head:**
- `newNode.next = head`
- `head = newNode`

**Insert After a Node:**
- `newNode.next = cur.next`
- `cur.next = newNode`
