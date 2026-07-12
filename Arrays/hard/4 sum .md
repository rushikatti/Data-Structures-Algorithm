# 4 SUM :

* similar to 3 sum.
  
## Brute force :

* Run 4 loops, i with 0, j with i+1, k with j+1. l eith k+1
* add i+j+k+l == 0, store them in temp List
* sort the temp list before adding to the Set<List<>>
* return new ArrayList<>(Set). 


## better approach :

* run 3 loops, i with 0, j with i+1, k ith j+1.
* calculate fourth element = target -(nums[i] + nums[j] + nums[k),
* check fourth in HASHSET if found , add i , j, k, fourth to temp LIST , and sort it before adding to Set.
* return new ArrayList<>(Set).


## optimal solution :

* use two pointer approach, and sort the array first.
* place pointer i at 0, j at 1,  left at j+1, right at n-1
* for every i, j calculate sum = nums[i] + nums[j] + nums[left] + nums[right]
* if sum < 0 , left++ increase the value to make sum 0
* else if sum > 0 , right-- decrease the value to make sum 0
* else sum =0, this willl be the quadrapule, add to temp list and add to ans list

  
