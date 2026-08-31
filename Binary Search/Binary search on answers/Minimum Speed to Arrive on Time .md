# 1870. Minimum Speed to Arrive on Time

## Solution Approach 1: Brute Force (Linear Search on Speed)

### Algorithm

1. Minimum speed = `1`
2. Maximum speed = large value (e.g., `10^7`)
3. Try each speed:
   - For each train:
     - For all except last → take `ceil(dist[i] / speed)`
     - For last → exact division
4. If total time ≤ `hour`, return speed

---

### Code

    class Solution {
        public int minSpeedOnTime(int[] dist, double hour) {

            for (int speed = 1; speed <= 10000000; speed++) {

                if (canReach(dist, hour, speed)) {
                    return speed;
                }
            }

            return -1;
        }

        private boolean canReach(int[] dist, double hour, int speed) {

            double time = 0.0;

            for (int i = 0; i < dist.length; i++) {

                if (i == dist.length - 1) {
                    time += (double) dist[i] / speed;
                } else {
                    time += (dist[i] + speed - 1) / speed;
                }
            }

            return time <= hour;
        }
    }

---

### Complexity

- **Time:** `O(n * maxSpeed)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. Search space:
   - `low = 1`
   - `high = 10^7`
2. While `low <= high`:
   - `mid = speed`
   - Compute total time
3. If time ≤ hour:
   - Try smaller speed → `high = mid - 1`
4. Else:
   - Increase speed → `low = mid + 1`
5. Return `low` if valid, else `-1`

---

### Code

    class Solution {
        public int minSpeedOnTime(int[] dist, double hour) {

            int low = 1, high = 10000000;
            int ans = -1;

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (canReach(dist, hour, mid)) {
                    ans = mid;
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return ans;
        }

        private boolean canReach(int[] dist, double hour, int speed) {

            double time = 0.0;

            for (int i = 0; i < dist.length; i++) {

                if (i == dist.length - 1) {
                    time += (double) dist[i] / speed;
                } else {
                    time += (dist[i] + speed - 1) / speed;
                }
            }

            return time <= hour;
        }
    }

---

### Complexity

- **Time:** `O(n log maxSpeed)`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Speed is the **answer space**
- Higher speed → less time
- Use **Binary Search on Answer**

---

## Example

    dist = [1,3,2]
    hour = 2.7

    Output → 3
