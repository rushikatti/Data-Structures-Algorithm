# Aggressive Cows (Maximize Minimum Distance)

## Problem

Given an array `stalls[]` representing positions of stalls and an integer `k` (number of cows),  
place the cows in stalls such that the **minimum distance between any two cows is maximized**.

Return that **maximum possible minimum distance**.

---

## Solution Approach 1: Brute Force (Linear Search on Distance)

### Algorithm

1. Sort the array `stalls[]`
2. Minimum distance = `1`
3. Maximum distance = `max(stalls) - min(stalls)`
4. Try every distance from `1 → max`
5. For each distance:
   - Place first cow at `stalls[0]`
   - Try placing next cows greedily:
     - Place cow only if distance ≥ current distance
6. If we can place ≥ `k` cows → valid
7. Return the **largest valid distance**

---

### Code

    import java.util.Arrays;

    class Solution {
        public int aggressiveCows(int[] stalls, int k) {

            Arrays.sort(stalls);

            int n = stalls.length;
            int maxDist = stalls[n - 1] - stalls[0];

            int ans = 0;

            for (int dist = 1; dist <= maxDist; dist++) {

                if (canPlace(stalls, k, dist)) {
                    ans = dist;
                }
            }

            return ans;
        }

        private boolean canPlace(int[] stalls, int k, int dist) {

            int count = 1;
            int last = stalls[0];

            for (int i = 1; i < stalls.length; i++) {

                if (stalls[i] - last >= dist) {
                    count++;
                    last = stalls[i];
                }
            }

            return count >= k;
        }
    }

---

### Complexity

- **Time:** `O(n * maxDistance)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. Sort `stalls[]`
2. Search space:
   - `low = 1`
   - `high = stalls[n-1] - stalls[0]`
3. While `low <= high`:
   - `mid = possible minimum distance`
4. If we can place cows with distance `mid`:
   - Try bigger distance → `low = mid + 1`
5. Else:
   - Reduce distance → `high = mid - 1`
6. Return `high`

---

### Code

    import java.util.Arrays;

    class Solution {
        public int aggressiveCows(int[] stalls, int k) {

            Arrays.sort(stalls);

            int low = 1;
            int high = stalls[stalls.length - 1] - stalls[0];

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (canPlace(stalls, k, mid)) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }

            return high;
        }

        private boolean canPlace(int[] stalls, int k, int dist) {

            int count = 1;
            int last = stalls[0];

            for (int i = 1; i < stalls.length; i++) {

                if (stalls[i] - last >= dist) {
                    count++;
                    last = stalls[i];
                }
            }

            return count >= k;
        }
    }

---

### Complexity

- **Time:** `O(n log(maxDistance))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- We are maximizing the **minimum distance**
- Distance is the **answer space**
- Use **Binary Search on Answer**

---

## Example

    stalls = [1,2,4,8,9]
    k = 3

    Output → 3

Explanation:
- Place cows at positions: 1, 4, 8
- Minimum distance = 3 (maximum possible)

---
