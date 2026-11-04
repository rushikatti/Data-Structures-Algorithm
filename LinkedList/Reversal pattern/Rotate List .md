# Rotate List (LeetCode 61)

## Problem

Given the head of a linked list, rotate the list to the right by `k` places.

**Example 1:**

Input:
`1 -> 2 -> 3 -> 4 -> 5`, `k = 2`

Output:
`4 -> 5 -> 1 -> 2 -> 3`

**Example 2:**

Input:
`0 -> 1 -> 2`, `k = 4`

Output:
`2 -> 0 -> 1`

---

## Approach 1: Brute Force (ArrayList)

### Idea

Store all node values in an ArrayList, calculate their new positions after rotation, and update the original linked list.

### Algorithm

1. Traverse the linked list and store values in an ArrayList.
2. Calculate effective rotation using `k = k % length`.
3. Create another ArrayList of the same size.
4. Calculate the new index of each element:

   `newIndex = (i + k) % length`

5. Store each value at its new index.
6. Update the original linked list with the rotated values.

### Code (Java)

    class Solution {
        public ListNode rotateRight(ListNode head, int k) {

            if (head == null || head.next == null || k == 0) {
                return head;
            }

            ListNode originalHead = head;

            ArrayList<Integer> list = new ArrayList<>();

            int length = 0;

            // Step 1: Store values
            while (head != null) {
                list.add(head.val);
                head = head.next;
                length++;
            }

            // Step 2: Calculate effective rotation
            k = k % length;

            if (k == 0) {
                return originalHead;
            }

            // Step 3: Create rotated list
            List<Integer> rotated = new ArrayList<>(
                Collections.nCopies(length, 0)
            );

            for (int i = 0; i < length; i++) {
                int newIndex = (i + k) % length;
                rotated.set(newIndex, list.get(i));
            }

            // Step 4: Update linked list
            ListNode curr = originalHead;
            int index = 0;

            while (curr != null) {
                curr.val = rotated.get(index++);
                curr = curr.next;
            }

            return originalHead;
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n)

---

## Approach 2: Optimal (Circular Linked List)

### Idea

Instead of repeatedly moving nodes, temporarily convert the linked list into a circular linked list.

Then find the new tail, update the head, and break the circle.

For a list of length `n`, effective rotation is:

`newk = k % n`

The new tail is at position:

`length - newk - 1` (0-based index).

### Algorithm

1. If the list is empty or contains only one node, return `head`.
2. Traverse the list to find its length and tail.
3. Calculate `newk = k % length`.
4. If `newk == 0`, return the original head.
5. Connect the tail to the head to make the list circular.
6. Move `length - newk - 1` steps from the head to find the new tail.
7. The node after the new tail becomes the new head.
8. Break the circle by setting `newTail.next = null`.
9. Return the new head.

### Code (Java)

    class Solution {
        public ListNode rotateRight(ListNode head, int k) {

            if (head == null || head.next == null || k == 0) {
                return head;
            }

            // Step 1: Find length and tail
            ListNode cur = head;
            int length = 1;

            while (cur.next != null) {
                cur = cur.next;
                length++;
            }

            // Step 2: Calculate effective rotation
            int newk = k % length;

            if (newk == 0) {
                return head;
            }

            // Step 3: Make list circular
            cur.next = head;

            // Step 4: Find new tail
            ListNode newcur = head;

            for (int i = 0; i < length - newk - 1; i++) {
                newcur = newcur.next;
            }

            // Step 5: Update head and break circle
            ListNode newhead = newcur.next;
            newcur.next = null;

            return newhead;
        }
    }

### Complexity

- **Time:** O(n) — finding length and locating the new tail.
- **Space:** O(1) — only pointers and integer variables are used.

---

## Dry Run (Optimal Approach)

Input:

    1 -> 2 -> 3 -> 4 -> 5
    k = 7

### Step 1: Find length and tail

    length = 5
    tail = 5

### Step 2: Calculate effective rotation

    newk = k % length
         = 7 % 5
         = 2

### Step 3: Make the list circular

    1 -> 2 -> 3 -> 4 -> 5
    ^                   |
    |___________________|

### Step 4: Find new tail

    steps = length - newk - 1
          = 5 - 2 - 1
          = 2

Move two steps from head:

    1 -> 2 -> 3 -> 4 -> 5
              ^
           newTail

### Step 5: Update head and break circle

    newHead = newTail.next
            = 4

    newTail.next = null

Final linked list:

    4 -> 5 -> 1 -> 2 -> 3

Output: `4 -> 5 -> 1 -> 2 -> 3`

---

## Edge Cases

| Input | k | Expected Output |
|---|---:|---|
| `1 -> 2 -> 3 -> 4 -> 5` | 2 | `4 -> 5 -> 1 -> 2 -> 3` |
| `0 -> 1 -> 2` | 4 | `2 -> 0 -> 1` |
| `1 -> 2` | 2 | `1 -> 2` |
| `1 -> 2 -> 3` | 3 | `1 -> 2 -> 3` |
| `1` | 100 | `1` |

---

## Approach Comparison

| Approach | Time | Space |
|---|---|---|
| Brute Force (ArrayList) | O(n) | O(n) |
| Optimal (Circular Linked List) | O(n) | O(1) |

## Important Patterns to Remember

1. **Length Calculation** — Find the total number of nodes.
2. **Modulo Operation** — Use `k % length` to eliminate unnecessary rotations.
3. **Circular Linked List** — Temporarily connect tail to head.
4. **Pointer Reconnection** — Find the new tail and update the head.
5. **Break the Circle** — Set `newTail.next = null`.

## Interview Takeaway

The most important optimization is:

    k = k % length;

For example, rotating a list of 5 nodes by 7 positions is equivalent to rotating it by 2 positions.

**Optimal complexity: O(n) time and O(1) auxiliary space.**

**Important:** Calculate `newk` and check whether it is zero before making the list circular. Otherwise, returning early can leave a cycle in the linked list.
