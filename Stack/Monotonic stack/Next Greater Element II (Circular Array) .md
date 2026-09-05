# 503. Next Greater Element II (Circular Array)

## Problem

Given a **circular array** `nums`, return an array `ans` such that:

- `ans[i]` = **next greater element** of `nums[i]`
- If no such element exists → `-1`
- Circular means: after last element, we wrap to the beginning

---

## Solution Approach 1: Brute Force

### Algorithm

1. For each index `i`
2. Traverse next `n-1` elements circularly:
   - Use `(i + j) % n`
3. Find first element greater than `nums[i]`
4. If found → store it, else `-1`

---

### Code

    class Solution {
        public int[] nextGreaterElements(int[] nums) {

            int n = nums.length;
            int[] ans = new int[n];

            for (int i = 0; i < n; i++) {

                ans[i] = -1;

                for (int j = 1; j < n; j++) {

                    int next = nums[(i + j) % n];

                    if (next > nums[i]) {
                        ans[i] = next;
                        break;
                    }
                }
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(n^2)`
- **Space:** `O(1)` (excluding output)

---

## Solution Approach 2: Optimal (Monotonic Stack - Circular Trick)

### 🔥 Key Idea

- Since array is circular → simulate it by iterating **2 times**
- Use a **monotonic decreasing stack**

---

### Algorithm

1. Initialize `ans[]` with `-1`
2. Traverse from `2n-1 → 0`
3. For each index:
   - `num = nums[i % n]`
4. While stack not empty AND `stack.peek() <= num`
   - Pop
5. If `i < n`:
   - Assign `ans[i] = stack.peek()` (if exists)
6. Push current number to stack

---

### Code

    import java.util.*;

    class Solution {
        public int[] nextGreaterElements(int[] nums) {

            int n = nums.length;
            int[] ans = new int[n];
            Arrays.fill(ans, -1);

            Stack<Integer> stack = new Stack<>();

            for (int i = 2 * n - 1; i >= 0; i--) {

                int num = nums[i % n];

                while (!stack.isEmpty() && stack.peek() <= num) {
                    stack.pop();
                }

                if (i < n && !stack.isEmpty()) {
                    ans[i] = stack.peek();
                }

                stack.push(num);
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## 🔥 Why 2*n Loop?

```text
Normal array → only right side
Circular array → right side + beginning
