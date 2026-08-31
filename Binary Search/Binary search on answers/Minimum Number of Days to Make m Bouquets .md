# 1482. Minimum Number of Days to Make m Bouquets

## Problem

Given an array `bloomDay[]`, where `bloomDay[i]` is the day the `i-th` flower blooms,  
and integers `m` (number of bouquets) and `k` (flowers per bouquet):

- Each bouquet needs **k adjacent flowers**
- Return the **minimum number of days** required to make `m` bouquets  
- If not possible → return `-1`

---

## Solution Approach 1: Brute Force (Linear Search on Days)

### Algorithm

1. If `m * k > n`, return `-1`
2. Find:
   - `low = min(bloomDay)`
   - `high = max(bloomDay)`
3. Try each day from `low → high`
4. For each day:
   - Count how many bouquets can be formed
   - Traverse array:
     - If `bloomDay[i] ≤ day`, increment `count`
     - If `count == k`, increment bouquets and reset count
     - Else reset count if not bloomed
5. If bouquets ≥ `m`, return current day

---

### Code

    class Solution {
        public int minDays(int[] bloomDay, int m, int k) {

            int n = bloomDay.length;

            if ((long) m * k > n) return -1;

            int low = Integer.MAX_VALUE;
            int high = Integer.MIN_VALUE;

            for (int b : bloomDay) {
                low = Math.min(low, b);
                high = Math.max(high, b);
            }

            for (int day = low; day <= high; day++) {

                if (canMake(bloomDay, m, k, day)) {
                    return day;
                }
            }

            return -1;
        }

        private boolean canMake(int[] bloomDay, int m, int k, int day) {

            int count = 0, bouquets = 0;

            for (int b : bloomDay) {

                if (b <= day) {
                    count++;
                    if (count == k) {
                        bouquets++;
                        count = 0;
                    }
                } else {
                    count = 0;
                }
            }

            return bouquets >= m;
        }
    }

---

### Complexity

- **Time:** `O(n * (max - min))`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Binary Search on Answer)

### Algorithm

1. If `m * k > n`, return `-1`
2. Define search space:
   - `low = min(bloomDay)`
   - `high = max(bloomDay)`
3. While `low <= high`:
   - `mid = current day`
4. If we can form ≥ `m` bouquets in `mid` days:
   - Try smaller day → `high = mid - 1`
5. Else:
   - Increase day → `low = mid + 1`
6. Return `low`

---

### Code

    class Solution {
        public int minDays(int[] bloomDay, int m, int k) {

            int n = bloomDay.length;

            if ((long) m * k > n) return -1;

            int low = Integer.MAX_VALUE;
            int high = Integer.MIN_VALUE;

            for (int bloom : bloomDay) {
                low = Math.min(low, bloom);
                high = Math.max(high, bloom);
            }

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (check(bloomDay, m, k, mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return low;
        }

        private boolean check(int[] bloomDay, int m, int k, int day) {

            int count = 0, bouquets = 0;

            for (int b : bloomDay) {

                if (b <= day) {
                    count++;
                    if (count == k) {
                        bouquets++;
                        count = 0;
                    }
                } else {
                    count = 0;
                }
            }

            return bouquets >= m;
        }
    }

---

### Complexity

- **Time:** `O(n log(max))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- Days is the **answer space**
- More days → more flowers bloom → more bouquets possible
- Use **Binary Search on Answer**

---

## Example

    bloomDay = [1,10,3,10,2]
    m = 3
    k = 1

    Output → 3

---
