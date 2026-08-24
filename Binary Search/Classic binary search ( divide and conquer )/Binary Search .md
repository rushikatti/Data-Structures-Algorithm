```md id="bs704"
# 704. Binary Search

## Solution Approach 1: Recursive Binary Search

### Algorithm

1. Define a recursive function with parameters:
   - `left (l)`
   - `right (r)`
2. Base case:
   - If `l > r`, return `-1`
3. Compute mid:
   - `mid = l + (r - l) / 2`
4. If `nums[mid] == target` → return `mid`
5. If `nums[mid] < target`:
   - Search in right half → `(mid + 1, r)`
6. Else:
   - Search in left half → `(l, mid - 1)`
7. Return result.

### Code

    class Solution {
        public int search(int[] nums, int target) {

            return binary(nums, 0, nums.length - 1, target);
        }

        private int binary(int[] nums, int l, int r, int target) {

            if (l > r) {
                return -1;
            }

            int mid = l + (r - l) / 2;

            if (nums[mid] == target) {
                return mid;
            }
            else if (nums[mid] < target) {
                return binary(nums, mid + 1, r, target);
            }
            else {
                return binary(nums, l, mid - 1, target);
            }
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(log n)` (recursion stack)

---

## Solution Approach 2: Iterative Binary Search (Optimal)

### Algorithm

1. Initialize:
   - `l = 0`
   - `r = n - 1`
2. While `l <= r`:
   - Compute `mid = l + (r - l) / 2`
3. If `nums[mid] == target` → return `mid`
4. If `nums[mid] < target`:
   - Move left pointer → `l = mid + 1`
5. Else:
   - Move right pointer → `r = mid - 1`
6. If not found → return `-1`

### Code

    class Solution {
        public int search(int[] nums, int target) {

            int l = 0, r = nums.length - 1;

            while (l <= r) {

                int mid = l + (r - l) / 2;

                if (nums[mid] == target) {
                    return mid;
                }
                else if (nums[mid] < target) {
                    l = mid + 1;
                }
                else {
                    r = mid - 1;
                }
            }

            return -1;
        }
    }

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---
```
