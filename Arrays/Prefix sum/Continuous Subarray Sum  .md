# 523. Continuous Subarray Sum

## Solution Approach 1: Brute Force

### Algorithm

1. Traverse every possible starting index `i`.
2. Initialize `sum = 0`.
3. Extend the subarray using another loop.
4. Add the current element to `sum`.
5. Check:
   - If the subarray length is at least `2`.
   - If `sum % k == 0`.
6. If both conditions are satisfied, return `true`.
7. If no valid subarray is found, return `false`.

### Code

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {

        int n = nums.length;

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += nums[j];

                if (j - i + 1 >= 2 && sum % k == 0) {
                    return true;
                }
            }
        }

        return false;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Prefix Sum + HashMap)

### Algorithm

1. Use prefix sum and remainder concept.
2. Maintain a `HashMap` to store the **first occurrence index** of each remainder.
3. Initialize map with `{0: -1}` to handle subarrays starting from index `0`.
4. Traverse the array:
   - Add current element to `sum`.
   - Compute `remainder = sum % k`.
   - If remainder exists in the map:
     - Check if subarray length is at least `2`:
       ```
       i - previousIndex >= 2
       ```
     - If yes, return `true`.
   - Otherwise, store the remainder with current index.
5. Return `false` if no valid subarray exists.

### Code

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {

        int n = nums.length;

        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);

        int sum = 0;

        for (int i = 0; i < n; i++) {

            sum += nums[i];

            int rem = sum % k;

            if (map.containsKey(rem)) {

                if (i - map.get(rem) >= 2) {
                    return true;
                }
            } 
            else {
                map.put(rem, i);
            }
        }

        return false;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(k)` *(for storing remainders)*
