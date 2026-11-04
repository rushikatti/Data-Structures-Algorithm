# 25. Reverse Nodes in k-Group (LeetCode 25)

**Problem:** Given the head of a linked list, reverse the nodes of the list `k` at a time and return the modified list.

- Only complete groups of `k` nodes should be reversed.
- If the remaining nodes are fewer than `k`, leave them unchanged.
- You must reverse actual nodes, not just their values.

**Example:**

    Input:  head = [1,2,3,4,5], k = 2
    Output: [2,1,4,3,5]

    Input:  head = [1,2,3,4,5], k = 3
    Output: [3,2,1,4,5]

---

## Approach 1: Brute Force – ArrayList

### Idea

1. Traverse the linked list and store node values in an ArrayList.
2. Process the ArrayList in groups of `k`.
3. Reverse only complete groups.
4. Copy the modified values back into the linked list.

### Algorithm

1. Store all node values in an ArrayList.
2. Iterate through the list with a step of `k`.
3. Check whether a complete group exists.
4. Reverse the group using two pointers, `left` and `right`.
5. Copy the updated values back into the linked list.

### Java Code

    class Solution {
        public ListNode reverseKGroup(ListNode head, int k) {

            if (head == null || k == 1) {
                return head;
            }

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            int n = list.size();

            for (int i = 0; i + k <= n; i += k) {

                int left = i;
                int right = i + k - 1;

                while (left < right) {

                    int temp = list.get(left);

                    list.set(left, list.get(right));
                    list.set(right, temp);

                    left++;
                    right--;
                }
            }

            cur = head;

            for (int i = 0; i < n; i++) {
                cur.val = list.get(i);
                cur = cur.next;
            }

            return head;
        }
    }

### Complexity

- **Time:** O(n) – traversing, reversing groups, and copying values.
- **Space:** O(n) – storing values in ArrayList.

**Limitation:** This approach swaps values rather than reversing actual nodes.

---

## Approach 2: Optimal – In-place Reversal

<badge color="success">Interview optimal</badge>

### Idea

Use a dummy node and reverse each complete group by changing the `next` references.

We use these pointers:

| Pointer | Purpose |
|---|---|
| `groupPrev` | Node immediately before the current group |
| `kth` | Last node of the current group |
| `groupNext` | First node after the current group |
| `prev` | Previous node during reversal |
| `curr` | Current node during reversal |
| `nextNode` | Saves the next node before changing links |



### Algorithm

1. Create a dummy node and connect it to `head`.
2. Set `groupPrev = dummy`.
3. Find the kth node from `groupPrev`.
4. If the kth node does not exist, stop.
5. Save the node after the group in `groupNext`.
6. Initialize:
   - `prev = groupNext`
   - `curr = groupPrev.next`
7. Reverse nodes until `curr == groupNext`.
8. Reconnect the reversed group:
   - `groupPrev.next = kth`
9. Move `groupPrev` to the old head of the group.
10. Repeat until no complete group remains.
11. Return `dummy.next`.

### Java Code

    class Solution {
        public ListNode reverseKGroup(ListNode head, int k) {

            if (head == null || k == 1) {
                return head;
            }

            ListNode dummy = new ListNode(0);
            dummy.next = head;

            ListNode groupPrev = dummy;

            while (true) {

                // Step 1: Find kth node
                ListNode kth = groupPrev;

                for (int i = 0; i < k && kth != null; i++) {
                    kth = kth.next;
                }

                // Incomplete group
                if (kth == null) {
                    break;
                }

                // Step 2: Save node after the group
                ListNode groupNext = kth.next;

                // Step 3: Reverse the group
                ListNode prev = groupNext;
                ListNode curr = groupPrev.next;

                while (curr != groupNext) {

                    ListNode nextNode = curr.next;

                    curr.next = prev;

                    prev = curr;
                    curr = nextNode;
                }

                // Step 4: Reconnect the reversed group
                ListNode oldGroupHead = groupPrev.next;

                groupPrev.next = kth;

                // Step 5: Move to the next group
                groupPrev = oldGroupHead;
            }

            return dummy.next;
        }
    }


### Complexity

- **Time Complexity:** O(n) – every node is visited and reversed at most once.
- **Space Complexity:** O(1) – only a fixed number of pointers are used.

---

## Important Concepts to Remember

### 1. Why initialize `prev = groupNext`?

    ListNode prev = groupNext;

This is important because the reversed group's last node must point to the remaining list.

For example:

    Before: 1 -> 2 -> 3 -> 4

    After:  3 -> 2 -> 1 -> 4

By starting `prev` at node `4`, the first node reversed (`1`) automatically connects to `4`.

### 2. Why use `curr != groupNext`?

    while (curr != groupNext)

We reverse only nodes belonging to the current group.

We stop exactly when we reach the first node outside the group.

### 3. Why move `groupPrev = oldGroupHead`?

Before reversal:

    1 -> 2 -> 3

After reversal:

    3 -> 2 -> 1

Node `1` becomes the last node of the reversed group. It is therefore the correct starting point for reconnecting the next group.

### 4. Why use a dummy node?

The first node changes after reversing the first group.

Instead of handling the head separately, we return:

    return dummy.next;

---

## Common Mistakes

1. Reversing the incomplete final group.
2. Forgetting to save `groupNext` before changing links.
3. Initializing `prev = null` instead of `prev = groupNext`.
4. Using `curr != null` instead of `curr != groupNext`.
5. Forgetting to reconnect `groupPrev.next = kth`.
6. Moving `groupPrev` to `kth` instead of `oldGroupHead`.

---

## Edge Cases

| Input | k | Output |
|---|---:|---|
| `1 -> 2 -> 3 -> 4 -> 5` | 2 | `2 -> 1 -> 4 -> 3 -> 5` |
| `1 -> 2 -> 3 -> 4 -> 5` | 3 | `3 -> 2 -> 1 -> 4 -> 5` |
| `1 -> 2 -> 3` | 3 | `3 -> 2 -> 1` |
| `1 -> 2` | 3 | `1 -> 2` |
| `1 -> 2 -> 3` | 1 | `1 -> 2 -> 3` |
| `1` | 2 | `1` |

---

## Approach Comparison

| Approach | Time | Space | Reverses actual nodes |
|---|---:|---:|---|
| ArrayList | O(n) | O(n) | No |
| In-place | O(n) | O(1) | Yes |

## Patterns to Master

This problem combines three important linked-list patterns:

1. **Dummy Node Pattern** – handles changes to the head.
2. **In-place Reversal Pattern** – saves the next node before changing links.
3. **Group Processing Pattern** – identifies and processes fixed-size groups.

**Interview takeaway:** Understand how `groupPrev`, `kth`, `groupNext`, `prev`, and `curr` work together. Once you understand this pointer arrangement, you can solve many advanced linked-list problems.
