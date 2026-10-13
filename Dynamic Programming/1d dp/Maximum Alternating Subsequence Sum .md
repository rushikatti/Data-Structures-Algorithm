# 1911. Maximum Alternating Subsequence Sum

## Problem

Given an integer array `nums`, find the maximum alternating sum of any subsequence.

The alternating sum is calculated by adding the elements at even positions and subtracting the elements at odd positions, starting with addition.

Example:

    Input: nums = [4, 2, 5, 3]

    Output: 7

    Explanation:
    Choose subsequence [4, 5].

    Alternating sum = 4 - 5? No.
    Choose subsequence [4, 2, 5].

    Alternating sum = 4 - 2 + 5 = 7.

---

## Approach 1: Recursion

### Approach

At every index, we have two choices:

- **Take:** Include the current element in the subsequence.
- **Skip:** Ignore the current element.

The sign of the current element depends on the position it would occupy in the chosen subsequence.

Maintain a boolean `isEven`:
- `true`: The next selected element is added.
- `false`: The next selected element is subtracted.

If we take the current element, switch the sign for the next selection. If we skip it, keep the same sign.

### Code

    class Solution {
        public long maxAlternatingSum(int[] nums) {
            return solve(nums, 0, true);
        }

        public long solve(int[] nums, int i, boolean isEven) {
            if (i == nums.length) {
                return 0;
            }

            long skip = solve(nums, i + 1, isEven);

            long value = isEven ? nums[i] : -nums[i];
            long take = value + solve(nums, i + 1, !isEven);

            return Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(2^n)
- **Space:** O(n) — recursion stack

---

## Approach 2: Recursion + Memoization (Top-Down DP)

### Approach

The recursive solution repeats the same calculations for a given index and sign.

Use `dp[i][0]` and `dp[i][1]` to store the answers:

- `dp[i][0]`: Maximum alternating sum from index `i` when the next selected element is subtracted.
- `dp[i][1]`: Maximum alternating sum from index `i` when the next selected element is added.

At each index, calculate the maximum of taking and skipping the current element.

### Code

    import java.util.Arrays;

    class Solution {
        public long maxAlternatingSum(int[] nums) {
            int n = nums.length;
            long[][] dp = new long[n][2];

            for (long[] row : dp) {
                Arrays.fill(row, Long.MIN_VALUE);
            }

            return solve(nums, 0, 1, dp);
        }

        public long solve(int[] nums, int i, int isEven, long[][] dp) {
            if (i == nums.length) {
                return 0;
            }

            if (dp[i][isEven] != Long.MIN_VALUE) {
                return dp[i][isEven];
            }

            long skip = solve(nums, i + 1, isEven, dp);

            long value = isEven == 1 ? nums[i] : -((long) nums[i]);
            long take = value + solve(nums, i + 1, 1 - isEven, dp);

            return dp[i][isEven] = Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n)

---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

Maintain two states for each prefix:

- `even`: Maximum alternating sum when the last selected element has a positive sign.
- `odd`: Maximum alternating sum when the last selected element has a negative sign.

Initially:

    even = 0
    odd = 0

For each element `x`:

    newEven = max(even, odd + x)
    newOdd  = max(odd, even - x)

The first state either keeps the previous positive-ending answer or selects `x` as a positive element after a negative-ending subsequence.

The second state either keeps the previous negative-ending answer or selects `x` as a negative element after a positive-ending subsequence.

### Code

    class Solution {
        public long maxAlternatingSum(int[] nums) {
            int n = nums.length;
            long[][] dp = new long[n + 1][2];

            for (int i = 1; i <= n; i++) {
                long x = nums[i - 1];

                dp[i][1] = Math.max(
                    dp[i - 1][1],
                    dp[i - 1][0] + x
                );

                dp[i][0] = Math.max(
                    dp[i - 1][0],
                    dp[i - 1][1] - x
                );
            }

            return dp[n][1];
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n)

---

## Approach 4: Space Optimized DP

### Approach

The tabulation solution only needs the two states from the previous iteration, not the entire DP array.

Maintain:

- `even`: Best alternating sum ending with a positive-sign selection.
- `odd`: Best alternating sum ending with a negative-sign selection.

For each number `x`, update both states using their previous values.

**Important:** Calculate both new values before overwriting either state.

### Code

    class Solution {
        public long maxAlternatingSum(int[] nums) {
            long even = 0;
            long odd = 0;

            for (int x : nums) {
                long newEven = Math.max(even, odd + x);
                long newOdd = Math.max(odd, even - x);

                even = newEven;
                odd = newOdd;
            }

            return even;
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Complexity Comparison

| Approach | Time | Space |
|---|---|---|
| Recursion | O(2^n) | O(n) |
| Memoization | O(n) | O(n) |
| Tabulation | O(n) | O(n) |
| Space Optimized DP | O(n) | O(1) |

---

## Key Takeaway

This problem follows the **Take or Skip + DP State** pattern.

At every index:
- Skip the element and preserve the current state.
- Take the element and switch between positive and negative signs.

The optimized solution runs in **O(n) time and O(1) space**.
