# 🔤 Remove All Adjacent Duplicates in String

## 🧠 Problem Statement

Given a string `s`, repeatedly remove **adjacent duplicate characters** until no more duplicates exist.

Return the final string.

### Example:
    Input:  "abbaca"
    Output: "ca"

---

# 💡 Approach 1: Brute Force (Repeated Removal)

## 🔹 Algorithm

1. Convert string → `StringBuilder`
2. Repeat:
   - Traverse string
   - If `sb[i] == sb[i+1]`:
       - Remove both characters
       - Restart traversal
3. Stop when no changes occur
4. Return string

---

## 🔹 Code

    class Solution {
        public String removeDuplicates(String s) {
            StringBuilder sb = new StringBuilder(s);
            boolean changed = true;

            while(changed){
                changed = false;

                for(int i = 0; i < sb.length() - 1; i++){
                    if(sb.charAt(i) == sb.charAt(i + 1)){
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

# 🚀 Approach 2: Optimal (Stack / StringBuilder)

## 🔹 Algorithm

1. Use `StringBuilder` as stack
2. Traverse characters:
   - If stack not empty AND top == current:
       - remove top (pop)
   - Else:
       - push current
3. Return result

---

## 🔹 Code

    class Solution {
        public String removeDuplicates(String s) {
            StringBuilder sb = new StringBuilder();

            for(char ch : s.toCharArray()){
                int len = sb.length();

                if(len > 0 && sb.charAt(len - 1) == ch){
                    sb.deleteCharAt(len - 1);
                } else {
                    sb.append(ch);
                }
            }

            return sb.toString();
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
| Brute Force  | O(N²) | O(N)  | Repeated deletions     |
| Stack        | O(N)  | O(N)  | Optimal single pass    |

---
