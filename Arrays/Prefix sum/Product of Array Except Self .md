# 238. Product of Array Except Self

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize an output array `ans` of size `n`.
2. For each index `i`:
   - Initialize `product = 1`.
   - Traverse the entire array.
   - Multiply all elements except `nums[i]`.
3. Store the result in `ans[i]`.
4. Return the result array.

### Code

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {

        int n = nums.length;
        int[] ans = new int[n];

        for (int i = 0; i < n; i++) {

            int prod = 1;

            for (int j = 0; j < n; j++) {

                if (j == i) continue;

                prod *= nums[j];
            }

            ans[i] = prod;
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)` *(excluding output array)*

---

## Solution Approach 2: Optimal (Prefix + Suffix Product)

### Algorithm

1. Create an output array `ans`.
2. First pass (Left → Right):
   - Store prefix product at each index.
   - `ans[i] = product of all elements to the left of i`.
3. Second pass (Right → Left):
   - Maintain a variable `rightProduct`.
   - Multiply `ans[i]` with the product of elements to the right.
4. Return the result.

### Code

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {

        int n = nums.length;
        int[] ans = new int[n];

        ans[0] = 1;

        // Prefix product
        for (int i = 1; i < n; i++) {
            ans[i] = ans[i - 1] * nums[i - 1];
        }

        int rightProduct = 1;

        // Suffix product
        for (int i = n - 1; i >= 0; i--) {
            ans[i] = ans[i] * rightProduct;
            rightProduct *= nums[i];
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)` *(excluding output array)*
