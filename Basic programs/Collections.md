## HashMap :

hashmap can store the values greater than 10^8, 
Map is better than array in terms of storing the frequency and fetching the element 
  
  for example :
  suppose we have an input like  arr = [2,5,2,6,4,34,78]
  in order to hash this in arr, we need arr of size arr[79],  but map can store the values like Key, value so it will store as 
  ```
  2 : 2
  4 : 1
  5 : 1
  6 : 1
  34 : 1
  78 : 1
  ```
 So TC will O(n), traverse the array once and SC will be O(n) storing n keys.


 ### Declaring the HashMap
 ```
 import java.util.HashMap;

HashMap<Integer, Integer> map = new HashMap<>();
```
we can also use:
```
HashMap<String, Integer> map = new HashMap<>();
```

### Inserting Values :

```
map.put(1, 10);
map.put(2, 20);
map.put(3, 30);
```

### Fetching the values :
```
System.out.println(map.get(1)); // 10
System.out.println(map.get(2)); // 20

```

### 🔹 containsKey() in HashMap

### Code
```java
import java.util.HashMap;

HashMap<Integer, Integer> map = new HashMap<>();

map.put(1, 10);
map.put(2, 20);

System.out.println(map.containsKey(1)); // true
System.out.println(map.containsKey(5)); // false
```

#### Meaning
```text
containsKey(x) → checks if key x exists in the map
```

#### Use in DSA
```java
if (!map.containsKey(num)) {
    map.put(num, 1);
}
```

---

### 🔹 Iterating a HashMap

#### Method 1: keySet()

```java
for (int key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}
```

---

#### Method 2: entrySet() (BEST WAY)

```java
for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

---

#### Output Format
```text
1 -> 10
2 -> 20
```

---

### 🔥 Quick Revision

```text
containsKey(k) → check if key exists

keySet()       → loop through keys
entrySet()     → loop through key-value pairs (best)
```

### example :

```java
import java.util.*;
class Solution {
    public void Frequency(int[] arr, int n){
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for(int i =0; i<n; i++){
            map.put(arr[i],map.getOrDefault(arr[i],0)+1);
        }
        
        for(Map.Entry<Integer,Integer> entry : map.entrySet()){
            System.out.println(entry.getKey()+" "+entry.getValue());
        }
    }
}
public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] arr = {1,2,3,1,12,31,2,2};
        int n = arr.length;
        sol.Frequency(arr,n);
        System.out.println("Start small. Ship something.");
    }
}
```
