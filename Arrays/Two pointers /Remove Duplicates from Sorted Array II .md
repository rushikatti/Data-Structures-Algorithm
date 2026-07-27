# 80. Remove Duplicates from Sorted Array II


## Solution Approach 1: Brute Force (In-Place)

### Algorithm

1. Traverse the array from left to right.
2. Keep a count of consecutive occurrences of the current number.
3. If the count becomes greater than `2`:
   - Shift all elements after the current index one position to the left.
   - Decrease the array length.
   - Stay at the same index to check the new element shifted into that position.
4. Continue until the end of the valid portion of the array.
5. Return the updated length.

### Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        int n = nums.length;

        int count = 1;
        int i = 1;

        while (i < n) {

            if (nums[i] == nums[i - 1]) {
                count++;
            } else {
                count = 1;
            }

            if (count > 2) {

                for (int j = i; j < n - 1; j++) {
                    nums[j] = nums[j + 1];
                }

                n--;
                count = 2;
            } else {
                i++;
            }
        }

        return n;
    }
}
```

### Complexity

- **Time:** `O(n²)` (each deletion may shift up to `n` elements)
- **Space:** `O(1)`
---

## Solution Approach 2: Optimal (Two Pointers)

### Algorithm

1. If the array has at most two elements, return its length.
2. Keep the first two elements as they are always valid.
3. Maintain a write pointer `k = 2`.
4. Traverse the array from index `2`.
5. If the current element is different from `nums[k - 2]`, copy it to `nums[k]` and increment `k`.
6. Skip the element if it would become the third occurrence.
7. Return `k`.

### Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        int n = nums.length;

        if (n <= 2) {
            return n;
        }

        int k = 2;

        for (int i = 2; i < n; i++) {

            if (nums[i] != nums[k - 2]) {
                nums[k] = nums[i];
                k++;
            }
        }

        return k;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
