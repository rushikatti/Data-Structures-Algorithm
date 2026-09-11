# 🔤 Minimum String Length After Removing Substrings

## 🧠 Problem Statement

Given a string `s`, repeatedly remove:
- `"AB"`
- `"CD"`

Return the **minimum length** of the string after all possible removals.

---

# 💡 Approach 1: Brute Force (Repeated Removal)

## 🔹 Algorithm

1. Convert string → `StringBuilder`
2. Repeat:
   - Traverse string
   - If `"AB"` or `"CD"` found:
       - Remove both characters
       - Restart traversal
3. Stop when no more removals possible
4. Return length

---

## 🔹 Code

    class Solution {
        public int minLength(String s) {
            StringBuilder sb = new StringBuilder(s);
            boolean changed = true;

            while(changed){
                changed = false;

                for(int i = 0; i < sb.length() - 1; i++){
                    char a = sb.charAt(i);
                    char b = sb.charAt(i + 1);

                    if((a == 'A' && b == 'B') || (a == 'C' && b == 'D')){
                        sb.delete(i, i + 2);
                        changed = true;
                        break;
                    }
                }
            }

            return sb.length();
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)**
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Stack / StringBuilder)

## 🔹 Algorithm

1. Use `StringBuilder` as stack
2. Traverse each character:
   - If stack not empty:
       - Check top + current
       - If `"AB"` or `"CD"` → remove top and skip current
   - Else → push current
3. Return stack size

---

## 🔹 Code

    class Solution {
        public int minLength(String s) {
            StringBuilder sb = new StringBuilder();

            for(char ch : s.toCharArray()){
                int len = sb.length();

                if(len > 0){
                    char last = sb.charAt(len - 1);

                    if((last == 'A' && ch == 'B') || (last == 'C' && ch == 'D')){
                        sb.deleteCharAt(len - 1);
                        continue;
                    }
                }

                sb.append(ch);
            }

            return sb.length();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach     | Time  | Space | Notes                  |
|--------------|-------|-------|------------------------|
| Brute Force  | O(N²) | O(N)  | Repeated scanning      |
| Stack        | O(N)  | O(N)  | Single pass optimal    |

---
