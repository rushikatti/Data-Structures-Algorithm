# LeetCode 160: Intersection of Two Linked Lists

## Approach 1: Brute Force

### Idea
For every node in List A, traverse all nodes in List B. If both pointers refer to the same node in memory, that node is the intersection.

**Important:** Compare node references using `==`, not node values.

### Algorithm
1. Traverse each node in List A.
2. For every node in A, traverse List B from its head.
3. If `currA == currB`, return `currA`.
4. If no matching node reference is found, return `null`.

### Code (Java)

    public class Solution {
        public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
            ListNode currA = headA;

            while (currA != null) {
                ListNode currB = headB;

                while (currB != null) {
                    if (currA == currB) {
                        return currA;
                    }

                    currB = currB.next;
                }

                currA = currA.next;
            }

            return null;
        }
    }

### Complexity
- **Time:** O(m × n), where m and n are the lengths of the lists.
- **Space:** O(1).

---

## Approach 2: Optimized — Two Pointers

### Idea
Use two pointers, one starting at each list's head. When a pointer reaches the end of its list, redirect it to the other list's head.

Both pointers travel the same total distance, `m + n`. They will meet at the intersection node or at `null` if there is no intersection.

### Algorithm
1. Initialize `a = headA` and `b = headB`.
2. While `a != b`:
   - If `a == null`, move it to `headB`; otherwise, move it to `a.next`.
   - If `b == null`, move it to `headA`; otherwise, move it to `b.next`.
3. Return `a`.

### Code (Java)

    public class Solution {
        public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
            ListNode a = headA;
            ListNode b = headB;

            while (a != b) {
                a = (a == null) ? headB : a.next;
                b = (b == null) ? headA : b.next;
            }

            return a;
        }
    }

### Complexity
- **Time:** O(m + n).
- **Space:** O(1).

---

## Comparison

| Feature | Brute Force | Two Pointers |
|---|---|---|
| Approach | Check every node pair | Switch list heads |
| Time | O(m × n) | O(m + n) |
| Space | O(1) | O(1) |
| Recommended | No | Yes |

## Key Takeaway

The **two-pointer approach** is optimal because it runs in linear time and uses constant extra space.

Always compare nodes using `==`, since an intersection means the two lists share the exact same node in memory—not just nodes with equal values.
