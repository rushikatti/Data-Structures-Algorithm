# Longest Substring with K Unique Characters

## Brute Force Approach

### Approach
- Let n = length of string s
- Initialize maxLen = 0
- Generate all substrings using two loops
- For each substring:
  - Use a HashSet or HashMap to count unique characters
  - If number of unique characters == k:
    - Update maxLen
- Return maxLen

### Code (Java)

    class Solution {
        public int longestKSubstr(String s, int k) {
            int n = s.length();
            int maxLen = -1;

            for (int i = 0; i < n; i++) {
                HashMap<Character, Integer> map = new HashMap<>();

                for (int j = i; j < n; j++) {
                    char c = s.charAt(j);
                    map.put(c, map.getOrDefault(c, 0) + 1);

                    if (map.size() == k) {
                        maxLen = Math.max(maxLen, j - i + 1);
                    }

                    if (map.size() > k) {
                        break;
                    }
                }
            }

            return maxLen;
        }
    }

### Complexity
- Time: O(n^2)
- Space: O(k)


## Optimized Approach (Sliding Window)

### Approach
- Use two pointers left and right
- Maintain a HashMap to store character frequencies
- Expand right pointer:
  - Add character to map
- If map size > k:
  - Shrink window from left until size <= k
- If map size == k:
  - Update maxLen
- Continue until end

### Code (Java)

    class Solution {
        public int longestKSubstr(String s, int k) {
            int n = s.length();
            int left = 0;
            int maxLen = -1;

            HashMap<Character, Integer> map = new HashMap<>();

            for (int right = 0; right < n; right++) {
                char c = s.charAt(right);
                map.put(c, map.getOrDefault(c, 0) + 1);

                while (map.size() > k) {
                    char leftChar = s.charAt(left);
                    map.put(leftChar, map.get(leftChar) - 1);

                    if (map.get(leftChar) == 0) {
                        map.remove(leftChar);
                    }
                    left++;
                }

                if (map.size() == k) {
                    maxLen = Math.max(maxLen, right - left + 1);
                }
            }

            return maxLen;
        }
    }

### Complexity
- Time: O(n)
- Space: O(k)
