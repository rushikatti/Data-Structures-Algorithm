# Permutation in String (LeetCode 567)

## Brute Force Approach

### Approach
- Let n = s1.length() and m = s2.length()
- If n > m, return false
- Compute frequency array freq1 for s1
- Iterate over every substring of s2 of size n
  - For each starting index i, build a frequency array freq2 for substring s2[i ... i+n-1]
  - Compare freq1 and freq2
  - If equal, return true
- If no match found, return false

### Code (Java)

    class Solution {
        public boolean checkInclusion(String s1, String s2) {

            int n = s1.length();
            int m = s2.length();

            if (n > m) return false;

            int[] freq1 = new int[26];

            for (char c : s1.toCharArray()) {
                freq1[c - 'a']++;
            }

            for (int i = 0; i <= m - n; i++) {

                int[] freq2 = new int[26];

                for (int j = i; j < i + n; j++) {
                    freq2[s2.charAt(j) - 'a']++;
                }

                if (matches(freq1, freq2)) return true;
            }

            return false;
        }

        private boolean matches(int[] a, int[] b) {
            for (int i = 0; i < 26; i++) {
                if (a[i] != b[i]) return false;
            }
            return true;
        }
    }

### Complexity
- Time: O(m * n)
- Space: O(1)


## Optimized Approach (Sliding Window)

### Approach
- Use a fixed-size sliding window of length n
- Maintain two frequency arrays:
  - freq1 for s1
  - freq2 for current window in s2
- Initialize freq1 and the first window freq2
- Compare both arrays
- Slide the window:
  - Add next character to freq2
  - Remove previous character from freq2
  - Compare again
- If any match, return true

### Code (Java)

    class Solution {
        public boolean checkInclusion(String s1, String s2) {

            int n = s1.length();
            int m = s2.length();

            if (n > m) return false;

            int[] freq1 = new int[26];
            int[] freq2 = new int[26];

            for (char c : s1.toCharArray()) {
                freq1[c - 'a']++;
            }

            for (int i = 0; i < n; i++) {
                freq2[s2.charAt(i) - 'a']++;
            }

            if (matches(freq1, freq2)) return true;

            for (int i = n; i < m; i++) {
                freq2[s2.charAt(i) - 'a']++;
                freq2[s2.charAt(i - n) - 'a']--;

                if (matches(freq1, freq2)) return true;
            }

            return false;
        }

        private boolean matches(int[] a, int[] b) {
            for (int i = 0; i < 26; i++) {
                if (a[i] != b[i]) return false;
            }
            return true;
        }
    }

### Complexity
- Time: O(m)
- Space: O(1)
