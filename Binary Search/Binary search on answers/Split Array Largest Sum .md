# 410. Split Array Largest Sum

## Problem

Given an array `nums[]` and an integer `k`, split the array into `k` or fewer **non-empty subarrays** such that:

- Each subarray is **contiguous**
- Minimize the **largest sum among these subarrays**

Return the **minimum possible largest sum**.

---

## Solution Approach 1: Brute Force (Linear Search on Answer)

### Algorithm

1. Define search space:
   - `low = max(nums)` → minimum possible largest sum
   - `high = sum(nums)` → maximum possible largest sum
2. Try every value from `low → high`
3. For each `maxSum`:
   - Traverse array and form subarrays:
     - Keep adding until sum exceeds `maxSum`
     - Then start a new subarray
4. Count number of subarrays formed
5. If `count ≤ k`, update answer
6. Return minimum valid value

---

### Code

    class Solution {
        public int splitArray(int[] nums, int k) {

            int low = 0, high = 0;

            for (int num : nums) {
                low = Math.max(low, num);
                high += num;
            }

            int ans = high;

            for (int maxSum = low; maxSum <= high; maxSum++) {

                if (check(nums, k, maxSum)) {
                    ans = maxSum;
                    break;  // first valid is minimum
                }
            }

            return ans;
        }

        private boolean check(int[] nums, int k, int maxSum) {

            int count = 1;
            int currSum = 0;

            for (int num : nums) {

                if (currSum + num <= maxSum) {
                    currSum += num;
                } else {
                    count++;
                    currSum = num;
                }
            }

            return count <= k;
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
   - `low = max(nums)`
   - `high = sum(nums)`
2. While `low <= high`:
   - `mid = possible largest sum`
3. If we can split into ≤ `k` subarrays:
   - Try smaller → `high = mid - 1`
4. Else:
   - Increase → `low = mid + 1`
5. Return `low`

---

### Code

    class Solution {
        public int splitArray(int[] nums, int k) {

            int low = 0, high = 0;

            for (int num : nums) {
                low = Math.max(low, num);
                high += num;
            }

            while (low <= high) {

                int mid = low + (high - low) / 2;

                if (check(nums, k, mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }

            return low;
        }

        private boolean check(int[] nums, int k, int maxSum) {

            int count = 1;
            int currSum = 0;

            for (int num : nums) {

                if (currSum + num <= maxSum) {
                    currSum += num;
                } else {
                    count++;
                    currSum = num;
                }
            }

            return count <= k;
        }
    }

---

### Complexity

- **Time:** `O(n log(sum))`
- **Space:** `O(1)`

---

## 🔥 Key Insight

- We minimize the **maximum subarray sum**
- Larger allowed sum → fewer subarrays needed
- Classic **Binary Search on Answer**

---

## Example

    nums = [7,2,5,10,8]
    k = 2

    Output → 18

Explanation:
- Split: [7,2,5] and [10,8]
- Largest sum = 18 (minimum possible)

---
