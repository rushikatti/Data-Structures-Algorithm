# 🔢 856. Score of Parentheses

## 🧠 Problem Statement

Given a **balanced parentheses string** `s`, return its **score** based on:

- `"()"` → 1  
- `AB` → A + B  
- `(A)` → 2 × A  



# 🚀 Approach 1: Depth Counting (Optimal)

## 🔹 Algorithm

1. Initialize:
       score = 0  
       depth = 0  

2. Traverse string:
   - If `'('` → depth++
   - If `')'`:
       - depth--
       - If previous char was `'('`:
            → add `2^depth` to score

3. Return score

---

## 🔹 Code

    class Solution {
        public int scoreOfParentheses(String s) {
            int score = 0;
            int depth = 0;

            for(int i = 0; i < s.length(); i++){
                if(s.charAt(i) == '('){
                    depth++;
                } else {
                    depth--;

                    if(s.charAt(i - 1) == '('){
                        score += 1 << depth;   // 2^depth
                    }
                }
            }

            return score;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(1)**

---

# 💡 Approach 2: Stack

## 🔹 Algorithm

1. Use stack
2. Traverse:
   - `'('` → push 0
   - `')'`:
       - Pop value `v`
       - If `v == 0` → value = 1
       - Else → value = 2 * v
       - Add to previous level

---

## 🔹 Code

    class Solution {
        public int scoreOfParentheses(String s) {
            Stack<Integer> st = new Stack<>();

            for(char ch : s.toCharArray()){
                if(ch == '('){
                    st.push(0);
                } else {
                    int v = st.pop();
                    int val = (v == 0) ? 1 : 2 * v;

                    if(!st.isEmpty()){
                        st.push(st.pop() + val);
                    } else {
                        st.push(val);
                    }
                }
            }

            return st.pop();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach        | Time  | Space | Notes                          |
|----------------|-------|-------|--------------------------------|
| Depth Counting | O(N)  | O(1)  | Best optimized                 |
| Stack          | O(N)  | O(N)  | Easier to understand           |

---

# 🧠 Key Insight

> `"()"` contributes `2^depth`, where depth is current nesting level

---
