# 🔤 1544. Make The String Great

## 🧠 Problem Statement

Given a string `s` with lowercase and uppercase letters.

A string is **bad** if it contains adjacent characters:
- Same letter
- Different case (e.g., `'a'` and `'A'`)

👉 Remove such pairs repeatedly until the string becomes **good**.

Return the final string.

---

# 💡 Approach 1: Brute Force (Repeated Scan)

## 🔹 Algorithm

1. Convert string → `StringBuilder`
2. Repeat:
   - Traverse string
   - If adjacent characters differ by 32 (ASCII case diff):
       - Remove both
       - Restart scan
3. Stop when no changes occur

---

## 🔹 Code

    class Solution {
        public String makeGood(String s) {
            StringBuilder sb = new StringBuilder(s);
            boolean changed = true;

            while(changed){
                changed = false;

                for(int i = 0; i < sb.length() - 1; i++){
                    if(Math.abs(sb.charAt(i) - sb.charAt(i+1)) == 32){
                        sb.delete(i, i + 2);
                        changed = true;
                        break;
                    }
                }
            }

            return sb.toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)**
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Stack)

## 🔹 Idea

Use stack:
- Compare current char with top
- If bad pair → pop
- Else → push

---

## 🔹 Algorithm

1. Initialize empty stack
2. Traverse characters:
   - If stack not empty AND  
     `abs(top - current) == 32` → pop
   - Else → push current
3. Build string from stack

---

## 🔹 Code

    class Solution {
        public String makeGood(String s) {

            Stack<Character> st = new Stack<>();

            for(char ch : s.toCharArray()){
                if(!st.isEmpty() && Math.abs(st.peek() - ch) == 32){
                    st.pop();
                }
                else{
                    st.push(ch);
                }
            }

            StringBuilder res = new StringBuilder();

            for(char c : st){
                res.append(c);
            }

            return res.toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach     | Time  | Space | Notes                    |
|--------------|-------|-------|--------------------------|
| Brute Force  | O(N²) | O(N)  | Repeated deletions       |
| Stack        | O(N)  | O(N)  | Optimal, single pass     |

---
