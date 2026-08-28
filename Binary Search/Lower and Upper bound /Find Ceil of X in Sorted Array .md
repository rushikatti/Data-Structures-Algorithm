# Find Ceil of X in Sorted Array

## Problem

Given a **sorted array `arr[]`** and an integer `x`, find the index (0-based) of the **smallest element ≥ x** (ceil of `x`).  
If no such element exists, return `-1`.

---

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Traverse array from index `0` to `n-1`.
2. For each element:
   - If `arr[i] >= x` → return `i`
3. If no such element found → return `-1`

---

### Code

    class Solution {
        public int ceilIndex(int[] arr, int x) {

            for (int i = 0; i < arr.length; i++) {
                if (arr[i] >= x) {
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

## Solution Approach 2: Optimal (Binary Search – Lower Bound)

### Algorithm

1. Initialize:
   - `left = 0`
   - `right = n - 1`
   - `ans = -1`
2. While `left <= right`:
   - Compute `mid = left + (right - left) / 2`
3. If `arr[mid] >= x`:
   - This is a possible answer
   - Store `ans = mid`
   - Move left → `right = mid - 1`
4. Else:
   - Move right → `left = mid + 1`
5. Return `ans`

---

### Code

    class Solution {
        public int ceilIndex(int[] arr, int x) {

            int left = 0, right = arr.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] >= x) {
                    ans = mid;
                    right = mid - 1;
                } else {
                    left = mid + 1;
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

## 🔥 Alternative (Classic Lower Bound Style)

### Algorithm

1. Use `left = 0`, `right = n`
2. While `left < right`:
   - If `arr[mid] >= x` → move left (`right = mid`)
   - Else → move right (`left = mid + 1`)
3. After loop:
   - If `left == n` → return `-1`
   - Else return `left`

---

### Code

    class Solution {
        public int ceilIndex(int[] arr, int x) {

            int left = 0, right = arr.length;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] >= x) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }

            return (left == arr.length) ? -1 : left;
        }
    }

---

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Key Insight

- Ceil = **first element ≥ x**
- This is exactly **Lower Bound**

---

## Example

    arr = [1, 2, 4, 6, 8]
    x = 5

    Ceil = 6 → index = 3

---
