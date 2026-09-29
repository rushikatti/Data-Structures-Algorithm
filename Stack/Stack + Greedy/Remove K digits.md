# 🔢 402. Remove K Digits

## 🧠 Problem Statement

Given a non-negative integer `num` (as string) and an integer `k`, remove **k digits** so that the resulting number is the **smallest possible**.

### Notes:
- No leading zeros (except `"0"`)
- If all digits are removed → return `"0"`

---

# 💡 Approach 1: Brute Force

## 🔹 Idea

At each step:
- Try removing **every possible digit**
- Choose the **smallest resulting number**
- Repeat this process **k times**

---

## 🔹 Algorithm

1. Repeat `k` times:
   - For each index `i`:
     - Remove digit at `i`
     - Form new number
   - Choose smallest among all candidates
2. Return final number

---

## 🔹 Code

    class Solution {
        public String removeKdigits(String num, int k) {

            while(k > 0){
                String best = null;

                for(int i = 0; i < num.length(); i++){
                    String candidate = num.substring(0, i) + num.substring(i + 1);

                    candidate = removeLeadingZeros(candidate);

                    if(best == null || isSmaller(candidate, best)){
                        best = candidate;
                    }
                }

                num = best;
                k--;
            }

            return num;
        }

        private String removeLeadingZeros(String s){
            int i = 0;
            while(i < s.length() && s.charAt(i) == '0'){
                i++;
            }
            return i == s.length() ? "0" : s.substring(i);
        }

        private boolean isSmaller(String a, String b){
            if(a.length() != b.length()){
                return a.length() < b.length();
            }
            return a.compareTo(b) < 0;
        }
    }

---

## ⏱ Complexity

- Time: **O(k * n²)** ❌  
- Space: **O(n)**  

---

# 🚀 Approach 2: Optimal (Monotonic Stack)

## 🔹 Idea

👉 Remove digits that are **greater than the next digit**

Maintain a **monotonically increasing sequence**

---

## 🔹 Algorithm

1. Initialize empty stack / StringBuilder
2. Traverse digits:
   - While:
        - k > 0  
        - stack not empty  
        - last digit > current digit  
     → remove last digit
   - Add current digit
3. If `k > 0` → remove last `k` digits
4. Remove leading zeros
5. Return result

---

## 🔹 Code

    class Solution {
        public String removeKdigits(String num, int k) {

            StringBuilder sb = new StringBuilder();

            for(char ch : num.toCharArray()){
                while(k > 0 && sb.length() > 0 && sb.charAt(sb.length() - 1) > ch){
                    sb.deleteCharAt(sb.length() - 1);
                    k--;
                }
                sb.append(ch);
            }

            // remove remaining digits from end
            sb.setLength(sb.length() - k);

            // remove leading zeros
            int start = 0;
            while(start < sb.length() && sb.charAt(start) == '0'){
                start++;
            }

            String ans = sb.substring(start);
            return ans.isEmpty() ? "0" : ans;
        }
    }

---

## ⏱ Complexity

- Time: **O(n)** ✅  
- Space: **O(n)**  

---

# 🧪 Example

    num = "1432219", k = 3

Steps:

    1 → push  
    4 → push  
    3 → pop 4 → push  
    2 → pop 3 → push  
    2 → push  
    1 → pop 2 → push  
    9 → push  

Result:

    "1219"

---

# 🏁 Summary

| Approach        | Time        | Space | Notes                      |
|----------------|-------------|-------|----------------------------|
| Brute Force    | O(k * n²)   | O(n)  | Try all removals           |
| Monotonic Stack| O(n)        | O(n)  | Optimal greedy solution    |

---

# 🧠 Key Insight

> Remove the **left larger digit** when a smaller digit appears

---

# 🔥 Pattern

👉 Same as:
- Remove Duplicate Letters (316)  
- Smallest Subsequence (1081)

---
