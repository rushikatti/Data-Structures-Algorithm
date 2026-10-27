# LeetCode 328: Odd Even Linked List

## Problem
Given the head of a singly linked list, group all nodes at **odd indices** together, followed by nodes at **even indices**, and return the reordered list.

- Indexing starts at 1.
- Preserve the relative order of nodes within each group.
- Rearrange nodes, not their values.

Example:

    Input:  1 → 2 → 3 → 4 → 5
    Output: 1 → 3 → 5 → 2 → 4

---

## Approach 1: Brute Force — Extra Lists

### Idea
Create two separate linked lists:
- One for nodes at odd positions.
- One for nodes at even positions.

Append nodes to the appropriate list, then connect the odd list to the even list.

For simplicity, use two `ArrayList` collections to store node references and reconnect them afterward.

### Code (Java)

    import java.util.ArrayList;
    import java.util.List;

    class Solution {
        public ListNode oddEvenList(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }

            List<ListNode> odd = new ArrayList<>();
            List<ListNode> even = new ArrayList<>();

            ListNode curr = head;
            int index = 1;

            while (curr != null) {
                if (index % 2 == 1) {
                    odd.add(curr);
                } else {
                    even.add(curr);
                }

                curr = curr.next;
                index++;
            }

            List<ListNode> all = new ArrayList<>();
            all.addAll(odd);
            all.addAll(even);

            for (int i = 0; i < all.size() - 1; i++) {
                all.get(i).next = all.get(i + 1);
            }

            all.get(all.size() - 1).next = null;

            return all.get(0);
        }
    }

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## Approach 2: Optimized — In-Place Two Pointers

### Idea
Maintain two separate chains within the original linked list:

- `odd` points to the last node in the odd-position chain.
- `even` points to the last node in the even-position chain.
- `evenHead` stores the beginning of the even-position chain.

Connect each odd node to the next odd node and each even node to the next even node. Finally, connect the odd chain to `evenHead`.

### Algorithm
1. If the list has zero or one node, return `head`.
2. Initialize:
   - `odd = head`
   - `even = head.next`
   - `evenHead = head.next`
3. While `even != null` and `even.next != null`:
   - Link `odd.next` to `even.next`.
   - Move `odd` forward.
   - Link `even.next` to `odd.next`.
   - Move `even` forward.
4. Connect `odd.next = evenHead`.
5. Return `head`.

### Code (Java)

    class Solution {
        public ListNode oddEvenList(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }

            ListNode odd = head;
            ListNode even = head.next;
            ListNode evenHead = even;

            while (even != null && even.next != null) {
                odd.next = even.next;
                odd = odd.next;

                even.next = odd.next;
                even = even.next;
            }

            odd.next = evenHead;

            return head;
        }
    }

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## Dry Run

Input:

    1 → 2 → 3 → 4 → 5

Initially:

    odd = 1
    even = 2
    evenHead = 2

**Iteration 1:**
- Connect `1 → 3`.
- Move `odd` to `3`.
- Connect `2 → 4`.
- Move `even` to `4`.

**Iteration 2:**
- Connect `3 → 5`.
- Move `odd` to `5`.
- Connect `4 → null`.
- Move `even` to `null`.

Finally, connect `odd.next = evenHead`:

    1 → 3 → 5 → 2 → 4 → null

---

## Comparison

| Feature | Brute Force | Optimized |
|---|---|---|
| Time | O(n) | O(n) |
| Extra space | O(n) | O(1) |
| Modifies links | Yes | Yes |
| Recommended | For understanding | For interviews |

## Key Takeaway

The optimized approach uses **two pointers and one saved reference (`evenHead`)** to rearrange the list without creating extra nodes or collections.

Remember: odd and even refer to **node positions**, not node values.
