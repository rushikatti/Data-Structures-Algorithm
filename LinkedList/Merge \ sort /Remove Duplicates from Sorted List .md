# LeetCode 83: Remove Duplicates from Sorted List

## Problem

Given the head of a sorted linked list, delete all duplicates such that each element appears only once.

Return the linked list sorted as well.

- The linked list is sorted in non-decreasing order.
- Keep only one occurrence of each value.
- Rearrange node connections to remove duplicates.

Example 1:

    Input:  head = [1,1,2]
    Output: [1,2]

Example 2:

    Input:  head = [1,1,2,3,3]
    Output: [1,2,3]

---

## Approach 1: Brute Force — Using HashSet

### Idea

Use a HashSet to track values that have already appeared.

- `set`: Stores unique values.
- `dummy`: Helps handle the head node.
- `prev`: Points to the last unique node.
- `cur`: Traverses the linked list.

If the current value already exists in the set, skip that node. Otherwise, add it to the set and move `prev` forward.

### Algorithm

1. Create a dummy node pointing to head.
2. Initialize an empty HashSet.
3. Set `prev = dummy` and `cur = head`.
4. Traverse the linked list:
   - If `cur.val` exists in the HashSet, skip the current node.
   - Otherwise, add `cur.val` to the HashSet and move `prev` to `cur`.
5. Move `cur` to the next node.
6. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode deleteDuplicates(ListNode head) {

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            HashSet<Integer> set = new HashSet<>();

            ListNode prev = dummy;
            ListNode cur = head;

            while (cur != null) {

                if (set.contains(cur.val)) {
                    prev.next = cur.next;
                } else {
                    set.add(cur.val);
                    prev = cur;
                }

                cur = cur.next;
            }

            return dummy.next;
        }
    }

### Dry Run

Input:

    1 → 1 → 2 → 3 → 3

Initially:

    set = {}
    prev = dummy
    cur = 1

**Iteration 1:**

    1 is not present in set.
    Add 1 to set.
    Move prev to 1.

    set = {1}

**Iteration 2:**

    1 already exists in set.
    Skip the duplicate node.

    1 → 2 → 3 → 3

**Iteration 3:**

    2 is not present.
    Add 2 to set.

    set = {1, 2}

**Iteration 4:**

    3 is not present.
    Add 3 to set.

    set = {1, 2, 3}

**Iteration 5:**

    3 already exists.
    Skip the duplicate node.

Final result:

    1 → 2 → 3

### Complexity

- **Time:** O(n) — each node is visited once. HashSet operations take O(1) average time.
- **Space:** O(n) — HashSet stores unique values.

---

## Approach 2: Optimal — Two Pointers

### Idea

Since the linked list is already sorted, duplicate values will always be next to each other.

We only need to compare the current node with the next node.

- `cur`: Traverses the linked list.
- If `cur.val == cur.next.val`, skip the next node.
- Otherwise, move `cur` forward.

### Algorithm

1. Initialize `cur = head`.
2. Traverse while `cur != null` and `cur.next != null`.
3. Compare the current node with the next node.
4. If both values are equal:
   - Skip the duplicate using `cur.next = cur.next.next`.
5. Otherwise, move `cur` to the next node.
6. Return head.

### Code (Java)

    class Solution {
        public ListNode deleteDuplicates(ListNode head) {

            ListNode cur = head;

            while (cur != null && cur.next != null) {

                if (cur.val == cur.next.val) {
                    cur.next = cur.next.next;
                } else {
                    cur = cur.next;
                }
            }

            return head;
        }
    }

### Dry Run

Input:

    1 → 1 → 2 → 3 → 3

Initially:

    cur = 1

**Iteration 1:**

    cur.val = 1
    cur.next.val = 1

    Both are equal.
    Skip the duplicate.

    1 → 2 → 3 → 3

**Iteration 2:**

    cur.val = 1
    cur.next.val = 2

    Not equal.
    Move cur forward.

    cur = 2

**Iteration 3:**

    cur.val = 2
    cur.next.val = 3

    Not equal.
    Move cur forward.

    cur = 3

**Iteration 4:**

    cur.val = 3
    cur.next.val = 3

    Both are equal.
    Skip the duplicate.

    1 → 2 → 3

Final result:

    1 → 2 → 3

### Complexity

- **Time:** O(n) — each node is visited at most once.
- **Space:** O(1) — only one pointer is used.

---

## Comparison

| Feature | HashSet | Two Pointers |
|---|---|---|
| Technique | HashSet | Adjacent comparison |
| Time | O(n) average | O(n) |
| Space | O(n) | O(1) |
| Requires sorted list | No | Yes |
| Recommended | General duplicate removal | Optimal for sorted list |

---

## Key Takeaways

1. In a sorted linked list, duplicate elements are always adjacent.
2. Compare `cur.val` with `cur.next.val` to identify duplicates.
3. `cur.next = cur.next.next` removes a duplicate node by changing links.
4. Do not move `cur` when removing a duplicate because multiple duplicates may appear consecutively.
5. The sorted property allows us to avoid using a HashSet.

## Interview Recommendation

- **HashSet:** Useful when the linked list is unsorted and duplicates need to be removed.
- **Two Pointers:** Best for this problem because the linked list is already sorted.

Prefer the two-pointer solution in interviews. It achieves O(n) time and O(1) auxiliary space.
