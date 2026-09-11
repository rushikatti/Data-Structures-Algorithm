# ⌨️ Backspace String Compare

## 🧠 Problem Statement

Given two strings `s` and `t`, return `true` if they are equal when both are typed into empty text editors.

- `'#'` means a **backspace** (delete last character if any)

### Example:
    Input:  s = "ab#c", t = "ad#c"
    Output: true   → both become "ac"

---

# 💡 Approach 1: Brute Force (Build Final Strings)

## 🔹 Algorithm

1. Create helper function:
   - Use `StringBuilder`
   - Traverse string:
       - If character ≠ '#' → append
       - If '#' → delete last character (if exists)
2. Build final string for both `s` and `t`
3. Compare both strings

---

## 🔹 Code

    class Solution {
        public boolean backspaceCompare(String s, String t) {
            return build(s).equals(build(t));
        }

        private String build(String str) {
            StringBuilder sb = new StringBuilder();

            for(char ch : str.toCharArray()){
                if(ch != '#'){
                    sb.append(ch);
                } else {
                    if(sb.length() > 0){
                        sb.deleteCharAt(sb.length() - 1);
                    }
                }
            }

            return sb.toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N + M)**
- Space: **O(N + M)**

---

# 🚀 Approach 2: Optimal (Two Pointers)

## 🔹 Idea

Traverse from **right → left**:
- Skip characters that are deleted by `#`
- Compare valid characters directly

---

## 🔹 Algorithm

1. Set pointers `i = s.length-1`, `j = t.length-1`
2. Maintain `skipS`, `skipT`
3. While `i >= 0` or `j >= 0`:
   - Move `i`:
       - If `#` → increment skip
       - Else if skip > 0 → skip char
       - Else → stop
   - Move `j` similarly
   - Compare characters
4. If mismatch → false
5. Return true

---

## 🔹 Code

    class Solution {
        public boolean backspaceCompare(String s, String t) {
            int i = s.length() - 1;
            int j = t.length() - 1;

            int skipS = 0, skipT = 0;

            while(i >= 0 || j >= 0){

                while(i >= 0){
                    if(s.charAt(i) == '#'){
                        skipS++;
                        i--;
                    }
                    else if(skipS > 0){
                        skipS--;
                        i--;
                    }
                    else break;
                }

                while(j >= 0){
                    if(t.charAt(j) == '#'){
                        skipT++;
                        j--;
                    }
                    else if(skipT > 0){
                        skipT--;
                        j--;
                    }
                    else break;
                }

                if(i >= 0 && j >= 0){
                    if(s.charAt(i) != t.charAt(j)) return false;
                }
                else{
                    if(i >= 0 || j >= 0) return false;
                }

                i--;
                j--;
            }

            return true;
        }
    }

---

## ⏱ Complexity

- Time: **O(N + M)**
- Space: **O(1)**

---

# 🏁 Summary

| Approach     | Time        | Space      | Notes                         |
|--------------|------------|------------|-------------------------------|
| Build String | O(N + M)   | O(N + M)   | Easy, uses extra space        |
| Two Pointer  | O(N + M)   | O(1)       | Optimal, no extra memory      |

---
