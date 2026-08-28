# Find Floor of X in Sorted Array

## Problem

Given a **sorted array `arr[]`** and an integer `x`, find the index (0-based) of the **largest element ≤ x** (floor of `x`).  
If no such element exists, return `-1`.

---

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Initialize `ans = -1`
2. Traverse array from `0` to `n-1`
3. For each element:
   - If `arr[i] ≤ x` → update `ans = i`
4. Return `ans`

---

### Code

    class Solution {
        public int floorIndex(int[] arr, int x) {

            int ans = -1;

            for (int i = 0; i < arr.length; i++) {

                if (arr[i] <= x) {
                    ans = i;
                }
            }

            return ans;
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search – Upper Bound Logic)

### Algorithm

1. Initialize:
   - `left = 0`
   - `right = n - 1`
   - `ans = -1`
2. While `left <= right`:
   - Compute `mid = left + (right - left) / 2`
3. If `arr[mid] ≤ x`:
   - This is a valid floor candidate
   - Store `ans = mid`
   - Move right → `left = mid + 1`
4. Else:
   - Move left → `right = mid - 1`
5. Return `ans`

---

### Code

    class Solution {
        public int floorIndex(int[] arr, int x) {

            int left = 0, right = arr.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] <= x) {
                    ans = mid;
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }

            return ans;
        }
    }

---

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## 🔥 Alternative (Upper Bound Style)

### Algorithm

1. Find **first index > x** (upper bound)
2. Floor index = `upperBound - 1`
3. If `upperBound == 0` → return `-1`

---

### Code

    class Solution {
        public int floorIndex(int[] arr, int x) {

            int left = 0, right = arr.length;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] > x) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }

            int idx = left - 1;

            return (idx >= 0) ? idx : -1;
        }
    }

---

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Key Insight

- Floor = **last element ≤ x**
- Equivalent to:
  
    floor = upperBound(x) - 1

---

## Example

    arr = [1, 2, 4, 6, 8]
    x = 5

    Floor = 4 → index = 2

---
