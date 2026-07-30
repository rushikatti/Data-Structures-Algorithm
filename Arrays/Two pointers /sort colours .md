# 75. Sort Colors

## Solution Approach 1: Better (Counting Sort)

### Algorithm

1. Traverse the array once and count the number of:
   - `0`s
   - `1`s
   - `2`s
2. Traverse the array again:
   - Fill the first `zeroCnt` positions with `0`.
   - Fill the next `oneCnt` positions with `1`.
   - Fill the remaining positions with `2`.

### Code

```java
class Solution {
    public void sortColors(int[] nums) {

        int zeroCnt = 0;
        int oneCnt = 0;
        int twoCnt = 0;

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == 0)
                zeroCnt++;

            if (nums[i] == 1)
                oneCnt++;

            if (nums[i] == 2)
                twoCnt++;
        }

        int i = 0;

        while (zeroCnt > 0) {
            nums[i] = 0;
            i++;
            zeroCnt--;
        }

        while (oneCnt > 0) {
            nums[i] = 1;
            i++;
            oneCnt--;
        }

        while (twoCnt > 0) {
            nums[i] = 2;
            i++;
            twoCnt--;
        }
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Dutch National Flag Algorithm)

### Algorithm

1. Initialize three pointers:
   - `left` → next position for `0`
   - `mid` → current element being processed
   - `right` → next position for `2`
2. Traverse while `mid <= right`:
   - If `nums[mid] == 0`, swap `nums[left]` and `nums[mid]`, then increment both `left` and `mid`.
   - If `nums[mid] == 1`, increment `mid`.
   - If `nums[mid] == 2`, swap `nums[mid]` and `nums[right]`, then decrement `right`.
3. Continue until all elements are placed in their correct regions.

### Code

```java
class Solution {
    public void sortColors(int[] nums) {

        int left = 0;
        int mid = 0;
        int right = nums.length - 1;

        while (mid <= right) {

            if (nums[mid] == 0) {

                nums[mid] = nums[left];
                nums[left] = 0;

                left++;
                mid++;
            }
            else if (nums[mid] == 1) {

                mid++;
            }
            else {

                nums[mid] = nums[right];
                nums[right] = 2;

                right--;
            }
        }
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
