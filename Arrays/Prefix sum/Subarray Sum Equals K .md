# 📊 Subarray Sum Equals K

## 🧠 Problem Statement

Given an integer array `nums[]` and an integer `k`, return the **total number of subarrays whose sum equals k**.

### Example:
    Input:  nums = [1,1,1], k = 2
    Output: 2

---

# 💡 Approach 1: Brute Force

## 🔹 Algorithm

1. Loop `i` from `0 → n-1`
2. Initialize `sum = 0`
3. Loop `j` from `i → n-1`
   - Add `nums[j]` to sum
   - If `sum == k`, increment count
4. Return count

---

## 🔹 Code

    class Solution {
        public int subarraySum(int[] nums, int k) {
            int n = nums.length;
            int count = 0;

            for(int i = 0; i < n; i++){
                int sum = 0;

                for(int j = i; j < n; j++){
                    sum += nums[j];

                    if(sum == k){
                        count++;
                    }
                }
            }

            return count;
        }
    }

---

## ⏱ Complexity

- Time: **O(N²)**
- Space: **O(1)**

---

# 🚀 Approach 2: Optimal (Prefix Sum + HashMap)

## 🔹 Algorithm

1. Initialize map with `(0 → 1)`
2. Maintain `sum = 0`, `count = 0`
3. For each element:
   - Add to `sum`
   - If `(sum - k)` exists in map:
       - Add its frequency to count
   - Update map with current sum frequency
4. Return count

---

## 🔹 Code

    class Solution {
        public int subarraySum(int[] nums, int k) {
            HashMap<Integer, Integer> map = new HashMap<>();
            map.put(0, 1);

            int sum = 0, count = 0;

            for(int num : nums){
                sum += num;

                if(map.containsKey(sum - k)){
                    count += map.get(sum - k);
                }

                map.put(sum, map.getOrDefault(sum, 0) + 1);
            }

            return count;
        }
    }

---

## ⏱ Complexity

- Time: **O(N)**
- Space: **O(N)**

---

# 🏁 Summary

| Approach        | Time Complexity | Space | Notes                     |
|----------------|---------------|-------|---------------------------|
| Brute Force    | O(N²)         | O(1)  | Check all subarrays       |
| Prefix Sum     | O(N)          | O(N)  | Handles negatives         |

---
