# Allocate Minimum Number of Pages

## Problem

Given an array `arr[]` where `arr[i]` represents the number of pages in the `i-th` book,  
and an integer `m` (number of students):

- Each student gets **at least one book**
- Books must be allocated in **contiguous order**
- Minimize the **maximum number of pages assigned to a student**

Return the **minimum possible maximum pages**.

If allocation is not possible → return `-1`.

---

## Solution Approach 1: Brute Force (Linear Search on Answer)

### Algorithm

1. If `m > n`, return `-1`
2. Find:
   - `low = max(arr)` → minimum possible answer
   - `high = sum(arr)` → maximum possible answer
3. Try every value from `low → high`
4. For each `maxPages`:
   - Allocate books greedily:
     - Keep adding pages until limit exceeded
     - Then assign to next student
5. Count number of students required
6. If students ≤ `m`, return current `maxPages`

---

### Code

    class Solution {
        public int findPages(int[] arr, int m) {

            int n = arr.length;
            if (m > n) return -1;

            int low = 0, high = 0;

            for (int p : arr) {
                low = Math.max(low, p);
                high += p;
            }

            for (int maxPages = low; maxPages <= high; maxPages++) {

                if (canAllocate(arr, m, maxPages)) {
                    return maxPages;
                }
            }

            return -1;
        }

        private boolean canAllocate(int[] arr, int m, int maxPages) {

            int students = 1;
            int pages = 0;

            for (int p : arr) {

                if (pages + p > maxPages) {
                    students++;
                    pages = p;
                } else {
                    pages += p;
                }
            }

            return students <= m;
        }
    }

---

### Complexity

- **Time:** `O(n * (sum - max))`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. If `m > n`, return `-1`
2. Define search space:
   - `low = max(arr)`
   - `high = sum(arr)`
3. While `low <= high`:
   - `mid = possible max pages`
4. If allocation possible with `mid`:
   - Try smaller → `high = mid - 1`
5. Else:
   - Increase → `low = mid + 1`
6. Return `low`

---

### Code

    class Solution {
        public int findPages(int[] arr, int m) {

            int n = arr.length;
            if (m > n) return -1;

            int low = 0, high = 0;

            for (int p : arr) {
                low = Math.max(low, p);
                high += p;
            }

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (canAllocate(arr, m, mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return low;
        }

        private boolean canAllocate(int[] arr, int m, int maxPages) {

            int students = 1;
            int pages = 0;

            for (int p : arr) {

                if (pages + p > maxPages) {
                    students++;
                    pages = p;
                } else {
                    pages += p;
                }
            }

            return students <= m;
        }
    }

---

### Complexity

- **Time:** `O(n log(sum))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- We minimize the **maximum load**
- Answer lies between:
  
    max(arr) ≤ answer ≤ sum(arr)

- Classic **Binary Search on Answer**

---

## Example

    arr = [12, 34, 67, 90]
    m = 2

    Output → 113

Explanation:
- Student 1 → [12, 34, 67] = 113
- Student 2 → [90]

Minimum possible maximum = 113

---
