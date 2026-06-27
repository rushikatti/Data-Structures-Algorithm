## 3105. Longest Strictly Increasing or Strictly Decreasing Subarray

## Approach

Maintain two counters:

* `increasing` → Current increasing subarray length.
* `decreasing` → Current decreasing subarray length.

### Logic

* `nums[i] > nums[i-1]` → `increasing++`, `decreasing = 1`
* `nums[i] < nums[i-1]` → `decreasing++`, `increasing = 1`
* `nums[i] == nums[i-1]` → Reset both to `1`
* Update `maxLength` after each iteration.

---

## Code

```java id="9g3fjc"
class Solution {
    public int longestMonotonicSubarray(int[] nums) {

        int increasing = 1;
        int decreasing = 1;
        int maxlength = 1;

        for(int i=1;i<nums.length;i++){
            if(nums[i] > nums[i-1]){
                increasing++;
                decreasing = 1;
            }
            else if(nums[i]<nums[i-1]){
                decreasing++;
                increasing = 1;
            }
            else{
                decreasing =1;
                increasing = 1;

            }
            maxlength = Math.max(maxlength,Math.max(increasing,decreasing));
        }

        return maxlength;
    }
}
```



## Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`



## Key Points

#### Why reset to `1`?

The current element starts a new subarray.

#### Why start from `i = 1`?

To safely compare `nums[i]` with `nums[i-1]`.

### Pattern

* Increase → `inc++`, `dec = 1`
* Decrease → `dec++`, `inc = 1`
* Equal → `inc = dec = 1`

