# 📈 Online Stock Span Problem

## 🧠 Problem Statement

Design a class `StockSpanner` which collects daily price quotes for a stock and returns the **span** of that stock’s price for the current day.

The **span** is defined as the maximum number of consecutive days (starting from today and going backward) for which the stock price was **less than or equal to today's price**.

### Example:

    Input:
    ["StockSpanner", "next", "next", "next", "next", "next", "next"]
    [[], [100], [80], [60], [70], [60], [75], [85]]

    Output:
    [null, 1, 1, 1, 2, 1, 4, 6]

---

## 💡 Approach 1: Brute Force

### Idea:
For each price, go backward and count how many consecutive days have price ≤ current.

### Algorithm:
1. Store all prices in a list.
2. For each new price:
   - Start from the last index and move backward.
   - Count until a greater price is found.

### Code:
    class StockSpanner {
        List<Integer> prices;

        public StockSpanner() {
            prices = new ArrayList<>();
        }

        public int next(int price) {
            prices.add(price);
            int span = 1;
            int i = prices.size() - 2;

            while (i >= 0 && prices.get(i) <= price) {
                span++;
                i--;
            }

            return span;
        }
    }

### Complexity:
- Time: O(N²) worst case
- Space: O(N)

---

## 🚀 Approach 2: Optimal (Monotonic Stack)

### Idea:
Use a **monotonic decreasing stack** that stores pairs of:
    (price, span)

We collapse previous smaller prices into one entry.

### Key Insight:
If current price is greater than stack top, it "absorbs" its span.

---

### Algorithm:
1. Maintain a stack of pairs (price, span).
2. For each incoming price:
   - Initialize span = 1
   - While stack not empty AND top.price ≤ current price:
       - Add top.span to span
       - Pop stack
   - Push (price, span) to stack
3. Return span

---

### Code:
    class StockSpanner {
        Stack<int[]> stack;

        public StockSpanner() {
            stack = new Stack<>();
        }

        public int next(int price) {
            int span = 1;

            while (!stack.isEmpty() && stack.peek()[0] <= price) {
                span += stack.pop()[1];
            }

            stack.push(new int[]{price, span});
            return span;
        }
    }

---

## 🔥 Dry Run Example

Prices: 100, 80, 60, 70, 60, 75, 85

Stack evolution:

    100 → [(100,1)] → span=1
    80  → [(100,1),(80,1)] → span=1
    60  → [(100,1),(80,1),(60,1)] → span=1
    70  → pop(60) → span=2 → [(100,1),(80,1),(70,2)]
    60  → [(100,1),(80,1),(70,2),(60,1)] → span=1
    75  → pop(60,1), pop(70,2) → span=4 → [(100,1),(80,1),(75,4)]
    85  → pop(75,4), pop(80,1) → span=6 → [(100,1),(85,6)]

---

## ⏱ Complexity

- Time: **O(N)** (each element pushed & popped once)
- Space: **O(N)**

---

## 🧩 Pattern Recognition

This is a classic **Monotonic Stack** problem:
- Stack maintains decreasing order
- Useful for:
  - Next Greater Element
  - Histogram problems
  - Span problems

---

## 🏁 Summary

| Approach        | Time Complexity | Space | Notes                  |
|----------------|---------------|-------|------------------------|
| Brute Force    | O(N²)         | O(N)  | Simple but inefficient |
| Monotonic Stack| O(N)          | O(N)  | Optimal solution       |

---
