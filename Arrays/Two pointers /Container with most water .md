# 11. Container With Most Water

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `maxArea = 0`.
2. Traverse every possible pair of lines using two nested loops.
3. For each pair:
   - Calculate the height as the minimum of the two heights.
   - Calculate the width as the distance between the indices.
   - Compute the area.
4. Update the maximum area if the current area is larger.
5. Return the maximum area.

### Code

```java
class Solution {
    public int maxArea(int[] height) {

        int maxArea = 0;

        for (int i = 0; i < height.length - 1; i++) {

            for (int j = i + 1; j < height.length; j++) {

                int h = Math.min(height[i], height[j]);
                int w = j - i;

                int area = h * w;

                maxArea = Math.max(maxArea, area);
            }
        }

        return maxArea;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Two Pointers)

### Algorithm

1. Initialize two pointers:
   - `left = 0`
   - `right = n - 1`
2. While `left < right`:
   - Compute the height as the minimum of the two heights.
   - Compute the width as `right - left`.
   - Calculate the current area.
   - Update the maximum area.
3. Move the pointer pointing to the shorter line:
   - If `height[left] <= height[right]`, increment `left`.
   - Otherwise, decrement `right`.
4. Return the maximum area.

### Code

```java
class Solution {
    public int maxArea(int[] height) {

        int left = 0;
        int right = height.length - 1;

        int maxArea = 0;

        while (left < right) {

            int h = Math.min(height[left], height[right]);
            int w = right - left;

            int area = h * w;

            maxArea = Math.max(maxArea, area);

            if (height[left] <= height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
