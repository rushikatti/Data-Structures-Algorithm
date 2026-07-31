# 42. Trapping Rain Water

## Solution Approach 1: Brute Force

### Algorithm

1. Initialize `water = 0`.
2. For every index `i`:
   - Find the maximum height on the left of `i` (including `i`).
   - Find the maximum height on the right of `i` (including `i`).
   - The water trapped at `i` is:
     ```
     min(leftMax, rightMax) - height[i]
     ```
3. Add the trapped water at every index.
4. Return the total trapped water.

### Code

```java
class Solution {
    public int trap(int[] height) {

        int n = height.length;
        int water = 0;

        for (int i = 0; i < n; i++) {

            int leftMax = 0;
            int rightMax = 0;

            for (int j = 0; j <= i; j++) {
                leftMax = Math.max(leftMax, height[j]);
            }

            for (int j = i; j < n; j++) {
                rightMax = Math.max(rightMax, height[j]);
            }

            water += Math.min(leftMax, rightMax) - height[i];
        }

        return water;
    }
}
```

### Complexity

- **Time:** `O(n²)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Two Pointers)

### Algorithm

1. Initialize:
   - `left = 0`
   - `right = n - 1`
   - `leftMax = height[left]`
   - `rightMax = height[right]`
2. While `left < right`:
   - If `leftMax < rightMax`:
     - Move `left` one step forward.
     - Update `leftMax`.
     - Add `leftMax - height[left]` to the answer.
   - Otherwise:
     - Move `right` one step backward.
     - Update `rightMax`.
     - Add `rightMax - height[right]` to the answer.
3. Return the total trapped water.

### Code

```java
class Solution {
    public int trap(int[] height) {

        int n = height.length;
        int water = 0;

        int left = 0;
        int right = n - 1;

        int leftMax = height[left];
        int rightMax = height[right];

        while (left < right) {

            if (leftMax < rightMax) {

                left++;

                leftMax = Math.max(leftMax, height[left]);

                water += leftMax - height[left];
            }
            else {

                right--;

                rightMax = Math.max(rightMax, height[right]);

                water += rightMax - height[right];
            }
        }

        return water;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`
