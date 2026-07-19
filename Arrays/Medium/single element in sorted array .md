# 540. Single Element in a Sorted Array

## Brute Force Solution

### Approach

- Traverse the array from left to right.
- Check whether the current element is different from both its previous and next elements.
- If yes, it is the single element.
- Handle the first and last elements separately.

### Code

```java
class Solution {

    public int singleNonDuplicate(int[] nums) {

        int n = nums.length;

        if (n == 1)
            return nums[0];

        if (nums[0] != nums[1])
            return nums[0];

        if (nums[n - 1] != nums[n - 2])
            return nums[n - 1];

        for (int i = 1; i < n - 1; i++) {

            if (nums[i] != nums[i - 1] && nums[i] != nums[i + 1]) {
                return nums[i];
            }
        }

        return -1;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Better Solution

### Approach

- XOR all the elements.
- Since every element appears exactly twice, duplicate elements cancel each other.
- The remaining value is the single element.

### Code

```java
class Solution {

    public int singleNonDuplicate(int[] nums) {

        int xor = 0;

        for (int num : nums) {
            xor ^= num;
        }

        return xor;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Optimal Solution

### Approach

- Since the array is sorted, duplicate elements always appear together.
- Before the single element:
  - The first occurrence of every pair is at an **even** index.
  - The second occurrence is at an **odd** index.
- After the single element, this pattern is reversed.
- Perform Binary Search:
  - Compute `mid`.
  - If `mid` is odd, decrement it by one to make it even.
  - If `nums[mid] == nums[mid + 1]`, the single element lies on the right.
  - Otherwise, it lies on the left (including `mid`).
- Continue until `left == right`.

### Code

```java
class Solution {

    public int singleNonDuplicate(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while (left < right) {

            int mid = left + (right - left) / 2;

            if (mid % 2 == 1) {
                mid--;
            }

            if (nums[mid] == nums[mid + 1]) {
                left = mid + 2;
            } else {
                right = mid;
            }
        }

        return nums[left];
    }
}
```

### Complexity

- **Time:** O(log n)
- **Space:** O(1)
