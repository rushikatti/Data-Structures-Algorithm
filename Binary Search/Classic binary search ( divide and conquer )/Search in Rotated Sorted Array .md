# 33. Search in Rotated Sorted Array

## Solution Approach 1: Brute Force (Linear Search)

### Algorithm

1. Traverse the array from index `0` to `n-1`.
2. For each element:
   - If `nums[i] == target` → return `i`.
3. If target not found → return `-1`.

### Code

    class Solution {
        public int search(int[] nums, int target) {

            for (int i = 0; i < nums.length; i++) {

                if (nums[i] == target) {
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

## Solution Approach 2: Optimal (Modified Binary Search)

### Algorithm

1. Initialize:
   - `left = 0`
   - `right = n - 1`
2. While `left <= right`:
   - Compute `mid = left + (right - left) / 2`
3. If `nums[mid] == target` → return `mid`
4. Check which half is sorted:
   - If `nums[left] <= nums[mid]` → left half is sorted
   - Else → right half is sorted :contentReference[oaicite:0]{index=0}
5. If left half is sorted:
   - If `nums[left] <= target < nums[mid]` → search left
   - Else → search right
6. If right half is sorted:
   - If `nums[mid] < target <= nums[right]` → search right
   - Else → search left
7. If not found → return `-1`

👉 Key Idea: At least one half is always sorted, even after rotation :contentReference[oaicite:1]{index=1}  

---

### Code

    class Solution {
        public int search(int[] nums, int target) {

            int left = 0, right = nums.length - 1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] == target) {
                    return mid;
                }

                // Left half is sorted
                if (nums[left] <= nums[mid]) {

                    if (nums[left] <= target && target < nums[mid]) {
                        right = mid - 1;
                    } else {
                        left = mid + 1;
                    }
                }
                // Right half is sorted
                else {

                    if (nums[mid] < target && target <= nums[right]) {
                        left = mid + 1;
                    } else {
                        right = mid - 1;
                    }
                }
            }

            return -1;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Solution Approach 3: Two-Pass (Find Pivot + Binary Search)

### Algorithm

1. First, find pivot (minimum element index).
2. Now array is split into two sorted parts.
3. Decide which half target belongs to:
   - If `target >= nums[0]` → search left part
   - Else → search right part
4. Perform normal binary search on selected half.
5. Return result.

---

### Code

    class Solution {
        public int search(int[] nums, int target) {

            int n = nums.length;

            int pivot = findPivot(nums);

            int left, right;

            if (target >= nums[0]) {
                left = 0;
                right = pivot - 1;
            } else {
                left = pivot;
                right = n - 1;
            }

            return binary(nums, left, right, target);
        }

        private int findPivot(int[] nums) {

            int l = 0, r = nums.length - 1;

            while (l < r) {

                int mid = l + (r - l) / 2;

                if (nums[mid] > nums[r]) {
                    l = mid + 1;
                } else {
                    r = mid;
                }
            }

            return l;
        }

        private int binary(int[] nums, int l, int r, int target) {

            while (l <= r) {

                int mid = l + (r - l) / 2;

                if (nums[mid] == target) return mid;

                if (nums[mid] < target) l = mid + 1;
                else r = mid - 1;
            }

            return -1;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---
