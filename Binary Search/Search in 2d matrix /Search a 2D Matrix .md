# 74. Search a 2D Matrix

## Solution Approach 1: Brute Force (Linear Search)

### Algorithm

1. Traverse each row of the matrix.
2. For every row, traverse each column element.
3. Compare each element with the target.
4. If found, return `true`.
5. If traversal completes without finding target, return `false`.

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

1. Traverse each row.
2. For each row:
   - If target lies within the row range:
     - Apply binary search on that row.
3. If found, return `true`.

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

                        if (matrix[i][mid] == target) {
                            return true;
                        }
                        else if (matrix[i][mid] < target) {
                            left = mid + 1;
                        }
                        else {
                            right = mid - 1;
                        }
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



## Solution Approach: Optimal (Two Binary Searches)

### Algorithm

1. Let:
   - `m = number of rows`
   - `n = number of columns`

2. **Step 1: Find the correct row**
   - Apply binary search on rows:
   - For each `mid` row:
     - If `target >= matrix[mid][0] && target <= matrix[mid][n-1]`
       → Target must be in this row → store row index
     - If `target < matrix[mid][0]`
       → Move up → `high = mid - 1`
     - Else
       → Move down → `low = mid + 1`

3. If no row found → return `false`

4. **Step 2: Binary search inside the row**
   - Apply standard binary search on that row

5. If found → return `true`, else → `false`

---

### Code

    class Solution {
        public boolean searchMatrix(int[][] matrix, int target) {
            
            int m = matrix.length;
            int n = matrix[0].length;

            int low = 0, high = m - 1;
            int row = -1;

            // Step 1: Find correct row
            while (low <= high) {
                int mid = low + (high - low) / 2;

                if (target >= matrix[mid][0] && target <= matrix[mid][n - 1]) {
                    row = mid;
                    break;
                }

                if (target < matrix[mid][0]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            if (row == -1) return false;

            // Step 2: Binary search in row
            int left = 0, right = n - 1;

            while (left <= right) {
                int mid = left + (right - left) / 2;

                if (matrix[row][mid] == target) {
                    return true;
                }
                else if (matrix[row][mid] < target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return false;
        }
    }

---

### Complexity

- **Time:** `O(log m + log n)`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Each row is sorted AND rows are disjoint
- First binary search narrows to one row
- Second binary search finds the element

---

## Example

    matrix = [
      [1, 3, 5, 7],
      [10, 11, 16, 20],
      [23, 30, 34, 60]
    ]

    target = 3

    Output → true

---
- Enables **binary search optimization**

---
