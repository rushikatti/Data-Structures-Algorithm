# 24. Swap Nodes in Pairs (LeetCode 24)

**Problem:** Given the head of a linked list, swap every two adjacent nodes and return the new head.

You must swap the actual nodes, not just their values.

**Example:**

    Input:  1 -> 2 -> 3 -> 4
    Output: 2 -> 1 -> 4 -> 3

    Input:  1 -> 2 -> 3
    Output: 2 -> 1 -> 3

---

## Approach 1: Brute Force – ArrayList

### Idea
1. Traverse the linked list and store all node values in an ArrayList.
2. Swap every two adjacent elements.
3. Traverse the linked list again and update node values.

### Code

    class Solution {
        public ListNode swapPairs(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            for (int i = 0; i + 1 < list.size(); i += 2) {
                int temp = list.get(i);
                list.set(i, list.get(i + 1));
                list.set(i + 1, temp);
            }

            cur = head;
            int i = 0;

            while (cur != null) {
                cur.val = list.get(i++);
                cur = cur.next;
            }

            return head;
        }
    }

### Complexity
- **Time:** O(n) – traversing and swapping elements.
- **Space:** O(n) – storing values in ArrayList.

**Limitation:** This approach swaps values, not actual nodes.

---

## Approach 2: Optimal – In-place Node Swapping

<text>**Idea:** Use a dummy node and change the `next` references to swap adjacent nodes.</text>

### Visual understanding

Initially:

    dummy -> 1 -> 2 -> 3 -> 4
              first second

After swapping the first pair:

    dummy -> 2 -> 1 -> 3 -> 4
                     |
                   prev

For the next pair:

    dummy -> 2 -> 1 -> 4 -> 3

### Algorithm

1. Create a dummy node and connect it to `head`.
2. Maintain `prev`, initially pointing to the dummy node.
3. Identify two nodes:
   - `first = prev.next`
   - `second = first.next`
4. Change the links in this order:
   - `prev.next = second`
   - `first.next = second.next`
   - `second.next = first`
5. Move `prev` to `first`, which is now the second node in the swapped pair.
6. Repeat while at least two nodes remain.
7. Return `dummy.next`.

### Java Code

    class Solution {
        public ListNode swapPairs(ListNode head) {

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode prev = dummy;

            while (prev.next != null && prev.next.next != null) {

                ListNode first = prev.next;
                ListNode second = first.next;

                // Swap the nodes
                prev.next = second;
                first.next = second.next;
                second.next = first;

                // Move to the next pair
                prev = first;
            }

            return dummy.next;
        }
    }

### Dry Run

Input:

    1 -> 2 -> 3 -> 4

**Iteration 1:**

    first  = 1
    second = 2

Update links:

    prev.next = second;       // dummy -> 2
    first.next = second.next; // 1 -> 3
    second.next = first;      // 2 -> 1

Result:

    dummy -> 2 -> 1 -> 3 -> 4

Move:

    prev = first; // prev points to node 1

**Iteration 2:**

    first  = 3
    second = 4

Update links:

    prev.next = second;       // 1 -> 4
    first.next = second.next; // 3 -> null
    second.next = first;      // 4 -> 3

Result:

    dummy -> 2 -> 1 -> 4 -> 3

No more pairs remain.

Return:

    2 -> 1 -> 4 -> 3

### Complexity

- **Time Complexity:** O(n) – each pair is processed once.
- **Space Complexity:** O(1) – only a few pointers are used.

---

## Important Concepts to Remember

| Code | Purpose |
|---|---|
| `dummy.next = head` | Handles swapping when the first node changes |
| `first = prev.next` | Gets the first node of the pair |
| `second = first.next` | Gets the second node of the pair |
| `prev.next = second` | Connects previous part to second node |
| `first.next = second.next` | Connects first node to the remaining list |
| `second.next = first` | Completes the swap |
| `prev = first` | Moves to the next pair |

## Common Mistakes

1. Using `dummy.next` instead of `prev.next` to get the first node. This repeatedly selects the first pair.
2. Moving `prev` to `second` instead of `first`. After swapping, `first` is the last node of the pair.
3. Forgetting to preserve `second.next` through the correct link updates.
4. Returning `head` instead of `dummy.next`. The original head is no longer the first node.

## Edge Cases

| Input | Output |
|---|---|
| `1 -> 2 -> 3 -> 4` | `2 -> 1 -> 4 -> 3` |
| `1 -> 2 -> 3` | `2 -> 1 -> 3` |
| `1 -> 2` | `2 -> 1` |
| `1` | `1` |
| `null` | `null` |

## Approach Comparison

| Approach | Time | Space | Actual node swapping |
|---|---:|---:|---|
| ArrayList | O(n) | O(n) | No |
| In-place | O(n) | O(1) | Yes |

**Interview takeaway:** Master the dummy-node pattern. It is useful in linked-list problems such as Reverse Linked List II, Remove Nth Node From End, and other node-reconnection problems.
