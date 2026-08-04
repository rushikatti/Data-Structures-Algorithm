# 904. Fruit Into Baskets

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxFruits = 0`.
2. For every starting index `left`:
   - Create a `HashMap` to store the frequency of fruit types.
   - Traverse from `left` using another pointer `right`.
   - Add the current fruit to the map.
   - If the map contains more than two fruit types, stop extending the window.
   - Otherwise, increment the current window length.
3. Update the maximum window length.
4. Return the maximum number of fruits collected.

### Code

```java
class Solution {
    public int totalFruit(int[] fruits) {

        int n = fruits.length;
        int ans = 0;

        for (int left = 0; left < n; left++) {

            HashMap<Integer, Integer> map = new HashMap<>();
            int count = 0;

            for (int right = left; right < n; right++) {

                map.put(fruits[right],
                        map.getOrDefault(fruits[right], 0) + 1);

                if (map.size() > 2) {
                    break;
                }

                count++;
            }

            ans = Math.max(ans, count);
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)` *(HashMap stores at most 3 fruit types before breaking, so the extra space is constant.)*

---

## Solution Approach 2: Optimal (Sliding Window)

### Algorithm

1. Initialize:
   - `left = 0`
   - `maxFruits = 0`
   - A `HashMap` to store the frequency of fruit types in the current window.
2. Traverse the array using the `right` pointer.
3. Add the current fruit to the map.
4. While the map contains more than two fruit types:
   - Decrease the frequency of `fruits[left]`.
   - Remove it from the map if its frequency becomes `0`.
   - Move `left` forward.
5. Update the maximum window size.
6. Return the maximum number of fruits collected.

### Code

```java
class Solution {
    public int totalFruit(int[] fruits) {

        int n = fruits.length;

        int left = 0;
        int ans = 0;

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int right = 0; right < n; right++) {

            map.put(fruits[right],
                    map.getOrDefault(fruits[right], 0) + 1);

            while (map.size() > 2) {

                map.put(fruits[left],
                        map.get(fruits[left]) - 1);

                if (map.get(fruits[left]) == 0) {
                    map.remove(fruits[left]);
                }

                left++;
            }

            ans = Math.max(ans, right - left + 1);
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)` *(The HashMap stores at most 3 fruit types during execution, so the extra space is constant.)*
