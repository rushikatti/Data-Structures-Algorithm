# 152. Maximum Product Subarray

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `max` with a very small value.
2. Traverse every possible starting index `i`.
3. Initialize `product = 1`.
4. Extend the subarray using another loop.
5. Multiply the current element into `product`.
6. Update `max` with the maximum product found.
7. Return the maximum product.

### Code

```java
class Solution {
    public int maxProduct(int[] nums) {

        int n = nums.length;
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++) {

            int prod = 1;

            for (int j = i; j < n; j++) {

                prod *= nums[j];
                max = Math.max(max, prod);
            }
        }

        return max;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Prefix + Suffix Scan)

### Algorithm

1. Initialize:
   - `prefix = 1`
   - `suffix = 1`
   - `max = Integer.MIN_VALUE`
2. Traverse the array:
   - Multiply `prefix` from left → right.
   - Multiply `suffix` from right → left.
3. If `prefix` becomes `0`, reset it to `1`.
4. If `suffix` becomes `0`, reset it to `1`.
5. Update `max` with the maximum of `prefix` and `suffix`.
6. Return the maximum product.

### Code

```java
class Solution {
    public int maxProduct(int[] nums) {

        int n = nums.length;
        int max = Integer.MIN_VALUE;

        int prefix = 1;
        int suffix = 1;

        for (int i = 0; i < n; i++) {

            if (prefix == 0) prefix = 1;
            if (suffix == 0) suffix = 1;

            prefix *= nums[i];
            suffix *= nums[n - 1 - i];

            max = Math.max(max, Math.max(prefix, suffix));
        }

        return max;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
