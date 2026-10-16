# 1048. Longest String Chain

## Problem

Given an array of strings `words`, return the length of the longest possible string chain.

A word `prev` is a predecessor of `curr` if we can insert exactly one character anywhere in `prev` to make `curr`.

Example:

    Input: words = ["a","b","ba","bca","bda","bdca"]
    Output: 4

    Explanation:
    One longest chain is:
    "a" -> "ba" -> "bda" -> "bdca"

---

## Approach 1: Recursion (Brute Force)

### Approach

Sort the words by length in ascending order so that every possible predecessor appears before its longer word.

At each word, we have two choices:

- **Take:** Include the word if it is a valid successor of the previously selected word.
- **Skip:** Ignore the word.

Maintain `prev`, the index of the previously selected word. Initially, `prev = -1`.

Two words form a valid predecessor-successor pair if their lengths differ by exactly one and deleting one character from the longer word produces the shorter word.

### Code

    import java.util.Arrays;

    class Solution {
        public int longestStrChain(String[] words) {
            Arrays.sort(words, (a, b) ->
                Integer.compare(a.length(), b.length()));

            return solve(words, 0, -1);
        }

        public int solve(String[] words, int i, int prev) {
            if (i == words.length) {
                return 0;
            }

            int skip = solve(words, i + 1, prev);

            int take = 0;

            if (prev == -1 || isPredecessor(words[prev], words[i])) {
                take = 1 + solve(words, i + 1, i);
            }

            return Math.max(take, skip);
        }

        public boolean isPredecessor(String shorter, String longer) {
            if (longer.length() != shorter.length() + 1) {
                return false;
            }

            int i = 0, j = 0;

            while (i < shorter.length() && j < longer.length()) {
                if (shorter.charAt(i) == longer.charAt(j)) {
                    i++;
                }
                j++;
            }

            return i == shorter.length();
        }
    }

### Complexity

- **Time:** O(2ⁿ × L), where `L` is the maximum word length, excluding sorting.
- **Space:** O(n) for the recursion stack.

---

## Approach 2: Recursion + Memoization (Top-Down DP)

### Approach

The recursive solution repeats the same subproblems.

The result depends on:

- `i`: Current word index.
- `prev`: Index of the previously selected word.

Use a 2D DP array to cache results:

    dp[i][prev + 1]

However, this approach requires O(n²) memory and is not the most efficient DP solution for this problem.

### Code

    import java.util.Arrays;

    class Solution {
        public int longestStrChain(String[] words) {
            Arrays.sort(words, (a, b) ->
                Integer.compare(a.length(), b.length()));

            int n = words.length;
            int[][] dp = new int[n][n + 1];

            for (int[] row : dp) {
                Arrays.fill(row, -1);
            }

            return solve(words, 0, -1, dp);
        }

        public int solve(String[] words, int i, int prev, int[][] dp) {
            if (i == words.length) {
                return 0;
            }

            if (dp[i][prev + 1] != -1) {
                return dp[i][prev + 1];
            }

            int skip = solve(words, i + 1, prev, dp);
            int take = 0;

            if (prev == -1 || isPredecessor(words[prev], words[i])) {
                take = 1 + solve(words, i + 1, i, dp);
            }

            return dp[i][prev + 1] = Math.max(take, skip);
        }

        public boolean isPredecessor(String shorter, String longer) {
            if (longer.length() != shorter.length() + 1) {
                return false;
            }

            int i = 0, j = 0;

            while (i < shorter.length() && j < longer.length()) {
                if (shorter.charAt(i) == longer.charAt(j)) {
                    i++;
                }
                j++;
            }

            return i == shorter.length();
        }
    }

### Complexity

Let `L` be the maximum word length.

- **Time:** O(n² × L), excluding sorting.
- **Space:** O(n²) for DP + O(n) recursion stack.

---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

This is the standard DP approach for Longest String Chain.

Sort words by length in ascending order.

Define:

    dp[i] = length of the longest string chain ending at words[i]

Initially, every word forms a chain of length `1`.

    dp[i] = 1

For each word `words[i]`, check all previous words `words[j]`.

If `words[j]` is a predecessor of `words[i]`:

    dp[i] = max(dp[i], dp[j] + 1)

Track the maximum value across the array.

### Code

    import java.util.Arrays;

    class Solution {
        public int longestStrChain(String[] words) {
            Arrays.sort(words, (a, b) ->
                Integer.compare(a.length(), b.length()));

            int n = words.length;
            int[] dp = new int[n];
            Arrays.fill(dp, 1);

            int ans = 1;

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < i; j++) {
                    if (isPredecessor(words[j], words[i])) {
                        dp[i] = Math.max(dp[i], dp[j] + 1);
                    }
                }

                ans = Math.max(ans, dp[i]);
            }

            return ans;
        }

        public boolean isPredecessor(String shorter, String longer) {
            if (longer.length() != shorter.length() + 1) {
                return false;
            }

            int i = 0, j = 0;

            while (i < shorter.length() && j < longer.length()) {
                if (shorter.charAt(i) == longer.charAt(j)) {
                    i++;
                }
                j++;
            }

            return i == shorter.length();
        }
    }

### Complexity

- **Time:** O(n² × L), excluding sorting.
- **Space:** O(n) for the DP array.

---

## Approach 4: HashMap + DP (Optimized)

### Approach

Instead of comparing each word against every previous word, generate its possible predecessors directly.

For each word:

1. Remove one character at every position.
2. Check whether the resulting string exists in the map.
3. If it exists, extend that predecessor's chain.
4. Store the longest chain ending at the current word.

For example:

    word = "bdca"

Possible predecessors:

    "dca"
    "bca"
    "bda"
    "bdc"

If `"bda"` has a chain length of `3`, then `"bdca"` can have a chain length of `4`.

### Code

    import java.util.*;

    class Solution {
        public int longestStrChain(String[] words) {
            Arrays.sort(words, (a, b) ->
                Integer.compare(a.length(), b.length()));

            Map<String, Integer> dp = new HashMap<>();
            int ans = 1;

            for (String word : words) {
                int best = 1;

                for (int i = 0; i < word.length(); i++) {
                    String prev = word.substring(0, i)
                                     + word.substring(i + 1);

                    best = Math.max(
                        best,
                        dp.getOrDefault(prev, 0) + 1
                    );
                }

                dp.put(word, best);
                ans = Math.max(ans, best);
            }

            return ans;
        }
    }

### Complexity

Let `L` be the maximum word length.

- **Time:** O(n log n + n × L²), assuming substring creation and hashing cost O(L).
- **Space:** O(n × L) for stored strings and map entries, excluding sorting overhead.

---

## Complexity Comparison

| Approach | Time (excluding sorting) | Auxiliary Space |
|---|---|---|
| Recursion | O(2ⁿ × L) | O(n) |
| Memoization | O(n² × L) | O(n²) |
| Tabulation | O(n² × L) | O(n) |
| HashMap + DP | O(n × L²) | O(n × L) |

---

## Key Takeaway

Longest String Chain is a **1D DP problem** in its standard tabulation form.

- **Recursion:** Take or skip each word.
- **Memoization:** Cache results using the current and previous word indices.
- **Tabulation:** Find the longest chain ending at each word.
- **HashMap + DP:** Generate each possible predecessor instead of checking every earlier word.

The HashMap approach is generally preferred because it avoids comparing every pair of words and efficiently builds chains from shorter words to longer words.
