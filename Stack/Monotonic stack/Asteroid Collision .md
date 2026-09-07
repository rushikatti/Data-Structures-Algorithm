# ☄️ Asteroid Collision

## 🧠 Problem Statement

Given an array `asteroids[]`:
- Positive → moving right ➡️
- Negative → moving left ⬅️

When two asteroids meet:
- Smaller one explodes
- If equal → both explode
- Same direction → no collision

Return final state after all collisions.

---

# 💡 Approach 1: Brute Force (Simulation using List)

## 🔹 Algorithm

1. Convert array → `List`
2. Use index `i = 0`
3. While `i < list.size() - 1`:
   - Let `a = list[i]`, `b = list[i+1]`
   - If `a > 0` and `b < 0` → collision:
     - If `|a| > |b|` → remove `b`
     - If `|b| > |a|` → remove `a`, move `i--`
     - If equal → remove both, move `i--`
   - Else → `i++`
4. Convert list → array

---

## 🔹 Code

    class Solution {
        public int[] asteroidCollision(int[] asteroids) {
            List<Integer> list = new ArrayList<>();

            for(int a : asteroids){
                list.add(a);
            }

            int i = 0;

            while(i < list.size() - 1){
                int a = list.get(i);
                int b = list.get(i + 1);

                if(a > 0 && b < 0){
                    if(Math.abs(a) > Math.abs(b)){
                        list.remove(i + 1);
                    }
                    else if(Math.abs(b) > Math.abs(a)){
                        list.remove(i);
                        if(i > 0) i--;
                    }
                    else{
                        list.remove(i + 1);
                        list.remove(i);
                        if(i > 0) i--;
                    }
                }
                else{
                    i++;
                }
            }

            int[] ans = new int[list.size()];
            for(int j = 0; j < list.size(); j++){
                ans[j] = list.get(j);
            }

            return ans;
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)** (due to repeated removals)
- Space: **O(N)**

---

# 🚀 Approach 2: Optimal (Stack)

## 🔹 Algorithm

1. Initialize empty stack
2. Traverse each asteroid `a`
3. While:
       stack not empty AND
       a < 0 AND
       stack.peek() > 0 AND
       stack.peek() < -a
   → pop stack

4. After loop:
   - If stack not empty AND a < 0 AND stack.peek() > 0:
        - If equal → pop
   - Else → push `a`

5. Convert stack → array (reverse order)

---

## 🔹 Code

    class Solution {
        public int[] asteroidCollision(int[] asteroids) {

            Stack<Integer> st = new Stack<>();

            for(int a : asteroids){

                while(!st.isEmpty() && a < 0 && st.peek() > 0 && st.peek() < -a){
                    st.pop();
                }

                if(!st.isEmpty() && a < 0 && st.peek() > 0){
                    if(st.peek() == -a){
                        st.pop();
                    }
                }
                else{
                    st.push(a);
                }
            }

            int[] ans = new int[st.size()];

            for(int i = st.size() - 1; i >= 0; i--){
                ans[i] = st.pop();
            }

            return ans;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach     | Time Complexity | Space | Notes                     |
|--------------|---------------|-------|---------------------------|
| Brute Force  | O(N²)         | O(N)  | Simulation with list      |
| Stack        | O(N)          | O(N)  | Monotonic collision logic |

---
