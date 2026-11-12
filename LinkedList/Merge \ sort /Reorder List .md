# LeetCode 143: Reorder List

## Problem

Given the head of a singly linked list, reorder the list in the following pattern:

L0 → L1 → L2 → ... → Ln-1 → Ln

Reorder it as:

L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → ...

- The first node should remain first.
- The last node should become second.
- Continue alternating between the beginning and end.
- Do not change node values in the optimal solution; rearrange the node links.

Example 1:

    Input:  head = [1,2,3,4,5]
    Output: [1,5,2,4,3]

Example 2:

    Input:  head = [1,2,3,4,5,6]
    Output: [1,6,2,5,3,4]

---

## Approach 1: Brute Force — Using ArrayList

### Idea

Store all node values in an ArrayList and use two pointers to rearrange the values.

- `left`: Starts at index 0.
- `right`: Starts at the last index.
- `list2`: Stores the reordered values.

Alternately pick elements from left and right and update the original linked list values.

### Algorithm

1. Traverse the linked list and store all node values in an ArrayList.
2. Initialize `left = 0` and `right = list.size() - 1`.
3. Create another ArrayList to store reordered values.
4. While `left <= right`:
   - Add the left element and increment `left`.
   - If elements remain, add the right element and decrement `right`.
5. Traverse the original linked list.
6. Update each node's value using the reordered ArrayList.

### Code (Java)

    class Solution {
        public void reorderList(ListNode head) {

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            int left = 0;
            int right = list.size() - 1;

            ArrayList<Integer> list2 = new ArrayList<>();

            while (left <= right) {

                list2.add(list.get(left++));

                if (left <= right) {
                    list2.add(list.get(right--));
                }
            }

            cur = head;
            int idx = 0;

            while (cur != null) {
                cur.val = list2.get(idx++);
                cur = cur.next;
            }
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → 4 → 5 → 6

Initially:

    left = 0
    right = 5

**Iteration 1:**

    Pick left = 1
    Pick right = 6

    Result: 1 → 6

**Iteration 2:**

    Pick left = 2
    Pick right = 5

    Result: 1 → 6 → 2 → 5

**Iteration 3:**

    Pick left = 3
    Pick right = 4

    Result: 1 → 6 → 2 → 5 → 3 → 4

Final result:

    1 → 6 → 2 → 5 → 3 → 4

### Complexity

- **Time:** O(n) — traversing the list, rearranging values, and updating nodes.
- **Space:** O(n) — two ArrayLists store the elements.

---

## Approach 2: Optimal — Slow & Fast Pointers + Reverse + Merge

### Idea

Divide the linked list into two halves, reverse the second half, and merge both halves alternately.

Use three main operations:

1. Find the middle using slow and fast pointers.
2. Reverse the second half using three pointers.
3. Merge both halves alternately.

### Algorithm

1. Initialize `slow = head` and `fast = head`.
2. Move slow one step and fast two steps until slow reaches the middle.
3. Split the list into two halves:
   - `first = head`
   - `second = slow.next`
   - Set `slow.next = null`.
4. Reverse the second half using `prev`, `cur`, and `next`.
5. Set `first = head` and `second = prev`.
6. Merge alternately:
   - Store `first.next` in `temp1`.
   - Store `second.next` in `temp2`.
   - Connect `first.next = second`.
   - Connect `second.next = temp1`.
   - Move both pointers forward.
7. Stop when the second half is exhausted.

### Code (Java)

    class Solution {
        public void reorderList(ListNode head) {

            if (head == null || head.next == null) {
                return;
            }

            // 1. Find middle
            ListNode slow = head;
            ListNode fast = head;

            while (fast.next != null && fast.next.next != null) {
                slow = slow.next;
                fast = fast.next.next;
            }

            // 2. Split into two halves
            ListNode second = slow.next;
            slow.next = null;

            // 3. Reverse second half
            ListNode prev = null;
            ListNode cur = second;

            while (cur != null) {
                ListNode next = cur.next;

                cur.next = prev;
                prev = cur;
                cur = next;
            }

            // 4. Merge alternately
            ListNode first = head;
            second = prev;

            while (second != null) {

                ListNode temp1 = first.next;
                ListNode temp2 = second.next;

                first.next = second;
                second.next = temp1;

                first = temp1;
                second = temp2;
            }
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → 4 → 5 → 6

**Step 1: Find the middle**

    slow = 3
    fast = 5

**Step 2: Split the list**

    First half:  1 → 2 → 3
    Second half: 4 → 5 → 6

**Step 3: Reverse the second half**

    First half:  1 → 2 → 3
    Second half: 6 → 5 → 4

**Step 4: Merge alternately**

    Pick 1 from first half.
    Pick 6 from second half.

    1 → 6 → 2 → 5 → 3 → 4

Final result:

    1 → 6 → 2 → 5 → 3 → 4

### Complexity

- **Time:** O(n) — finding the middle, reversing the second half, and merging.
- **Space:** O(1) — only pointers are used.

---

## Comparison

| Feature | ArrayList | Optimal |
|---|---|---|
| Technique | Two pointers | Slow/fast + reverse + merge |
| Time | O(n) | O(n) |
| Space | O(n) | O(1) |
| Changes node values | Yes | No |
| Rearranges node links | No | Yes |
| Recommended | Beginner-friendly | Interview optimal |

---

## Key Takeaways

1. Two pointers can rearrange elements from opposite ends of an array.
2. Slow and fast pointers help find the middle of a linked list.
3. Reversing the second half is a common linked-list technique.
4. Merging two lists alternately is useful in many linked-list problems.
5. The optimal solution uses O(1) auxiliary space.

## Interview Recommendation

Know both approaches:

- **ArrayList:** Easy to understand and implement, but uses O(n) extra space and changes node values.
- **Optimal:** Combines three important linked-list patterns and rearranges actual node connections.

For interviews, prefer the optimal solution because it achieves O(n) time and O(1) auxiliary space.
