# Find K Rotations (Number of Times Sorted Array is Rotated)

## Problem

Given an **increasing sorted array rotated k times**, find the value of `k`.

👉 `k` = index of the **minimum element**

---

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Initialize:
   - `min = arr[0]`
   - `index = 0`
2. Traverse array from `1` to `n-1`
3. If `arr[i] < min`:
   - Update `min = arr[i]`
   - Update `index = i`
4. Return `index`

---

### Code

    class Solution {
        public int findKRotation(int[] arr) {

            int min = arr[0];
            int index = 0;

            for (int i = 1; i < arr.length; i++) {

                if (arr[i] < min) {
                    min = arr[i];
                    index = i;
                }
            }

            return index;
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
3. Compare `arr[mid]` with `arr[right]`:
   - If `arr[mid] > arr[right]`:
     - Minimum lies in right half → `left = mid + 1`
   - Else:
     - Minimum lies in left half → `right = mid`
4. Loop ends when `left == right`
5. Return `left` → rotation count

---

### Code

    class Solution {
        public int findKRotation(int[] arr) {

            int left = 0, right = arr.length - 1;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] > arr[right]) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            return left;
        }
    }

---

### Complexity

- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## Key Insight

- Rotation shifts the **smallest element** from index `0` to index `k`
- So:
  
    k = index of minimum element

---

## Example

    arr = [4, 5, 6, 7, 0, 1, 2]

    Minimum element = 0
    Index = 4

    → k = 4

---
