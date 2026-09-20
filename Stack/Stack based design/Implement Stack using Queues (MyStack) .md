# 🔢 Implement Stack using Queues (MyStack)

## 🧠 Problem Statement

Implement a **stack (LIFO)** using only **queues (FIFO)**.

Support operations:
- `push(x)` → push element  
- `pop()` → remove top  
- `top()` → get top  
- `empty()` → check if empty  

---

# 💡 Approach 1: Brute Force (Push Costly)

## 🔹 Idea

Maintain stack order inside `q1` by reordering on every push.

---

## 🔹 Algorithm

### push(x)
1. Push `x` into `q2`
2. Move all elements from `q1 → q2`
3. Assign `q1 = q2`
4. Reset `q2`

### pop / top
- Directly operate on `q1`

---

## 🔹 Code

    class MyStack {
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();

        public MyStack() {}

        public void push(int x) {
            q2.offer(x);

            while(!q1.isEmpty()){
                q2.offer(q1.poll());
            }

            q1 = q2;
            q2 = new LinkedList<>();
        }

        public int pop() {
            return q1.poll();
        }

        public int top() {
            return q1.peek();
        }

        public boolean empty() {
            return q1.isEmpty();
        }
    }

---

## ⏱ Complexity

- push → **O(N)** ❌  
- pop → **O(1)**  
- top → **O(1)**  

---

# 🚀 Approach 2: Optimal (Pop/Top Costly)

## 🔹 Idea

Push is simple. Reorder only when needed during pop/top.

---

## 🔹 Algorithm

### push(x)
- Add directly to `q1`

### pop()
1. Move `n-1` elements from `q1 → q2`
2. Remove last element (top of stack)
3. Swap `q1` and `q2`

### top()
1. Move `n-1` elements from `q1 → q2`
2. Read last element
3. Put it back into `q2`
4. Swap queues

---

## 🔹 Code

    class MyStack {
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();

        public MyStack() {}

        public void push(int x) {
            q1.offer(x);
        }

        public int pop() {
            while(q1.size() > 1){
                q2.offer(q1.poll());
            }

            int val = q1.poll();

            q1 = q2;
            q2 = new LinkedList<>();

            return val;
        }

        public int top() {
            while(q1.size() > 1){
                q2.offer(q1.poll());
            }

            int val = q1.peek();
            q2.offer(q1.poll());

            q1 = q2;
            q2 = new LinkedList<>();

            return val;
        }

        public boolean empty() {
            return q1.isEmpty();
        }
    }

---

## ⏱ Complexity

- push → **O(1)**  
- pop → **O(N)**  
- top → **O(N)**  

---

# 🏁 Summary

| Approach        | Push | Pop | Top | Notes                      |
|----------------|------|-----|-----|----------------------------|
| Push Costly    | O(N) | O(1)| O(1)| Reorder during push        |
| Pop Costly     | O(1) | O(N)| O(N)| Reorder during pop/top     |

---

# 🧠 Key Insight

> Use queues to simulate stack by **reversing order of elements**

---
