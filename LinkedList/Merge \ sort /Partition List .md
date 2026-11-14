# LeetCode 86: Partition List

## Problem

Given the head of a linked list and a value `x`, partition it such that all nodes with values less than `x` come before nodes with values greater than or equal to `x`.

You should preserve the original relative order of the nodes in each of the two partitions.

- All nodes with values `< x` should come first.
- All nodes with values `>= x` should come after.
- Maintain the original relative order.
- Do not change node values; rearrange the node links in the optimal solution.

Example 1:

    Input:  head = [1,4,3,2,5,2], x = 3
    Output: [1,2,2,4,3,5]

Example 2:

    Input:  head = [2,1], x = 2
    Output: [1,2]

---

## Approach 1: Brute Force — Using ArrayList (My Approach)

### Idea

Use an ArrayList to store elements in the required partition order.

- `l1`: Stores all elements smaller than `x`.
- Traverse the list again and store all elements greater than or equal to `x`.
- Finally, update the original linked list using the ArrayList.

Since we traverse the original list from beginning to end in both passes, the relative order is maintained.

### Algorithm

1. Create an empty ArrayList `l1`.
2. Traverse the linked list:
   - If `cur.val < x`, add the value to `l1`.
3. Traverse the linked list again:
   - If `cur.val >= x`, add the value to `l1`.
4. Traverse the original linked list again.
5. Update each node's value using elements from `l1`.
6. Return head.

### Code (Java)

    class Solution {
        public ListNode partition(ListNode head, int x) {

            ArrayList<Integer> l1 = new ArrayList<>();

            ListNode cur = head;

            // Store elements smaller than x
            while (cur != null) {
                if (cur.val < x) {
                    l1.add(cur.val);
                }
                cur = cur.next;
            }

            cur = head;

            // Store elements greater than or equal to x
            while (cur != null) {
                if (cur.val >= x) {
                    l1.add(cur.val);
                }
                cur = cur.next;
            }

            // Update original linked list
            cur = head;
            int index = 0;

            while (cur != null) {
                cur.val = l1.get(index++);
                cur = cur.next;
            }

            return head;
        }
    }


### Complexity

- **Time:** O(n) — three traversals of the linked list.
- **Space:** O(n) — ArrayList stores all node values.

---

## Approach 2: Optimal — Two Dummy Nodes (Two Lists)

### Idea

Create two separate linked lists:

- `small`: Stores nodes with values smaller than `x`.
- `large`: Stores nodes with values greater than or equal to `x`.

Use dummy nodes to simplify list construction.

- `smalldummy`: Dummy head of the smaller list.
- `largedummy`: Dummy head of the larger list.
- `small`: Points to the last node in the smaller list.
- `large`: Points to the last node in the larger list.

After traversing the original list, connect both lists.

### Algorithm

1. Create two dummy nodes:
   - `smalldummy`
   - `largedummy`
2. Initialize `small = smalldummy` and `large = largedummy`.
3. Traverse the original linked list using `cur`.
4. For each node:
   - If `cur.val < x`, attach it to the smaller list and move `small`.
   - Otherwise, attach it to the larger list and move `large`.
5. Connect the smaller list to the larger list:
   - `small.next = largedummy.next`
6. Terminate the larger list:
   - `large.next = null`
7. Return `smalldummy.next`.

### Code (Java)

    class Solution {
        public ListNode partition(ListNode head, int x) {

            ListNode smalldummy = new ListNode(0);
            ListNode largedummy = new ListNode(0);

            ListNode small = smalldummy;
            ListNode large = largedummy;

            ListNode cur = head;

            while (cur != null) {

                if (cur.val < x) {
                    small.next = cur;
                    small = small.next;
                }
                else {
                    large.next = cur;
                    large = large.next;
                }

                cur = cur.next;
            }

            // Connect both lists
            small.next = largedummy.next;

            // Terminate the larger list
            large.next = null;

            return smalldummy.next;
        }
    }



### Complexity

- **Time:** O(n) — one traversal of the linked list.
- **Space:** O(1) — only dummy nodes and pointers are used; no additional nodes proportional to input size.

---

## Comparison

| Feature | ArrayList | Two Dummy Nodes |
|---|---|---|
| Technique | Store and update values | Build two linked lists |
| Time | O(n) | O(n) |
| Space | O(n) | O(1) |
| Changes node values | Yes | No |
| Rearranges node links | No | Yes |
| Preserves relative order | Yes | Yes |
| Recommended | Beginner-friendly | Interview optimal |

---

## Key Takeaways

1. Partitioning a linked list means separating nodes based on a given condition.
2. Two separate lists can maintain the relative order of elements.
3. Dummy nodes simplify insertion into initially empty linked lists.
4. `small.next = largedummy.next` connects both partitions.
5. `large.next = null` is important to avoid retaining unwanted links or creating a cycle.
6. Always save the next node before modifying links when using an existing linked list.

## Interview Recommendation

Know both approaches:

- **ArrayList:** Easy to understand, but uses O(n) extra space and changes node values.
- **Two Dummy Nodes:** Optimal because it rearranges actual node connections while preserving relative order.

Prefer the two-dummy-node solution in interviews. It achieves O(n) time and O(1) auxiliary space.
