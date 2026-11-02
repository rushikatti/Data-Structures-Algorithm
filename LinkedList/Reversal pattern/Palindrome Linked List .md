# Palindrome Linked List (LeetCode 234)

## Problem

Given the head of a singly linked list, determine whether it is a palindrome.

A palindrome reads the same forward and backward.

**Examples:**

- Input: `1 -> 2 -> 2 -> 1`  
  Output: `true`

- Input: `1 -> 2 -> 3`  
  Output: `false`

---

## Approach 1: Brute Force (ArrayList)

### Idea

Store all linked-list values in an ArrayList. Then compare elements from both ends.

### Algorithm

1. Create an ArrayList.
2. Traverse the linked list and store every node's value.
3. Initialize two pointers:
   - `left = 0`
   - `right = list.size() - 1`
4. Compare the values at both indices.
5. If any values differ, return `false`.
6. Move `left` forward and `right` backward.
7. If all values match, return `true`.

### Code (Java)

    class Solution {
        public boolean isPalindrome(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode curr = head;

            while (curr != null) {
                list.add(curr.val);
                curr = curr.next;
            }

            int left = 0;
            int right = list.size() - 1;

            while (left < right) {

                if (!list.get(left).equals(list.get(right))) {
                    return false;
                }

                left++;
                right--;
            }

            return true;
        }
    }

### Complexity

- **Time:** O(n) — traverse the list and compare elements.
- **Space:** O(n) — ArrayList stores all node values.

---

## Approach 2: Optimal (Slow-Fast + Reverse Second Half)

### Idea

Instead of using an ArrayList, find the middle of the linked list, reverse the second half, and compare both halves.

### Algorithm

1. Initialize `slow` and `fast` at `head`.
2. Move `slow` one step and `fast` two steps until the middle is reached.
3. Reverse the second half starting from `slow`.
4. Initialize:
   - `first = head`
   - `second = prev` (head of the reversed second half)
5. Compare the values of both halves.
6. If any values differ, return `false`.
7. If all corresponding values match, return `true`.

### Code (Java)

    class Solution {
        public boolean isPalindrome(ListNode head) {

            if (head == null || head.next == null) {
                return true;
            }

            // Step 1: Find the middle
            ListNode slow = head;
            ListNode fast = head;

            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
            }

            // Step 2: Reverse the second half
            ListNode prev = null;
            ListNode curr = slow;

            while (curr != null) {
                ListNode nextNode = curr.next;
                curr.next = prev;
                prev = curr;
                curr = nextNode;
            }

            // Step 3: Compare both halves
            ListNode first = head;
            ListNode second = prev;

            while (second != null) {

                if (first.val != second.val) {
                    return false;
                }

                first = first.next;
                second = second.next;
            }

            return true;
        }
    }

### Complexity

- **Time:** O(n) — finding middle + reversing + comparing.
- **Space:** O(1) — reversal is performed in-place.

---

## Dry Run (Optimal Approach)

Input:

    1 -> 2 -> 2 -> 1

**Step 1: Find middle**

    slow = second node containing 2

**Step 2: Reverse second half**

    Original:  1 -> 2 -> 2 -> 1
    First:     1 -> 2 -> 2
    Reversed:  1 -> 2

**Step 3: Compare both halves**

| First | Second | Comparison |
|---:|---:|---|
| 1 | 1 | Match |
| 2 | 2 | Match |

Output: `true`

---

## Approach Comparison

| Approach | Time | Space |
|---|---|---|
| Brute Force (ArrayList) | O(n) | O(n) |
| Optimal (Reverse second half) | O(n) | O(1) |

---

## Important Patterns to Remember

1. **Slow and Fast Pointers** — Find the middle of a linked list.
2. **In-place Reversal** — Reverse the second half using `prev`, `curr`, and `nextNode`.
3. **Two Pointers** — Compare both halves simultaneously.

## Interview Takeaway

Both approaches take O(n) time.

The ArrayList approach is easier to implement, while the optimal approach reduces auxiliary space from O(n) to O(1).

**Related Problems:**
- Maximum Twin Sum of a Linked List (LeetCode 2130)
- Reverse Linked List (LeetCode 206)
- Middle of the Linked List (LeetCode 876)
