# 350. Intersection of Two Arrays II

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order. 

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

### Data Structure

* **HashMap<Integer, Integer>** → Stores **number → frequency**.

### Why HashMap?

* **Duplicates matter, so we need the frequency of each number.**

### Algorithm

1. Store frequencies of `nums1` in a `HashMap`.
2. Traverse `nums2`.
3. If frequency > 0, add the number to the answer and decrement its count.
4. Return the answer.

### Java Code

```java
HashMap<Integer, Integer> map = new HashMap<>();

for (int num : nums1) {
    map.put(num, map.getOrDefault(num, 0) + 1);
}

List<Integer> list = new ArrayList<>();

for (int num : nums2) {
    if (map.containsKey(num) && map.get(num) > 0) {
        list.add(num);
        map.put(num, map.get(num) - 1);
    }
}

int[] ans = new int[list.size()];
for (int i = 0; i < list.size(); i++) {
    ans[i] = list.get(i);
}

return ans;
```

### Complexity

* **Time:** `O(n + m)`
* **Space:** `O(n)`

---

## Quick Clarifications

**Q1. Why not HashSet?**
→ `HashSet` stores only unique elements, but this problem needs frequencies.

**Q2. Why use `List<Integer>`?**
→ The answer size is unknown until all elements are processed.

**Q3. Why can't we return the `List`?**
→ The method return type is `int[]`, not `List<Integer>`.

**Q4. Can we avoid `List`?**
→ Yes, use an array of size `min(nums1.length, nums2.length)` and return `Arrays.copyOf(ans, index)`.

