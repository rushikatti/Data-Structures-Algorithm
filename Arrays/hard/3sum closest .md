
# LeetCode 16 - 3Sum Closest

---

# 1. Brute Force

## Approach

1. Initialize the closest sum using the first three elements.
2. Generate all possible triplets using three nested loops.
3. Calculate the sum of each triplet.
4. Compare the current sum with the target.
5. If the current sum is closer to the target than the previous closest sum, update the answer.
6. Return the closest sum.

## Java Code

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {

        int n = nums.length;
        int closest = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {

                    int sum = nums[i] + nums[j] + nums[k];

                    if (Math.abs(sum - target) < Math.abs(closest - target)) {
                        closest = sum;
                    }
                }
            }
        }

        return closest;
    }
}
```

## Complexity

- **Time Complexity:** `O(n³)`
- **Space Complexity:** `O(1)`

---

# 2. Better Approach

**No standard better solution exists for this problem.**

The optimal solution directly improves the brute-force approach from **O(n³)** to **O(n²)** using sorting and the two-pointer technique.

---

# 3. Optimal Approach (Sorting + Two Pointers)

## Approach

1. Sort the array.
2. Initialize the closest sum using the first three elements.
3. Fix one element using a loop.
4. Use two pointers (`left` and `right`) to find the remaining two elements.
5. Calculate the current sum.
6. If the current sum is closer to the target, update the closest sum.
7. If the sum is smaller than the target, move the left pointer to increase the sum.
8. If the sum is greater than the target, move the right pointer to decrease the sum.
9. If the sum equals the target, return it immediately.
10. Return the closest sum after all iterations.

## Java Code

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {

        Arrays.sort(nums);

        int n = nums.length;
        int closest = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < n - 2; i++) {

            int left = i + 1;
            int right = n - 1;

            while (left < right) {

                int sum = nums[i] + nums[left] + nums[right];

                if (Math.abs(sum - target) < Math.abs(closest - target)) {
                    closest = sum;
                }

                if (sum < target) {
                    left++;
                } else if (sum > target) {
                    right--;
                } else {
                    return sum;
                }
            }
        }

        return closest;
    }
}
```

## Complexity

- **Time Complexity:** `O(n²)`
- **Space Complexity:** `O(1)`
````

