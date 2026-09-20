# 🧱 Min Stack

## 🧠 Problem Statement

Design a stack that supports:

- `push(x)` → push element  
- `pop()` → remove top  
- `top()` → return top element  
- `getMin()` → return **minimum element**

👉 All operations must run in **O(1)** time

---

# 💡 Approach 1: Brute Force

## 🔹 Idea

Use a normal stack.  
Each time `getMin()` is called → scan entire stack.

---

## 🔹 Code

    class MinStack {
        Stack<Integer> st;

        public MinStack() {
            st = new Stack<>();
        }

        public void push(int val) {
            st.push(val);
        }

        public void pop() {
            st.pop();
        }

        public int top() {
            return st.peek();
        }

        public int getMin() {
            int min = Integer.MAX_VALUE;

            for(int x : st){
                min = Math.min(min, x);
            }

            return min;
        }
    }

---

## ⏱ Complexity

- push/pop/top → **O(1)**
- getMin → **O(N)** ❌

---

# 🚀 Approach 2: Optimal (Two Stacks)

## 🔹 Idea

Maintain:
- `st` → main stack  
- `minSt` → track minimums  

---

## 🔹 Algorithm

### push(val)
- Push into `st`
- If `minSt` empty OR `val <= minSt.peek()` → push into `minSt`

### pop()
- If `st.peek() == minSt.peek()` → pop from `minSt`
- Always pop from `st`

### getMin()
- Return `minSt.peek()`

---

## 🔹 Code

    class MinStack {
        Stack<Integer> st;
        Stack<Integer> minSt;

        public MinStack() {
            st = new Stack<>();
            minSt = new Stack<>();
        }

        public void push(int val) {
            st.push(val);

            if(minSt.isEmpty() || val <= minSt.peek()){
                minSt.push(val);
            }
        }

        public void pop() {
            if(st.peek().equals(minSt.peek())){
                minSt.pop();
            }
            st.pop();
        }

        public int top() {
            return st.peek();
        }

        public int getMin() {
            return minSt.peek();
        }
    }

---

## ⏱ Complexity

- All operations → **O(1)**
- Space → **O(N)**

---

# ⚡ Approach 3: Optimal (Single Stack + Encoding Trick)

## 🔹 Idea

Store modified values when a new minimum comes.

---

## 🔹 Algorithm

Maintain:
- `min` variable

### push(val)
- If empty:
    → push val, set min = val  
- If val ≥ min:
    → push val  
- If val < min:
    → push encoded value = `2*val - min`
    → update min = val  

### pop()
- If top < min:
    → restore previous min  

---

## 🔹 Code

    class MinStack {
        Stack<Long> st;
        long min;

        public MinStack() {
            st = new Stack<>();
        }

        public void push(int val) {
            if(st.isEmpty()){
                st.push((long)val);
                min = val;
            }
            else if(val >= min){
                st.push((long)val);
            }
            else{
                st.push(2L * val - min);
                min = val;
            }
        }

        public void pop() {
            if(st.peek() < min){
                min = 2 * min - st.pop();
            } else {
                st.pop();
            }
        }

        public int top() {
            if(st.peek() < min){
                return (int)min;
            }
            return st.peek().intValue();
        }

        public int getMin() {
            return (int)min;
        }
    }

---

## ⏱ Complexity

- Time: **O(1)** for all operations  
- Space: **O(1)** extra  

---

# 🏁 Summary

| Approach        | Time | Space | Notes                      |
|----------------|------|-------|----------------------------|
| Brute Force    | O(N) | O(N)  | getMin slow                |
| Two Stacks     | O(1) | O(N)  | Most used                  |
| Encoding Trick | O(1) | O(1)  | Advanced optimization      |

---

# 🧠 Key Insight

> Track minimum **during push/pop**, not by recomputing.

---
