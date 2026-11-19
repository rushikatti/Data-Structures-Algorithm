# LeetCode 2487: Remove Nodes From Linked List

## Problem

Given the head of a linked list, remove every node that has a node with a strictly greater value somewhere to its right.

Return the head of the modified linked list.

**Example 1:**

Input: `head = [5,2,13,3,8]`

Output: `[13,8]`

**Example 2:**

Input: `head = [1,1,1,1]`

Output: `[1,1,1,1]`

---

## Approach 1: Brute Force — ArrayList

### Idea

Store all node values in an ArrayList.

For each node, check whether a greater value exists to its right. If no greater value exists, keep that node.

Finally, update the original linked list with the remaining values.

### Algorithm

1. Traverse the linked list and store all values in an ArrayList.
2. Create another ArrayList to store the valid values.
3. For every element, check whether any element to its right is greater.
4. If a greater element exists, skip the current element.
5. Otherwise, add it to the result list.
6. Traverse the original linked list and update its values.
7. Disconnect the remaining nodes by setting the last node's `next` to `null`.
8. Return the head.

### Code (Java)

    class Solution {
        public ListNode removeNodes(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            ArrayList<Integer> result = new ArrayList<>();

            for (int i = 0; i < list.size(); i++) {

                boolean greater = false;

                for (int j = i + 1; j < list.size(); j++) {

                    if (list.get(j) > list.get(i)) {
                        greater = true;
                        break;
                    }
                }

                if (!greater) {
                    result.add(list.get(i));
                }
            }

            cur = head;
            int i = 0;

            while (i < result.size()) {
                cur.val = result.get(i);
                cur = cur.next;
                i++;
            }

            cur.next = null;

            return head;
        }
    }

### Complexity

- **Time:** O(n²) — checking every element against the elements to its right.
- **Space:** O(n) — storing the original and result values.

---

## Approach 2: Better — Monotonic Stack

### Idea

Use a stack to maintain values in decreasing order.

Traverse the linked list from left to right.

For every node:
1. While the stack is not empty and the current value is greater than the stack's top, remove the top.
2. Push the current value.

The remaining stack contains only the values that should stay in the list.

### Algorithm

1. Create an ArrayDeque to use as a stack.
2. Traverse the linked list.
3. While the stack is not empty and the current node's value is greater than the stack's top, pop the stack.
4. Push the current node's value.
5. After traversal, the stack contains the valid values in decreasing order.
6. Rebuild the linked list using those values.
7. Return the new head.

### Code (Java)

    class Solution {
        public ListNode removeNodes(ListNode head) {

            Deque<Integer> stack = new ArrayDeque<>();

            ListNode cur = head;

            while (cur != null) {

                while (!stack.isEmpty() && stack.peek() < cur.val) {
                    stack.pop();
                }

                stack.push(cur.val);
                cur = cur.next;
            }

            ListNode dummy = new ListNode(0);
            ListNode tail = dummy;

            while (!stack.isEmpty()) {

                tail.next = new ListNode(stack.removeLast());
                tail = tail.next;
            }

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(n) — each value is pushed and popped at most once.
- **Space:** O(n) — stack stores the remaining values.

---

## Approach 3: Optimal — Reverse the Linked List

### Idea

Instead of checking every node against the nodes on its right, reverse the linked list.

After reversing, the original right-side nodes become the nodes on the left.

Now traverse the reversed list while maintaining the maximum value seen so far.

- If the current node's value is smaller than the maximum, remove it.
- Otherwise, keep it and update the maximum.

Finally, reverse the list again to restore the original order.

### Algorithm

**Step 1: Reverse the linked list**
- Reverse all links using three pointers: `prev`, `cur`, and `next`.

**Step 2: Remove smaller nodes**
- Initialize `max` with the first node's value.
- Traverse the reversed list.
- If `cur.val < max`, remove the current node by updating `prev.next`.
- Otherwise, update `max` and move `prev`.

**Step 3: Reverse again**
- Reverse the modified list to restore the original order.
- Return the new head.

### Code (Java)

    class Solution {

        public ListNode removeNodes(ListNode head) {

            head = reverse(head);

            ListNode cur = head;
            int max = cur.val;

            ListNode prev = cur;
            cur = cur.next;

            while (cur != null) {

                if (cur.val < max) {
                    prev.next = cur.next;
                } else {
                    max = cur.val;
                    prev = cur;
                }

                cur = cur.next;
            }

            return reverse(head);
        }

        private ListNode reverse(ListNode head) {

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

- **Time:** O(n) — two reversals and one traversal.
- **Space:** O(1) — only pointers and one maximum variable.

---

## Comparison

| Approach | Time | Space | Technique |
|---|---|---|---|
| ArrayList | O(n²) | O(n) | Nested loops |
| Monotonic Stack | O(n) | O(n) | Stack |
| Reverse Linked List | O(n) | O(1) | Reverse + maximum |

## Key Takeaways

1. A node must be removed if any strictly greater value exists to its right.
2. Brute force checks every element to its right.
3. A monotonic stack efficiently removes smaller previous values.
4. Reversing the list changes the right-side comparison into a left-to-right maximum check.
5. The reverse approach modifies links directly without extra data structures.

## Interview Recommendation

Use **Reverse Linked List**.

It achieves O(n) time and O(1) auxiliary space, making it the most space-efficient approach.
