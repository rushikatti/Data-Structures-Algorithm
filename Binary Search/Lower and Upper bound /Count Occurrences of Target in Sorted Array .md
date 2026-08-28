# Count Occurrences of Target in Sorted Array

## Problem

Given a **sorted array `arr[]`** and a number `target`, find the **number of occurrences** of `target`.

---

## Solution Approach 1: Brute Force (Linear Scan)

### Algorithm

1. Initialize `count = 0`
2. Traverse the array from `0` to `n-1`
3. If `arr[i] == target`, increment `count`
4. Return `count`

---

### Code

    class Solution {
        public int countOccurrences(int[] arr, int target) {

            int count = 0;

            for (int i = 0; i < arr.length; i++) {
                if (arr[i] == target) {
                    count++;
                }
            }

            return count;
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search – Lower & Upper Bound)

### Algorithm

1. Find **first occurrence (lower bound)**:
   - Smallest index where `arr[i] == target`
2. Find **last occurrence (upper bound)**:
   - Largest index where `arr[i] == target`
3. If target not found → return `0`
4. Else:
   
    count = last - first + 1

---

### Code

    class Solution {
        public int countOccurrences(int[] arr, int target) {

            int first = findFirst(arr, target);

            if (first == -1) return 0;

            int last = findLast(arr, target);

            return last - first + 1;
        }

        private int findFirst(int[] arr, int target) {

            int left = 0, right = arr.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] == target) {
                    ans = mid;
                    right = mid - 1;
                }
                else if (arr[mid] < target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return ans;
        }

        private int findLast(int[] arr, int target) {

            int left = 0, right = arr.length - 1;
            int ans = -1;

            while (left <= right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] == target) {
                    ans = mid;
                    left = mid + 1;
                }
                else if (arr[mid] < target) {
                    left = mid + 1;
                }
                else {
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

## 🔥 Key Insight

- Sorted array → use **binary search**
- Count = **(last index - first index + 1)**
- No need to scan entire array

---

## ⚡ Alternative (Using Lower & Upper Bound Directly)

### Idea

- `lowerBound = first index >= target`
- `upperBound = first index > target`
- Count = `upperBound - lowerBound`

---

### Code

    class Solution {
        public int countOccurrences(int[] arr, int target) {

            int lb = lowerBound(arr, target);
            int ub = upperBound(arr, target);

            if (lb == arr.length || arr[lb] != target) return 0;

            return ub - lb;
        }

        private int lowerBound(int[] arr, int target) {

            int left = 0, right = arr.length;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] >= target) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }

            return left;
        }

        private int upperBound(int[] arr, int target) {

            int left = 0, right = arr.length;

            while (left < right) {

                int mid = left + (right - left) / 2;

                if (arr[mid] > target) {
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
