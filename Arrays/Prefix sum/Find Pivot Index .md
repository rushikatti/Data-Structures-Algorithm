# 724. Find Pivot Index

## Solution Approach 1: Brute Force

### Algorithm

1. Traverse every index `i` in the array.
2. Calculate the sum of all elements to the left of `i`.
3. Calculate the sum of all elements to the right of `i`.
4. If both sums are equal, return the current index.
5. If no such index exists, return `-1`.

### Code

```java
class Solution {
    public int pivotIndex(int[] nums) {

        for (int i = 0; i < nums.length; i++) {

            int leftSum = 0;

            for (int j = 0; j < i; j++) {
                leftSum += nums[j];
            }

            int rightSum = 0;

            for (int j = i + 1; j < nums.length; j++) {
                rightSum += nums[j];
            }

            if (leftSum == rightSum) {
                return i;
            }
        }

        return -1;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Prefix Sum)

### Algorithm

1. Calculate the total sum of the array.
2. Initialize `leftSum = 0`.
3. Traverse the array:
   - Compute the right sum as:
     ```
     rightSum = totalSum - leftSum - nums[i]
     ```
   - If `leftSum == rightSum`, return the current index.
   - Otherwise, add the current element to `leftSum`.
4. If no pivot index exists, return `-1`.

### Code

```java
class Solution {
    public int pivotIndex(int[] nums) {

        int totalSum = 0;

        for (int num : nums) {
            totalSum += num;
        }

        int leftSum = 0;

        for (int i = 0; i < nums.length; i++) {

            int rightSum = totalSum - leftSum - nums[i];

            if (leftSum == rightSum) {
                return i;
            }

            leftSum += nums[i];
        }

        return -1;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
