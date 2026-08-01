# 977. Squares of a Sorted Array

## Solution Approach 1: Brute Force

### Algorithm

1. Traverse the array and replace each element with its square.
2. Sort the modified array.
3. Return the sorted array.

### Code

```java
class Solution {
    public int[] sortedSquares(int[] nums) {

        for (int i = 0; i < nums.length; i++) {
            nums[i] = nums[i] * nums[i];
        }

        Arrays.sort(nums);

        return nums;
    }
}
```

### Complexity

- **Time:** `O(n log n)`
- **Space:** `O(1)` (excluding the sorting algorithm's internal space)

---

## Solution Approach 2: Optimal (Two Pointers)

### Algorithm

1. Create an answer array of the same size.
2. Initialize:
   - `left = 0`
   - `right = n - 1`
   - `index = n - 1`
3. While `left <= right`:
   - Compare the absolute values of `nums[left]` and `nums[right]`.
   - Place the larger square at `ans[index]`.
   - Move the corresponding pointer.
   - Decrement `index`.
4. Return the answer array.

### Code

```java
class Solution {
    public int[] sortedSquares(int[] nums) {

        int n = nums.length;

        int[] ans = new int[n];

        int left = 0;
        int right = n - 1;
        int index = n - 1;

        while (left <= right) {

            if (Math.abs(nums[left]) > Math.abs(nums[right])) {

                ans[index] = nums[left] * nums[left];
                left++;
            }
            else {

                ans[index] = nums[right] * nums[right];
                right--;
            }

            index--;
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`
