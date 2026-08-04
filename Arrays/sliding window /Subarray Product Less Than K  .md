# 713. Subarray Product Less Than K

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `count = 0`.
2. Traverse every possible starting index `i`.
3. Initialize `product = 1`.
4. Extend the subarray from `i` using another loop.
5. Multiply the current element into the product.
6. If the product becomes greater than or equal to `k`, stop extending the current subarray.
7. Otherwise, increment the count.
8. Return the total count.

### Code

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {

        int n = nums.length;
        int count = 0;

        for (int i = 0; i < n; i++) {

            int prod = 1;

            for (int j = i; j < n; j++) {

                prod *= nums[j];

                if (prod >= k) {
                    break;
                }

                count++;
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Sliding Window)

### Algorithm

1. If `k <= 1`, return `0` because no positive product can be less than `1`.
2. Initialize:
   - `left = 0`
   - `product = 1`
   - `count = 0`
3. Traverse the array using the `right` pointer.
4. Multiply `nums[right]` into the current product.
5. While the product is greater than or equal to `k`:
   - Divide the product by `nums[left]`.
   - Move `left` forward.
6. All subarrays ending at `right` and starting between `left` and `right` are valid.
7. Add `right - left + 1` to the answer.
8. Return the total count.

### Code

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {

        if (k <= 1) {
            return 0;
        }

        int left = 0;
        int prod = 1;
        int count = 0;

        for (int right = 0; right < nums.length; right++) {

            prod *= nums[right];

            while (prod >= k) {

                prod /= nums[left];
                left++;
            }

            count += right - left + 1;
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
