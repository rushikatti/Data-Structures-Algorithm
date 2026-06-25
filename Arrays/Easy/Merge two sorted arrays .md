### 88. Merge Sorted Array

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

### Bruteforce
```
Idea
Create a new array.
Copy all m elements from nums1.
Copy all n elements from nums2.
Sort the new array.
Copy it back to nums1.
```
* code :
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int[] temp = new int[m + n];

        int index = 0;

        // Copy nums1
        for (int i = 0; i < m; i++) {
            temp[index++] = nums1[i];
        }

        // Copy nums2
        for (int i = 0; i < n; i++) {
            temp[index++] = nums2[i];
        }

        // Sort
        java.util.Arrays.sort(temp);

        // Copy back
        for (int i = 0; i < m + n; i++) {
            nums1[i] = temp[i];
        }
    }
}
```

### Optimal solution :

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {

            if (nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            } else {
                nums1[k] = nums2[j];
                j--;
            }

            k--;
        }

        // Copy remaining elements from nums2
        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }
}
```
