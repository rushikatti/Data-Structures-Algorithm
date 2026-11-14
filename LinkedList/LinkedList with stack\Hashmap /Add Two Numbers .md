# LeetCode 2: Add Two Numbers

## Problem

You are given two non-empty linked lists representing two non-negative integers.

The digits are stored in **reverse order**, and each node contains a single digit.

Add the two numbers and return the sum as a linked list.

**Example:**

Input:
- `l1 = [2,4,3]`
- `l2 = [5,6,4]`

Output: `[7,0,8]`

Explanation: 342 + 465 = 807.

---

## Approach 1: Brute Force — ArrayList

### Idea

Convert both linked lists into ArrayLists, then perform addition digit by digit using a carry.

Store the result in another ArrayList and convert it back into a linked list.

### Algorithm

1. Traverse the first linked list and store its values in `list1`.
2. Traverse the second linked list and store its values in `list2`.
3. Initialize two pointers `i`, `j` and `carry = 0`.
4. Continue while either list has remaining digits or carry is not zero.
5. Calculate the sum of the current digits and carry.
6. Store `sum % 10` in the result ArrayList.
7. Update carry using `sum / 10`.
8. Create a new linked list using the result ArrayList.
9. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

            ArrayList<Integer> list1 = new ArrayList<>();
            ArrayList<Integer> list2 = new ArrayList<>();

            while (l1 != null) {
                list1.add(l1.val);
                l1 = l1.next;
            }

            while (l2 != null) {
                list2.add(l2.val);
                l2 = l2.next;
            }

            ArrayList<Integer> ans = new ArrayList<>();

            int i = 0, j = 0, carry = 0;

            while (i < list1.size() || j < list2.size() || carry != 0) {

                int sum = carry;

                if (i < list1.size()) {
                    sum += list1.get(i++);
                }

                if (j < list2.size()) {
                    sum += list2.get(j++);
                }

                ans.add(sum % 10);
                carry = sum / 10;
            }

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            for (int num : ans) {
                cur.next = new ListNode(num);
                cur = cur.next;
            }

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(n + m) — traversing both lists and building the result.
- **Space:** O(n + m) — storing both input lists and the result ArrayList.

---

## Approach 2: Optimal — Direct Linked List Addition

### Idea

Instead of storing values in ArrayLists, perform addition directly while traversing both linked lists.

Use:
- `carry` to store the carry from the previous addition.
- `dummy` to simplify result-list creation.
- `cur` to build the result linked list.

### Algorithm

1. Create a dummy node and initialize `cur = dummy`.
2. Initialize `carry = 0`.
3. Continue while `l1 != null`, `l2 != null`, or `carry != 0`.
4. Initialize `sum = carry`.
5. If `l1` is not null:
   - Add `l1.val` to sum.
   - Move `l1` forward.
6. If `l2` is not null:
   - Add `l2.val` to sum.
   - Move `l2` forward.
7. Calculate the new carry using `sum / 10`.
8. Create a new node with `sum % 10`.
9. Move `cur` forward.
10. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            int carry = 0;

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

            return dummy.next;
        }
    }

### Complexity

Let `n` be the length of the first list and `m` be the length of the second list.

- **Time:** O(max(n, m)) — each node is visited once.
- **Space:** O(max(n, m)) — for the newly created result linked list.
- **Auxiliary Space:** O(1) — no additional collection or recursion is used.

---

## Comparison

| Approach | Time | Extra Space (excluding output) |
|---|---|---|
| ArrayList | O(n + m) | O(n + m) |
| Direct Linked List | O(max(n, m)) | O(1) |

## Key Takeaways

1. Since digits are stored in reverse order, addition starts from the head.
2. `sum % 10` gives the digit to store in the result.
3. `sum / 10` gives the carry for the next addition.
4. Use `dummy` to simplify result linked-list creation.
5. The loop condition must include `carry != 0` to handle a final carry.
6. The optimal approach processes both lists directly without converting them into collections.

## Interview Recommendation

Use **Approach 2: Direct Linked List Addition**.

It is the optimal approach because it takes O(max(n, m)) time and uses O(1) auxiliary space, excluding the output linked list.
