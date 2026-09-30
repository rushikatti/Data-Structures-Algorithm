# 🔢 Reverse a Stack using Recursion

## 🧠 Problem Statement

Given a stack, reverse it **using recursion only**  
👉 No extra data structures allowed (except recursion call stack)

---

# 💡 Core Idea

We use **2 recursive functions**:

1. **reverse()**
   - Removes top element
   - Recursively reverses remaining stack
   - Inserts removed element at **bottom**

2. **insertAtBottom()**
   - Inserts an element at the bottom using recursion

---

# 🔁 How It Works

Example:

    Stack (top → bottom): 1 2 3

Steps:

    reverse(1,2,3)
        pop 1 → reverse(2,3)
            pop 2 → reverse(3)
                pop 3 → reverse()
                    empty → return
                insertAtBottom(3)
            insertAtBottom(2)
        insertAtBottom(1)

Result:

    Stack: 3 2 1

---

# 🚀 Code

    class Solution {

        public static void reverse(Stack<Integer> st){
            if(st.isEmpty()) return;

            int top = st.pop();

            reverse(st);

            insertAtBottom(st, top);
        }

        private static void insertAtBottom(Stack<Integer> st, int val){
            if(st.isEmpty()){
                st.push(val);
                return;
            }

            int top = st.pop();

            insertAtBottom(st, val);

            st.push(top);
        }
    }

---

# 🧪 Dry Run

Initial:

    [1, 2, 3]  (3 is top)

Call:

    reverse(st)

Execution:

    pop 3 → reverse [1,2]
    pop 2 → reverse [1]
    pop 1 → reverse []

Now inserting back:

    insertAtBottom(1) → [1]
    insertAtBottom(2) → [2,1]
    insertAtBottom(3) → [3,2,1]

---

# ⏱ Complexity

- Time: **O(N²)**
  - Each insertAtBottom → O(N)

- Space: **O(N)**
  - Recursion stack

---

# 🧠 Key Insight

> Reverse =  
> 👉 Remove top  
> 👉 Reverse rest  
> 👉 Insert removed element at bottom

---

# 🏁 One-line Intuition

> “Take top out, reverse remaining, then push it at the bottom”

---
