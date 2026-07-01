# Maximum Subarray Sum 

## Brute force :

for every element i, explore al the elements using j , traverse the subarray i to j add the sum. return the max sum

* this will trigger time limit exceeeded error.

### algorithm :

* run outer loop
* run inner lop j from i to n
* intialise the sum = 0
* run loop from i to j and add the sum
