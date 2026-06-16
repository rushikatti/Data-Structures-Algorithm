                                                                     

## Why hashing : 

So, if i want to find how many times does 2, 3, 5, occured in the following array [2,6,7,3,3,4,5,5,3,2,5]
I have to run the for loop like this
count = 0
for(int i = 0;i<n:i++){
  if(arr[i] == 2){
  count += 1
  }
}
return count

but this take the  TC O(n)  to find one element in the array,   if we want to find all targets once then TC will be  O(q * n).

if the array size is 10^5 and target size is 10^5, then TC will be O(10^5 * 10^5) = O(10^10).  

but to excuete the code of 10 ^ 8 , will take 1 sec. then 10 ^ 10  will take 100 seconds.. which is inefficnet so the Hashing will be helpfull here


## How to do Hashing :

### Integer Hashing :
```
  1) pre compute
  2) fetch
```               

we need to precompute the array to store the count of elements in hash.

arr [2,6,7,3,3,4,5,5,3,2,5]       hash store the count of the values starting from the 0
so if length of arr is 11, hash will store 12 element counts

like    hash [0,1,2,3,4,5,6,7,8,9,10,11,12]  these are the index and hash will store the count of that index in the arr.
like   hash[arr] = [0,0,2,3,1,3,1,1,0,0,0,0,0]

> pre compute  :

   ```
   int[] hash = new int[13];
   for (int i = 0; i < n; i++) {
   hash[arr[i]] += 1;
   }
   ```

   this can store the value upto  10 ^ 6 for int ,  10 ^ 7 for the boolean  - if declared in main function
   if the hash declared as globally outside the fuction, int can store upto 10^7 , and bollean 10 ^ 8


> Fetch :
```
System.out.println(hash[number]);
```

where the number is input query we give to fetch the count of that number in th arr.



* Charecter hashing :

 it is same as the integer hashing but use the ASCII (American Standard Code for Information Interchange)
 
