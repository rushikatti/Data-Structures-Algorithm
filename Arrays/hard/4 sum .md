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



### brute force code :

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;

        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                for(int k=j+1;k<n;k++){
                    for(int l=k+1;l<n;l++){
                        if(nums[i]+nums[j]+nums[k]+nums[l]==target){
                            List<Integer> temp = Arrays.asList(nums[i],nums[j],nums[k],nums[l]);
                            Collections.sort(temp);
                            set.add(temp);
                        }
                    }
                }
            }
            
        }
        return new ArrayList<>(set);
    }
}

```

### complexity :

* time : O(n^4)
* space : O(2 * no of quadrapules)


### Better Solution :
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;

        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                Set<Integer> seen = new HashSet<>();
                for(int k=j+1;k<n;k++){

                    long fourth = (long) target -nums[i]-nums[j]-nums[k];

                    if(seen.contains((int) fourth)){
                        List<Integer> temp = Arrays.asList(nums[i],nums[j],nums[k],(int) fourth);
                        Collections.sort(temp);
                        set.add(temp);
                    }

                    seen.add(nums[k]);
                }
            }
        }
        return new ArrayList<>(set);
    }
}
```

### complexity :

* time : O(n^3 + log(m))
* space : O(2 * no of quadrapules) + O(n)


### optimal Solution :

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;
        Arrays.sort(nums);
        for(int i=0;i<n;i++){
            if(i>0 && nums[i]==nums[i-1]) continue;
            for(int j=i+1;j<n;j++){
                if(j>i+1 && nums[j]==nums[j-1]) continue;

                int left = j+1 , right = n-1;

                while(left<right){
                    long sum =  nums[i] + nums[j];
                    sum += nums[left];
                    sum += nums[right];

                    if(sum < target){
                        left++;
                    }
                    else if(sum > target){
                        right--;
                    }
                    else{
                        List<Integer> temp = Arrays.asList(nums[i],nums[j],nums[left],nums[right]);
                        set.add(temp);
                        left++;
                        right--;

                        while (left < right && nums[left] == nums[left - 1]) left++;
                        while (left < right && nums[right] == nums[right + 1]) right--;

                        
                    }
                } 
                              
            }
        }
        return new ArrayList<>(set);
    }
}

```

### complexity :

* time : O(n^3)
* space : O(no of quadrapules)


