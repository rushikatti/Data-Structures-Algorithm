# 198. House Robber

## Approach 1: Recursion

### Approach

At every house, we have two choices:

- **Steal:** Rob the current house and skip the next house.
- **Skip:** Leave the current house and move to the next house.

Take the maximum of both choices.

    steal = nums[i] + solve(i + 2)
    skip  = solve(i + 1)

    solve(i) = max(steal, skip)

Base case:

    if (i >= n) return 0;

### Code

    class Solution {
        public int rob(int[] nums) {
            return solve(nums, 0, nums.length);
        }

        public int solve(int[] nums, int i, int n) {
            if (i >= n) {
                return 0;
            }

            int steal = nums[i] + solve(nums, i + 2, n);
            int skip = solve(nums, i + 1, n);

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

Use `arr[i]` to store the maximum money that can be robbed starting from house `i`.

1. If `arr[i] != -1`, return the stored result.
2. Calculate the steal and skip choices.
3. Store and return their maximum.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            int[] arr = new int[n];
            Arrays.fill(arr, -1);

            return solve(nums, arr, 0, n);
        }

        public int solve(int[] nums, int[] arr, int i, int n) {
            if (i >= n) {
                return 0;
            }

            if (arr[i] != -1) {
                return arr[i];
            }

            int steal = nums[i] + solve(nums, arr, i + 2, n);
            int skip = solve(nums, arr, i + 1, n);

            return arr[i] = Math.max(steal, skip);
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n) — DP array + recursion stack


---

## Approach 3: Tabulation (Bottom-Up DP)

### Approach

Instead of solving recursively, calculate the answer from the first house to the last.

Define:

    arr[i] = maximum money obtainable from the first i houses

Base cases:

    arr[0] = 0
    arr[1] = nums[0]

For each house:

    steal = nums[i - 1] + arr[i - 2]
    skip  = arr[i - 1]

    arr[i] = max(steal, skip)

Return `arr[n]`.

### Code

    class Solution {
        public int rob(int[] nums) {
            int n = nums.length;

            if (n == 1) {
                return nums[0];
            }

            int[] arr = new int[n + 1];

            arr[0] = 0;
            arr[1] = nums[0];

            for (int i = 2; i <= n; i++) {
                int steal = nums[i - 1] + arr[i - 2];
                int skip = arr[i - 1];

                arr[i] = Math.max(steal, skip);
            }

            return arr[n];
        }
    }

### Complexity

- **Time:** O(n)
- **Space:** O(n)


---

## Complexity Comparison

| Approach | Time | Space |
|---|---|---|
| Recursion | O(2^n) | O(n) |
| Memoization | O(n) | O(n) |
| Tabulation | O(n) | O(n) |

**Key pattern:** At each index, choose between taking the current element and skipping it. This is a classic **Dynamic Programming — Take or Skip** pattern.
