# LeetCode 141: Linked List Cycle

## Problem

Given the head of a linked list, determine whether the linked list contains a cycle.

A cycle exists when a node's `next` pointer points back to a previously visited node.

Example 1:

    Input:  3 → 2 → 0 → -4
                ↑         |
                └─────────┘

    Output: true

Example 2:

    Input:  1 → 2 → null

    Output: false

---

## Approach 1: Brute Force — HashSet

### Idea

Use a HashSet to store the addresses (node references) of visited nodes.

While traversing:
- If the current node is already present in the HashSet, a cycle exists.
- Otherwise, add it to the HashSet and move forward.
- If we reach null, there is no cycle.

### Code (Java)

    import java.util.HashSet;
    import java.util.Set;

    public class Solution {
        public boolean hasCycle(ListNode head) {
            Set<ListNode> visited = new HashSet<>();

            ListNode curr = head;

            while (curr != null) {
                if (visited.contains(curr)) {
                    return true;
                }

                visited.add(curr);
                curr = curr.next;
            }

            return false;
        }
    }

### Complexity

- **Time:** O(n) average.
- **Space:** O(n) — HashSet stores visited nodes.

---

## Approach 2: Optimized — Floyd's Cycle Detection (Slow and Fast Pointers)

### Idea

Use two pointers moving at different speeds:

- `slow` moves one step at a time.
- `fast` moves two steps at a time.

If a cycle exists, the fast pointer will eventually catch up with the slow pointer.

If no cycle exists, the fast pointer will reach `null`.

### Algorithm

1. Initialize `slow = head` and `fast = head`.
2. Traverse while `fast != null` and `fast.next != null`.
3. Move:
   - `slow = slow.next`
   - `fast = fast.next.next`
4. If `slow == fast`, return `true`.
5. If the loop ends, return `false`.

### Code (Java)

    public class Solution {
        public boolean hasCycle(ListNode head) {
            ListNode slow = head;
            ListNode fast = head;

            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;

                if (slow == fast) {
                    return true;
                }
            }

            return false;
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Dry Run

Input:

    3 → 2 → 0 → -4
        ↑         |
        └─────────┘

Initially:

    slow = 3
    fast = 3

| Iteration | Slow | Fast |
|---|---|---|
| Start | 3 | 3 |
| 1 | 2 | 0 |
| 2 | 0 | 2 |
| 3 | -4 | -4 |

At iteration 3:

    slow == fast

Therefore, return `true`.

---

## Why does the fast pointer catch the slow pointer?

Inside a cycle:
- Slow moves 1 step.
- Fast moves 2 steps.
- Fast gains 1 node on slow in every iteration.

Since the cycle has a finite number of nodes, fast eventually meets slow.

---

## Comparison

| Feature | Brute Force | Optimized |
|---|---|---|
| Technique | HashSet | Slow/Fast pointers |
| Time | O(n) average | O(n) |
| Space | O(n) | O(1) |
| Recommended | Easy to understand | Interview optimal |

## Key Takeaways

1. Compare nodes using `slow == fast`, not their values.
2. Always check `fast != null && fast.next != null` before moving fast by two steps.
3. Floyd's Cycle Detection is the optimal approach because it uses O(1) extra space.
4. This technique is also used in **LeetCode 142: Linked List Cycle II**, where we find the starting node of the cycle.
