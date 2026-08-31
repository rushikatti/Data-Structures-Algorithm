# 1011. Capacity To Ship Packages Within D Days

## Solution Approach 1: Brute Force (Linear Search on Capacity)

### Algorithm

1. Find:
   - `low = max(weights)` → minimum possible capacity
   - `high = sum(weights)` → maximum possible capacity
2. Try every capacity from `low` to `high`
3. For each capacity:
   - Simulate shipping using helper function
   - Count required days
4. If required days ≤ given `days`, return capacity

---

### Code

    class Solution {
        public int shipWithinDays(int[] weights, int days) {

            int low = 0, high = 0;

            for (int w : weights) {
                low = Math.max(low, w);
                high += w;
            }

            for (int cap = low; cap <= high; cap++) {

                if (check(weights, days, cap)) {
                    return cap;
                }
            }

            return -1;
        }

        private boolean check(int[] weights, int days, int cap) {

            int load = 0;
            int day = 1;

            for (int w : weights) {

                if (load + w > cap) {
                    day++;
                    load = w;
                } else {
                    load += w;
                }
            }

            return day <= days;
        }
    }

---

### Complexity

- **Time:** `O(n * (sum - max))`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. Define search space:
   - `low = max(weights)`
   - `high = sum(weights)`
2. While `low <= high`:
   - `mid = capacity`
   - Check if shipping is possible within `days`
3. If possible:
   - Try smaller capacity → `high = mid - 1`
4. Else:
   - Increase capacity → `low = mid + 1`
5. Return `low`

---

### Code

    class Solution {
        public int shipWithinDays(int[] weights, int days) {

            int low = 0, high = 0;

            for (int w : weights) {
                low = Math.max(low, w);
                high += w;
            }

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (check(weights, days, mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return low;
        }

        private boolean check(int[] weights, int days, int cap) {

            int load = 0;
            int day = 1;

            for (int w : weights) {

                if (load + w > cap) {
                    day++;
                    load = w;
                } else {
                    load += w;
                }
            }

            return day <= days;
        }
    }

---

### Complexity

- **Time:** `O(n log(sum))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Capacity is the **answer space**
- We apply **Binary Search on Answer**
- Helper function validates feasibility

---

## Example

    weights = [1,2,3,4,5,6,7,8,9,10]
    days = 5

    Output → 15

---
