# 918. Maximum Sum Circular Subarray

## Solution Approach 1: Brute Force

### Algorithm

1. Consider every possible subarray in circular manner.
2. Duplicate the array (conceptually) to handle circular cases.
3. For each starting index `i`, compute subarray sums up to length `n`.
4. Track the maximum sum encountered.
5. Return the maximum sum.

### Code

```java
class Solution {
    public int maxSubarraySumCircular(int[] nums) {

        int n = nums.length;
        int maxSum = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = 0; j < n; j++) {

                sum += nums[(i + j) % n];
                maxSum = Math.max(maxSum, sum);
            }
        }

        return maxSum;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Better (Kadane Twice)

### Algorithm

1. Find **normal max subarray sum** using Kadane.
2. Find **minimum subarray sum** using modified Kadane.
3. Compute total sum of array.
4. Circular max = `totalSum - minSubarraySum`.
5. Edge case:
   - If all numbers are negative → return normal max.
6. Return maximum of:
   - normal max
   - circular max

### Code

```java
class Solution {
    public int maxSubarraySumCircular(int[] nums) {

        int totalSum = 0;

        int maxSum = nums[0];
        int curMax = 0;

        int minSum = nums[0];
        int curMin = 0;

        for (int num : nums) {

            curMax = Math.max(num, curMax + num);
            maxSum = Math.max(maxSum, curMax);

            curMin = Math.min(num, curMin + num);
            minSum = Math.min(minSum, curMin);

            totalSum += num;
        }

        // all elements negative
        if (maxSum < 0) {
            return maxSum;
        }

        return Math.max(maxSum, totalSum - minSum);
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
