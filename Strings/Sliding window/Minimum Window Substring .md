```md
# Minimum Window Substring (LeetCode 76)

---

## 1. Brute Force (Your First Approach)

### Approach
- Create frequency map `map1` for string `t`
- For every index `i` in `s`:
  - Create a new map `map2`
  - Expand `j` from `i → n-1`
  - Add characters to `map2`
  - Check if `map2` satisfies `map1` using `isValid`
  - If valid:
    - Update answer
    - Break (first valid window is smallest for that `i`)
- Return smallest substring

### Code (Java)

    class Solution {
        public String minWindow(String s, String t) {
            int n = s.length();
            int m = t.length();

            HashMap<Character, Integer> map1 = new HashMap<>();

            for (int i = 0; i < m; i++) {
                map1.put(t.charAt(i), map1.getOrDefault(t.charAt(i), 0) + 1);
            }

            String ans = "";

            for (int i = 0; i < n; i++) {
                HashMap<Character, Integer> map2 = new HashMap<>();

                for (int j = i; j < n; j++) {
                    char ch = s.charAt(j);
                    map2.put(ch, map2.getOrDefault(ch, 0) + 1);

                    if (isValid(map1, map2)) {
                        String sub = s.substring(i, j + 1);

                        if (ans.equals("") || sub.length() < ans.length()) {
                            ans = sub;
                        }
                        break;
                    }
                }
            }
            return ans;
        }

        private boolean isValid(Map<Character, Integer> map1, Map<Character, Integer> map2) {
            for (char c : map1.keySet()) {
                if (map2.getOrDefault(c, 0) < map1.get(c)) {
                    return false;
                }
            }
            return true;
        }
    }

### Complexity
- Time: O(n^2 * k)
- Space: O(k)

---

## 2. Sliding Window with Two Maps (Your Second Approach)

### Approach
- Maintain:
  - `map1` → required frequencies
  - `map2` → current window frequencies
- Use two pointers `left` and `right`
- Expand `right`:
  - Add char to `map2`
  - If valid char and within required freq → decrement `count`
- When `count == 0`:
  - Try shrinking from `left`
  - Update minimum window
  - Remove left char from `map2`
  - If requirement breaks → increment `count`

### Code (Java)

    class Solution {
        public String minWindow(String s, String t) {
            int n = s.length();
            int m = t.length();

            HashMap<Character, Integer> map1 = new HashMap<>();
            for (int i = 0; i < m; i++) {
                map1.put(t.charAt(i), map1.getOrDefault(t.charAt(i), 0) + 1);
            }

            HashMap<Character, Integer> map2 = new HashMap<>();

            int left = 0;
            int count = m;
            int minlen = Integer.MAX_VALUE;
            String ans = "";

            for (int right = 0; right < n; right++) {
                char ch = s.charAt(right);
                map2.put(ch, map2.getOrDefault(ch, 0) + 1);

                if (map1.containsKey(ch) && map2.get(ch) <= map1.get(ch)) {
                    count--;
                }

                while (count == 0) {
                    if (right - left + 1 < minlen) {
                        minlen = right - left + 1;
                        ans = s.substring(left, right + 1);
                    }

                    char c = s.charAt(left);
                    map2.put(c, map2.get(c) - 1);

                    if (map1.containsKey(c) && map2.get(c) < map1.get(c)) {
                        count++;
                    }

                    left++;
                }
            }

            return minlen == Integer.MAX_VALUE ? "" : ans;
        }
    }

### Complexity
- Time: O(n)
- Space: O(k)

---

## 3. Optimized Sliding Window (Single Map) (Your Third Approach)

### Approach
- Use only one map initialized with `t`
- Map stores **remaining required characters**
- Expand window:
  - Decrease count in map
  - If char was needed → decrement `count`
- When `count == 0`:
  - Window is valid
  - Try shrinking
  - While shrinking:
    - Increase map value
    - If requirement breaks → increment `count`

### Code (Java)

    class Solution {
        public String minWindow(String s, String t) {
            int n = s.length();
            int m = t.length();

            HashMap<Character, Integer> map = new HashMap<>();

            for (int i = 0; i < m; i++) {
                map.put(t.charAt(i), map.getOrDefault(t.charAt(i), 0) + 1);
            }

            int left = 0;
            int count = m;
            int minlen = Integer.MAX_VALUE;
            String ans = "";

            for (int right = 0; right < n; right++) {
                char ch = s.charAt(right);

                if (map.containsKey(ch)) {
                    if (map.get(ch) > 0) {
                        count--;
                    }
                    map.put(ch, map.get(ch) - 1);
                }

                while (count == 0) {
                    if (right - left + 1 < minlen) {
                        minlen = right - left + 1;
                        ans = s.substring(left, right + 1);
                    }

                    char c = s.charAt(left);

                    if (map.containsKey(c)) {
                        map.put(c, map.get(c) + 1);
                        if (map.get(c) > 0) {
                            count++;
                        }
                    }

                    left++;
                }
            }

            return minlen == Integer.MAX_VALUE ? "" : ans;
        }
    }

### Complexity
- Time: O(n)
- Space: O(k)

---

## Final Summary

| Approach                      | Time Complexity | Space |
|------------------------------|----------------|-------|
| Brute Force                  | O(n^2 * k)     | O(k)  |
| Sliding Window (Two Maps)    | O(n)           | O(k)  |
| Sliding Window (Single Map)  | O(n)           | O(k)  |

```
