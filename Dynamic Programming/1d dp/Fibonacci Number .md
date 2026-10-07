```md
# Fibonacci Number

## Problem

Given an integer `n`, return the `n`th Fibonacci number.

The Fibonacci sequence is:

    F(0) = 0
    F(1) = 1

    F(n) = F(n - 1) + F(n - 2)

Example:

    Input: 5
    Output: 5

    Fibonacci sequence:
    0, 1, 1, 2, 3, 5, 8...

---

# 1. Recursion — Brute Force

## Concept

The Fibonacci definition itself is recursive:

    fib(n) = fib(n - 1) + fib(n - 2)

So we can directly implement the recurrence.

## Code

    class Solution {
        public int fib(int n) {

            if (n <= 1) {
                return n;
            }

            return fib(n - 1) + fib(n - 2);
        }
    }

## How it works

For:

    fib(5)

The recursion becomes:

    fib(5)
       /    \
    fib(4)  fib(3)
     /  \    /  \
   fib3 fib2 fib2 fib1

The same values are calculated multiple times.

For example:

    fib(3)

is calculated more than once.

## Complexity

    Time:  O(2^n)
    Space: O(n)

The `O(n)` space comes from the recursion call stack.

---

# 2. Memoization — Top-Down DP

## Concept

The problem with normal recursion is repeated calculation.

For example:

    fib(5)
       |
      fib(4)
       |
      fib(3)

If `fib(3)` has already been calculated, we should not calculate it again.

So we store each calculated result in an array called `dp`.

This is called:

    Memoization
    = Recursion + Cache

This is a **Top-Down Dynamic Programming** approach.

## Code

    class Solution {
        public int fib(int n) {

            int[] dp = new int[n + 1];

            Arrays.fill(dp, -1);

            return fibonacci(n, dp);
        }

        public int fibonacci(int n, int[] dp) {

            if (n <= 1) {
                return n;
            }

            if (dp[n] != -1) {
                return dp[n];
            }

            dp[n] = fibonacci(n - 1, dp)
                  + fibonacci(n - 2, dp);

            return dp[n];
        }
    }

## Important Part

    if (dp[n] != -1) {
        return dp[n];
    }

This checks whether we already calculated `fib(n)`.

If not:

    dp[n] = fibonacci(n - 1, dp)
          + fibonacci(n - 2, dp);

Then we store the result.

## Example

For `n = 5`:

    dp[0] = 0
    dp[1] = 1
    dp[2] = 1
    dp[3] = 2
    dp[4] = 3
    dp[5] = 5

Now if `fib(3)` is requested again:

    dp[3] != -1

So we directly return:

    dp[3] = 2

No recalculation.

## Complexity

    Time:  O(n)
    Space: O(n)

`O(n)` space comes from:

    dp array       -> O(n)
    recursion stack -> O(n)

---

# 3. Tabulation — Bottom-Up DP

## Concept

Instead of starting from `fib(n)` and recursively going down, we calculate the answers from the bottom.

Start with:

    dp[0] = 0
    dp[1] = 1

Then:

    dp[2] = dp[1] + dp[0]
    dp[3] = dp[2] + dp[1]
    dp[4] = dp[3] + dp[2]
    ...

This is called:

    Tabulation
    = Bottom-Up Dynamic Programming

## Code

    class Solution {
        public int fib(int n) {

            int[] dp = new int[n + 1];

            if (n <= 1) {
                return n;
            }

            dp[0] = 0;
            dp[1] = 1;

            for (int i = 2; i <= n; i++) {
                dp[i] = dp[i - 1] + dp[i - 2];
            }

            return dp[n];
        }
    }

## Dry Run

For:

    n = 5

Initially:

    dp[0] = 0
    dp[1] = 1

i = 2:

    dp[2] = dp[1] + dp[0]
          = 1 + 0
          = 1

i = 3:

    dp[3] = dp[2] + dp[1]
          = 1 + 1
          = 2

i = 4:

    dp[4] = dp[3] + dp[2]
          = 2 + 1
          = 3

i = 5:

    dp[5] = dp[4] + dp[3]
          = 3 + 2
          = 5

Answer:

    5

## Complexity

    Time:  O(n)
    Space: O(n)

---

# 4. Space Optimized DP

## Concept

Look at the Fibonacci formula:

    fib(n) = fib(n - 1) + fib(n - 2)

To calculate the next number, we only need the previous two numbers.

We don't actually need the entire `dp` array.

Instead of:

    dp[i - 2]
    dp[i - 1]
    dp[i]

we maintain:

    a = previous previous
    b = previous
    c = current

## Code

    class Solution {
        public int fib(int n) {

            if (n <= 1) {
                return n;
            }

            int c = 0;
            int a = 0;
            int b = 1;

            for (int i = 1; i < n; i++) {

                c = a + b;

                a = b;
                b = c;
            }

            return c;
        }
    }

## Dry Run

For:

    n = 5

Initial:

    a = 0
    b = 1

### i = 1

    c = 0 + 1 = 1

    a = 1
    b = 1

### i = 2

    c = 1 + 1 = 2

    a = 1
    b = 2

### i = 3

    c = 1 + 2 = 3

    a = 2
    b = 3

### i = 4

    c = 2 + 3 = 5

    a = 3
    b = 5

Return:

    c = 5

## Complexity

    Time:  O(n)
    Space: O(1)

---

# Comparison of All Approaches

| Approach | Time | Space | Technique |
|---|---:|---:|---|
| Recursion | O(2^n) | O(n) | Recursion |
| Memoization | O(n) | O(n) | Top-Down DP |
| Tabulation | O(n) | O(n) | Bottom-Up DP |
| Space Optimized | O(n) | O(1) | Bottom-Up DP |

---

# Key DP Concept

The evolution is:

    Recursion
       ↓
    Repeated calculations
       ↓
    Memoization
       ↓
    Store previous results
       ↓
    Tabulation
       ↓
    Notice only previous 2 values are needed
       ↓
    Space Optimization

So the four approaches are:

    1. Recursion
    2. Recursion + Memoization
    3. Tabulation
    4. Space Optimized Tabulation

---

# Interview Takeaway

If asked to solve Fibonacci:

### Start with recursion

    fib(n) = fib(n-1) + fib(n-2)

Then explain the problem:

    Same subproblems are calculated repeatedly.

Improve it using memoization:

    Recursion + dp[] = O(n)

Then explain:

    Since Fibonacci only needs the previous two values,
    we can remove the dp array.

Final optimized solution:

    Time:  O(n)
    Space: O(1)

This progression is important because it demonstrates the core DP optimization pattern:

    Recursion → Memoization → Tabulation → Space Optimization
```
