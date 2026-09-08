# 🧮 224. Basic Calculator

## 🧠 Problem Statement

Given a string `s` containing:
- digits
- `+`, `-`
- parentheses `(` `)`
- spaces

Evaluate and return the result.

👉 No `*`, `/`  
👉 No `eval()` allowed  

---

# 💡 Approach 1: Brute Force (Expression Simulation)

## 🔹 Idea

- Use stack to handle parentheses
- Build numbers digit by digit
- Apply sign when needed

---

## 🔹 Algorithm

1. Initialize:
   - `result = 0`
   - `number = 0`
   - `sign = +1`
2. Traverse string:
   - If digit → build number
   - If `+` → add previous number
   - If `-` → add previous number
   - If `(` → push `(result, sign)` and reset
   - If `)` → resolve expression inside
3. Add last number

---

## 🔹 Code

    class Solution {
        public int calculate(String s) {
            Stack<Integer> st = new Stack<>();

            int result = 0;
            int number = 0;
            int sign = 1;

            for(char ch : s.toCharArray()){

                if(Character.isDigit(ch)){
                    number = number * 10 + (ch - '0');
                }

                else if(ch == '+'){
                    result += sign * number;
                    number = 0;
                    sign = 1;
                }

                else if(ch == '-'){
                    result += sign * number;
                    number = 0;
                    sign = -1;
                }

                else if(ch == '('){
                    st.push(result);
                    st.push(sign);

                    result = 0;
                    sign = 1;
                }

                else if(ch == ')'){
                    result += sign * number;
                    number = 0;

                    result *= st.pop();   // sign
                    result += st.pop();   // previous result
                }
            }

            result += sign * number;
            return result;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Same Stack, Cleaner Flow)

## 🔹 Algorithm

1. Use variables:
   - `res`, `num`, `sign`
2. Use stack for:
   - previous result
   - previous sign
3. Traverse string:
   - digit → build number
   - `+/-` → apply previous
   - `(` → save state
   - `)` → compute and merge

---

## 🔹 Code

    class Solution {
        public int calculate(String s) {

            int res = 0;
            int num = 0;
            int sign = 1;

            Stack<Integer> st = new Stack<>();

            for(int i = 0; i < s.length(); i++){
                char ch = s.charAt(i);

                if(Character.isDigit(ch)){
                    num = num * 10 + (ch - '0');
                }

                else if(ch == '+'){
                    res += sign * num;
                    num = 0;
                    sign = 1;
                }

                else if(ch == '-'){
                    res += sign * num;
                    num = 0;
                    sign = -1;
                }

                else if(ch == '('){
                    st.push(res);
                    st.push(sign);

                    res = 0;
                    sign = 1;
                }

                else if(ch == ')'){
                    res += sign * num;
                    num = 0;

                    res *= st.pop();
                    res += st.pop();
                }
            }

            return res + sign * num;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach        | Time | Space | Notes                          |
|----------------|------|-------|--------------------------------|
| Simulation     | O(N) | O(N)  | Handles parentheses with stack |
| Optimized      | O(N) | O(N)  | Cleaner implementation         |

---
