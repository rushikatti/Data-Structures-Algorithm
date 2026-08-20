# 3. Longest Substring Without Repeating Characters

## Solution Approach 1: Brute Force (HashSet)

### Algorithm

1. Iterate over each starting index `i`.
2. For every `i`, create a new `HashSet` to track unique characters.
3. Extend substring using index `j`:
   - If character already exists → break.
   - Else → add to set.
4. Update maximum length:
   - `maxlen = max(maxlen, j - i + 1)`
5. Return `maxlen`.

### Code

    import java.util.HashSet;

    class Solution {
        public int lengthOfLongestSubstring(String s) {

            int n = s.length();
            int maxlen = 0;

            for (int i = 0; i < n; i++) {

                HashSet<Character> set = new HashSet<>();

                for (int j = i; j < n; j++) {

                    if (set.contains(s.charAt(j))) {
                        break;
                    }

                    set.add(s.charAt(j));
                    maxlen = Math.max(maxlen, j - i + 1);
                }
            }

            return maxlen;
        }
    }

### Complexity

- **Time:** `O(n^2)`
- **Space:** `O(n)`

---

## Solution Approach 2: Sliding Window (HashMap Frequency)

### Algorithm

1. Use two pointers:
   - `left = 0`
   - `right = 0`
2. Maintain a `HashMap<Character, Integer>` for frequency.
3. Traverse with `right`:
   - Add character to map
4. If frequency > 1:
   - Remove characters from left
   - Move `left++`
5. Update max length.
6. Return result.

### Code

    import java.util.HashMap;

    class Solution {
        public int lengthOfLongestSubstring(String s) {

            int n = s.length();
            int maxlen = 0;

            HashMap<Character, Integer> map = new HashMap<>();

            int left = 0;

            for (int right = 0; right < n; right++) {

                char ch = s.charAt(right);
                map.put(ch, map.getOrDefault(ch, 0) + 1);

                while (map.get(ch) > 1) {

                    char leftchar = s.charAt(left);
                    map.put(leftchar, map.get(leftchar) - 1);
                    left++;
                }

                maxlen = Math.max(maxlen, right - left + 1);
            }

            return maxlen;
        }
    }

### Complexity

- **Time:** `O(n*26)`
- **Space:** `O(n)`

---

## Solution Approach 3: Optimal (Sliding Window + Last Seen Index)

### Algorithm

1. Use a `HashMap` to store last index of each character.
2. Maintain `left = 0`.
3. Traverse using `right`:
   - If character seen before:
     - Move `left = max(left, lastIndex + 1)`
4. Update index of character.
5. Update max length.
6. Return result.

### Code

    import java.util.HashMap;

    class Solution {
        public int lengthOfLongestSubstring(String s) {

            int n = s.length();
            int maxlen = 0;

            HashMap<Character, Integer> map = new HashMap<>();

            int left = 0;

            for (int right = 0; right < n; right++) {

                char ch = s.charAt(right);

                if (map.containsKey(ch)) {
                    left = Math.max(left, map.get(ch) + 1);
                }

                map.put(ch, right);

                maxlen = Math.max(maxlen, right - left + 1);
            }

            return maxlen;
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---
