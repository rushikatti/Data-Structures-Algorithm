## Merge Sort :
Merge sort divides the array recursuvely into the equal halfs untill single element found, then compare the single elements and return with sorted array.

Time Complexity: O(N*logN), merging two arrays take linear time and array is recursively divided into halves (logN times).

Space Complexity: O(N), we use a temporary array to store elements in sorted order.

* divide :
```
                [4 2 7 1 5 3]
                   /       \
            [4 2 7]       [1 5 3]
            /    \         /    \
        [4 2]   [7]    [1 5]   [3]
        /  \             /  \
      [4] [2]         [1] [5]
```

* Merge :
```
         [4]   [2]                    [1]   [5]
           \   /                        \   /
          [2,4]                       [1,5]
             \                         /  \
              \                       /    \
             [2,4,7]             [1,3,5]
                    \           /
                     \         /
                 [1,2,3,4,5,7]
```


#### Algorithm :
* If the array has only one or zero elements, it is already sorted, so we return it as is.
* Else, we divide the array into two halves by finding the middle index.
* we then apply the merge sort algorithm recursively on each of the two halves to sort them individually.
Once we have two sorted halves, we need to merge them into a single sorted array.
* To merge, we compare elements from both halves one by one and place the smaller element into a new array, continuing this until all elements from both halves are used.
* This process is repeated at every level of recursion, and finally, we get one fully sorted array after all merges are complete.

#### Code :

```java
import java.util.*;
class Solution{
    public void merge(int[] arr, int low, int mid, int high){
        List<Integer> temp = new ArrayList<>();
        int left = low, right = mid + 1;
        
        while(left<=mid && right<=high){
            if(arr[left]<arr[right]){                        ----> while loop runs until the elements become empty either
                temp.add(arr[left++]);                                in left or right halfs.
            }else{                                               check element from both halfs and place them in temp array
                temp.add(arr[right++]);
            }          
        }
        while(left<=mid){
            temp.add(arr[left++]);                            -----> if any element remains in left part
        }
        while(right<=high){                                   -----> if any element remains in right part
            temp.add(arr[right++]);
        }
        for(int i = low;i<=high;i++){                         ---> copy the temp array to original array
            arr[i] = temp.get(i-low);
        }
    }
    public void mergeSort(int[] arr, int low, int high){
    if(low>=high){
        return;                                         ----> this base cases will return once the recursion
    }                                                         reaches the single element.
    int mid = (low + high)/2;
    
    mergeSort(arr,low,mid);
    mergeSort(arr,mid+1,high);
    merge(arr,low,mid,high);
    
    }
    
}
```
