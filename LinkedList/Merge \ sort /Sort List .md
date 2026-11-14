# LeetCode 148: Sort List

## Problem

Given the head of a linked list, return the list after sorting it in ascending order.

**Example:**

Input: `head = [4,2,1,3]`

Output: `[1,2,3,4]`

---

## Approach 1: Brute Force — ArrayList

### Idea
Store all node values in an ArrayList, sort the list, and update the original linked list with the sorted values.

### Algorithm
1. Traverse the linked list and store all values in an ArrayList.
2. Sort the ArrayList using `Collections.sort()`.
3. Traverse the linked list again.
4. Update each node's value using the sorted ArrayList.
5. Return the original head.

### Code (Java)

    class Solution {
        public ListNode sortList(ListNode head) {

            if (head == null || head.next == null) {
                return head;
            }

            ArrayList<Integer> list = new ArrayList<>();

            ListNode cur = head;

            // Store all values
            while (cur != null) {
                list.add(cur.val);
                cur = cur.next;
            }

            // Sort values
            Collections.sort(list);

            // Update linked list
            cur = head;
            int i = 0;

            while (cur != null) {
                cur.val = list.get(i);
                cur = cur.next;
                i++;
            }

            return head;
        }
    }

### Complexity
- **Time:** O(n log n) — sorting the ArrayList.
- **Space:** O(n) — storing all node values.

---

## Approach 2: Better — Copy to Array and Sort

### Idea
Convert the linked list into an array, sort the array, and copy the sorted values back into the linked list.

This is similar to the ArrayList approach, but uses an array.

### Algorithm
1. Count the number of nodes.
2. Create an integer array of that size.
3. Copy all node values into the array.
4. Sort the array using `Arrays.sort()`.
5. Copy the sorted values back into the linked list.
6. Return the head.

### Code (Java)

    class Solution {
        public ListNode sortList(ListNode head) {

            if (head == null || head.next == null) {
                return head;
            }

            int n = 0;
            ListNode cur = head;

            while (cur != null) {
                n++;
                cur = cur.next;
            }

            int[] arr = new int[n];

            cur = head;
            int i = 0;

            while (cur != null) {
                arr[i++] = cur.val;
                cur = cur.next;
            }

            Arrays.sort(arr);

            cur = head;
            i = 0;

            while (cur != null) {
                cur.val = arr[i++];
                cur = cur.next;
            }

            return head;
        }
    }

### Complexity
- **Time:** O(n log n) — sorting the array.
- **Space:** O(n) — creating the array.

---

## Approach 3: Optimal — Merge Sort (Divide and Conquer)

### Idea
Use Merge Sort to sort the linked list.

Merge Sort works by:
1. Finding the middle of the linked list.
2. Splitting the list into two halves.
3. Recursively sorting both halves.
4. Merging the two sorted halves.

Unlike array-based sorting, this approach rearranges the linked-list nodes directly without using extra arrays.

### Algorithm

**Step 1: Find the middle**
- Use slow and fast pointers.
- Move slow by one step and fast by two steps.
- When fast reaches the end, slow is near the middle.

**Step 2: Split the list**
- Store `slow.next` as the head of the second half.
- Set `slow.next = null` to separate the two halves.

**Step 3: Recursively sort**
- Call `sortList()` on both halves.

**Step 4: Merge**
- Compare the values of both sorted lists.
- Attach the smaller node to the result.
- Continue until both lists are merged.

### Code (Java)

    class Solution {

        public ListNode sortList(ListNode head) {

            if (head == null || head.next == null) {
                return head;
            }

            // Find middle
            ListNode slow = head;
            ListNode fast = head;
            ListNode prev = null;

            while (fast != null && fast.next != null) {
                prev = slow;
                slow = slow.next;
                fast = fast.next.next;
            }

            // Split into two halves
            prev.next = null;

            // Recursively sort both halves
            ListNode left = sortList(head);
            ListNode right = sortList(slow);

            // Merge sorted halves
            return merge(left, right);
        }

        private ListNode merge(ListNode list1, ListNode list2) {

            ListNode dummy = new ListNode(0);
            ListNode tail = dummy;

            while (list1 != null && list2 != null) {

                if (list1.val <= list2.val) {
                    tail.next = list1;
                    list1 = list1.next;
                } else {
                    tail.next = list2;
                    list2 = list2.next;
                }

                tail = tail.next;
            }

            // Attach remaining nodes
            if (list1 != null) {
                tail.next = list1;
            } else {
                tail.next = list2;
            }

            return dummy.next;
        }
    }

### Complexity
- **Time:** O(n log n)
  - The list is divided into log n levels.
  - Each level processes all n nodes during merging.
- **Space:** O(log n) — recursion stack.
  - No additional array or collection is used.

---

## Comparison

| Approach | Time | Space | Technique |
|---|---|---|---|
| ArrayList | O(n log n) | O(n) | Store, sort, update |
| Array | O(n log n) | O(n) | Copy, sort, update |
| Merge Sort | O(n log n) | O(log n) | Divide and conquer |

## Key Takeaways

1. Merge Sort is well suited for linked lists.
2. Slow and fast pointers help find the middle.
3. `slow.next = null` splits the linked list.
4. Recursion sorts each half independently.
5. Merge combines two already sorted linked lists.
6. The optimal approach rearranges existing nodes instead of copying values.

## Interview Recommendation

Use **Merge Sort** for LeetCode 148.

It achieves O(n log n) time and O(log n) auxiliary space, making it the standard optimal approach for sorting a linked list.
