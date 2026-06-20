## Quick Sort :

In quick we pick an pivot element and place it into its correct position. and that position is called Partition index.

we swap other smaller elements to left of the partition index and larger elements to the right of partition index.

* Time Complexity  :  O ( n * log n),     becuase it divides the array n times, and swapping will take n number of steps.
* Space Complexity : O ( n )    it n spaces to store the partial arrays.

```
                    Array
                      |
                    Pivot
                   /     \
          Smaller Elements  Larger Elements
                /               \
             Pivot             Pivot
             /  \              /  \
           ...  ...          ...  ...
```

#### Algorithm :

* select an pivot element from array.
* Rearrange the array like smaller one to left and larger to right.
* After partitioning, the pivot is in its correct sorted position.
* Recursively apply the same process to the subarrays on the left and right of the pivot.
* Base condition for recursion is when the subarray has zero or one element, as it's already sorted.
* Combine the results of the recursive calls to obtain the fully sorted array.

#### Flow :
```java
Initial Array
[5,3,8,4,2,7]

Pivot = 5
Smaller = [3,4,2]
Larger  = [8,7]

                                    [5,3,8,4,2,7]
                                          |
                             Pivot = 5 (first element)
                                          |
                     ------------------------------------------------
                     |                                              |
         Smaller than 5                                   Greater than 5
           [3,4,2]                                            [8,7]
               |                                                 |
         Pivot = 3                                         Pivot = 8
               |                                                 |
        -----------------                               -----------------
        |               |                               |               |
     [2]             [4]                            [7]              []
     <3              >3                             <8              >8
        |               |                             |               |
      Sorted         Sorted                        Sorted          Sorted


Leaf Nodes:
[2]   [4]   [7]

Build Back Up:

            [2] + [3] + [4]
                  =
               [2,3,4]

            [7] + [8] + []
                  =
                [7,8]

Final Merge:

      [2,3,4] + [5] + [7,8]

                  =
          [2,3,4,5,7,8]
```

#### Code

