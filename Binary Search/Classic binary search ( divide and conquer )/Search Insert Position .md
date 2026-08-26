# 35. Search Insert Position

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Traverse the array from index `0` to `n-1`.
2. For each index `i`:
   - If `nums[i] == target` → return `i`
   - If `nums[i] > target` → return `i` (insert position)
3. If target is greater than all elements → return `n`.

### Code

    class Solution {
        public int searchInsert(int[] nums, int target) {

            for (int i = 0; i < nums.length; i++) {

                if (nums[i] >= target) {
                    return i;
                }
            }

            return nums.length;
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
2. While `left <= right`:
   - Compute `mid = left + (right - left) / 2`
3. If `nums[mid] == target` → return `mid`
4. If `nums[mid] < target`:
   - Move left → `left = mid + 1`
5. Else:
   - Move right → `right = mid - 1`
6. When loop ends:
   - `left` is the correct insert position
7. Return `left`.

### Code

    class Solution {
        public int searchInsert(int[] nums, int target) {

            int left = 0, right = nums.length - 1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] == target) {
                    return mid;
                }
                else if (nums[mid] < target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return left;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---
