# 🔢 Minimum Remove to Make Valid Parentheses

## 🧠 Problem Statement

Given a string `s` containing `'('`, `')'` and lowercase letters, remove the **minimum number of parentheses** so that the string becomes **valid**.

👉 Return the **valid string**

---

# 💡 Approach 1: Brute Force

## 🔹 Idea

- Try removing characters one by one
- Check if resulting string is valid
- Return first valid with minimum removals

---

## 🔹 Code (Conceptual)

    class Solution {
        public String minRemoveToMakeValid(String s) {
            // BFS or recursion (not practical)
            return "";
        }
    }

---

## ⏱ Complexity

- Time: **Exponential** ❌  
- Not practical

---

# 🚀 Approach 2: Stack + Marking (Optimal)

## 🔹 Idea

👉 Track invalid indices and remove them

---

## 🔹 Steps

1. Traverse string
2. If `'('` → push index into stack  
3. If `')'`:
   - If stack not empty → match (pop)
   - Else → mark this index for removal
4. After traversal:
   - Remaining stack indices = unmatched `'('`
5. Remove all marked indices

---

## 🔹 Code

    class Solution {
        public String minRemoveToMakeValid(String s) {
            Stack<Integer> st = new Stack<>();
            boolean[] remove = new boolean[s.length()];

            for(int i = 0; i < s.length(); i++){
                char ch = s.charAt(i);

                if(ch == '('){
                    st.push(i);
                } 
                else if(ch == ')'){
                    if(!st.isEmpty()){
                        st.pop();
                    } else {
                        remove[i] = true;
                    }
                }
            }

            // remaining '(' are invalid
            while(!st.isEmpty()){
                remove[st.pop()] = true;
            }

            // build result
            StringBuilder sb = new StringBuilder();
            for(int i = 0; i < s.length(); i++){
                if(!remove[i]){
                    sb.append(s.charAt(i));
                }
            }

            return sb.toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)** ✅  
- Space: **O(N)**  

---

# 💡 Approach 3: Two-Pass (No Stack)

## 🔹 Idea

👉 First remove extra `')'`  
👉 Then remove extra `'('`

---

## 🔹 Code

    class Solution {
        public String minRemoveToMakeValid(String s) {

            // pass 1 → remove extra ')'
            StringBuilder sb = new StringBuilder();
            int open = 0;

            for(char ch : s.toCharArray()){
                if(ch == '('){
                    open++;
                    sb.append(ch);
                } 
                else if(ch == ')'){
                    if(open > 0){
                        open--;
                        sb.append(ch);
                    }
                } 
                else {
                    sb.append(ch);
                }
            }

            // pass 2 → remove extra '('
            StringBuilder result = new StringBuilder();
            int balance = 0;

            for(int i = sb.length() - 1; i >= 0; i--){
                char ch = sb.charAt(i);

                if(ch == '(' && balance > 0){
                    balance--;
                    continue;
                }

                if(ch == ')'){
                    balance++;
                }

                result.append(ch);
            }

            return result.reverse().toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)** ✅  
- Space: **O(N)**  

---

# 🧪 Example

    s = "a)b(c)d"

Step:

    remove invalid ')'

Result:

    "ab(c)d"

---

# 🏁 Summary

| Approach        | Time        | Space | Notes                        |
|----------------|-------------|-------|------------------------------|
| Brute Force    | Exponential | —     | Not usable                   |
| Stack          | O(N)        | O(N)  | Easy to understand           |
| Two-Pass       | O(N)        | O(N)  | Clean, no stack              |

---

# 🧠 Key Insight

> Remove unmatched parentheses:
> - Extra `)` while scanning left  
> - Extra `(` while scanning right  

---

# 🔥 Pattern

👉 Same as:
- Valid Parentheses  
- Minimum Add to Make Valid  

---
