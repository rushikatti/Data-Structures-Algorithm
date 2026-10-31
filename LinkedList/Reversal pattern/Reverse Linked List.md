# LeetCode 206: Reverse Linked List

## Problem

Given the head of a singly linked list, reverse the list and return its new head.

Example:

    Input:  1 → 2 → 3 → 4 → 5 → null
    Output: 5 → 4 → 3 → 2 → 1 → null

---

## Approach 1: Iterative — Head Insertion (My Approach)

### Idea

Use a dummy node and repeatedly move the node after `cur` to the beginning of the linked list.

- `dummy` acts as the node before the actual head.
- `prev` remains at the dummy node.
- `cur` stays at the original head.
- In every iteration, move `cur.next` to the front.

### Algorithm

1. Create a dummy node and connect it to head.
2. Initialize `prev = dummy` and `cur = head`.
3. While `cur != null` and `cur.next != null`:
   - Store the first node in `temp`.
   - Move `cur.next` to the beginning.
   - Remove the moved node from its original position.
   - Connect the moved node to the previous first node.
4. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode reverseList(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }

            ListNode dummy = new ListNode(1);
            dummy.next = head;

            ListNode prev = dummy;
            ListNode cur = prev.next;

            while (cur != null && cur.next != null) {
                ListNode temp = prev.next;

                prev.next = cur.next;
                cur.next = cur.next.next;
                prev.next.next = temp;
            }

            return dummy.next;
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → 4 → 5

Initially:

    dummy → 1 → 2 → 3 → 4 → 5

`cur` stays at node 1.

| Iteration | Operation | Linked List |
|---|---|---|
| Initial | Original list | 1 → 2 → 3 → 4 → 5 |
| 1 | Move 2 to front | 2 → 1 → 3 → 4 → 5 |
| 2 | Move 3 to front | 3 → 2 → 1 → 4 → 5 |
| 3 | Move 4 to front | 4 → 3 → 2 → 1 → 5 |
| 4 | Move 5 to front | 5 → 4 → 3 → 2 → 1 |

Final:

    5 → 4 → 3 → 2 → 1 → null

### Complexity

- **Time:** O(n) — each node is moved once.
- **Space:** O(1) — only pointers are used.

---

## Approach 2: Iterative — Three Pointers

### Idea

Use three pointers to reverse the links one by one.

- `prev`: Stores the previous node.
- `curr`: Points to the current node.
- `next`: Temporarily stores the next node.

### Algorithm

1. Initialize `prev = null` and `curr = head`.
2. Traverse while `curr != null`.
3. Store the next node: `next = curr.next`.
4. Reverse the current link: `curr.next = prev`.
5. Move `prev` forward: `prev = curr`.
6. Move `curr` forward: `curr = next`.
7. Return `prev`.

### Code (Java)

    class Solution {
        public ListNode reverseList(ListNode head) {
            ListNode prev = null;
            ListNode curr = head;

            while (curr != null) {
                ListNode next = curr.next;

                curr.next = prev;

                prev = curr;
                curr = next;
            }

            return prev;
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → null

| Iteration | prev | curr | Reversed Portion |
|---|---|---|---|
| Start | null | 1 | null |
| 1 | 1 | 2 | 1 → null |
| 2 | 2 | 3 | 2 → 1 → null |
| 3 | 3 | null | 3 → 2 → 1 → null |

Final:

    3 → 2 → 1 → null

### Complexity

- **Time:** O(n) — each node is visited once.
- **Space:** O(1) — three pointers are used.

---

## Approach 3: Recursive

### Idea

Recursively reverse the remaining linked list first. Once the last node becomes the new head, reverse the links while returning from the recursive calls.

### Algorithm

1. Base case: If head is null or has only one node, return head.
2. Recursively reverse the list starting from `head.next`.
3. Reverse the link between the current node and its next node:
   `head.next.next = head`.
4. Set `head.next = null` to avoid a cycle.
5. Return the new head.

### Code (Java)

    class Solution {
        public ListNode reverseList(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }

            ListNode newHead = reverseList(head.next);

            head.next.next = head;
            head.next = null;

            return newHead;
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → null

Recursive calls:

    reverseList(1)
        reverseList(2)
            reverseList(3)
                return 3

Now recursion starts returning.

**At node 2:**

    head.next.next = head;

    3 → 2

**At node 1:**

    head.next.next = head;

    3 → 2 → 1

Finally:

    head.next = null;

Result:

    3 → 2 → 1 → null

### Complexity

- **Time:** O(n) — each node is processed once.
- **Space:** O(n) — recursion call stack.

---

## Comparison of All Three Approaches

| Feature | Head Insertion | Three Pointers | Recursion |
|---|---|---|---|
| Technique | Move nodes to front | Reverse links | Recursive reversal |
| Time | O(n) | O(n) | O(n) |
| Space | O(1) | O(1) | O(n) |
| Dummy node | Yes | No | No |
| Extra stack | No | No | Yes |

## Key Takeaways

1. **Head Insertion:** Keep the original head fixed and repeatedly move the next node to the front.
2. **Three Pointers:** Reverse each link individually using `prev`, `curr`, and `next`.
3. **Recursion:** Reverse the remaining list first, then reverse links while returning.
4. All three approaches take O(n) time.
5. Head insertion and three pointers both achieve O(1) auxiliary space.

## Interview Recommendation

- Know all three approaches.
- Your head-insertion solution is a valid optimized solution.
- Three pointers is the most commonly expected iterative approach in interviews.
- Recursive reversal is useful for understanding recursion and pointer manipulation.
