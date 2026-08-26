# 162. Find Peak Element

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Traverse the array from index `0` to `n-1`.
2. For each index `i`, check:
   - Left neighbor → `i == 0` OR `nums[i] > nums[i-1]`
   - Right neighbor → `i == n-1` OR `nums[i] > nums[i+1]`
3. If both conditions are satisfied → `nums[i]` is a peak.
4. Return index `i`.

### Code

    class Solution {
        public int findPeakElement(int[] nums) {

            int n = nums.length;

            for (int i = 0; i < n; i++) {

                boolean leftOk = (i == 0) || nums[i] > nums[i - 1];
                boolean rightOk = (i == n - 1) || nums[i] > nums[i + 1];

                if (leftOk && rightOk) {
                    return i;
                }
            }

            return -1;
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search)

### Algorithm

1. Initialize:
   - `left = 0`
   - `right = n - 1`
2. While `left < right`:
   - Compute `mid = left + (right - left) / 2`
3. Compare `nums[mid]` with `nums[mid + 1]`:
   - If `nums[mid] > nums[mid + 1]`:
     - You are in descending slope → peak is on left side (including mid)
     - `right = mid`
   - Else:
     - You are in ascending slope → peak is on right side
     - `left = mid + 1`
4. When loop ends:
   - `left == right` → index of peak
5. Return `left`.

### Code

    class Solution {
        public int findPeakElement(int[] nums) {

            int left = 0, right = nums.length - 1;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] > nums[mid + 1]) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }

            return left;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Key Insight

- A peak element is **greater than its neighbors**
- Array behaves like a combination of increasing/decreasing slopes
- Binary search works because:
  - If you are going up → peak is ahead
  - If you are going down → peak is behind

---
