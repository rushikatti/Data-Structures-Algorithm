# 21. Merge Two Sorted Lists (LeetCode 21)

**Problem:** You are given the heads of two sorted linked lists, `list1` and `list2`.

Merge both lists into one sorted linked list and return its head.

The merged list should be made by splicing together the nodes of the first two lists.


## Approach 1: Brute Force – ArrayList

### Idea

1. Traverse both linked lists.
2. Store all values in an ArrayList.
3. Sort the ArrayList.
4. Create a new linked list using the sorted values.

### Algorithm

1. Create an ArrayList.
2. Add all values from `list1`.
3. Add all values from `list2`.
4. Sort the ArrayList.
5. Create a new linked list using a dummy node.
6. Return `dummy.next`.

### Java Code

    class Solution {
        public ListNode mergeTwoLists(ListNode list1, ListNode list2) {

            ArrayList<Integer> list = new ArrayList<>();

            while (list1 != null) {
                list.add(list1.val);
                list1 = list1.next;
            }

            while (list2 != null) {
                list.add(list2.val);
                list2 = list2.next;
            }

            Collections.sort(list);

            ListNode dummy = new ListNode(0);
            ListNode cur = dummy;

            for (int num : list) {
                cur.next = new ListNode(num);
                cur = cur.next;
            }

            return dummy.next;
        }
    }

### Complexity

- **Time:** O((n + m) log(n + m)) – sorting all elements.
- **Space:** O(n + m) – storing all values and creating a new list.

---

## Approach 2: Optimal – Two Pointers

<badge color="success">Interview optimal</badge>

### Idea

Both linked lists are already sorted.

Compare the current nodes of both lists and attach the smaller node to the merged list.

Continue until one list becomes empty. Finally, attach the remaining nodes of the other list.


### Algorithm

1. Create a dummy node.
2. Create a pointer `cur` pointing to the dummy node.
3. Compare `list1.val` and `list2.val`.
4. Attach the smaller node to `cur.next`.
5. Move the pointer of the list from which the node was selected.
6. Move `cur` forward.
7. Repeat while both lists are not empty.
8. Attach the remaining list using `cur.next`.
9. Return `dummy.next`.

### Java Code

    class Solution {
        public ListNode mergeTwoLists(ListNode list1, ListNode list2) {

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

            // Attach remaining nodes
            if (list1 != null) {
                cur.next = list1;
            } else {
                cur.next = list2;
            }

            return dummy.next;
        }
    }

### Complexity

- **Time Complexity:** O(n + m) – each node is visited at most once.
- **Space Complexity:** O(1) – only a few pointers are used; existing nodes are reused.

---



## Important Concepts to Remember

### 1. Why use a dummy node?

    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;

The first selected node becomes the actual head of the merged list.

Using a dummy node avoids writing separate logic for the first node.

### 2. Why use `cur.next = list1`?

    cur.next = list1;
    list1 = list1.next;

We connect the existing node instead of creating a new node.

Then we move `list1` to its next node.

### 3. Why attach the remaining list directly?

    cur.next = (list1 != null) ? list1 : list2;

Once one list becomes empty, the other list is already sorted.

Therefore, no further comparisons are required.

### 4. Why return `dummy.next`?

The dummy node is only a starting point. It is not part of the actual answer.

    return dummy.next;

---

## Common Mistakes

1. Returning `dummy` instead of `dummy.next`.
2. Forgetting to move `cur` after attaching a node.
3. Forgetting to advance `list1` or `list2`.
4. Forgetting to attach the remaining nodes.
5. Creating unnecessary new nodes in the optimal approach.

---

## Edge Cases

| Input | Output |
|---|---|
| `1 -> 2 -> 4`, `1 -> 3 -> 4` | `1 -> 1 -> 2 -> 3 -> 4 -> 4` |
| `null`, `1 -> 2` | `1 -> 2` |
| `1 -> 2`, `null` | `1 -> 2` |
| `null`, `null` | `null` |
| `1 -> 1`, `1 -> 1` | `1 -> 1 -> 1 -> 1` |

---

## Approach Comparison

| Approach | Time | Space |
|---|---:|---:|
| ArrayList + Sorting | O((n + m) log(n + m)) | O(n + m) |
| Two Pointers | O(n + m) | O(1) |

## Patterns to Master

This problem teaches three important concepts:

1. **Dummy Node Pattern** – simplifies building a new linked-list sequence.
2. **Two Pointers Pattern** – compares nodes from two sorted lists.
3. **In-place Linking** – reuses existing nodes instead of creating new ones.

**Interview takeaway:** Whenever two sorted linked lists need to be combined, compare their current nodes, attach the smaller one, and advance its pointer. Remember to attach the remaining list at the end.
