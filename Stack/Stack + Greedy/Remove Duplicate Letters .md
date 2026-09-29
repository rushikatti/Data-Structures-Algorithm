# 🔢 316. Remove Duplicate Letters

## 🧠 Problem Statement

Given a string `s`, remove duplicate letters so that:
- Every letter appears **once and only once**
- The result is the **smallest in lexicographical order**

---

# 💡 Approach 1: Brute Force

## 🔹 Idea

- Generate **all subsequences**
- Keep only those:
  - Having all **distinct characters exactly once**
- Return the **lexicographically smallest**

---

## 🔹 Code (Conceptual)

    class Solution {
        String ans = null;

        public String removeDuplicateLetters(String s) {
            boolean[] present = new boolean[26];
            int distinct = 0;

            // count distinct characters
            for(char ch : s.toCharArray()){
                if(!present[ch - 'a']){
                    present[ch - 'a'] = true;
                    distinct++;
                }
            }

            backtrack(s, 0, new StringBuilder(), distinct, new boolean[26]);
            return ans;
        }

        private void backtrack(String s, int idx, StringBuilder curr,
                               int distinct, boolean[] used){

            if(curr.length() == distinct){
                String candidate = curr.toString();

                if(ans == null || candidate.compareTo(ans) < 0){
                    ans = candidate;
                }
                return;
            }

            if(idx == s.length()) return;

            char ch = s.charAt(idx);

            // take
            if(!used[ch - 'a']){
                used[ch - 'a'] = true;
                curr.append(ch);

                backtrack(s, idx + 1, curr, distinct, used);

                curr.deleteCharAt(curr.length() - 1);
                used[ch - 'a'] = false;
            }

            // skip
            backtrack(s, idx + 1, curr, distinct, used);
        }
    }

---

## ⏱ Complexity

- Time: **O(2^N)** ❌  
- Space: **O(N)**  

---

# 🚀 Approach 2: Optimal (Greedy + Monotonic Stack)

## 🔹 Idea

👉 Build result while:
- Keeping **unique characters**
- Maintaining **smallest lexicographical order**

---

## 🔹 Key Components

1. **Last Occurrence Array**
    
        last[ch] = last index of character

2. **Visited Array**
    
        visited[ch] = already in result

3. **Stack / StringBuilder**
    
        stores answer

---

## 🔹 Algorithm

For each character `ch`:

### Step 1: Skip duplicates

    if visited[ch] → continue

---

### Step 2: Maintain lexicographical order

While:
- stack not empty  
- top > current char  
- top appears later again  

    → pop from stack

---

### Step 3: Add character

    push ch
    mark visited[ch] = true

---

## 🔹 Code

    class Solution {
        public String removeDuplicateLetters(String s) {
            int[] last = new int[26];

            // last occurrence
            for(int i = 0; i < s.length(); i++){
                last[s.charAt(i) - 'a'] = i;
            }

            boolean[] visited = new boolean[26];
            StringBuilder sb = new StringBuilder();

            for(int i = 0; i < s.length(); i++){
                char ch = s.charAt(i);

                if(visited[ch - 'a']) continue;

                while(sb.length() > 0 &&
                      sb.charAt(sb.length() - 1) > ch &&
                      last[sb.charAt(sb.length() - 1) - 'a'] > i){

                    visited[sb.charAt(sb.length() - 1) - 'a'] = false;
                    sb.deleteCharAt(sb.length() - 1);
                }

                sb.append(ch);
                visited[ch - 'a'] = true;
            }

            return sb.toString();
        }
    }

---

## ⏱ Complexity

- Time: **O(N)** ✅  
- Space: **O(1)**  

---

# 🧪 Example

    s = "cbacdcbc"

Steps:

    c → push → "c"
    b → pop c → push b → "b"
    a → pop b → push a → "a"
    c → push → "ac"
    d → push → "acd"
    c → skip
    b → push → "acdb"
    c → skip

Answer:

    "acdb"

---

# 🏁 Summary

| Approach        | Time     | Space | Notes                          |
|----------------|----------|-------|--------------------------------|
| Brute Force    | O(2^N)   | O(N)  | Try all subsequences           |
| Optimal        | O(N)     | O(1)  | Greedy + monotonic stack       |

---

# 🧠 Key Insight

> Remove a character only if:
> - It is **greater than current**
> - AND it appears **later again**

---

# 🔥 Pattern

👉 Same as:
- Remove K Digits (402)  
- Smallest Subsequence (1081)

---
