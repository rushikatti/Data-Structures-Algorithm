```md id="q4m9t1"
# 📊 Largest Rectangle in Histogram

## 🧠 Problem Statement

Given an array `heights[]`, return the **largest rectangular area** in the histogram.

---

# 💡 Approach 1: Brute Force (Double Loop)

## 🔹 Algorithm

1. Loop `i` from `0 → n-1`
2. Set `h = heights[i]`
3. Loop `j` from `i → n-1`
   - Update `h = min(h, heights[j])`
   - Width = `j - i + 1`
   - Area = `h * width`
   - Update max area

---

## 🔹 Code

    class Solution {
        public int largestRectangleArea(int[] heights) {
            int maxarea = 0;

            for(int i = 0; i < heights.length; i++){
                int h = heights[i];

                for(int j = i; j < heights.length; j++){
                    h = Math.min(h, heights[j]);
                    int w = j - i + 1;

                    maxarea = Math.max(maxarea, h * w);
                }
            }

            return maxarea;
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)**
- Space: **O(1)**

---

# 🚀 Approach 2: Optimal (Monotonic Stack)

## 🔹 Algorithm

1. Initialize stack
2. Loop `i = 0 → n`
   - `h = (i == n) ? 0 : heights[i]`
3. While stack not empty AND `h < heights[stack.peek()]`:
   - Pop index
   - `height = heights[popped]`
   - `width = (stack empty) ? i : i - stack.peek() - 1`
   - Update max area
4. Push index `i`

---

## 🔹 Code

    class Solution {
        public int largestRectangleArea(int[] heights) {

            int n = heights.length;
            Stack<Integer> st = new Stack<>();
            int maxarea = 0;

            for(int i = 0; i <= n; i++){
                int h = (i == n) ? 0 : heights[i];

                while(!st.isEmpty() && h < heights[st.peek()]){
                    int height = heights[st.pop()];

                    int width = st.isEmpty() ? i : i - st.peek() - 1;

                    int area = height * width;
                    maxarea = Math.max(maxarea, area);
                }

                st.push(i);
            }

            return maxarea;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---
```
