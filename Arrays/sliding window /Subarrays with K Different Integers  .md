# 992. Subarrays with K Different Integers

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `count = 0`.
2. Traverse every possible starting index `i`.
3. Create a `HashMap` to store the frequency of elements in the current subarray.
4. Extend the subarray using another loop.
5. Add the current element to the map.
6. If the number of distinct elements is:
   - Equal to `k`, increment `count`.
   - Greater than `k`, stop extending the current subarray.
7. Return the total count.

### Code

```java
class Solution {
    public int subarraysWithKDistinct(int[] nums, int k) {

        int n = nums.length;
        int count = 0;

        for (int i = 0; i < n; i++) {

            HashMap<Integer, Integer> map = new HashMap<>();

            for (int j = i; j < n; j++) {

                map.put(nums[j],
                        map.getOrDefault(nums[j], 0) + 1);

                if (map.size() == k) {
                    count++;
                }
                else if (map.size() > k) {
                    break;
                }
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(k)` *(At most `k + 1` distinct elements are stored before breaking.)*

---

## Solution Approach 2: Optimal (Sliding Window + At Most K Trick)

### Algorithm

1. Count the number of subarrays with **at most `k` distinct** elements.
2. Count the number of subarrays with **at most `k - 1` distinct** elements.
3. The number of subarrays with **exactly `k` distinct** elements is:
   ```
   AtMost(k) - AtMost(k - 1)
   ```
4. Use a sliding window and a `HashMap` to count subarrays with at most `k` distinct elements.
5. Return the difference.

### Code

```java
class Solution {
    public int subarraysWithKDistinct(int[] nums, int k) {
        return atMost(nums, k) - atMost(nums, k - 1);
    }

    private int atMost(int[] nums, int k) {

        int left = 0;
        int count = 0;

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int right = 0; right < nums.length; right++) {

            map.put(nums[right],
                    map.getOrDefault(nums[right], 0) + 1);

            while (map.size() > k) {

                map.put(nums[left], map.get(nums[left]) - 1);

                if (map.get(nums[left]) == 0) {
                    map.remove(nums[left]);
                }

                left++;
            }

            count += right - left + 1;
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(k)`
