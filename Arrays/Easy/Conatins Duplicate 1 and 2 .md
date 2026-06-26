# Contains Duplicate Problems

## 217. Contains Duplicate



Given an integer array `nums`, return `true` if any value appears at least twice.



**HashSet**

* Stores only unique elements.
* If an element already exists, it is a duplicate.

###  Code

```java
import java.util.HashSet;

class Solution {
    public boolean containsDuplicate(int[] nums) {

        HashSet<Integer> set = new HashSet<>();

        for (int num : nums) {

            if (set.contains(num)) {
                return true;
            }

            set.add(num);
        }

        return false;
    }
}
```

### Complexity

* **Time:** O(n)
* **Space:** O(n)

---

# 219. Contains Duplicate II

### Problem

Given an integer array `nums` and an integer `k`, return `true` if there are two equal numbers whose index difference is at most `k`. 

Condition:

```
nums[i] == nums[j]
abs(i - j) <= k
```

**HashMap**

* **Key** → Number
* **Value** → Last index where the number appeared


A `HashSet` only tells whether a number exists.

This problem also requires knowing **where** the number was previously seen to calculate:

```
abs(i - previousIndex)
```

Therefore, we store the latest index of each number.

### Algorithm

1. Create a `HashMap`.
2. Traverse the array.
3. If the current number already exists:

   * Get its previous index.
   * If `currentIndex - previousIndex <= k`, return `true`.
4. Update the current number's index in the map.
5. If traversal completes, return `false`.

### Java Code

```java
import java.util.HashMap;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {

        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {

            if (map.containsKey(nums[i])) {

                int previousIndex = map.get(nums[i]);

                if (i - previousIndex <= k) {
                    return true;
                }
            }

            map.put(nums[i], i);
        }

        return false;
    }
}
```

### Complexity

* **Time:** O(n)
* **Space:** O(n)

---


## Rule to Remember

* **Need to know if a value exists?** → `HashSet`
* **Need to know where a value exists?** → `HashMap<Value, Index>`
* **Need frequency/count of values?** → `HashMap<Value, Count>`
