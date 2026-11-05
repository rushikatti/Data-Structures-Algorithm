# 23. Merge k Sorted Lists (LeetCode 23)

**Problem:** You are given an array of `k` sorted linked lists. Merge all the linked lists into one sorted linked list and return its head.

---

## Approach 1: Brute Force – ArrayList

### Idea

1. Traverse all `k` linked lists.
2. Store every node value in an ArrayList.
3. Sort the ArrayList.
4. Create a new linked list using the sorted values.

### Algorithm

1. Create an ArrayList.
2. Iterate through each linked list.
3. Store all node values.
4. Sort the ArrayList.
5. Create a new linked list using a dummy node.
6. Return `dummy.next`.

### Java Code

    class Solution {
        public ListNode mergeKLists(ListNode[] lists) {

            ArrayList<Integer> values = new ArrayList<>();

            for (ListNode node : lists) {

                while (node != null) {
                    values.add(node.val);
                    node = node.next;
                }
            }

            Collections.sort(values);

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            for (int num : values) {
                cur.next = new ListNode(num);
                cur = cur.next;
            }

            return dummy.next;
        }
    }

### Complexity

Let:
- `k` = number of linked lists.
- `N` = total number of nodes across all lists.

- **Time:** O(N log N) – sorting all node values.
- **Space:** O(N) – storing values and creating a new linked list.

---

## Approach 2: Better – Sequential Merging

### Idea

Use the `mergeTwoLists()` approach repeatedly.

Merge the first two lists, then merge the result with the third list, and continue until all lists are merged.

### Algorithm

1. If the array is empty, return `null`.
2. Set the result to the first linked list.
3. Iterate through the remaining lists.
4. Merge the current result with the next list using `mergeTwoLists()`.
5. Return the final merged list.

### Java Code

    class Solution {

        public ListNode mergeKLists(ListNode[] lists) {

            if (lists == null || lists.length == 0) {
                return null;
            }

            ListNode result = lists[0];

            for (int i = 1; i < lists.length; i++) {
                result = mergeTwoLists(result, lists[i]);
            }

            return result;
        }

        private ListNode mergeTwoLists(ListNode list1, ListNode list2) {

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            while (list1 != null && list2 != null) {

                if (list1.val <= list2.val) {
                    cur.next = list1;
                    list1 = list1.next;
                } else {
                    cur.next = list2;
                    list2 = list2.next;
                }

                cur = cur.next;
            }

            cur.next = (list1 != null) ? list1 : list2;

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(Nk) – each merge can traverse a large portion of the accumulated result.
- **Space:** O(1) auxiliary space – existing nodes are reused.

---

## Approach 3: Optimal – Divide and Conquer

<badge color="success">Interview optimal</badge>

### Idea

Instead of merging lists one by one, merge them in pairs.

Keep dividing the range of lists into two halves until each range contains one list. Then merge the pairs and combine the results.

This is similar to the Merge Sort algorithm.

### Algorithm

1. If there are no lists, return `null`.
2. Set `interval = 1`.
3. Merge lists in pairs:
   - Merge `lists[i]` with `lists[i + interval]`.
   - Store the merged result in `lists[i]`.
4. Double the interval after each round.
5. Continue until the interval is greater than or equal to `k`.
6. Return `lists[0]`.

### Java Code

    class Solution {

        public ListNode mergeKLists(ListNode[] lists) {

            if (lists == null || lists.length == 0) {
                return null;
            }

            int interval = 1;
            int k = lists.length;

            while (interval < k) {

                for (int i = 0; i + interval < k; i += interval * 2) {

                    lists[i] = mergeTwoLists(
                        lists[i],
                        lists[i + interval]
                    );
                }

                interval *= 2;
            }

            return lists[0];
        }

        private ListNode mergeTwoLists(ListNode list1, ListNode list2) {

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            while (list1 != null && list2 != null) {

                if (list1.val <= list2.val) {
                    cur.next = list1;
                    list1 = list1.next;
                } else {
                    cur.next = list2;
                    list2 = list2.next;
                }

                cur = cur.next;
            }

            cur.next = (list1 != null) ? list1 : list2;

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(N log k) – each node is processed once per merging level, and there are O(log k) levels.
- **Space:** O(1) auxiliary space for the iterative implementation, excluding the input array and reused nodes.

---

## Approach 4: Optimal – Min Heap (PriorityQueue)

### Idea

Use a Min Heap to always get the smallest node among the current nodes of all `k` lists.

Java provides `PriorityQueue`, which implements a Min Heap by default when supplied with an appropriate comparator.

### Algorithm

1. Create a Min Heap using `PriorityQueue`.
2. Insert the head of every non-empty linked list.
3. Create a dummy node and a `cur` pointer.
4. While the heap is not empty:
   - Remove the node with the smallest value.
   - Attach it to the merged list.
   - If that node has a next node, insert the next node into the heap.
5. Return `dummy.next`.

### Java Code

    class Solution {

        public ListNode mergeKLists(ListNode[] lists) {

            PriorityQueue<ListNode> pq =
                new PriorityQueue<>(
                    (a, b) -> Integer.compare(a.val, b.val)
                );

            // Add the first node of each list
            for (ListNode node : lists) {
                if (node != null) {
                    pq.offer(node);
                }
            }

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            while (!pq.isEmpty()) {

                ListNode smallest = pq.poll();

                cur.next = smallest;
                cur = cur.next;

                if (smallest.next != null) {
                    pq.offer(smallest.next);
                }
            }

            cur.next = null;

            return dummy.next;
        }
    }

### Complexity

- **Time:** O(N log k) – each node is inserted into and removed from the heap once.
- **Space:** O(k) – the heap contains at most one node from each list.

---

## Important Concepts to Remember

### 1. Why use `PriorityQueue`?

    PriorityQueue<ListNode> pq =
        new PriorityQueue<>(
            (a, b) -> Integer.compare(a.val, b.val)
        );

The comparator tells Java to prioritize the node with the smallest `val`.

### 2. Why insert only the next node?

    if (smallest.next != null) {
        pq.offer(smallest.next);
    }

Each individual linked list is already sorted.

Therefore, after removing its current smallest available node, only its next node needs to be considered.

### 3. Why use `Integer.compare()`?

    (a, b) -> Integer.compare(a.val, b.val)

This safely compares integer values without the potential integer overflow of:

    a.val - b.val

### 4. Why set `cur.next = null`?

    cur.next = null;

This ensures the final merged list terminates properly, especially when reusing existing nodes.

---

## Approach Comparison

Let `N` be the total number of nodes and `k` be the number of lists.

| Approach | Time | Auxiliary Space |
|---|---:|---:|
| ArrayList + Sorting | O(N log N) | O(N) |
| Sequential Merging | O(Nk) | O(1) |
| Divide and Conquer | O(N log k) | O(1) |
| Min Heap | O(N log k) | O(k) |

## Which Approach Should You Use?

- **ArrayList:** Easy to understand, but not optimal.
- **Sequential merging:** Simple reuse of Merge Two Sorted Lists, but inefficient for many lists.
- **Divide and conquer:** Excellent approach to understand and implement.
- **Min Heap:** Very common interview solution and useful for problems involving multiple sorted streams.

## Patterns to Master

1. **Two Pointers:** Merge Two Sorted Lists.
2. **Divide and Conquer:** Merge Sort and Merge k Sorted Lists.
3. **Min Heap / PriorityQueue:** Kth Largest Element, Top K Frequent Elements, and Smallest Range Covering Elements from K Lists.

**Interview takeaway:** Know both Divide and Conquer and Min Heap approaches. Both achieve O(N log k) time complexity.
