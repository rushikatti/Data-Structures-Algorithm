# LeetCode 92: Reverse Linked List II

## Problem

Given the head of a singly linked list and two positions `left` and `right`, reverse the nodes from position `left` to position `right` and return the modified list.

- Positions are 1-indexed.
- Reverse only the specified portion.
- Do not change the values; rearrange the node links.

Example 1:

    Input:  head = [1,2,3,4,5], left = 2, right = 4
    Output: [1,4,3,2,5]

Example 2:

    Input:  head = [5], left = 1, right = 1
    Output: [5]

---

## Approach 1: Iterative — Head Insertion (My Approach)

### Idea

Use a dummy node and repeatedly move the node after `cur` to the beginning of the sublist being reversed.

- `dummy`: Handles the case where `left == 1`.
- `prev`: Points to the node just before the reversal section.
- `cur`: Remains at the original first node of the reversal section.
- `temp`: Temporarily stores the first node of the current sublist.

In every iteration, move `cur.next` to the position immediately after `prev`.

### Algorithm

1. Create a dummy node and connect it to head.
2. Initialize `prev = dummy`.
3. Move `prev` to the node just before position `left`.
4. Initialize `cur = prev.next`.
5. Repeat `right - left` times:
   - Store the current first node: `temp = prev.next`.
   - Move `cur.next` after `prev`.
   - Remove the moved node from its original position.
   - Connect the moved node to `temp`.
6. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode reverseBetween(ListNode head, int left, int right) {

            if (head == null || head.next == null) {
                return head;
            }

            ListNode dummy = new ListNode(1);
            dummy.next = head;

            ListNode prev = dummy;

            for (int i = 1; i < left; i++) {
                prev = prev.next;
            }

            ListNode cur = prev.next;

            for (int i = 1; i <= right - left; i++) {
                ListNode temp = prev.next;

                prev.next = cur.next;
                cur.next = cur.next.next;
                prev.next.next = temp;
            }

            return dummy.next;
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → 4 → 5
    left = 2, right = 4

Initially:

    dummy → 1 → 2 → 3 → 4 → 5

Move `prev` to the node before position 2:

    prev = 1
    cur = 2

**Iteration 1: Move node 3 to the beginning of the sublist**

    1 → 3 → 2 → 4 → 5

**Iteration 2: Move node 4 to the beginning of the sublist**

    1 → 4 → 3 → 2 → 5

Final result:

    1 → 4 → 3 → 2 → 5

### Complexity

- **Time:** O(n) — locating the starting position and reversing the sublist.
- **Space:** O(1) — only pointers are used.

---

## Approach 2: Iterative — Three Pointers

### Idea

First reach the node at position `left`. Then reverse the sublist using the standard three-pointer technique.

Use:
- `prev`: Previous node during reversal.
- `curr`: Current node.
- `next`: Temporarily stores the next node.

After reversing the sublist, reconnect it to the remaining list.

### Algorithm

1. Create a dummy node pointing to head.
2. Move `before` to the node just before position `left`.
3. Set `curr = before.next`.
4. Reverse exactly `right - left + 1` nodes using three pointers.
5. Connect `before.next` to the new head of the reversed section.
6. Connect the original first node of the section to the remaining list.
7. Return `dummy.next`.

### Code (Java)

    class Solution {
        public ListNode reverseBetween(ListNode head, int left, int right) {

            if (head == null || head.next == null || left == right) {
                return head;
            }

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode before = dummy;

            for (int i = 1; i < left; i++) {
                before = before.next;
            }

            ListNode curr = before.next;
            ListNode prev = null;

            for (int i = 0; i < right - left + 1; i++) {
                ListNode next = curr.next;

                curr.next = prev;
                prev = curr;
                curr = next;
            }

            before.next.next = curr;
            before.next = prev;

            return dummy.next;
        }
    }

### Dry Run

Input:

    1 → 2 → 3 → 4 → 5
    left = 2, right = 4

Before reversal:

    before = 1
    curr = 2

Reverse the sublist:

    2 → 3 → 4

After reversing:

    4 → 3 → 2

Reconnect:

    before.next = 4
    2.next = 5

Final result:

    1 → 4 → 3 → 2 → 5

### Complexity

- **Time:** O(n) — one traversal to locate the position and one to reverse.
- **Space:** O(1).

---

## Comparison

| Feature | Head Insertion | Three Pointers |
|---|---|---|
| Technique | Move nodes to front | Reverse links |
| Time | O(n) | O(n) |
| Space | O(1) | O(1) |
| Dummy node | Yes | Yes |
| Reversal iterations | right - left | right - left + 1 |
| Recommended | Your approach | Standard approach |

---

## Key Takeaways

1. Your head-insertion approach is a valid optimized solution.
2. `prev` always stays at the node before the reversal section.
3. `cur` remains at the original first node of the section throughout head insertion.
4. Each iteration moves one node from after `cur` to immediately after `prev`.
5. The dummy node handles the edge case where `left = 1`.
6. When `left == right`, no reversal is required.

## Interview Recommendation

Know both approaches:

- **Head Insertion:** Particularly useful for reversing a sublist because it avoids reconnecting the reversed section separately.
- **Three Pointers:** A standard reversal technique that builds on LeetCode 206.

Both achieve O(n) time and O(1) auxiliary space.
