# LeetCode 19: Remove Nth Node From End of List

## Problem

Given the head of a linked list, remove the nth node from the end of the list and return its head.

Example 1:

    Input:  1 → 2 → 3 → 4 → 5, n = 2
    Output: 1 → 2 → 3 → 5

Example 2:

    Input:  1 → 2, n = 2
    Output: 2

---

## Approach 1: Brute Force — Two Traversals

### Idea

First calculate the total number of nodes. Then calculate the position of the node to remove from the beginning.

If the list has `length` nodes:

    Position from beginning = length - n

We need to reach the node just before the target and update its `next` pointer.

### Algorithm

1. Traverse the list and calculate its length.
2. Calculate `index = length - n`.
3. If `index == 0`, remove the head and return `head.next`.
4. Otherwise, traverse to the node at position `index - 1`.
5. Skip the target node using `curr.next = curr.next.next`.
6. Return head.

### Code (Java)

    class Solution {
        public ListNode removeNthFromEnd(ListNode head, int n) {
            int length = 0;
            ListNode curr = head;

            // Count nodes
            while (curr != null) {
                length++;
                curr = curr.next;
            }

            // Position from beginning
            int index = length - n;

            // Remove head
            if (index == 0) {
                return head.next;
            }

            curr = head;

            // Reach node before target
            for (int i = 0; i < index - 1; i++) {
                curr = curr.next;
            }

            // Delete target node
            curr.next = curr.next.next;

            return head;
        }
    }

### Complexity

- **Time:** O(n) — two traversals.
- **Space:** O(1).

---

## Approach 2: Optimized — Two Pointers + Dummy Node

### Idea

Use two pointers, `fast` and `slow`, with a gap of `n` nodes between them.

Move `fast` ahead by `n + 1` steps from the dummy node. Then move both pointers together until `fast` reaches null.

At that point, `slow` will be just before the node that needs to be removed.

### Why do we need a Dummy Node?

Consider:

    1 → 2 → 3 → 4 → 5

If we need to remove the 5th node from the end, we must remove the head itself.

Without a dummy node, we need a separate condition to handle head deletion.

With a dummy node:

    dummy → 1 → 2 → 3 → 4 → 5

Now even the head can be removed using the same pointer operation:

    slow.next = slow.next.next;

### Algorithm

1. Create a dummy node pointing to head.
2. Initialize `slow` and `fast` at dummy.
3. Move `fast` ahead by `n + 1` steps.
4. Move both pointers together until `fast == null`.
5. Remove the target node using `slow.next = slow.next.next`.
6. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode removeNthFromEnd(ListNode head, int n) {
            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode slow = dummy;
            ListNode fast = dummy;

            // Move fast n + 1 steps ahead
            for (int i = 0; i <= n; i++) {
                fast = fast.next;
            }

            // Move both pointers
            while (fast != null) {
                slow = slow.next;
                fast = fast.next;
            }

            // Remove target node
            slow.next = slow.next.next;

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(n) — one traversal.
- **Space:** O(1).

---

## Dry Run

Input:

    1 → 2 → 3 → 4 → 5
    n = 2

Initially:

    dummy → 1 → 2 → 3 → 4 → 5
    slow = dummy
    fast = dummy

### Step 1: Move fast n + 1 steps

Since `n = 2`, move fast 3 steps.

    slow = dummy
    fast = 3

### Step 2: Move both pointers

| Iteration | Slow | Fast |
|---|---|---|
| Start | dummy | 3 |
| 1 | 1 | 4 |
| 2 | 2 | 5 |
| 3 | 3 | null |

Now `slow` is at node `3`, just before the target node `4`.

### Step 3: Delete target

    slow.next = slow.next.next;

This changes:

    3 → 4 → 5

Into:

    3 → 5

Final list:

    1 → 2 → 3 → 5

---

## Comparison

| Feature | Brute Force | Optimized |
|---|---|---|
| Technique | Count + traverse | Two pointers |
| Traversals | 2 | 1 |
| Time | O(n) | O(n) |
| Space | O(1) | O(1) |
| Dummy node | Not required | Used |
| Recommended | Easy to understand | Interview optimal |

## Key Takeaways

1. `length - n` gives the target node's zero-based index from the beginning.
2. In the optimized approach, maintain a gap of `n + 1` between `fast` and `slow`, starting from dummy.
3. `slow` must stop at the node before the target because deletion requires changing the previous node's `next`.
4. Dummy nodes simplify edge cases, especially when deleting the head.
5. This is a classic **Fast and Slow Pointer pattern**.
