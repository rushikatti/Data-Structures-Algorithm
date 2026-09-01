# 1552. Magnetic Force Between Two Balls (Aggressive Cows Variant)

## Problem

Given an array `position[]` representing positions on a line and an integer `m` (number of balls),  
place the balls such that the **minimum distance between any two balls is maximized**.

Return the **maximum possible minimum distance**.

---

## Solution Approach 1: Brute Force (Linear Search on Distance)

### Algorithm

1. Sort the array `position[]`
2. Minimum distance = `1`
3. Maximum distance = `max(position) - min(position)`
4. Try every distance from `1 → maxDistance`
5. For each distance:
   - Place first ball at `position[0]`
   - Try placing next balls greedily:
     - Place if `position[i] - last >= distance`
6. If we can place ≥ `m` balls → valid
7. Return the **largest valid distance**

---

### Code

    import java.util.Arrays;

    class Solution {
        public int maxDistance(int[] position, int m) {

            Arrays.sort(position);

            int n = position.length;
            int maxDist = position[n - 1] - position[0];

            int ans = 0;

            for (int dist = 1; dist <= maxDist; dist++) {

                if (canPlace(position, m, dist)) {
                    ans = dist;
                }
            }

            return ans;
        }

        private boolean canPlace(int[] position, int m, int dist) {

            int count = 1;
            int last = position[0];

            for (int i = 1; i < position.length; i++) {

                if (position[i] - last >= dist) {
                    count++;
                    last = position[i];
                }
            }

            return count >= m;
        }
    }

---

### Complexity

- **Time:** `O(n * maxDistance)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. Sort `position[]`
2. Define search space:
   - `low = 1`
   - `high = position[n-1] - position[0]`  ✅ (important)
3. While `low <= high`:
   - `mid = possible minimum distance`
4. If we can place balls with distance `mid`:
   - Try bigger distance → `low = mid + 1`
5. Else:
   - Reduce distance → `high = mid - 1`
6. Return `high` (or `ans`)

---

### Code

    import java.util.Arrays;

    class Solution {
        public int maxDistance(int[] position, int m) {

            Arrays.sort(position);

            int low = 1;
            int high = position[position.length - 1] - position[0];

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (check(position, m, mid)) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }

            return high;
        }

        private boolean check(int[] position, int m, int gap) {

            int count = 1;
            int last = position[0];

            for (int i = 1; i < position.length; i++) {

                if (position[i] - last >= gap) {
                    count++;
                    last = position[i];
                }
            }

            return count >= m;
        }
    }

---

### Complexity

- **Time:** `O(n log(maxDistance))`
- **Space:** `O(1)`

---

## ❗ Bug in Your Code (Important Fix)

You wrote:

    int high = 0;
    for(int p : position){
        high = Math.max(high,p);
    }

👉 ❌ This is wrong for this problem

✔ Correct:

    high = position[n-1] - position[0];

---

## 🔥 Key Insight

- We are maximizing the **minimum distance**
- Distance is the **answer space**
- Use **Binary Search on Answer**

---

## Example

    position = [1,2,3,4,7]
    m = 3

    Output → 3

Explanation:
- Place balls at: 1, 4, 7
- Minimum distance = 3 (maximum possible)

---
