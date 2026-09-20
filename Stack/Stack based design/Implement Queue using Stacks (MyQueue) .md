# 🔢 Implement Queue using Stacks (MyQueue)

## 🧠 Problem Statement

Implement a **queue (FIFO)** using only **stacks (LIFO)**.

Support operations:
- `push(x)` → insert element  
- `pop()` → remove front element  
- `peek()` → get front  
- `empty()` → check if empty  

---

# 💡 Approach 1: Brute Force (Push Costly)

## 🔹 Idea

Maintain queue order inside `st1` by reversing elements every time we push.

---

## 🔹 Algorithm

### push(x)
1. Move all elements from `st1 → st2`
2. Push `x` into `st1`
3. Move back all elements `st2 → st1`

### pop / peek
- Directly operate on `st1`

---

## 🔹 Code

    class MyQueue {
        Stack<Integer> st1;
        Stack<Integer> st2;

        public MyQueue() {
            st1 = new Stack<>();
            st2 = new Stack<>();
        }
        
        public void push(int x) {
            while(!st1.isEmpty()){
                st2.push(st1.pop());
            }

            st1.push(x);

            while(!st2.isEmpty()){
                st1.push(st2.pop());
            }
        }
        
        public int pop() {
            return st1.pop();
        }
        
        public int peek() {
            return st1.peek();
        }
        
        public boolean empty() {
            return st1.isEmpty();
        }
    }

---

## ⏱ Complexity

- push → **O(N)** ❌  
- pop → **O(1)**  
- peek → **O(1)**  

---

# 🚀 Approach 2: Optimal (Amortized O(1))

## 🔹 Idea

Use:
- `st1` → input stack (push here)
- `st2` → output stack (pop/peek from here)

Transfer only when needed.

---

## 🔹 Algorithm

### push(x)
- Push into `st1`

### pop()
- If `st2` empty:
    → move all elements `st1 → st2`
- Pop from `st2`

### peek()
- Same as pop but return top

### empty()
- Both stacks empty

---

## 🔹 Code

    class MyQueue {
        Stack<Integer> st1;
        Stack<Integer> st2;

        public MyQueue() {
            st1 = new Stack<>();
            st2 = new Stack<>();
        }
        
        public void push(int x) {
            st1.push(x);
        }
        
        public int pop() {
            if(st2.isEmpty()){
                while(!st1.isEmpty()){
                    st2.push(st1.pop());
                }
            }
            return st2.pop();
        }
        
        public int peek() {
            if(st2.isEmpty()){
                while(!st1.isEmpty()){
                    st2.push(st1.pop());
                }
            }
            return st2.peek();
        }
        
        public boolean empty() {
            return st1.isEmpty() && st2.isEmpty();
        }
    }

---

## ⏱ Complexity

- push → **O(1)**  
- pop → **Amortized O(1)**  
- peek → **Amortized O(1)**  
- space → **O(N)**  

---

# 🏁 Summary

| Approach        | Push | Pop | Peek | Notes                      |
|----------------|------|-----|------|----------------------------|
| Brute Force    | O(N) | O(1)| O(1) | Reverse every push         |
| Optimal        | O(1) | O(1)* | O(1)* | Lazy transfer (amortized) |

---

# 🧠 Key Insight

> Use **two stacks** to reverse order:
> - One for input
> - One for output

---
