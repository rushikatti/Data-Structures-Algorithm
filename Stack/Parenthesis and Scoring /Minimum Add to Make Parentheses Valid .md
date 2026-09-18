# 🔢 921. Minimum Add to Make Parentheses Valid

## 🧠 Problem Statement

Given a string `s` consisting of `'('` and `')'`, return the **minimum number of insertions** required to make it valid.

A string is valid if:
- Every `'('` has a matching `')'`
- Order is correct

---

# 💡 Approach 1: Brute Force (StringBuilder Simulation)

## 🔹 Algorithm

1. Convert string → `StringBuilder`
2. Traverse with index `i`
3. If adjacent pair `"()"` found:
   - Remove both characters
   - Move one step back (`i--`)
4. Else move forward
5. At end, remaining characters = insertions needed

---

## 🔹 Code

    class Solution {
        public int minAddToMakeValid(String s) {

            StringBuilder sb = new StringBuilder(s);
            int i = 0;

            while(i < sb.length() - 1){
                char a = sb.charAt(i);
                char b = sb.charAt(i + 1);

                if(a == '(' && b == ')'){
                    sb.delete(i, i + 2);

                    if(i > 0){
                        i--;
                    }
                }
                else{
                    i++;
                }
            }

            return sb.length();
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)** (due to shifting on delete)
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Stack)

## 🔹 Algorithm

1. Initialize empty stack
2. Traverse characters:
   - If `'('` → push
   - If `')'`:
       - If stack not empty → pop
       - Else → push (unmatched `')'`)
3. Remaining stack size = insertions needed

---

## 🔹 Code

    class Solution {
        public int minAddToMakeValid(String s) {

            Stack<Character> st = new Stack<>();

            for(char ch : s.toCharArray()){
                if(ch == '('){
                    st.push(ch);
                } else {
                    if(!st.isEmpty() && st.peek() == '('){
                        st.pop();
                    } else {
                        st.push(ch);
                    }
                }
            }

            return st.size();
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
| StringBuilder  | O(N²) | O(N)  | Repeated deletions             |
| Stack          | O(N)  | O(N)  | Optimal and standard solution  |

---
