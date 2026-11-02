# Maximum Twin Sum of a Linked List (LeetCode 2130)

## Problem

Given the head of an even-length linked list, find the maximum twin sum.

The twin of the node at index `i` is the node at index `n - 1 - i`.

Twin sum = `first.val + second.val`

Return the maximum twin sum among all pairs.

**Example:**

Input:
`5 -> 4 -> 2 -> 1`

Twin pairs:
- (5, 1) = 6
- (4, 2) = 6

Output: `6`

---

## Approach 1: Brute Force (ArrayList)

### Idea

1. Traverse the linked list and store all node values in an ArrayList.
2. Use two indices:
   - `left` starts at index 0.
   - `right` starts at the last index.
3. Calculate twin sums and track the maximum.

### Algorithm

1. Create an ArrayList.
2. Traverse the linked list and add each node's value.
3. Initialize `maxSum = 0`.
4. Iterate from the beginning to the middle.
5. Calculate `list.get(i) + list.get(n - 1 - i)`.
6. Update the maximum sum.
7. Return `maxSum`.

### Code (Java)

    class Solution {
        public int pairSum(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode curr = head;

            while (curr != null) {
                list.add(curr.val);
                curr = curr.next;
            }

            int maxSum = 0;
            int n = list.size();

            for (int i = 0; i < n / 2; i++) {
                int sum = list.get(i) + list.get(n - 1 - i);
                maxSum = Math.max(maxSum, sum);
            }

            return maxSum;
        }
    }

### Complexity

- **Time:** O(n) — traverse the list and calculate twin sums.
- **Space:** O(n) — ArrayList stores all node values.

---

## Approach 2: Optimal (Slow-Fast + Reverse Second Half)

### Idea

Instead of storing values in an ArrayList, reverse the second half of the linked list and calculate twin sums using two pointers.

### Algorithm

1. Initialize `slow` and `fast` at `head`.
2. Move `slow` one step and `fast` two steps until the middle is reached.
3. Reverse the second half starting from `slow`.
4. Initialize:
   - `first = head`
   - `second = prev` (head of reversed second half)
5. Traverse both halves simultaneously.
6. Calculate `first.val + second.val` and update the maximum.
7. Return the maximum sum.

### Code (Java)

    class Solution {
        public int pairSum(ListNode head) {

            // Step 1: Find the middle
            ListNode slow = head;
            ListNode fast = head;

            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
            }

            // Step 2: Reverse the second half
            ListNode prev = null;
            ListNode cur = slow;

            while (cur != null) {
                ListNode next = cur.next;
                cur.next = prev;
                prev = cur;
                cur = next;
            }

            // Step 3: Calculate maximum twin sum
            ListNode first = head;
            ListNode second = prev;

            int maxSum = 0;

            while (second != null) {
                int sum = first.val + second.val;
                maxSum = Math.max(maxSum, sum);

                first = first.next;
                second = second.next;
            }

            return maxSum;
        }
    }

### Complexity

- **Time:** O(n) — finding middle + reversing + calculating twin sums.
- **Space:** O(1) — reversal is performed in-place.

---

## Dry Run (Optimal Approach)

Input:

    5 -> 4 -> 2 -> 1

**Step 1: Find middle**

    slow = node containing 2

**Step 2: Reverse second half**

    Original:  5 -> 4 -> 2 -> 1
    First:     5 -> 4 -> 2
    Reversed:  1 -> 2

**Step 3: Calculate twin sums**

| First | Second | Twin Sum |
|---:|---:|---:|
| 5 | 1 | 6 |
| 4 | 2 | 6 |

Maximum twin sum = `6`

---

## Approach Comparison

| Approach | Time | Space |
|---|---|---|
| Brute Force (ArrayList) | O(n) | O(n) |
| Optimal (Reverse second half) | O(n) | O(1) |

## Important Patterns to Remember

1. **Slow and Fast Pointers** — Find the middle of a linked list.
2. **In-place Reversal** — Reverse the second half using `prev`, `cur`, and `next`.
3. **Two Pointers** — Traverse both halves simultaneously.
4. **Maximum Calculation** — Use `Math.max()` to track the highest twin sum.

**Interview takeaway:** Both approaches have O(n) time complexity, but reversing the second half reduces auxiliary space from O(n) to O(1).
