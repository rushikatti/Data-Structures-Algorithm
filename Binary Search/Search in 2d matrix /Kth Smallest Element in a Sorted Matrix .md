# 378. Kth Smallest Element in a Sorted Matrix

## Problem

Given an `n x n` matrix where:

- Each row is sorted (left → right)
- Each column is sorted (top → bottom)

Return the **kth smallest element** in the matrix.

---

## Solution Approach 1: Brute Force (Flatten + Sort)

### Algorithm

1. Traverse the matrix and store all elements in a list
2. Sort the list
3. Return element at index `k-1`

---

### Code

    import java.util.*;

    class Solution {
        public int kthSmallest(int[][] matrix, int k) {

            List<Integer> list = new ArrayList<>();

            for (int[] row : matrix) {
                for (int val : row) {
                    list.add(val);
                }
            }

            Collections.sort(list);

            return list.get(k - 1);
        }
    }

---

### Complexity

- **Time:** `O(n^2 log n)`
- **Space:** `O(n^2)`

---



## Solution Approach 3: Optimal (Binary Search on Answer)

### Algorithm

1. Define search space:
   - `low = matrix[0][0]`
   - `high = matrix[n-1][n-1]`

2. While `low <= high`:
   - `mid = value`
   - Count elements ≤ `mid`

3. If count < k:
   - Move right → `low = mid + 1`
4. Else:
   - Move left → `high = mid - 1`

5. Return `low`

---

### Code

    class Solution {
        public int kthSmallest(int[][] matrix, int k) {

            int n = matrix.length;

            int low = matrix[0][0];
            int high = matrix[n - 1][n - 1];

            while (low <= high) {

                int mid = low + (high - low) / 2;

                int count = countLessEqual(matrix, mid);

                if (count < k) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }

            return low;
        }

        private int countLessEqual(int[][] matrix, int target) {

            int n = matrix.length;
            int row = n - 1;
            int col = 0;
            int count = 0;

            while (row >= 0 && col < n) {

                if (matrix[row][col] <= target) {
                    count += (row + 1);
                    col++;
                } else {
                    row--;
                }
            }

            return count;
        }
    }

---

### Complexity

- **Time:** `O(n log(range))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Matrix is sorted row-wise and column-wise
- Use **Binary Search on Values**, not indices
- Count elements ≤ mid efficiently using staircase pattern

---

## Example

    matrix = [
      [1, 5, 9],
      [10,11,13],
      [12,13,15]
    ]

    k = 8

    Output → 13

---
