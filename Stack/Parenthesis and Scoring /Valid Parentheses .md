# 🔢 Valid Parentheses

## 🧠 Problem Statement

Given a string `s` containing:
- `'(' , ')'`
- `'{' , '}'`
- `'[' , ']'`

Return `true` if the string is **valid**.

### A string is valid if:
1. Every opening bracket has a matching closing bracket  
2. Brackets are closed in the correct order  

---

# 💡 Approach 1: Brute Force (StringBuilder Simulation)

## 🔹 Algorithm

1. Convert string → `StringBuilder`
2. Traverse with index `i`
3. If adjacent valid pair found:
   - `"()"`, `"{}"`, `"[]"`
   - Remove both characters
   - Move one step back (`i--`)
4. Else move forward
5. If string becomes empty → valid

---

## 🔹 Code

    class Solution {
        public boolean isValid(String s) {

            StringBuilder sb = new StringBuilder(s);
            int i = 0;

            while(i < sb.length() - 1){
                char a = sb.charAt(i);
                char b = sb.charAt(i + 1);

                if((a == '(' && b == ')') ||
                   (a == '{' && b == '}') ||
                   (a == '[' && b == ']')){

                    sb.delete(i, i + 2);

                    if(i > 0){
                        i--;
                    }
                }
                else{
                    i++;
                }
            }

            return sb.length() == 0;
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)** (due to shifting on delete)
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Stack)

## 🔹 Algorithm

1. Initialize stack
2. Traverse characters:
   - If opening → push
   - If closing:
       - If stack empty → false
       - If top doesn't match → false
       - Else → pop
3. At end, stack must be empty

---

## 🔹 Code

    class Solution {
        public boolean isValid(String s) {

            Stack<Character> st = new Stack<>();

            for(char ch : s.toCharArray()){

                if(ch == '(' || ch == '{' || ch == '['){
                    st.push(ch);
                }
                else{
                    if(st.isEmpty()) return false;

                    char top = st.peek();

                    if((ch == ')' && top != '(') ||
                       (ch == '}' && top != '{') ||
                       (ch == ']' && top != '[')){
                        return false;
                    }

                    st.pop();
                }
            }

            return st.isEmpty();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach        | Time  | Space | Notes                        |
|----------------|-------|-------|------------------------------|
| StringBuilder  | O(N²) | O(N)  | Repeated deletion            |
| Stack          | O(N)  | O(N)  | Standard optimal solution    |

---
