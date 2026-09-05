# 496. Next Greater Element I

## Problem

The **next greater element** of an element `x` is the **first greater element to the right** of `x` in the same array.

Given:
- `nums1` ⊆ `nums2`
- All elements are **distinct**

For each element in `nums1`, find its next greater element in `nums2`.

If it doesn't exist → return `-1`.

---

## Solution Approach 1: Brute Force

### Algorithm

1. For each element in `nums1`:
2. Find its index in `nums2`
3. Traverse right from that index
4. Find first greater element
5. If none found → `-1`

---

### Code

    class Solution {
        public int[] nextGreaterElement(int[] nums1, int[] nums2) {

            int[] ans = new int[nums1.length];

            for (int i = 0; i < nums1.length; i++) {

                int target = nums1[i];
                int nge = -1;

                // find index in nums2
                int j = 0;
                while (nums2[j] != target) {
                    j++;
                }

                // search to the right
                for (int k = j + 1; k < nums2.length; k++) {
                    if (nums2[k] > target) {
                        nge = nums2[k];
                        break;
                    }
                }

                ans[i] = nge;
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(n1 * n2)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Monotonic Stack + HashMap)

### 🔥 Key Idea

Instead of searching repeatedly:

👉 Precompute next greater for every element in `nums2`

---

### Algorithm

1. Use a **monotonic decreasing stack**
2. Traverse `nums2`:
   - While stack not empty AND current > stack top:
     - Pop element → its next greater = current
   - Push current element
3. Store results in a `HashMap`
4. For remaining stack elements → no NGE → `-1`
5. Build result for `nums1` using map

---

### Code

    import java.util.*;

    class Solution {
        public int[] nextGreaterElement(int[] nums1, int[] nums2) {

            HashMap<Integer, Integer> map = new HashMap<>();
            Stack<Integer> stack = new Stack<>();

            // Step 1: process nums2
            for (int num : nums2) {

                while (!stack.isEmpty() && num > stack.peek()) {
                    map.put(stack.pop(), num);
                }

                stack.push(num);
            }

            // remaining elements → no greater element
            while (!stack.isEmpty()) {
                map.put(stack.pop(), -1);
            }

            // Step 2: build result
            int[] ans = new int[nums1.length];

            for (int i = 0; i < nums1.length; i++) {
                ans[i] = map.get(nums1[i]);
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(n1 + n2)`
- **Space:** `O(n2)`

---

## 🔥 Why Stack Works

```text
We maintain decreasing order:
top → smallest
bottom → largest



# Next Greater Element I — Stack Only Approach (No HashMap)

## 🔥 Idea

Instead of using a `HashMap`, we can:

1. Compute **Next Greater Element (NGE)** for every index in `nums2`
2. Store results in an array `nge[]`
3. For each element in `nums1`, **find its index in nums2** and return `nge[index]`

---

## Solution Approach: Stack + Array

### Algorithm

### Step 1: Compute NGE for nums2

1. Create an array `nge[]` of size `n`
2. Use a **monotonic decreasing stack (store indices)**
3. Traverse from **right → left**
4. For each element:
   - Pop until stack top is **greater**
   - If stack empty → `nge[i] = -1`
   - Else → `nge[i] = nums2[stack.peek()]`
   - Push current index

---

### Step 2: Build Answer for nums1

1. For each element in `nums1`
2. Find its index in `nums2`
3. Use `nge[index]`

---

## Code

    import java.util.*;

    class Solution {
        public int[] nextGreaterElement(int[] nums1, int[] nums2) {

            int n = nums2.length;
            int[] nge = new int[n];
            Stack<Integer> stack = new Stack<>();

            // Step 1: Compute NGE for nums2
            for (int i = n - 1; i >= 0; i--) {

                while (!stack.isEmpty() && nums2[stack.peek()] <= nums2[i]) {
                    stack.pop();
                }

                if (stack.isEmpty()) {
                    nge[i] = -1;
                } else {
                    nge[i] = nums2[stack.peek()];
                }

                stack.push(i);
            }

            // Step 2: Build result for nums1
            int[] ans = new int[nums1.length];

            for (int i = 0; i < nums1.length; i++) {

                int target = nums1[i];

                // find index in nums2
                int idx = 0;
                for (int j = 0; j < n; j++) {
                    if (nums2[j] == target) {
                        idx = j;
                        break;
                    }
                }

                ans[i] = nge[idx];
            }

            return ans;
        }
    }

---

## Complexity

- **Time:** `O(n2 + n1 * n2)`
  - NGE computation → `O(n2)`
  - Searching index → `O(n1 * n2)`

- **Space:** `O(n2)`

---

## 🔥 Key Insight

- Stack gives **Next Greater in O(n)**
- But without map → we pay cost in lookup

---

## ⚡ Optimization Note

If you add a `HashMap`:
👉 lookup becomes `O(1)`  
👉 total becomes `O(n1 + n2)`

---

## 🧠 Pattern

- Use **stack for structure**
- Use **map for fast lookup**

---

## 🚀 Interview Tip

If interviewer says:

👉 “Can you do it without extra space?”

You can say:

> “Yes, using only stack + array, but lookup becomes O(n), so overall slightly slower.”

---
