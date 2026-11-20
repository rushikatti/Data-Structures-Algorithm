# Search in a Linked List

## Problem

Given the head of a singly linked list and an integer `key`, search for the key in the linked list.

Return `true` if the key exists; otherwise, return `false`.

**Example 1:**

Input: `head = [10,20,30,40], key = 30`

Output: `true`

**Example 2:**

Input: `head = [10,20,30,40], key = 50`

Output: `false`

---

## Approach 1: Iterative — Linear Search

### Idea

Traverse the linked list from the head and compare each node's value with the given key.

If a match is found, return `true`. If the traversal reaches `null`, return `false`.

### Algorithm

1. Initialize a pointer `cur` at `head`.
2. Traverse while `cur != null`.
3. If `cur.val == key`, return `true`.
4. Otherwise, move to the next node.
5. If the entire list is traversed without finding the key, return `false`.

### Code (Java)

    class Solution {
        public boolean searchKey(ListNode head, int key) {

            ListNode cur = head;

            while (cur != null) {

                if (cur.val == key) {
                    return true;
                }

                cur = cur.next;
            }

            return false;
        }
    }

### Complexity

- **Time:** O(n) — in the worst case, every node is visited.
- **Space:** O(1) — only one pointer is used.

---

## Approach 2: Recursive Search

### Idea

Use recursion to check the current node and then search the remaining linked list.

### Algorithm

1. If `head == null`, return `false`.
2. If `head.val == key`, return `true`.
3. Otherwise, recursively search from `head.next`.
4. Return the recursive result.

### Code (Java)

    class Solution {
        public boolean searchKey(ListNode head, int key) {

            if (head == null) {
                return false;
            }

            if (head.val == key) {
                return true;
            }

            return searchKey(head.next, key);
        }
    }

### Complexity

- **Time:** O(n) — each node is visited at most once.
- **Space:** O(n) — recursive call stack in the worst case.

---

## Comparison

| Approach | Time | Space | Technique |
|---|---|---|---|
| Iterative | O(n) | O(1) | Linear Search |
| Recursive | O(n) | O(n) | Recursion |

## Key Takeaways

1. A linked list does not support direct index-based access.
2. Searching requires traversing nodes one by one.
3. Iterative search is more space-efficient than recursive search.
4. Always check `cur != null` before accessing `cur.val`.

## Interview Recommendation

Use **Iterative Linear Search**.

It is simple and achieves O(n) time with O(1) auxiliary space.
