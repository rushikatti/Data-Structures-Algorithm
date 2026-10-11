# 213. House Robber II

## Problem

Houses are arranged in a circle. Each house contains some money, and adjacent houses cannot both be robbed.

Since the houses form a circle, the **first and last houses are also adjacent**.

Return the maximum amount of money that can be robbed without robbing two adjacent houses.

---

## Approach 1: Recursion (Brute Force)

### Approach

For every house, we have two choices:

- **Steal:** Add the current house's money and move two steps forward.
- **Skip:** Move to the next house.

Since the first and last houses are adjacent, we cannot apply the normal House Robber solution directly to the entire array.

Instead, solve two cases:

1. Rob houses from index `0` to `n - 2` (exclude the last house).
2. Rob houses from index `1` to `n - 1` (exclude the first house).

Return the maximum of both cases.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            if (n == 1) {
                return nums[0];
            }

            int excludeLast = solve(nums, 0, n - 2);
            int excludeFirst = solve(nums, 1, n - 1);

            return Math.max(excludeLast, excludeFirst);
        }

        public int solve(int[] nums, int i, int r) {
            if (i > r) {
                return 0;
            }

            int steal = nums[i] + solve(nums, i + 2, r);
            int skip = solve(nums, i + 1, r);

            return Math.max(steal, skip);
        }
    }

### Complexity

- **Time:** O(2^n)
- **Space:** O(n) — recursion stack

---

## Approach 2: Recursion + Memoization (Top-Down DP)

### Approach

The recursive solution recalculates the same subproblems multiple times.

Use a DP array to store the maximum money obtainable starting at each index. Because the two cases use different ranges, create a fresh DP array for each case.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            if (n == 1) {
                return nums[0];
            }

            int[] dp1 = new int[n];
            int[] dp2 = new int[n];

            Arrays.fill(dp1, -1);
            Arrays.fill(dp2, -1);

            int excludeLast = solve(nums, 0, n - 2, dp1);
            int excludeFirst = solve(nums, 1, n - 1, dp2);

            return Math.max(excludeLast, excludeFirst);
        }

        public int solve(int[] nums, int i, int r, int[] dp) {
            if (i > r) {
                return 0;
            }

            if (dp[i] != -1) {
                return dp[i];
            }

            int steal = nums[i] + solve(nums, i + 2, r, dp);
            int skip = solve(nums, i + 1, r, dp);

            return dp[i] = Math.max(steal, skip);
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n) — DP arrays and recursion stack

---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

Use the normal House Robber recurrence:

    dp[i] = max(nums[i] + dp[i - 2], dp[i - 1])

Solve two cases:

1. Exclude the last house: process indices `0` through `n - 2`.
2. Exclude the first house: process indices `1` through `n - 1`.

Take the maximum of both results.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            if (n == 1) {
                return nums[0];
            }

            int excludeLast = solve(nums, 0, n - 2);
            int excludeFirst = solve(nums, 1, n - 1);

            return Math.max(excludeLast, excludeFirst);
        }

        public int solve(int[] nums, int l, int r) {
            int[] dp = new int[r - l + 2];

            dp[0] = 0;
            dp[1] = nums[l];

            for (int i = 2; i < dp.length; i++) {
                int currentHouse = nums[l + i - 1];

                int steal = currentHouse + dp[i - 2];
                int skip = dp[i - 1];

                dp[i] = Math.max(steal, skip);
            }

            return dp[dp.length - 1];
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n)

---

## Approach 4: Space Optimized DP

### Approach

We only need the previous two DP results to calculate the current result.

Maintain:

- `prevprev`: maximum money up to two positions back.
- `prev`: maximum money up to the previous position.

For each house:

    steal = nums[i] + prevprev
    skip = prev

    current = max(steal, skip)

Then update `prevprev` and `prev`.

Run this logic for both ranges:

- `0` to `n - 2`
- `1` to `n - 1`

Finally, return the larger result.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            if (n == 1) {
                return nums[0];
            }

            if (n == 2) {
                return Math.max(nums[0], nums[1]);
            }

            int excludeLast = solve(nums, 0, n - 2);
            int excludeFirst = solve(nums, 1, n - 1);

            return Math.max(excludeLast, excludeFirst);
        }

        public int solve(int[] nums, int l, int r) {
            int prev = 0;
            int prevprev = 0;

            for (int i = l; i <= r; i++) {
                int steal = nums[i] + prevprev;
                int skip = prev;

                int current = Math.max(steal, skip);

                prevprev = prev;
                prev = current;
            }

            return prev;
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Complexity Comparison

| Approach | Time | Auxiliary Space |
|---|---|---|
| Recursion | O(2^n) | O(n) |
| Memoization | O(n) | O(n) |
| Tabulation | O(n) | O(n) |
| Space Optimized DP | O(n) | O(1) |

---

## Key Takeaway

House Robber II is an extension of House Robber I.

The only new challenge is the circular arrangement: **the first and last houses cannot both be robbed**.

Break the circular problem into two linear problems:

    Case 1: Exclude the last house
            solve(nums, 0, n - 2)

    Case 2: Exclude the first house
            solve(nums, 1, n - 1)

    Answer = max(Case 1, Case 2)

Your space-optimized solution is the most space-efficient of these approaches, taking **O(n) time and O(1) auxiliary space**.
