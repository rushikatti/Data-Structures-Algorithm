# Climbing Stairs

## Approach 1: Recursion

### Approach

At every stair, there are two choices:

- Take 1 step → solve(n - 1)
- Take 2 steps → solve(n - 2)

So:

    solve(n) = solve(n - 1) + solve(n - 2)

Base cases:

    n < 0 → 0
    n == 0 → 1

`n == 0` returns `1` because reaching exactly the top represents one valid way.

### Code

    class Solution {

        public int solve(int n) {
            if (n < 0) return 0;

            if (n == 0) return 1;

            int one_step = solve(n - 1);
            int two_step = solve(n - 2);

            return one_step + two_step;
        }

        public int climbStairs(int n) {
            return solve(n);
        }
    }

### Complexity

    Time:  O(2^n)
    Space: O(n)


---

# Approach 2: Recursion + Memoization

### Approach

The recursive solution calculates the same subproblems multiple times.

Store each calculated result in `arr[n]`.

If `arr[n]` is already calculated, return it directly.

This converts the recursive solution into **Top-Down Dynamic Programming**.

### Code

    class Solution {

        public int solve(int n, int[] arr) {
            if (n < 0) return 0;

            if (n == 0) return 1;

            if (arr[n] != -1) {
                return arr[n];
            }

            int one_step = solve(n - 1, arr);
            int two_step = solve(n - 2, arr);

            return arr[n] = one_step + two_step;
        }

        public int climbStairs(int n) {
            int[] arr = new int[n + 1];

            Arrays.fill(arr, -1);

            return solve(n, arr);
        }
    }

### Complexity

    Time:  O(n)
    Space: O(n)

    O(n) → DP array
    O(n) → recursion stack


---

# Approach 3: Tabulation

### Approach

Build the answer from the bottom up.

For every stair:

    arr[i] = arr[i - 1] + arr[i - 2]

Base cases:

    arr[1] = 1
    arr[2] = 2

This is **Bottom-Up Dynamic Programming**.

### Code

    class Solution {
        public int climbStairs(int n) {

            if (n == 0 || n == 1 || n == 2) {
                return n;
            }

            int[] arr = new int[n + 1];

            arr[0] = 0;
            arr[1] = 1;
            arr[2] = 2;

            for (int i = 3; i <= n; i++) {
                arr[i] = arr[i - 1] + arr[i - 2];
            }

            return arr[n];
        }
    }

### Complexity

    Time:  O(n)
    Space: O(n)


---

# Approach 4: Space Optimized DP

### Approach

To calculate the current answer, we only need the previous two values.

So instead of storing the entire array, maintain:

    a = previous previous value
    b = previous value
    c = current value

This reduces the space from `O(n)` to `O(1)`.

### Code

    class Solution {
        public int climbStairs(int n) {

            if (n == 0 || n == 1 || n == 2) {
                return n;
            }

            int a = 1;
            int b = 2;
            int c = 3;

            for (int i = 3; i <= n; i++) {

                c = a + b;

                int temp = b;
                b = c;
                a = temp;
            }

            return c;
        }
    }

### Complexity

    Time:  O(n)
    Space: O(1)


---

# Complexity Comparison

| Approach | Time | Space |
|---|---:|---:|
| Recursion | O(2^n) | O(n) |
| Memoization | O(n) | O(n) |
| Tabulation | O(n) | O(n) |
| Space Optimized DP | O(n) | O(1) |
