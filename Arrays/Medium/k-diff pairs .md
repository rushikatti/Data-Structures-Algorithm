# 532. K-diff Pairs in an Array

## Brute Force Solution

### Approach

- Check every possible pair `(i, j)` where `i < j`.
- If `|nums[i] - nums[j]| == k`, add the pair to a `HashSet` to avoid duplicates.
- Store each pair in sorted order `(min, max)` so that duplicate pairs are counted only once.
- Return the size of the set.

### Code

```java
class Solution {

    public int findPairs(int[] nums, int k) {

        Set<String> set = new HashSet<>();

        for (int i = 0; i < nums.length; i++) {

            for (int j = i + 1; j < nums.length; j++) {

                if (Math.abs(nums[i] - nums[j]) == k) {

                    int a = Math.min(nums[i], nums[j]);
                    int b = Math.max(nums[i], nums[j]);

                    set.add(a + "#" + b);
                }
            }
        }

        return set.size();
    }
}
```

### Complexity

- **Time:** O(n²)
- **Space:** O(n)

---

## Better Solution

### Approach

- Build a frequency map of all numbers.
- If `k == 0`, count numbers whose frequency is greater than `1`.
- Otherwise, for every unique number `x`, check whether `x + k` exists in the map.
- Count all such unique pairs.

### Code

```java
class Solution {

    public int findPairs(int[] nums, int k) {

        if (k < 0)
            return 0;

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        int count = 0;

        for (int num : map.keySet()) {

            if (k == 0) {

                if (map.get(num) > 1)
                    count++;

            } else {

                if (map.containsKey(num + k))
                    count++;
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(n)

---

## Optimal Solution

### Approach

- Sort the array.
- Use two pointers `left` and `right`.
- If the difference is smaller than `k`, move `right`.
- If the difference is larger than `k`, move `left`.
- If the difference equals `k`, count the pair and skip duplicate values.
- Ensure `left` and `right` never point to the same index.

### Code

```java
class Solution {

    public int findPairs(int[] nums, int k) {

        if (k < 0)
            return 0;

        Arrays.sort(nums);

        int left = 0;
        int right = 1;
        int count = 0;

        while (right < nums.length) {

            if (left == right || nums[right] - nums[left] < k) {

                right++;

            } else if (nums[right] - nums[left] > k) {

                left++;

            } else {

                count++;
                left++;
                right++;

                while (right < nums.length && nums[right] == nums[right - 1]) {
                    right++;
                }
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** O(n log n)
- **Space:** O(1)
