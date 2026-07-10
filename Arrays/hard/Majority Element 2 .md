* problem : return the majority element which appeared more than n/3 times.

## bruteforce :

* run 2 loops and count each element . if the count is > n/3 and ans list does not have the num. update the ans list with that num.

## Better Solution :

* store the freq of elements in Hashmap,  after storing in the same loop check freq of element.
* if it is greater than n/3 + 1 and ans does not contain the element, add the element to the ans List.
* after adding to ans, check size of the ans if it is = 2 then break the loop,   

### bruteforce  code :

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {

        List<Integer> ans = new ArrayList<>();

        for(int i=0;i<nums.length;i++){
            int count = 0;
            for(int j=0;j<nums.length;j++){
                if(nums[j]==nums[i]){
                    count++;
                }
            }
            if(count > nums.length/3 && !ans.contains(nums[i])){
                ans.add(nums[i]);
            }
        }return ans;
        
    }
}
```

### Complexity :

* time complexity : O(n^2)
* space complexity : O(1)


### Better code :

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {

       List<Integer> ans = new ArrayList<>();

       HashMap<Integer,Integer> map = new HashMap<>();

       int min = (nums.length/3) + 1;

       for(int i=0;i<nums.length;i++){
        map.put(nums[i],map.getOrDefault(nums[i],0)+1);

        if(map.get(nums[i]) >= min && !ans.contains(nums[i])){
            ans.add(nums[i]);
        }

        if(ans.size()==2){
            break;
        }

       }


    return ans;

    }
}
```

### Complexity :

* time complexity : O(n) + o(log n)
* space complexity : O(n)
