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
