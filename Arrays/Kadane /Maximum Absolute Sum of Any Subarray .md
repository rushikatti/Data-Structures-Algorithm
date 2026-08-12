# 1749. Maximum Absolute Sum of Any Subarray

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxAbs = 0`.
2. Traverse every possible starting index `i`.
3. Initialize `sum = 0`.
4. Extend the subarray using another loop.
5. Add the current element to `sum`.
6. Update `maxAbs = max(maxAbs, abs(sum))`.
7. Return the maximum absolute sum.

### Code

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {

        int n = nums.length;
        int maxAbs = 0;

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += nums[j];
                maxAbs = Math.max(maxAbs, Math.abs(sum));
            }
        }

        return maxAbs;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Kadane for Max & Min)

### Algorithm

1. We need both:
   - Maximum subarray sum
   - Minimum subarray sum
2. Initialize:
   - `curMax = 0`, `maxSum = 0`
   - `curMin = 0`, `minSum = 0`
3. Traverse the array:
   - Update `curMax = max(num, curMax + num)`
   - Update `maxSum = max(maxSum, curMax)`
   - Update `curMin = min(num, curMin + num)`
   - Update `minSum = min(minSum, curMin)`
4. Answer = `max(abs(maxSum), abs(minSum))`
5. Return the result.

### Code

```java
class Solution {
    public int maxAbsoluteSum(int[] nums) {

        int curMax = 0, maxSum = 0;
        int curMin = 0, minSum = 0;

        for (int num : nums) {

            curMax = Math.max(num, curMax + num);
            maxSum = Math.max(maxSum, curMax);

            curMin = Math.min(num, curMin + num);
            minSum = Math.min(minSum, curMin);
        }

        return Math.max(Math.abs(maxSum), Math.abs(minSum));
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
