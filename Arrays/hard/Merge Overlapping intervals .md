# LeetCode 56 - Merge Intervals

## Approach 1: Brute Force

1. Sort the intervals based on their starting time.
2. Traverse each interval one by one.
3. For every interval, compare it with the following intervals.
4. If the next interval overlaps (`nextStart <= currentEnd`), merge them by updating the ending time.
5. Continue merging until there is no overlap.
6. Add the merged interval to the answer.
7. Repeat the process for all remaining intervals.


# Approach 2: Optimal (Single Pass)

1. Sort the intervals based on their starting time.
2. Create an empty list to store the merged intervals.
3. Traverse the sorted intervals.
4. If the answer list is empty or the current interval does not overlap with the last merged interval, add it directly.
5. Otherwise, merge the intervals by updating the ending time of the last interval to the maximum ending value.
6. Continue until all intervals are processed.
7. Return the merged intervals.

### Bruetforce code :

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        
        Arrays.sort(intervals, (a,b) -> Integer.compare(a[0],b[0]));

  
        List<int[]> ans = new ArrayList<>();
      
        for(int[] interval : intervals){
            if(ans.isEmpty() || ans.get(ans.size()-1).get(1) < interval[0]){
                ans.add(Arrays.asList(interval[0],interval[1]));
            }
            else{
                int last = ans.size()-1;
                int maxEnd = Math.max(ans.get(last).get(1),interval[1]);
                ans.get(last).set(1,maxEnd);
            }

        }

        return ans.toArray(new int[ans.size()][]);
    }
}
```
###  Complexity :

* time :
- O(n log n) for sorting
- O(n) for traversal
- Overall: O(n log n)

* Space Complexity :  O(n) (for storing the merged intervals)

### Optimal code :

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        
        Arrays.sort(intervals, (a,b) -> Integer.compare(a[0],b[0]));

  
        List<int[]> ans = new ArrayList<>();
      
        for(int[] interval : intervals){
            if(ans.isEmpty() || ans.get(ans.size()-1)[1] < interval[0]){
                ans.add(new int[]{interval[0], interval[1]});
            }
            else{
                int last = ans.size() - 1;
                ans.get(last)[1] = Math.max(ans.get(last)[1], interval[1]);
            }

        }

       return ans.toArray(new int[ans.size()][]);
    }
}
```




### Complexity

* time complexity :
- O(n log n) for sorting
- O(n) for single traversal
- Overall: O(n log n)

* Space Complexity - O(n) (for storing the merged intervals)


---

## Difference Between the Two Approaches

| Brute Force | Optimal |
|-------------|---------|
| Explicitly checks and merges consecutive overlapping intervals using nested progression. | Maintains the last merged interval and updates it whenever an overlap occurs. |
| Slightly more complex due to nested merging logic. | Simpler and more intuitive after sorting. |
| O(n log n) overall. | O(n log n) overall. |
| Good for understanding the merging process. | Preferred in interviews and production code. |
