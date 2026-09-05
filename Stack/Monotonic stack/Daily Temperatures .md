# 739. Daily Temperatures

## Problem

Given an array `temperatures[]`, return an array `ans[]` such that:

- `ans[i]` = number of days you have to wait after day `i` to get a **warmer temperature**
- If no future day exists → `0`

---

## Solution Approach 1: Brute Force

### Algorithm

1. For each day `i`
2. Check all future days `j = i+1 → n-1`
3. Find first `j` such that:
   - `temperatures[j] > temperatures[i]`
4. Store `j - i`
5. If not found → `0`

---

### Code

    class Solution {
        public int[] dailyTemperatures(int[] temperatures) {

            int n = temperatures.length;
            int[] ans = new int[n];

            for (int i = 0; i < n - 1; i++) {

                for (int j = i + 1; j < n; j++) {

                    if (temperatures[j] > temperatures[i]) {
                        ans[i] = j - i;
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

## Solution Approach 2: Optimal (Monotonic Stack)

### 🔥 Key Idea

- We need **next greater element (future warmer day)**
- Use a **monotonic decreasing stack**
- Store **indices**, not values

---

### Algorithm

1. Traverse from **right → left**
2. Maintain stack such that:
   - Top always has **greater temperature**
3. For each index `i`:
   - Pop until stack top has higher temperature
   - If stack not empty:
     - `ans[i] = stack.peek() - i`
   - Push current index

---

### Code

    import java.util.*;

    class Solution {
        public int[] dailyTemperatures(int[] temperatures) {

            int n = temperatures.length;
            int[] ans = new int[n];

            Stack<Integer> st = new Stack<>();

            for (int i = n - 1; i >= 0; i--) {

                while (!st.isEmpty() && temperatures[st.peek()] <= temperatures[i]) {
                    st.pop();
                }

                if (!st.isEmpty()) {
                    ans[i] = st.peek() - i;
                }

                st.push(i);
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## 🔥 Why Stack Works

```text
We eliminate useless elements:
If a future day is colder → it will never be answer
