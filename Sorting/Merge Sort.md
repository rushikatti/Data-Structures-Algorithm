## Merge Sort :
Merge sort divides the array recursuvely into the equal halfs untill single element found, then compare the single elements and return with sorted array.

Time Complexity: O(N*logN), merging two arrays take linear time and array is recursively divided into halves (logN times).

Space Complexity: O(N), we use a temporary array to store elements in sorted order.
```
                [4 2 7 1 5 3]
                   /       \
            [4 2 7]       [1 5 3]
            /    \         /    \
        [4 2]   [7]    [1 5]   [3]
        /  \             /  \
      [4] [2]         [1] [5]
```                                        
