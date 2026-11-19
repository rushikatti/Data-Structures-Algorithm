# LeetCode 1019: Next Greater Node In Linked List

## Problem

Given the head of a linked list, return an array containing the next greater value for every node.

The next greater value of a node is the first value that is strictly greater than its value among the nodes that come after it.

If there is no greater value, store `0`.

**Example 1:**

Input: `head = [2,1,5]`

Output: `[5,5,0]`

**Example 2:**

Input: `head = [2,7,4,3,5]`

Output: `[7,0,5,5,0]`

---

## Approach 1: Brute Force — Nested Loops

### Idea

For every node, traverse the remaining nodes to find the first greater value.

If a greater value is found, store it. Otherwise, store `0`.

### Algorithm

1. Traverse the linked list and store all node values in an ArrayList.
2. Create an integer array of size `n`.
3. For each element, check all elements to its right.
4. If an element greater than the current value is found, store it and stop searching.
5. If no greater element exists, keep the result as `0`.
6. Return the result array.

### Code (Java)

    class Solution {
        public int[] nextLargerNodes(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            int n = list.size();
            int[] result = new int[n];

            for (int i = 0; i < n; i++) {

                for (int j = i + 1; j < n; j++) {

                    if (list.get(j) > list.get(i)) {
                        result[i] = list.get(j);
                        break;
                    }
                }
            }

            return result;
        }
    }

### Complexity

- **Time:** O(n²) — nested loops check the elements to the right.
- **Space:** O(n) — ArrayList stores all node values. The result array is also O(n).

---

## Approach 2: Optimal — Monotonic Stack

### Idea

Use a monotonic decreasing stack to find the next greater element efficiently.

Instead of searching for the next greater value for every node, process the values from left to right.

Maintain a stack containing indices of elements whose next greater value has not been found yet.

For every current value:
- While the stack is not empty and the current value is greater than the value at the stack's top index, the current value is the next greater element for that index.
- Store the current value in the result array.
- Push the current index onto the stack.

### Algorithm

1. Traverse the linked list and store all node values in an ArrayList.
2. Create a result array of size `n`. By default, all values are `0`.
3. Create a stack to store indices.
4. Traverse the ArrayList using index `i`.
5. While the stack is not empty and the current value is greater than the value at the top index:
   - Pop the index.
   - Set `result[index] = list.get(i)`.
6. Push the current index onto the stack.
7. Return the result array.

### Code (Java)

    class Solution {
        public int[] nextLargerNodes(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            int n = list.size();
            int[] result = new int[n];

            Deque<Integer> stack = new ArrayDeque<>();

            for (int i = 0; i < n; i++) {

                while (!stack.isEmpty() &&
                       list.get(i) > list.get(stack.peek())) {

                    int index = stack.pop();

                    result[index] = list.get(i);
                }

                stack.push(i);
            }

            return result;
        }
    }

### Complexity

- **Time:** O(n) — every index is pushed and popped at most once.
- **Space:** O(n) — ArrayList and stack store up to n elements. The result array also requires O(n) space.

---

## Comparison

| Approach | Time | Space | Technique |
|---|---|---|---|
| Brute Force | O(n²) | O(n) | Nested loops |
| Monotonic Stack | O(n) | O(n) | Stack + indices |

## Key Takeaways

1. Next Greater Element means finding the first strictly greater element on the right.
2. Brute force checks every element to the right.
3. A monotonic decreasing stack helps solve the problem in O(n).
4. Store indices in the stack, not values, because we need to update the correct result positions.
5. Elements remaining in the stack have no next greater element, so their result stays `0`.
6. Each index is pushed and popped at most once.

## Interview Recommendation

Use the **Monotonic Stack** approach.

It reduces the time complexity from O(n²) to O(n), making it the optimal solution.
