
# 228. Summary Ranges (Easy)

## Approach 1: Brute Force

### Idea

For every element:

- Start a new range.
- Keep checking the next elements until the consecutive sequence ends.
- Store the range.
- Continue from the next unused element.

Although this is called brute force, each element is still visited only once because the index jumps to the end of the current range.

---

### Algorithm

1. Initialize `i = 0`.
2. Let `start = nums[i]`.
3. Move `j` while:


nums[j + 1] == nums[j] + 1


4. If

```
start == nums[j]
```

store

```
start
```

otherwise store

```
start->nums[j]
```

5. Continue from `j + 1`.

---

### Code (Java)

```java
class Solution {

    public List<String> summaryRanges(int[] nums) {

        List<String> ans = new ArrayList<>();

        int n = nums.length;

        int i = 0;

        while (i < n) {

            int start = nums[i];

            int j = i;

            while (j + 1 < n &&
                    nums[j + 1] == nums[j] + 1) {

                j++;
            }

            if (start == nums[j])
                ans.add(String.valueOf(start));
            else
                ans.add(start + "->" + nums[j]);

            i = j + 1;
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)` (excluding output)

---

# Approach 2: Better (Single Pass)

### Idea

Instead of using two pointers (`i` and `j`),

maintain the start of the current range.

Whenever the consecutive sequence breaks,

store the current range and start a new one.

This uses only one traversal.

---

### Algorithm

1. Start a range from the first element.
2. Traverse the array.
3. If the next element is **not consecutive**,
   - Store the current range.
   - Start a new range.
4. After the loop, store the last range.

---

### Code (Java)

```java
class Solution {

    public List<String> summaryRanges(int[] nums) {

        List<String> ans = new ArrayList<>();

        if (nums.length == 0)
            return ans;

        int start = nums[0];

        for (int i = 1; i < nums.length; i++) {

            if (nums[i] != nums[i - 1] + 1) {

                if (start == nums[i - 1])
                    ans.add(String.valueOf(start));
                else
                    ans.add(start + "->" + nums[i - 1]);

                start = nums[i];
            }
        }

        if (start == nums[nums.length - 1])
            ans.add(String.valueOf(start));
        else
            ans.add(start + "->" + nums[nums.length - 1]);

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)` (excluding output)

---

# Approach 3: Optimal (Two Pointers)

## Idea

Use two pointers:

- `start` → beginning of the current range.
- `end` → extend while numbers remain consecutive.

Whenever the sequence breaks:

- Output the range.
- Move both pointers to the next range.

This is the cleanest and most intuitive solution.

---

### Algorithm

1. Set `start = 0`.
2. Expand `end` while consecutive numbers exist.
3. Output:
   - Single number if `start == end`.
   - Otherwise `"start->end"`.
4. Move to the next range.

---

### Code (Java)

```java
class Solution {

    public List<String> summaryRanges(int[] nums) {

        List<String> ans = new ArrayList<>();

        int n = nums.length;

        int start = 0;

        while (start < n) {

            int end = start;

            while (end + 1 < n &&
                    nums[end + 1] == nums[end] + 1) {

                end++;
            }

            if (start == end)
                ans.add(String.valueOf(nums[start]));
            else
                ans.add(nums[start] + "->" + nums[end]);

            start = end + 1;
        }

        return ans;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)` (excluding output)

---

# Summary

| Approach | Idea | Time | Space |
|----------|------|------|-------|
| Brute Force | Expand each range using nested loop | `O(n)` | `O(1)` |
| Better | Single-pass traversal with current range start | `O(n)` | `O(1)` |
| Optimal | Two pointers to identify consecutive ranges | `O(n)` | `O(1)` |
