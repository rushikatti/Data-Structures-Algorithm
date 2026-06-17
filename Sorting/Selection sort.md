## Selection Sort

In selection sort we need to find the min element and swap with first element in every iterations.

For every iteration the array size reduces. to swap min element with the first index of current array.
#### Algorithm :
* Run an outer loop from i = 0 to n -1 -- no need to traverse the last element
* intialize the minIdx variable and assigh the value i -- the first element
* Run an innner loop from j = i + 1 to n
* check the condition arr[j] < arr[minidx], If yes then minIdx = j  -- we got the min element idx
* Swap the elements
* ```
  temp = arr[minIdx];
  arr[minIdx] = arr[i];
  arr[i] = arr[minIdx];
  ```
* arr is sorted . print the arr

#### FLow :

```java
[64,25,12,22,11]
      │
      ├─ Pass 1: Min=11 at index 4
      ├─ Swap arr[0] ↔ arr[4]
      ▼
[11,25,12,22,64]
      │
      ├─ Pass 2: Min=12 at index 2
      ├─ Swap arr[1] ↔ arr[2]
      ▼
[11,12,25,22,64]
      │
      ├─ Pass 3: Min=22 at index 3
      ├─ Swap arr[2] ↔ arr[3]
      ▼
[11,12,22,25,64]
      │
      ├─ Pass 4: Min=25 at index 3
      ├─ No Swap
      ▼
[11,12,22,25,64]
      │
      ▼
    END
```


#### Code :
```java
class SelectionSort{
    public void selectionSort(int[] arr){
        int n = arr.length;
        for(int i = 0; i<n-1; i++){
            int minIdx = i;
            for(int j =i+1;j<n;j++){
                if(arr[j]<arr[minIdx]){
                    minIdx = j;
                }
            }
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
        for(int num : arr){
            System.out.print(num+" ");
        }
    }
}
```
