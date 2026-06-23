### Single number :

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## bruteforce :
* Approach
First, we will run a loop to select the elements of the array one by one.
For every element of the array, we will perform a linear search using another loop and count its occurrence.
If for any element the occurrence is 1, we will return it.
```java
class Solution {
    // Function to find the single element using brute force
    public int getSingleElement(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            int num = arr[i];
            int count = 0;

            // Count how many times num occurs
            for (int j = 0; j < n; j++) {
                if (arr[j] == num)
                    count++;
            }

            // If only once, return it
            if (count == 1) return num;
        }

        return -1; // fallback, won't be hit if array has a single element
    }

```
Time Complexity: O(N*N), since nested for loops are used

Space Complexity: O(1). No extra space used

* we can also do it using the hashMap, hashArray.

### Optimised solution :

```
class Solution {
    // Function to find the element that appears once using XOR
    public int getSingleElement(int[] arr) {
        int xorr = 0;

        // XOR all elements — duplicates cancel each other out
        for (int num : arr) {
            xorr ^= num;
        }

        return xorr;
    }
```

2 ^ 2 = 0, 1 ^ 0 = 1

Time Complexity: O(N). Where N is the size of the array

Space Complexity: O(1). No extra space used

