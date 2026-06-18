## Insertion Sort :

Here we take one element as KEY and compare with all the previous elements. if there is larger element present in the previous, we move that element to the right and insert the KEY into the currect position.

#### Algorithm :
* Run outer loop from i =1 to i < n ,           ----> started with 1 because to compare previous element.
* intialise the KEY = arr[i].  j = i -1.
* run inner while loop( j >= 0 && arr[j] > key)
* if true,  move the arr[j] to right , i,e arr[j+1] = arr[j]. and J-- to check all the previous elements.
* Insert key into the currect position. i,e  arr[j+1] = key.
* Arr is Sorted.

#### Flow :
```java
[8,5,3,2]

i=1, key=5
[8,8,3,2]      (shift 8)
[5,8,3,2]      (insert 5)

i=2, key=3
[5,8,8,2]      (shift 8)
[5,5,8,2]      (shift 5)
[3,5,8,2]      (insert 3)

i=3, key=2
[3,5,8,8]      (shift 8)
[3,5,5,8]      (shift 5)
[3,3,5,8]      (shift 3)
[2,3,5,8]      (insert 2)

Sorted
```

#### code :

```java
class InsertionSort{
    public void insertionSort(int[] nums){
        int n = nums.length;
        for(int i=1;i<n;i++){
            int key = nums[i];                                        TC : O(n²)
            int j = i-1;                                              SC : O(1)  
            while(j>=0 && nums[j]>key){
                nums[j+1] = nums[j];
                j--;                
            }
            nums[j+1] = key;
        }
        for(int num : nums){
            System.out.print(num+" ");
        
        }        
    }
}
```
* Space Complexity will be O(1), becuase we are sorting the array in place and not using any additional data structures that grow with input size.
