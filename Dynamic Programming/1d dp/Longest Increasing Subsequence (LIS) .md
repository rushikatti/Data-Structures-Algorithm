# 300. Longest Increasing Subsequence (LIS)

## Problem

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A subsequence is formed by deleting zero or more elements without changing the order of the remaining elements.

Example:

    Input: nums = [10, 9, 2, 5, 3, 7, 101, 18]
    Output: 4

    Explanation:
    One LIS is [2, 3, 7, 101].
    Another LIS is [2, 3, 7, 18].

---

## Approach 1: Recursion (Brute Force)

### Approach

At every index, we have two choices:

- **Take:** Include the current element if it is greater than the previously selected element.
- **Skip:** Ignore the current element.

To track the previous selected element, maintain `prev`.

Initially, `prev = -1`, meaning no element has been selected.

### Code

    class Solution {
        public int lengthOfLIS(int[] nums) {
            return solve(nums, 0, -1);
        }

        public int solve(int[] nums, int i, int prev) {
            if (i == nums.length) {
                return 0;
            }

            int skip = solve(nums, i + 1, prev);

            int take = 0;
            if (prev == -1 || nums[i] > nums[prev]) {
                take = 1 + solve(nums, i + 1, i);
            }

            return Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(2^n)
- **Space:** O(n) — recursion stack

---

## Approach 2: Recursion + Memoization (Top-Down DP)

### Approach

The recursive solution repeats the same subproblems.

The result depends on two variables:

- `i`: Current index.
- `prev`: Index of the previously selected element.

Therefore, use a **2D DP array**:

    dp[i][prev + 1]

We use `prev + 1` because `prev = -1` is a valid initial state, and Java array indices cannot be negative.

### Code

    import java.util.Arrays;

    class Solution {
        public int lengthOfLIS(int[] nums) {
            int n = nums.length;
            int[][] dp = new int[n][n + 1];

            for (int[] row : dp) {
                Arrays.fill(row, -1);
            }

            return solve(nums, 0, -1, dp);
        }

        public int solve(int[] nums, int i, int prev, int[][] dp) {
            if (i == nums.length) {
                return 0;
            }

            if (dp[i][prev + 1] != -1) {
                return dp[i][prev + 1];
            }

            int skip = solve(nums, i + 1, prev, dp);

            int take = 0;
            if (prev == -1 || nums[i] > nums[prev]) {
                take = 1 + solve(nums, i + 1, i, dp);
            }

            return dp[i][prev + 1] = Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(n²)
- **Space:** O(n²) — DP array, plus O(n) recursion stack

---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

Define:

    dp[i] = length of the LIS ending at index i

Initially, every element forms an increasing subsequence of length `1`.

    dp[i] = 1

For each index `i`, check every earlier index `j`.

If:

    nums[i] > nums[j]

then `nums[i]` can extend the increasing subsequence ending at `j`.

Update:

    dp[i] = max(dp[i], dp[j] + 1)

The final answer is the maximum value in `dp`.

### Code

    class Solution {
        public int lengthOfLIS(int[] nums) {
            int n = nums.length;
            int[] dp = new int[n];

            Arrays.fill(dp, 1);

            int ans = 1;

            for (int i = 1; i < n; i++) {
                for (int j = 0; j < i; j++) {
                    if (nums[i] > nums[j]) {
                        dp[i] = Math.max(dp[i], dp[j] + 1);
                    }
                }

                ans = Math.max(ans, dp[i]);
            }

            return ans;
        }
    }

### Complexity

- **Time:** O(n²)
- **Space:** O(n)

---

## Approach 4: Binary Search (Optimized)

### Approach

Maintain an array called `tails`.

    tails[len - 1] = smallest possible ending value
                      of an increasing subsequence of length len

For every number `x`:

1. Use binary search to find the first element in `tails` that is greater than or equal to `x`.
2. Replace that element with `x`.
3. If no such element exists, append `x` to the end.

The length of `tails` gives the LIS length.

**Important:** `tails` does not necessarily contain the actual LIS. It stores useful minimum ending values for subsequences of different lengths.

### Code

    class Solution {
        public int lengthOfLIS(int[] nums) {
            int n = nums.length;
            int[] tails = new int[n];
            int size = 0;

            for (int x : nums) {
                int left = 0;
                int right = size;

                while (left < right) {
                    int mid = left + (right - left) / 2;

                    if (tails[mid] < x) {
                        left = mid + 1;
                    } else {
                        right = mid;
                    }
                }

                tails[left] = x;

                if (left == size) {
                    size++;
                }
            }

            return size;
        }
    }

### Complexity

- **Time:** O(n log n)
- **Space:** O(n)

---

## Complexity Comparison

| Approach | Time | Space | DP Type |
|---|---|---|---|
| Recursion | O(2ⁿ) | O(n) | Recursive |
| Memoization | O(n²) | O(n²) | 2D DP |
| Tabulation | O(n²) | O(n) | 1D DP |
| Binary Search | O(n log n) | O(n) | Optimized LIS technique |

---

## Key Takeaway

LIS can be approached in multiple ways:

- **Recursion:** Take or skip each element.
- **Memoization:** Cache states based on the current index and previous selected index.
- **Tabulation:** Calculate the LIS ending at each index.
- **Binary Search:** Maintain minimum ending values to achieve an O(n log n) solution.

For DP classification, the memoization solution uses **2D DP** because its state depends on `i` and `prev`. The tabulation solution uses **1D DP** because `dp[i]` represents the LIS ending at index `i`.
