# Largest Sum Contiguous Subarray

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxSum` with the first element.
2. Traverse every possible starting index `i`.
3. Initialize `sum = 0`.
4. Extend the subarray using another loop.
5. Add the current element to `sum`.
6. Update `maxSum` with the maximum of current sum and previous `maxSum`.
7. Return the maximum subarray sum.

### Code

```java
class Solution {
    public int maxSubArray(int[] nums) {

        int n = nums.length;
        int maxSum = nums[0];

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += nums[j];
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

## Solution Approach 2: Optimal (Kadane’s Algorithm)

### Algorithm

1. Initialize:
   - `maxSum = nums[0]`
   - `curSum = 0`
2. Traverse the array:
   - Add current element to `curSum`.
   - Update `maxSum`.
   - If `curSum < 0`, reset it to `0`.
3. Return `maxSum`.

### Code

```java
class Solution {
    public int maxSubArray(int[] nums) {

        int maxSum = nums[0];
        int curSum = 0;

        for (int num : nums) {

            curSum += num;
            maxSum = Math.max(maxSum, curSum);

            if (curSum < 0) {
                curSum = 0;
            }
        }

        return maxSum;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
