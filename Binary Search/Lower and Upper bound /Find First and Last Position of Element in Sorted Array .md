# 34. Find First and Last Position of Element in Sorted Array

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Initialize:
   - `first = -1`
   - `last = -1`
2. Traverse the array from `0` to `n-1`.
3. If `nums[i] == target`:
   - If `first == -1`, set `first = i`
   - Always update `last = i`
4. After traversal, return `[first, last]`.

### Code

    class Solution {
        public int[] searchRange(int[] nums, int target) {

            int first = -1, last = -1;

            for (int i = 0; i < nums.length; i++) {

                if (nums[i] == target) {

                    if (first == -1) {
                        first = i;
                    }

                    last = i;
                }
            }

            return new int[]{first, last};
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search – Lower Bound + Upper Bound)

### Algorithm

1. Find **first occurrence (lower bound)**:
   - Move left when `nums[mid] >= target`
2. Find **last occurrence (upper bound)**:
   - Move right when `nums[mid] <= target`
3. Combine both results:
   - If target not found → return `[-1, -1]`
4. Else return `[first, last]`.

---

### Code

    class Solution {
        public int[] searchRange(int[] nums, int target) {

            int first = findFirst(nums, target);
            int last = findLast(nums, target);

            return new int[]{first, last};
        }

        private int findFirst(int[] nums, int target) {

            int left = 0, right = nums.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] == target) {
                    ans = mid;
                    right = mid - 1; // move left
                }
                else if (nums[mid] < target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return ans;
        }

        private int findLast(int[] nums, int target) {

            int left = 0, right = nums.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (nums[mid] == target) {
                    ans = mid;
                    left = mid + 1; // move right
                }
                else if (nums[mid] < target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return ans;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Key Insight

- Use binary search twice:
  - First → find leftmost occurrence
  - Second → find rightmost occurrence
- This avoids scanning entire array

---
