# LeetCode 142: Linked List Cycle II

## Problem

Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

You must solve it without modifying the linked list and using O(1) extra space.

Example:

    Input:  3 → 2 → 0 → -4
                ↑         |
                └─────────┘

    Output: Node with value 2

---

## Approach 1: Brute Force — HashSet

### Idea

Store every visited node in a HashSet.

- If the current node is already present, it is the starting node of the cycle.
- Otherwise, add the node and move forward.
- If we reach null, no cycle exists.

### Code (Java)

    import java.util.HashSet;
    import java.util.Set;

    public class Solution {
        public ListNode detectCycle(ListNode head) {
            Set<ListNode> visited = new HashSet<>();

            ListNode curr = head;

            while (curr != null) {
                if (visited.contains(curr)) {
                    return curr;
                }

                visited.add(curr);
                curr = curr.next;
            }

            return null;
        }
    }

### Complexity

- **Time:** O(n) average.
- **Space:** O(n).

---

## Approach 2: Optimized — Floyd's Cycle Detection

### Idea

Use two pointers:

- `slow` moves one step.
- `fast` moves two steps.

There are two phases:

**Phase 1: Detect the cycle**

Move slow and fast until they meet.

If fast reaches null, no cycle exists.

**Phase 2: Find the cycle starting node**

1. Keep the meeting point of slow and fast.
2. Move `slow` back to `head`.
3. Keep `fast` at the meeting point.
4. Move both pointers one step at a time.
5. The node where they meet again is the cycle starting node.

### Code (Java)

    public class Solution {
        public ListNode detectCycle(ListNode head) {
            ListNode slow = head;
            ListNode fast = head;

            // Phase 1: Detect cycle
            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;

                if (slow == fast) {
                    break;
                }
            }

            // No cycle
            if (fast == null || fast.next == null) {
                return null;
            }

            // Phase 2: Find cycle starting node
            slow = head;

            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;
            }

            return slow;
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Dry Run

Consider:

    3 → 2 → 0 → -4
        ↑         |
        └─────────┘

The cycle starts at node `2`.

### Phase 1: Detect cycle

Initially:

    slow = 3
    fast = 3

| Iteration | Slow | Fast |
|---|---|---|
| Start | 3 | 3 |
| 1 | 2 | 0 |
| 2 | 0 | 2 |
| 3 | -4 | -4 |

Both pointers meet at node `-4`.

### Phase 2: Find cycle start

Reset slow to head:

    slow = 3
    fast = -4

Move both one step at a time:

| Iteration | Slow | Fast |
|---|---|---|
| Start | 3 | -4 |
| 1 | 2 | 2 |

Both pointers meet at node `2`.

Therefore, return node `2`.

---

## Why does Phase 2 work?

Let:

- `L` = distance from head to cycle starting node.
- `C` = length of the cycle.
- `X` = distance from cycle start to the meeting point.
- `S` = number of steps taken by slow.
- `F` = number of steps taken by fast.

Since fast moves twice as fast:

    F = 2S

At the meeting point, fast has completed some extra full cycles:

    F - S = k × C

Therefore:

    S = k × C

But slow's distance is:

    S = L + X

So:

    L + X = k × C

Rearranging:

    L = k × C - X

This means the distance from the head to the cycle start equals the distance from the meeting point to the cycle start, when moving forward around the cycle.

That's why resetting one pointer to `head` and moving both one step at a time makes them meet at the cycle start.

---

## Comparison

| Feature | Brute Force | Optimized |
|---|---|---|
| Technique | HashSet | Floyd's algorithm |
| Time | O(n) average | O(n) |
| Space | O(n) | O(1) |
| Extra storage | HashSet | None |
| Recommended | Understandable | Interview optimal |

## Linked List Cycle I vs Cycle II

| Cycle I (141) | Cycle II (142) |
|---|---|
| Detect whether cycle exists | Find where cycle begins |
| Returns boolean | Returns ListNode or null |
| Slow/fast pointers | Slow/fast + second phase |
| O(n) time | O(n) time |
| O(1) space | O(1) space |

## Key Takeaways

1. Cycle I asks: **Does a cycle exist?**
2. Cycle II asks: **Where does the cycle start?**
3. Both use Floyd's slow and fast pointer technique.
4. Cycle II requires resetting one pointer to the head after the first meeting.
5. Compare node references using `slow == fast`, not node values.
