# 1004. Max Consecutive Ones III

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxLength = 0`.
2. For every starting index `i`:
   - Initialize `zeroCount = 0`.
   - Traverse the array from `i` using another loop.
   - If the current element is `0`, increment `zeroCount`.
   - If `zeroCount` becomes greater than `k`, stop extending the current subarray.
   - Otherwise, update the maximum length.
3. Return the maximum length.

### Code

```java
class Solution {
    public int longestOnes(int[] nums, int k) {

        int n = nums.length;
        int max = 0;

        for (int i = 0; i < n; i++) {

            int zeroCnt = 0;

            for (int j = i; j < n; j++) {

                if (nums[j] == 0) {
                    zeroCnt++;
                }

                if (zeroCnt > k) {
                    break;
                }

                max = Math.max(max, j - i + 1);
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

## Solution Approach 2: Better (Sliding Window)

### Algorithm

1. Initialize:
   - `left = 0`
   - `zeroCount = 0`
   - `maxLength = 0`
2. Traverse the array using the `right` pointer.
3. If `nums[right]` is `0`, increment `zeroCount`.
4. While `zeroCount > k`:
   - If `nums[left]` is `0`, decrement `zeroCount`.
   - Move `left` forward.
5. Update the maximum window length.
6. Return the maximum length.

### Code

```java
class Solution {
    public int longestOnes(int[] nums, int k) {

        int n = nums.length;

        int left = 0;
        int zeroCnt = 0;
        int max = 0;

        for (int right = 0; right < n; right++) {

            if (nums[right] == 0) {
                zeroCnt++;
            }

            while (zeroCnt > k) {

                if (nums[left] == 0) {
                    zeroCnt--;
                }

                left++;
            }

            max = Math.max(max, right - left + 1);
        }

        return max;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 3: Optimal (Optimized Sliding Window)

### Algorithm

1. Initialize:
   - `left = 0`
   - `zeroCount = 0`
   - `maxLength = 0`
2. Traverse the array using the `right` pointer.
3. If `nums[right]` is `0`, increment `zeroCount`.
4. If `zeroCount > k`:
   - If `nums[left]` is `0`, decrement `zeroCount`.
   - Move `left` forward by one position.
5. Update the maximum window length.
6. Return the maximum length.

### Code

```java
class Solution {
    public int longestOnes(int[] nums, int k) {

        int n = nums.length;

        int left = 0;
        int zeroCnt = 0;
        int max = 0;

        for (int right = 0; right < n; right++) {

            if (nums[right] == 0) {
                zeroCnt++;
            }

            if (zeroCnt > k) {

                if (nums[left] == 0) {
                    zeroCnt--;
                }

                left++;
            }

            max = Math.max(max, right - left + 1);
        }

        return max;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
