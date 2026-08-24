# 69. Sqrt(x)


## Solution Approach 2: Brute Force (Linear Search)

### Algorithm

1. Start from `i = 1`.
2. While `i * i <= x`:
   - Increment `i`.
3. When condition fails, `i - 1` is the answer.
4. Return `i - 1`.

### Code

    class Solution {
        public int mySqrt(int x) {

            if (x < 2) return x;

            int i = 1;

            while ((long) i * i <= x) {
                i++;
            }

            return i - 1;
        }
    }

### Complexity

- **Time:** `O(√x)`
- **Space:** `O(1)`

---
## Solution Approach 1: Binary Search (Optimal)

### Algorithm

1. If `x < 2`, return `x`.
2. Initialize:
   - `left = 0`
   - `right = x / 2`
3. While `left <= right`:
   - Compute `mid = left + (right - left) / 2`
   - Compute `square = mid * mid`
4. If `square == x` → return `mid`
5. If `square < x`:
   - Move left → `left = mid + 1`
6. Else:
   - Move right → `right = mid - 1`
7. When loop ends, `right` is the integer square root.
8. Return `right`.

### Code

    class Solution {
        public int mySqrt(int x) {

            if (x < 2) return x;

            long left = 0;
            long right = x / 2;

            while (left <= right) {

                long mid = left + (right - left) / 2;
                long square = mid * mid;

                if (square == x) {
                    return (int) mid;
                }
                else if (square < x) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }

            return (int) right;
        }
    }

### Complexity

- **Time:** `O(log x)`
- **Space:** `O(1)`

---





---
