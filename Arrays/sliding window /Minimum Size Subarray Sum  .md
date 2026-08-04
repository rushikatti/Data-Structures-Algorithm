# 209. Minimum Size Subarray Sum

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `minLength = Integer.MAX_VALUE`.
2. Traverse every possible starting index `i`.
3. Initialize `sum = 0`.
4. Extend the subarray from `i` using another loop.
5. Add the current element to `sum`.
6. If `sum >= target`:
   - Update the minimum length.
   - Stop extending the current subarray.
7. If no valid subarray is found, return `0`; otherwise, return the minimum length.

### Code

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

        int n = nums.length;
        int min = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += nums[j];

                if (sum >= target) {

                    min = Math.min(min, j - i + 1);
                    break;
                }
            }
        }

        if (min == Integer.MAX_VALUE) {
            return 0;
        }

        return min;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Sliding Window)

### Algorithm

1. Initialize:
   - `left = 0`
   - `sum = 0`
   - `minLength = Integer.MAX_VALUE`
2. Traverse the array using the `right` pointer.
3. Add `nums[right]` to the current sum.
4. While `sum >= target`:
   - Update the minimum window length.
   - Remove `nums[left]` from the sum.
   - Move `left` forward.
5. If no valid subarray exists, return `0`; otherwise, return the minimum length.

### Code

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

        int n = nums.length;

        int left = 0;
        int sum = 0;
        int min = Integer.MAX_VALUE;

        for (int right = 0; right < n; right++) {

            sum += nums[right];

            while (sum >= target) {

                min = Math.min(min, right - left + 1);

                sum -= nums[left];
                left++;
            }
        }

        if (min == Integer.MAX_VALUE) {
            return 0;
        }

        return min;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
