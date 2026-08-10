# 974. Subarray Sums Divisible by K

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `count = 0`.
2. Traverse every possible starting index `i`.
3. Initialize `sum = 0`.
4. Extend the subarray using another loop.
5. Add the current element to `sum`.
6. If `sum % k == 0`, increment `count`.
7. Return the total count.

### Code

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {

        int n = nums.length;
        int count = 0;

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += nums[j];

                if (sum % k == 0) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Prefix Sum + HashMap)

### Algorithm

1. Use a prefix sum approach.
2. Maintain a `HashMap` to store the frequency of remainders.
3. Initialize the map with `{0:1}` to handle subarrays starting from index `0`.
4. Traverse the array:
   - Add the current number to `sum`.
   - Compute `remainder = sum % k`.
   - If remainder is negative, adjust it by adding `k`.
   - If the remainder exists in the map, add its frequency to `count`.
   - Update the map with the current remainder.
5. Return the total count.

### Code

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {

        int count = 0;
        int sum = 0;

        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        for (int num : nums) {

            sum += num;

            int rem = sum % k;

            if (rem < 0) {
                rem += k;
            }

            if (map.containsKey(rem)) {
                count += map.get(rem);
            }

            map.put(rem, map.getOrDefault(rem, 0) + 1);
        }

        return count;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(k)` *(for storing remainder frequencies)*
