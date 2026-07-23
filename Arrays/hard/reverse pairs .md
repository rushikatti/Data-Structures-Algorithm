````md id="f8k2wx"
# 493. Reverse Pairs

## Brute Force Solution

### Approach

- Iterate through every possible pair `(i, j)` where `i < j`.
- Check whether `nums[i] > 2 * nums[j]`.
- If the condition is satisfied, increment the count.
- Return the total number of reverse pairs.

### Code

```java
class Solution {

    public int reversePairs(int[] nums) {

        int count = 0;

        for (int i = 0; i < nums.length; i++) {

            for (int j = i + 1; j < nums.length; j++) {

                if ((long) nums[i] > 2L * nums[j]) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

### Complexity

- **Time:** O(n²)
- **Space:** O(1)

---

## Optimal Solution (Merge Sort)

### Approach

- Use Merge Sort to divide the array into two sorted halves.
- Before merging the two halves:
  - Count reverse pairs using two pointers.
  - For every element in the left half, move a pointer in the right half while `nums[i] > 2 * nums[j]`.
  - Since both halves are sorted, all remaining elements before `j` also satisfy the condition.
- Merge the two sorted halves.
- Sum the counts from the left half, right half, and cross pairs.

### Code

```java
class Solution {

    public int reversePairs(int[] nums) {
        return mergeSort(nums, 0, nums.length - 1);
    }

    private int mergeSort(int[] nums, int low, int high) {

        if (low >= high)
            return 0;

        int mid = low + (high - low) / 2;

        int count = mergeSort(nums, low, mid);
        count += mergeSort(nums, mid + 1, high);
        count += countPairs(nums, low, mid, high);

        merge(nums, low, mid, high);

        return count;
    }

    private int countPairs(int[] nums, int low, int mid, int high) {

        int count = 0;
        int right = mid + 1;

        for (int left = low; left <= mid; left++) {

            while (right <= high &&
                   (long) nums[left] > 2L * nums[right]) {
                right++;
            }

            count += right - (mid + 1);
        }

        return count;
    }

    private void merge(int[] nums, int low, int mid, int high) {

        ArrayList<Integer> temp = new ArrayList<>();

        int left = low;
        int right = mid + 1;

        while (left <= mid && right <= high) {

            if (nums[left] <= nums[right]) {
                temp.add(nums[left++]);
            } else {
                temp.add(nums[right++]);
            }
        }

        while (left <= mid)
            temp.add(nums[left++]);

        while (right <= high)
            temp.add(nums[right++]);

        for (int i = low; i <= high; i++) {
            nums[i] = temp.get(i - low);
        }
    }
}
```

### Complexity

- **Time:** O(n log n)
- **Space:** O(n)
````

**Note:** Unlike many problems, there is **no valid "better" solution** between the brute force `O(n²)` approach and the merge sort `O(n log n)` solution. The merge sort approach is the expected optimal solution in interviews.
