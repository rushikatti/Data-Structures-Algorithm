
# 153. Find Minimum in Rotated Sorted Array

## Brute Force Solution

### Approach

- Traverse the entire array.
- Keep track of the smallest element encountered.
- Return the minimum element after the traversal.

### Code

```java
class Solution {

    public int findMin(int[] nums) {

        int min = nums[0];

        for (int num : nums) {
            min = Math.min(min, num);
        }

        return min;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Better Solution

### Approach

- Traverse the array from left to right.
- Find the first position where the current element is smaller than the previous element.
- That element is the minimum.
- If no such element exists, the array was never rotated, so return the first element.

### Code

```java
class Solution {

    public int findMin(int[] nums) {

        for (int i = 1; i < nums.length; i++) {

            if (nums[i] < nums[i - 1]) {
                return nums[i];
            }
        }

        return nums[0];
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Optimal Solution (Binary Search)

### Approach

- Use Binary Search since the array is sorted and rotated.
- Maintain two pointers: `left` and `right`.
- If the current range is already sorted (`nums[left] <= nums[right]`), then `nums[left]` is the minimum.
- Find the middle element:
  - If `nums[mid] >= nums[left]`, the left half is sorted, so the minimum must be in the right half.
  - Otherwise, the minimum lies in the left half (including `mid`).
- Continue until the minimum is found.

### Code

```java
class Solution {

    public int findMin(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while (left < right) {

            if (nums[left] < nums[right]) {
                return nums[left];
            }

            int mid = left + (right - left) / 2;

            if (nums[mid] >= nums[left]) {
                left = mid + 1;
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

