# 🔢 Design a Stack With Increment Operation (CustomStack)

## 🧠 Problem Statement

Design a stack that supports:

- `push(x)` → push element if not full  
- `pop()` → remove and return top (or `-1` if empty)  
- `increment(k, val)` → add `val` to **bottom k elements**

---

# 💡 Approach 1: Brute Force (Array Simulation)

## 🔹 Idea

Use array to simulate stack.  
For `increment`, directly update first `k` elements.

---

## 🔹 Algorithm

### push(x)
- If stack is full → ignore  
- Else → insert at top  

### pop()
- If empty → return -1  
- Else → return top element and decrement index  

### increment(k, val)
- Traverse first `k` elements  
- Add `val` to each  

---

## 🔹 Code

    class CustomStack {
        int[] stack;
        int index;
        int maxSize;

        public CustomStack(int maxSize) {
            this.maxSize = maxSize;
            stack = new int[maxSize];
            index = -1;
        }
        
        public void push(int x) {
            if(index == maxSize - 1){
                return;
            }
            stack[++index] = x;
        }
        
        public int pop() {
            if(index == -1){
                return -1;
            }
            return stack[index--];
        }
        
        public void increment(int k, int val) {
            int limit = Math.min(k, index + 1);

            for(int i = 0; i < limit; i++){
                stack[i] += val;
            }
        }
    }

---

## ⏱ Complexity

- push → **O(1)**  
- pop → **O(1)**  
- increment → **O(K)** ❌  

---

# 🚀 Approach 2: Optimal (Lazy Increment)

## 🔹 Idea

Avoid updating all elements every time.  
Use an extra array `inc[]` to store **pending increments**.

---

## 🔹 Algorithm

Maintain:
- `stack[]` → values  
- `inc[]` → lazy increments  

### push(x)
- Push normally  

### increment(k, val)
- Instead of updating all:
    → `inc[k-1] += val`

### pop()
- Add pending increment before returning  
- Propagate increment downward  

---

## 🔹 Code

    class CustomStack {
        int[] stack;
        int[] inc;
        int index;

        public CustomStack(int maxSize) {
            stack = new int[maxSize];
            inc = new int[maxSize];
            index = -1;
        }
        
        public void push(int x) {
            if(index == stack.length - 1){
                return;
            }
            stack[++index] = x;
        }
        
        public int pop() {
            if(index == -1){
                return -1;
            }

            int res = stack[index] + inc[index];

            if(index > 0){
                inc[index - 1] += inc[index];
            }

            inc[index] = 0;
            index--;

            return res;
        }
        
        public void increment(int k, int val) {
            int i = Math.min(k, index + 1) - 1;

            if(i >= 0){
                inc[i] += val;
            }
        }
    }

---

## ⏱ Complexity

- push → **O(1)**  
- pop → **O(1)**  
- increment → **O(1)** ✅  

---

# 🏁 Summary

| Approach        | push | pop | increment | Notes                    |
|----------------|------|-----|-----------|--------------------------|
| Brute Force    | O(1) | O(1)| O(K)      | Direct update            |
| Lazy Increment | O(1) | O(1)| O(1)      | Optimal solution         |

---

# 🧠 Key Insight

> Instead of updating all elements, store increment lazily and apply it during pop.

---
