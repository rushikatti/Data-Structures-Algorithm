# Rearrange Array Elements by Sign

## Bruteforce :

save positive elements in one and negative elements in another array and fill the ans array in alternating positions

### algorithm :

* initialise the positive array, negative array
* traverse the given array and check if (nums[i] >0) then positive.add(nums[i]), if(nums[i]<0) then negative.add(nums[i]).
* run an another loop from i =0 to i= n/2
* fill arr[2*i] = positive.get(i),  arr[2*i+1] = positive.get(i)
* return arr

### code :
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {

        int n = nums.length;

        ArrayList<Integer> positive = new ArrayList<>();

        ArrayList<Integer> negative = new ArrayList<>();

        for(int i=0;i<n;i++){
            if(nums[i]>0){
                positive.add(nums[i]);
            }else{
                negative.add(nums[i]);
            }
        }

        for(int i=0;i<n/2;i++){
            nums[2*i] = positive.get(i);
            nums[2*i+1] = negative.get(i);       
            }
        return nums;
        
    }
}
```

### complexity :

* Time complexity : O(n) + O(n) --> O(2n)
