# LeetCode 82: Remove Duplicates from Sorted List II

## Problem

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Return the linked list sorted as well.

- Remove all occurrences of duplicate values.
- Keep only values that appear exactly once.
- The linked list is sorted in non-decreasing order.
- Rearrange node connections to remove duplicates.

Example 1:

    Input:  head = [1,2,3,3,4,4,5]
    Output: [1,2,5]

Example 2:

    Input:  head = [1,1,1,2,3]
    Output: [2,3]

---

## Approach 1: Brute Force — Using HashMap

### Idea

Use a HashMap to count the frequency of each element.

- `map`: Stores each value and its frequency.
- First traversal counts the occurrences.
- Second traversal keeps only nodes whose frequency is exactly one.

### Algorithm

1. Create a HashMap to store element frequencies.
2. Traverse the linked list and calculate the frequency of each value.
3. Create a dummy node pointing to head.
4. Initialize `prev = dummy` and `cur = head`.
5. Traverse the linked list again:
   - If the frequency of `cur.val` is greater than one, skip the node.
   - Otherwise, connect `prev.next` to `cur` and move `prev` forward.
6. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode deleteDuplicates(ListNode head) {

            HashMap<Integer, Integer> map = new HashMap<>();

            ListNode cur = head;

            // Count frequencies
            while (cur != null) {
                map.put(cur.val, map.getOrDefault(cur.val, 0) + 1);
                cur = cur.next;
            }

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode prev = dummy;
            cur = head;

            // Keep only unique elements
            while (cur != null) {

                if (map.get(cur.val) > 1) {
                    prev.next = cur.next;
                } else {
                    prev = cur;
                }

                cur = cur.next;
            }

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(n) — two traversals of the linked list.
- **Space:** O(n) — HashMap stores the frequencies.

---

## Approach 2: Optimal — Two Pointers

### Idea

Since the linked list is sorted, duplicate values will always be adjacent.

Use a dummy node and two pointers to identify and remove all occurrences of duplicate values.

- `dummy`: Handles cases where the head itself contains duplicates.
- `prev`: Points to the last confirmed unique node.
- `cur`: Traverses the linked list.

If the current node has duplicates, skip all nodes having the same value. Otherwise, move `prev` forward.

### Algorithm

1. Create a dummy node and connect it to head.
2. Initialize `prev = dummy` and `cur = head`.
3. Traverse while `cur != null`.
4. Check whether `cur.next` exists and has the same value as `cur`.
5. If duplicates are found:
   - Store the duplicate value in a variable.
   - Skip all nodes containing that value.
   - Connect `prev.next` to the first different node.
6. If no duplicates are found:
   - Move `prev` to `cur`.
   - Move `cur` to the next node.
7. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode deleteDuplicates(ListNode head) {

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode prev = dummy;
            ListNode cur = head;

            while (cur != null) {

                if (cur.next != null && cur.val == cur.next.val) {

                    int duplicate = cur.val;

                    while (cur != null && cur.val == duplicate) {
                        cur = cur.next;
                    }

                    prev.next = cur;

                } else {

                    prev = cur;
                    cur = cur.next;
                }
            }

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(n) — each node is visited at most once.
- **Space:** O(1) — only pointers and a variable are used.

---

## Comparison

| Feature | HashMap | Two Pointers |
|---|---|---|
| Technique | Frequency counting | Adjacent comparison |
| Time | O(n) | O(n) |
| Space | O(n) | O(1) |
| Requires sorted list | No | Yes |
| Removes all duplicate occurrences | Yes | Yes |
| Recommended | General approach | Interview optimal |

---

## Key Takeaways

1. LeetCode 83 keeps one occurrence of duplicates, whereas LeetCode 82 removes all occurrences of duplicate values.
2. In a sorted linked list, duplicate values are always adjacent.
3. A dummy node helps handle duplicate values at the beginning of the list.
4. `prev.next = cur` skips all nodes containing a duplicate value.
5. Do not move `prev` when duplicates are found.
6. The sorted property allows us to solve the problem without a HashMap.

## Interview Recommendation

- **HashMap:** Useful when the linked list is unsorted and all occurrences of duplicate values must be removed.
- **Two Pointers:** Best for this problem because the list is sorted.

Prefer the two-pointer solution in interviews. It achieves O(n) time and O(1) auxiliary space.
