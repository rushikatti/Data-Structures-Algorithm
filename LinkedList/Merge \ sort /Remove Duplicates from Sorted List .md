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

## Approach 1: Brute Force — Using ArrayList

### Idea

Store all unique elements in an ArrayList and then update the original linked list using those elements.

- `list`: Stores unique values.
- `cur`: Traverses the original linked list.
- Check the last stored element before adding a new value because the list is sorted.

### Algorithm

1. Create an empty ArrayList.
2. Traverse the linked list using `cur`.
3. For each node:
   - If the ArrayList is empty or its last element is different from `cur.val`, add the value.
   - Otherwise, skip the duplicate.
4. Traverse the original linked list again.
5. Update each node's value using the ArrayList.
6. Disconnect the remaining nodes by setting the last node's `next` to null.
7. Return head.

### Code (Java)

    class Solution {
        public ListNode deleteDuplicates(ListNode head) {

            if (head == null) {
                return head;
            }

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {

                if (list.isEmpty() || list.get(list.size() - 1) != cur.val) {
                    list.add(cur.val);
                }

                cur = cur.next;
            }

            cur = head;
            int idx = 0;

            while (idx < list.size()) {
                cur.val = list.get(idx++);
                if (idx == list.size()) {
                    cur.next = null;
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

    list = []

**Iteration 1:**

    cur.val = 1
    list = [1]

**Iteration 2:**

    cur.val = 1
    Duplicate found. Skip.

**Iteration 3:**

    cur.val = 2
    list = [1, 2]

**Iteration 4:**

    cur.val = 3
    list = [1, 2, 3]

**Iteration 5:**

    cur.val = 3
    Duplicate found. Skip.

Update the original linked list:

    1 → 2 → 3

Final result:

    1 → 2 → 3

### Complexity

- **Time:** O(n) — traversing the list twice.
- **Space:** O(n) — ArrayList stores unique elements.

---

## Approach 2: Optimal — Two Pointers

### Idea

Since the linked list is already sorted, duplicate values will always be next to each other.

Compare the current node with the next node and skip duplicates by changing the links.

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



### Complexity

- **Time:** O(n) — each node is visited at most once.
- **Space:** O(1) — only one pointer is used.

---

## Comparison

| Feature | ArrayList | Two Pointers |
|---|---|---|
| Technique | Store unique values | Adjacent comparison |
| Time | O(n) | O(n) |
| Space | O(n) | O(1) |
| Requires sorted list | Yes (for this implementation) | Yes |
| Modifies node values | Yes | No |
| Recommended | Beginner-friendly | Interview optimal |

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
