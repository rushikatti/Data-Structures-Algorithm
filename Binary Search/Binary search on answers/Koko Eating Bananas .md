# 875. Koko Eating Bananas

## Solution Approach 1: Brute Force (Linear Search on Speed)

### Algorithm

1. Minimum speed = `1`
2. Maximum speed = `max(piles)`
3. Try every speed from `1 → max`
4. For each speed:
   - Calculate total hours required:
     
        hours += ceil(piles[i] / speed)
5. If total hours ≤ `h`, return speed

---

### Code

    class Solution {
        public int minEatingSpeed(int[] piles, int h) {

            int max = 0;
            for (int p : piles) {
                max = Math.max(max, p);
            }

            for (int speed = 1; speed <= max; speed++) {

                if (canFinish(piles, h, speed)) {
                    return speed;
                }
            }

            return -1;
        }

        private boolean canFinish(int[] piles, int h, int speed) {

            int hours = 0;

            for (int p : piles) {
                hours += (p + speed - 1) / speed; // ceil division
            }

            return hours <= h;
        }
    }

---

### Complexity

- **Time:** `O(n * max(piles))`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. Search space:
   - `low = 1`
   - `high = max(piles)`
2. While `low <= high`:
   - `mid = speed`
   - Calculate required hours
3. If hours ≤ `h`:
   - Try smaller speed → `high = mid - 1`
4. Else:
   - Increase speed → `low = mid + 1`
5. Return `low`

---

### Code

    class Solution {
        public int minEatingSpeed(int[] piles, int h) {

            int low = 1, high = 0;

            for (int p : piles) {
                high = Math.max(high, p);
            }

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (canFinish(piles, h, mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return low;
        }

        private boolean canFinish(int[] piles, int h, int speed) {

            int hours = 0;

            for (int p : piles) {
                hours += (p + speed - 1) / speed;
            }

            return hours <= h;
        }
    }

---

### Complexity

- **Time:** `O(n log max(piles))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Speed is the **answer space**
- More speed → fewer hours
- Use **Binary Search on Answer**

---

## Example

    piles = [3,6,7,11]
    h = 8

    Output → 4

---



---
