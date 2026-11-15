# LeetCode 445: Add Two Numbers II

## Problem

You are given two non-empty linked lists representing two non-negative integers.

The most significant digit comes first, and each node contains a single digit.

Add the two numbers and return the sum as a linked list.

**Example:**

Input:
- `l1 = [7,2,4,3]`
- `l2 = [5,6,4]`

Output: `[7,8,0,7]`

Explanation: 7243 + 564 = 7807.

---

## Approach 1: Reverse Linked Lists

### Idea

Reverse both input linked lists so that the least significant digits come first.

Then perform normal addition, just like LeetCode 2.

After creating the result, reverse it again to restore the required forward order.

### Algorithm

1. Reverse both input linked lists using a `reverse()` method.
2. Initialize `carry = 0`.
3. Create a dummy node and initialize `cur = dummy`.
4. Traverse both reversed lists while either list has nodes or carry is not zero.
5. Initialize `sum = carry`.
6. If `l1` is not null:
   - Add `l1.val` to sum.
   - Move `l1` forward.
7. If `l2` is not null:
   - Add `l2.val` to sum.
   - Move `l2` forward.
8. Calculate the new carry using `sum / 10`.
9. Create a new node with `sum % 10` and attach it to the result.
10. Reverse the result linked list.
11. Return the reversed result.

### Code (Java)

    class Solution {
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

            l1 = reverse(l1);
            l2 = reverse(l2);

            int carry = 0;

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            while (l1 != null || l2 != null || carry != 0) {

                int sum = carry;

                if (l1 != null) {
                    sum += l1.val;
                    l1 = l1.next;
                }

                if (l2 != null) {
                    sum += l2.val;
                    l2 = l2.next;
                }

                carry = sum / 10;

                cur.next = new ListNode(sum % 10);
                cur = cur.next;
            }

            return reverse(dummy.next);
        }

        public ListNode reverse(ListNode head) {

            ListNode prev = null;
            ListNode cur = head;

            while (cur != null) {

                ListNode next = cur.next;
                cur.next = prev;

                prev = cur;
                cur = next;
            }

            return prev;
        }
    }

### Complexity

Let `n` and `m` be the lengths of the two linked lists.

- **Time:** O(n + m) — reversing both lists and performing addition.
- **Auxiliary Space:** O(1) — no additional collection or recursion is used.
- **Output Space:** O(max(n, m)) — for the newly created result list.

**Note:** This approach modifies the original input linked lists because they are reversed.

---

## Approach 2: Stack

### Idea

Since the digits are stored in forward order, the least significant digit is at the end of each linked list.

Use two stacks to access the digits from the end without modifying the original linked lists.

Perform addition using carry and insert every result digit at the beginning of the result linked list.

### Algorithm

1. Create two stacks: `s1` and `s2`.
2. Traverse the first linked list and push all its values into `s1`.
3. Traverse the second linked list and push all its values into `s2`.
4. Initialize `carry = 0` and `head = null`.
5. Continue while either stack has elements or carry is not zero.
6. Initialize `sum = carry`.
7. If `s1` is not empty, pop one digit and add it to sum.
8. If `s2` is not empty, pop one digit and add it to sum.
9. Calculate the new carry using `sum / 10`.
10. Create a new node with `sum % 10`.
11. Insert the new node at the beginning of the result list.
12. Return `head`.

### Code (Java)

    class Solution {
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

            Stack<Integer> s1 = new Stack<>();
            Stack<Integer> s2 = new Stack<>();

            while (l1 != null) {
                s1.push(l1.val);
                l1 = l1.next;
            }

            while (l2 != null) {
                s2.push(l2.val);
                l2 = l2.next;
            }

            int carry = 0;
            ListNode head = null;

            while (!s1.isEmpty() || !s2.isEmpty() || carry != 0) {

                int sum = carry;

                if (!s1.isEmpty()) {
                    sum += s1.pop();
                }

                if (!s2.isEmpty()) {
                    sum += s2.pop();
                }

                carry = sum / 10;

                ListNode node = new ListNode(sum % 10);

                node.next = head;
                head = node;
            }

            return head;
        }
    }

### Complexity

Let `n` and `m` be the lengths of the two linked lists.

- **Time:** O(n + m) — pushing and popping each digit once.
- **Auxiliary Space:** O(n + m) — storing digits in two stacks.
- **Output Space:** O(max(n, m)) — for the result linked list.

**Note:** This approach does not modify the original input linked lists.

---

## Comparison

| Approach | Time | Auxiliary Space | Modifies Input? |
|---|---|---|---|
| Reverse Linked Lists | O(n + m) | O(1) | Yes |
| Stack | O(n + m) | O(n + m) | No |

## Key Takeaways

1. LeetCode 445 stores digits in forward order.
2. Normal addition starts from the least significant digit.
3. Reversing the lists allows direct addition from the head.
4. Stacks provide access to the last node without reversing the original lists.
5. `sum % 10` gives the result digit.
6. `sum / 10` gives the carry.
7. Always include `carry != 0` in the loop condition to handle a remaining carry.

## Interview Recommendation

Both approaches achieve O(n + m) time.

- **Reverse Linked Lists:** Better auxiliary space complexity, O(1), but modifies the input lists.
- **Stack:** Preserves the original input lists but requires O(n + m) auxiliary space.

Use the **Stack approach** when you should not modify the input lists. Use the **Reverse Linked Lists approach** when O(1) auxiliary space is preferred and modifying the input lists is acceptable.
