# 153. Find Minimum in Rotated Sorted Array

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Initialize `min = nums[0]`.
2. Traverse the array from index `1` to `n-1`.
3. Update `min = min(min, nums[i])`.
4. Return `min`.

### Code

    class Solution {
        public int findMin(int[] nums) {

            int min = nums[0];

            for (int i = 1; i < nums.length; i++) {
                if (nums[i] < min) {
                    min = nums[i];
                }
            }

            return min;
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
3. Compare `nums[mid]` with `nums[right]`:
   - If `nums[mid] > nums[right]`:
     - Minimum lies in right half → `left = mid + 1`
   - Else:
     - Minimum lies in left half (including mid) → `right = mid`
4. When loop ends:
   - `left == right` → index of minimum
5. Return `nums[left]`.

### Code

    class Solution {
        public int findMin(int[] nums) {

            int left = 0, right = nums.length - 1;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] > nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            return nums[left];
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Solution Approach 3: Binary Search (With Early Exit Optimization)

### Algorithm

1. If array is already sorted:
   - `nums[left] < nums[right]` → return `nums[left]`
2. Otherwise:
   - Perform binary search similar to above
3. Check mid:
   - If `nums[mid] > nums[mid+1]` → answer is `nums[mid+1]`
   - If `nums[mid] < nums[mid-1]` → answer is `nums[mid]`
4. Adjust search range accordingly.

### Code

    class Solution {
        public int findMin(int[] nums) {

            int left = 0, right = nums.length - 1;

            if (nums[left] <= nums[right]) {
                return nums[left];
            }

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (mid < right && nums[mid] > nums[mid + 1]) {
                    return nums[mid + 1];
                }

                if (mid > left && nums[mid] < nums[mid - 1]) {
                    return nums[mid];
                }

                if (nums[mid] >= nums[left]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }

            return -1;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---
