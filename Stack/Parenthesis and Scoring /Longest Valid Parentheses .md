# 🔢 32. Longest Valid Parentheses

## 🧠 Problem Statement

Given a string `s` containing only `'('` and `')'`, return the **length of the longest valid (well-formed) parentheses substring**.

---

# 💡 Approach 1: Brute Force (All Substrings + Valid Check)

## 🔹 Algorithm

1. Generate all substrings using two loops
2. For each substring:
   - Check if it is valid:
       - `'('` → +1
       - `')'` → -1
       - Count should never go negative
       - Final count must be 0
3. Track maximum valid length

---

## 🔹 Code

    class Solution {
        public int longestValidParentheses(String s) {
            int n = s.length();
            int maxLen = 0;

            for(int i = 0; i < n; i++){
                for(int j = i + 1; j < n; j++){

                    if(isValid(s, i, j)){
                        maxLen = Math.max(maxLen, j - i + 1);
                    }
                }
            }

            return maxLen;
        }

        private boolean isValid(String s, int l, int r){
            int count = 0;

            for(int i = l; i <= r; i++){
                if(s.charAt(i) == '('){
                    count++;
                } else {
                    count--;
                }

                if(count < 0) return false;
            }

            return count == 0;
        }
    }

---

## ⏱ Complexity

- Time: **O(N³)**
- Space: **O(1)**

---

# 🚀 Approach 2: Stack (Index Based)

## 🔹 Algorithm

1. Initialize stack and push `-1`
2. Traverse:
   - `'('` → push index
   - `')'`:
       - Pop
       - If empty → push current index
       - Else → update max = `i - stack.peek()`

---

## 🔹 Code

    class Solution {
        public int longestValidParentheses(String s) {
            Stack<Integer> st = new Stack<>();
            st.push(-1);

            int maxLen = 0;

            for(int i = 0; i < s.length(); i++){
                if(s.charAt(i) == '('){
                    st.push(i);
                } else {
                    st.pop();

                    if(st.isEmpty()){
                        st.push(i);
                    } else {
                        maxLen = Math.max(maxLen, i - st.peek());
                    }
                }
            }

            return maxLen;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# ⚡ Approach 3: Two Pass (Counter)

## 🔹 Algorithm

### Left → Right

- `left++` for `'('`
- `right++` for `')'`

- If equal → update max  
- If `right > left` → reset  

### Right → Left

- Same logic reversed
- If `left > right` → reset  

---

## 🔹 Code

    class Solution {
        public int longestValidParentheses(String s) {
            int left = 0, right = 0, max = 0;

            for(int i = 0; i < s.length(); i++){
                if(s.charAt(i) == '(') left++;
                else right++;

                if(left == right){
                    max = Math.max(max, right * 2);
                }

                if(right > left){
                    left = right = 0;
                }
            }

            left = right = 0;

            for(int j = s.length() - 1; j >= 0; j--){
                if(s.charAt(j) == '('){
                    left++;
                } else {
                    right++;
                }

                if(left == right){
                    max = Math.max(max, left * 2);
                }

                if(left > right){
                    left = right = 0;
                }
            }

            return max;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(1)**

---

# 🏁 Summary

| Approach        | Time   | Space | Notes                          |
|----------------|--------|-------|--------------------------------|
| Brute Force    | O(N³)  | O(1)  | Check all substrings           |
| Stack          | O(N)   | O(N)  | Most common solution           |
| Two Pass       | O(N)   | O(1)  | Best space optimized           |

---
