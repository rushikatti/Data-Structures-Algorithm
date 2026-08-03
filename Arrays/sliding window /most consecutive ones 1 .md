# 485. Max Consecutive Ones

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxOnes = 0`.
2. For every index `i`:
   - Start counting consecutive `1`s from index `i`.
   - Stop when a `0` is encountered.
   - Update `maxOnes`.
3. Return the maximum count.

### Code

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int n = nums.length;
        int maxOnes = 0;

        for (int i = 0; i < n; i++) {

            int count = 0;

            for (int j = i; j < n; j++) {

                if (nums[j] == 1) {
                    count++;
                } else {
                    break;
                }
            }

            maxOnes = Math.max(maxOnes, count);
        }

        return maxOnes;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Single Traversal)

### Algorithm

1. Initialize:
   - `count = 0`
   - `maxOnes = 0`
2. Traverse the array:
   - If the current element is `1`, increment `count` and update `maxOnes`.
   - If the current element is `0`, reset `count` to `0`.
3. Return `maxOnes`.

### Code

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int count = 0;
        int maxOnes = 0;

        for (int num : nums) {

            if (num == 1) {
                count++;
                maxOnes = Math.max(maxOnes, count);
            } else {
                count = 0;
            }
        }

        return maxOnes;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
