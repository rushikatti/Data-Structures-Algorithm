# 167. Two Sum II - Input Array Is Sorted

## Solution Approach 1: Brute Force

### Algorithm

1. Traverse the array using the first loop (`i`).
2. For every element, traverse the remaining elements using the second loop (`j`).
3. Compute the sum of `numbers[i]` and `numbers[j]`.
4. If the sum equals the target, return their **1-based indices**.
5. If no pair is found, return `{-1, -1}`.

### Code

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length;

        for (int i = 0; i < n - 1; i++) {

            for (int j = i + 1; j < n; j++) {

                int sum = numbers[i] + numbers[j];

                if (sum == target) {
                    return new int[]{i + 1, j + 1};
                }
            }
        }

        return new int[]{-1, -1};
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---


## Solution Approach 3: Optimal (Two Pointers)

### Algorithm

1. Initialize two pointers:
   - `left = 0`
   - `right = n - 1`
2. Calculate the sum of the elements at the two pointers.
3. If the sum equals the target, return their **1-based indices**.
4. If the sum is greater than the target, move the `right` pointer left.
5. If the sum is smaller than the target, move the `left` pointer right.
6. Continue until the pair is found.

### Code

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {

        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {

            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                return new int[]{left + 1, right + 1};
            }
            else if (sum > target) {
                right--;
            }
            else {
                left++;
            }
        }

        return new int[]{-1, -1};
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
