## Longest subarray with sum k :

#### Bruteforce :
```
We can solve using the 3 loops 
* one outer loop
* one inner loop
* one loop to count the sum of inner loop
```
```java
import java.util.*;

class Solution {

    public int longestSubarray(int[] nums, int k) {
        int n = nums.length;
        int maxLength = 0;

        // starting index
        for (int startIndex = 0; startIndex < n; startIndex++) {
            // ending index
            for (int endIndex = startIndex; endIndex < n; endIndex++) {

                /* add all the elements of
                   subarray = nums[startIndex...endIndex] */
                int currentSum = 0;
                for (int i = startIndex; i <= endIndex; i++) {
                    currentSum += nums[i];
                }

                if (currentSum == k) {
                    maxLength = Math.max(maxLength, endIndex - startIndex + 1);
                }
            }
        }
        return maxLength;

    }
}
```
* Time Complexity: O(n3), where n is the size of the array. This is because we have three nested loops: one for the starting index, one for the ending index, and one for calculating the sum of the subarray.

* Space Complexity: O(1), as we are using a constant amount of space for variables and not using any additional data structures that grow with input size.

## Better Solution : 

#### Data Structure

* **HashMap<Integer, Integer>**

  * **Key** → Prefix Sum
  * **Value** → First index of that prefix sum

---

### Logic

* Calculate the running prefix sum.
* If `sum == k`, the subarray from index `0` to `i` has sum `k`.
* Check if `sum - k` exists in the map.
* If it exists, update the maximum length.
* Store the prefix sum only if it is not already present.

---

### Java Code

```java
HashMap<Integer, Integer> map = new HashMap<>();

int sum = 0;
int maxLength = 0;

for (int i = 0; i < arr.length; i++) {

    sum += arr[i];

    if (sum == k) {
        maxLength = i + 1;
    }

    if (map.containsKey(sum - k)) {
        maxLength = Math.max(maxLength, i - map.get(sum - k));
    }

    if (!map.containsKey(sum)) {
        map.put(sum, i);
    }
}

return maxLength;
```

---

### Complexity

* **Time:** `O(n)`
* **Space:** `O(n)`

---

#### Quick Notes

**Why `sum == k`?**
→ Subarray from index `0` to `i` has sum `k`.

**Why `sum - k`?**
→ `Current Prefix Sum - Previous Prefix Sum = k`.

**Why store only the first occurrence?**
→ It gives the longest possible subarray.

**For Sum = 0:**
→ Check `sum == 0` and `map.containsKey(sum)`.

**For Sum = K:**
→ Check `sum == k` and `map.containsKey(sum - k)`.


## Optimal Solution :

* useing the left and right pointer, and calculation the sum

#### code :
```java
import java.util.*;

// Class containing the sliding window algorithm
class Solution {
    public int longestSubarray(int[] nums, int k) {
        int n = nums.length;

        // To store the maximum length of the subarray
        int maxLen = 0;

        // Pointers for sliding window
        int left = 0, right = 0;

        // Sum of the current window
        int sum = nums[0];

        // Traverse through the array
        while (right < n) {

            // Shrink the window if sum exceeds k
            while (left <= right && sum > k) {
                sum -= nums[left];
                left++;
            }

            // Update max length if sum equals k
            if (sum == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }

            // Expand the window to the right
            right++;
            if (right < n) {
                sum += nums[right];
            }
        }

        return maxLen;
    }
}
```
* Time Complexity: O(N), where N is the size of the array. The algorithm traverses the array once with two pointers, making it linear in time complexity.

* Space Complexity: O(1), as it uses a constant amount of space.

