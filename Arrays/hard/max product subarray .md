# 152. Maximum Product Subarray

## Brute Force Solution

### Approach

- Consider every possible subarray.
- For each starting index, continuously multiply elements until the end of the array.
- Keep track of the maximum product encountered.

### Code

```java
class Solution {
    public int maxProduct(int[] nums) {

        int maxProduct = nums[0];

        for (int i = 0; i < nums.length; i++) {

            int prod = 1;

            for (int j = i; j < nums.length; j++) {

                prod *= nums[j];
                maxProduct = Math.max(maxProduct, prod);
            }
        }

        return maxProduct;
    }
}
```

### Complexity

- **Time:** O(n²)
- **Space:** O(1)

---

## Better Solution (Prefix & Suffix Product)

### Approach

- Traverse the array from both the left and the right simultaneously.
- Maintain:
  - `pre` = Prefix product.
  - `suf` = Suffix product.
- If either product becomes `0`, reset it to `1`.
- At every step, update the maximum product using both prefix and suffix products.
- This works because the maximum product subarray may exclude either the prefix or suffix around a negative number.

### Code

```java
class Solution {
    public int maxProduct(int[] nums) {

        int pre = 1;
        int suf = 1;

        int ans = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {

            if (pre == 0)
                pre = 1;

            if (suf == 0)
                suf = 1;

            pre *= nums[i];
            suf *= nums[nums.length - i - 1];

            ans = Math.max(ans, Math.max(pre, suf));
        }

        return ans;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Optimal Solution (Kadane's Variant)

### Approach

- Maintain two variables:
  - `maxProduct` = Maximum product ending at the current index.
  - `minProduct` = Minimum product ending at the current index.
- The minimum product is needed because multiplying a negative number by another negative number can produce the maximum product.
- If the current element is negative, swap `maxProduct` and `minProduct`.
- Update both products and keep track of the overall maximum.

### Code

```java
class Solution {
    public int maxProduct(int[] nums) {

        int maxProduct = nums[0];
        int minProduct = nums[0];
        int ans = nums[0];

        for (int i = 1; i < nums.length; i++) {

            int curr = nums[i];

            if (curr < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(curr, maxProduct * curr);
            minProduct = Math.min(curr, minProduct * curr);

            ans = Math.max(ans, maxProduct);
        }

        return ans;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)
