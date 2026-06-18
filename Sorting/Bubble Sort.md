## Bubble Sort:
It pushes the Max element to the last by adjecent swapping.

The size of the array reduced every iteration from the end side. and the outer loop runs like.
 ```
            0-n-1
            0-n-2                           for(int i = n-1; i>= 1 ; i--)
            0-n-3
            0-n-4
            .
            .
            0 - 1     -->  need two element to compare
```


#### Algorithm :

* Run outer loop from n-1 to 1
* Run inner loop from 0 to i-1 --> we have skip the last element of current iteration becuase it does not have next element to compare.
* compare adjecents,   arr[j] > arr[j+1],
* if true, store the smaller one i,e arr[j+1] in temp variable
* swap the variable to farward the bigger the element
```
temp = arr[j+1];
arr[j+1] = arr[j];
arr[j] = temp;
```
* array is sorted.


####  Flow :
``` java
Initial
[5, 1, 4, 2, 8]                                       1 teration flow

5 > 1 ? ──Yes──► Swap
[1, 5, 4, 2, 8]

5 > 4 ? ──Yes──► Swap
[1, 4, 5, 2, 8]

5 > 2 ? ──Yes──► Swap
[1, 4, 2, 5, 8]

5 > 8 ? ──No──► No Swap
[1, 4, 2, 5, 8]

Pass 1 Complete ──► 8 Fixed at End
```


#### Code
``` java
class BubbleSort {
    public void bubbleSort(int[] arr){
        int n = arr.length;
        for(int i = n-1; i>=1; i--){
            for(int j = 0; j<=i-1;j++){                             TC = O(n²)
                if(arr[j]>arr[j+1]){
                    int temp = arr[j+1];
                    arr[j+1] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        for(int num : arr){
            System.out.print(num+" ");
        }
    }
    
}
```

If Array is already sorted then also it take TC :  O(n²).   
So this Optimal Solution takes O(n) for sorted input.
``` java
class BubbleSort {
    public void bubbleSort(int[] arr){
        int n = arr.length;                                                        
        for(int i = n-1; i>=1; i--){
            int sorted = 0;                     ------ >  variable 
            for(int j = 0; j<=i-1;j++){
                if(arr[j]>arr[j+1]){
                    int temp = arr[j+1];
                    arr[j+1] = arr[j];
                    arr[j] = temp;
                    sorted = 1;                ---------> update if swapped
                }
            }
            if(sorted == 0){                  -------> if nothing swapped in 1st iteration, 
                break;                                 then it is already sorted.
            }
        }
        for(int num : arr){
            System.out.print(num+" ");
        }
    }
    
}
```
