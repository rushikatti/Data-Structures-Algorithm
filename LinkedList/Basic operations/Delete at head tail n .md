# Deletion in a Singly Linked List

Deletion in a linked list can be performed at three common positions:

1. Delete at Head
2. Delete at Tail
3. Delete at a Given Position (N)

---

## 1. Delete at Head

### Idea

Move the head pointer to the next node.

The first node will no longer be part of the linked list.

### Algorithm

1. If `head == null`, return `null`.
2. Store or directly move to `head.next`.
3. Update `head = head.next`.
4. Return the updated head.

### Code (Java)

    class Solution {
        public ListNode deleteAtHead(ListNode head) {

            if (head == null) {
                return null;
            }

            head = head.next;

            return head;
        }
    }

### Complexity

- **Time:** O(1)
- **Space:** O(1)

---

## 2. Delete at Tail

### Idea

Traverse to the second-last node and set its `next` to `null`.

If the list contains only one node, return `null`.

### Algorithm

1. If `head == null` or `head.next == null`, return `null`.
2. Initialize `cur` at head.
3. Traverse until `cur.next.next == null`.
4. Set `cur.next = null`.
5. Return head.

### Code (Java)

    class Solution {
        public ListNode deleteAtTail(ListNode head) {

            if (head == null || head.next == null) {
                return null;
            }

            ListNode cur = head;

            while (cur.next.next != null) {
                cur = cur.next;
            }

            cur.next = null;

            return head;
        }
    }

### Complexity

- **Time:** O(n) — traversal to the second-last node.
- **Space:** O(1)

---

## 3. Delete at a Given Position (N)

### Idea

Traverse to the node immediately before the node that needs to be deleted.

Update its `next` pointer to skip the target node.

Assume positions are **1-based**:

- Position 1 means delete the head.
- Position 2 means delete the second node.
- Position `n` means delete the last node.

### Algorithm

1. If the list is empty or position is invalid, return head.
2. If position is 1, delete the head by returning `head.next`.
3. Initialize `cur` at head.
4. Traverse until the node at position `pos - 1`.
5. If the position is invalid, return the original head.
6. If the target node exists, set `cur.next = cur.next.next`.
7. Return head.

### Code (Java)

    class Solution {
        public ListNode deleteAtPosition(ListNode head, int pos) {

            if (head == null || pos <= 0) {
                return head;
            }

            // Delete at head
            if (pos == 1) {
                return head.next;
            }

            ListNode cur = head;

            // Reach the node before the target position
            for (int i = 1; i < pos - 1 && cur != null; i++) {
                cur = cur.next;
            }

            // Invalid position
            if (cur == null || cur.next == null) {
                return head;
            }

            // Skip the target node
            cur.next = cur.next.next;

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
| Delete at Head | O(1) | O(1) |
| Delete at Tail | O(n) | O(1) |
| Delete at Position N | O(n) | O(1) |

## Key Takeaways

1. Deleting the head requires only updating the head pointer.
2. Deleting the tail requires reaching the second-last node.
3. Deleting at a given position requires reaching the previous node.
4. `cur.next = cur.next.next` skips the node that needs to be deleted.
5. Always handle empty lists, single-node lists, and invalid positions.

## Interview Recommendation

Remember these pointer operations:

**Delete at Head:**

    head = head.next;

**Delete at Tail:**

    cur.next = null;

**Delete at Position:**

    cur.next = cur.next.next;
