# LeetCode 876: Middle of the Linked List

## Problem
Given the head of a singly linked list, return the middle node.

- If the number of nodes is odd, return the exact middle node.
- If the number of nodes is even, return the second middle node.

Example 1:

    Input:  1 → 2 → 3 → 4 → 5
    Output: 3 → 4 → 5

Example 2:

    Input:  1 → 2 → 3 → 4 → 5 → 6
    Output: 4 → 5 → 6

---

## Approach 1: Brute Force — Count Nodes

### Idea
First calculate the total number of nodes. Then traverse again to reach the middle position.

### Algorithm
1. Traverse the list and calculate its length `n`.
2. Calculate the middle index using `n / 2`.
3. Traverse from the head for `n / 2` steps.
4. Return the current node.

### Code (Java)

    class Solution {
        public ListNode middleNode(ListNode head) {
            int n = 0;
            ListNode curr = head;

            // Count nodes
            while (curr != null) {
                n++;
                curr = curr.next;
            }

            // Find middle
            curr = head;

            for (int i = 0; i < n / 2; i++) {
                curr = curr.next;
            }

            return curr;
        }
    }

### Complexity
- **Time:** O(n) — two traversals.
- **Space:** O(1).

---

## Approach 2: Optimized — Slow and Fast Pointers

### Idea
Use two pointers moving at different speeds:

- `slow` moves one step at a time.
- `fast` moves two steps at a time.

When `fast` reaches the end, `slow` will be at the middle.

### Algorithm
1. Initialize both pointers at `head`.
2. While `fast != null` and `fast.next != null`:
   - Move `slow` one step.
   - Move `fast` two steps.
3. Return `slow`.

### Code (Java)

    class Solution {
        public ListNode middleNode(ListNode head) {
            ListNode slow = head;
            ListNode fast = head;

            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
            }

            return slow;
        }
    }

### Complexity
- **Time:** O(n) — one traversal.
- **Space:** O(1).

---

## Dry Run

Input:

    1 → 2 → 3 → 4 → 5 → 6

Initially:

    slow = 1
    fast = 1

| Iteration | Slow | Fast |
|---|---|---|
| Start | 1 | 1 |
| 1 | 2 | 3 |
| 2 | 3 | 5 |
| 3 | 4 | null |

Loop stops because `fast` is null.

Answer:

    4 → 5 → 6

---

## Comparison

| Feature | Brute Force | Optimized |
|---|---|---|
| Technique | Count + traverse | Slow/fast pointers |
| Time | O(n) | O(n) |
| Space | O(1) | O(1) |
| Traversals | 2 | 1 |

## Key Takeaways

1. Slow and fast pointer is also called the **Tortoise and Hare technique**.
2. Always use `fast != null && fast.next != null` as the loop condition.
3. Starting both pointers at `head` ensures that an even-length list returns the **second middle node**.
