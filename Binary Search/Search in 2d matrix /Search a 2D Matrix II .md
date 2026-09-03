# 240. Search a 2D Matrix II

## Problem

Given an `m x n` matrix with the following properties:

- Integers in each row are sorted in ascending order (left → right)
- Integers in each column are sorted in ascending order (top → bottom)

Return `true` if `target` exists in the matrix, else return `false`.

---

## Solution Approach 1: Brute Force (Linear Search)

### Algorithm

1. Traverse every element in the matrix
2. Compare each element with target
3. If found → return `true`
4. If not found after full traversal → return `false`

---

### Code

    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {

            int m = matrix.length;
            int n = matrix[0].length;

            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    if (matrix[i][j] == target) {
                        return true;
                    }
                }
            }

            return false;
        }
    }

---

### Complexity

- **Time:** `O(m * n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Better (Row-wise Binary Search)

### Algorithm

1. For each row:
   - If `target` lies between first and last element of row
   - Apply binary search on that row
2. If found → return `true`

---

### Code

    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {

            int m = matrix.length;
            int n = matrix[0].length;

            for (int i = 0; i < m; i++) {

                if (target >= matrix[i][0] && target <= matrix[i][n - 1]) {

                    int left = 0, right = n - 1;

                    while (left <= right) {

                        int mid = left + (right - left) / 2;

                        if (matrix[i][mid] == target) return true;
                        else if (matrix[i][mid] < target) left = mid + 1;
                        else right = mid - 1;
                    }
                }
            }

            return false;
        }
    }

---

### Complexity

- **Time:** `O(m * log n)`
- **Space:** `O(1)`

---

## Solution Approach 3: Optimal (Staircase Search)

### Algorithm

1. Start from **top-right corner**:
   - `row = 0`
   - `col = n - 1`

2. While within bounds:
   - If current == target → return `true`
   - If current > target → move left (`col--`)
   - If current < target → move down (`row++`)

3. If traversal ends → return `false`

---

### Code

    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {

            int m = matrix.length;
            int n = matrix[0].length;

            int row = 0;
            int col = n - 1;

            while (row < m && col >= 0) {

                if (matrix[row][col] == target) {
                    return true;
                }
                else if (matrix[row][col] > target) {
                    col--;   // move left
                }
                else {
                    row++;   // move down
                }
            }

            return false;
        }
    }

---

### Complexity

- **Time:** `O(m + n)`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Each move eliminates one row or one column
- Start from a corner where decisions are deterministic

---

## Example

    matrix = [
      [1,  4,  7, 11, 15],
      [2,  5,  8, 12, 19],
      [3,  6,  9, 16, 22],
      [10,13, 14,17, 24],
      [18,21, 23,26, 30]
    ]

    target = 5

    Output → true

---

## 🧠 Pattern Recognition

| Matrix Type | Approach |
|------------|--------|
| Fully sorted | Binary Search |
| Row + Column sorted | Staircase Search |

---
