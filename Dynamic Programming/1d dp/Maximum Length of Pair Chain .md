# 646. Maximum Length of Pair Chain

## Problem

You are given an array of pairs `pairs`, where `pairs[i] = [a, b]`.

A pair `[c, d]` can follow `[a, b]` if `b < c`.

Return the maximum length of a chain that can be formed.

Example:

    Input: pairs = [[1,2], [2,3], [3,4]]
    Output: 2

    Explanation:
    One longest chain is [1,2] -> [3,4].
    Since 2 is not less than 2, [2,3] cannot follow [1,2].

---

## Approach 1: Recursion (Brute Force)

### Approach

For every pair, we have two choices:

- **Take:** Include the current pair if its start is greater than the end of the previously selected pair.
- **Skip:** Ignore the current pair.

Maintain `prev`, the index of the previously selected pair. Initially, `prev = -1`, meaning no pair has been selected.

### Code

    class Solution {
        public int findLongestChain(int[][] pairs) {
            Arrays.sort(pairs, (a, b) -> Integer.compare(a[0], b[0]));
            return solve(pairs, 0, -1);
        }

        public int solve(int[][] pairs, int i, int prev) {
            if (i == pairs.length) {
                return 0;
            }

            int skip = solve(pairs, i + 1, prev);

            int take = 0;

            if (prev == -1 || pairs[i][0] > pairs[prev][1]) {
                take = 1 + solve(pairs, i + 1, i);
            }

            return Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(2ⁿ)
- **Space:** O(n) — recursion stack

---

## Approach 2: Recursion + Memoization (Top-Down DP)

### Approach

The recursive solution recalculates the same subproblems.

The result depends on:

- `i`: Current pair index.
- `prev`: Index of the previously selected pair.

Use a 2D DP array to store the results. Since `prev` can be `-1`, access the state using `prev + 1`.

### Code

    import java.util.Arrays;

    class Solution {
        public int findLongestChain(int[][] pairs) {
            int n = pairs.length;
            Arrays.sort(pairs, (a, b) -> Integer.compare(a[0], b[0]));
            int[][] dp = new int[n][n + 1];

            for (int[] row : dp) {
                Arrays.fill(row, -1);
            }

            return solve(pairs, 0, -1, dp);
        }

        public int solve(int[][] pairs, int i, int prev, int[][] dp) {
            if (i == pairs.length) {
                return 0;
            }

            if (dp[i][prev + 1] != -1) {
                return dp[i][prev + 1];
            }

            int skip = solve(pairs, i + 1, prev, dp);

            int take = 0;

            if (prev == -1 || pairs[i][0] > pairs[prev][1]) {
                take = 1 + solve(pairs, i + 1, i, dp);
            }

            return dp[i][prev + 1] = Math.max(take, skip);
        }
    }

### Complexity

- **Time:** O(n²)
- **Space:** O(n²) for DP + O(n) recursion stack

---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

Define:

    dp[i] = maximum chain length ending at pair i

Initialize every value to `1`, because every individual pair forms a chain of length one.

For each pair `i`, check every earlier pair `j`.

If:

    pairs[j][1] < pairs[i][0]

then pair `i` can follow pair `j`.

Update:

    dp[i] = max(dp[i], dp[j] + 1)

The answer is the maximum value in `dp`.

**Important:** This implementation sorts pairs by their starting value so that earlier candidates are considered first.

### Code

    import java.util.Arrays;

    class Solution {
        public int findLongestChain(int[][] pairs) {
            Arrays.sort(pairs, (a, b) -> Integer.compare(a[0], b[0]));

            int n = pairs.length;
            int[] dp = new int[n];
            Arrays.fill(dp, 1);

            int ans = 0;

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < i; j++) {
                    if (pairs[j][1] < pairs[i][0]) {
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
- **Space:** O(n) auxiliary space, excluding sorting overhead

---

## Approach 4: Greedy (Optimal)

### Approach

Sort the pairs by their **ending value** in ascending order.

Then:

1. Select the pair that ends earliest.
2. For each next pair, select it if its start is greater than the end of the previously selected pair.
3. Update the previous end whenever a pair is selected.
4. Count the selected pairs.

Choosing the earliest-ending compatible pair leaves the most room for future pairs.

### Code

    import java.util.Arrays;

    class Solution {
        public int findLongestChain(int[][] pairs) {
            Arrays.sort(pairs, (a, b) -> Integer.compare(a[1], b[1]));

            int count = 0;
            int lastEnd = Integer.MIN_VALUE;

            for (int[] pair : pairs) {
                if (pair[0] > lastEnd) {
                    count++;
                    lastEnd = pair[1];
                }
            }

            return count;
        }
    }

### Complexity

- **Time:** O(n log n) — sorting
- **Space:** O(1) auxiliary space, excluding sorting overhead

---

## Complexity Comparison

| Approach | Time | Auxiliary Space |
|---|---|---|
| Recursion | O(2ⁿ) | O(n) |
| Memoization | O(n²) | O(n²) |
| Tabulation | O(n²) | O(n) |
| Greedy | O(n log n) | O(1) auxiliary |

---

## Key Takeaway

Maximum Length of Pair Chain is closely related to **Longest Increasing Subsequence (LIS)**.

- **Recursion:** Take or skip each pair.
- **Memoization:** Cache results using the current index and previous selected index.
- **Tabulation:** Find the longest chain ending at each pair.
- **Greedy:** Sort by ending value and select the earliest-ending compatible pair.

The greedy approach achieves **O(n log n)** time and is optimal for this problem.
