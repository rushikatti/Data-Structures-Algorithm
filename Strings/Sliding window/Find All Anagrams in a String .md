
# 438. Find All Anagrams in a String

## Solution Approach 1: Brute Force (Check Every Substring)

### Algorithm

1. Let `x = p.length()`.
2. Traverse string `s` from index `0` to `n - x`.
3. For every index `i`:
   - Create a frequency array `scount[26]`.
   - Count characters for substring `s[i ... i+x-1]`.
4. Compare `scount` with `pcount`.
5. If equal → add index `i` to result.
6. Return result list.

### Code

    class Solution {
        public List<Integer> findAnagrams(String s, String p) {

            int n = s.length();
            int x = p.length();

            List<Integer> res = new ArrayList<>();

            if (n < x) return res;

            int[] pcount = new int[26];

            for (char c : p.toCharArray()) {
                pcount[c - 'a']++;
            }

            for (int i = 0; i <= n - x; i++) {

                int[] scount = new int[26];

                for (int j = i; j < i + x; j++) {
                    scount[s.charAt(j) - 'a']++;
                }

                if (Arrays.equals(scount, pcount)) {
                    res.add(i);
                }
            }

            return res;
        }
    }

### Complexity

- **Time:** `O(n * x)`
- **Space:** `O(1)`

---

## Solution Approach 2: Optimal (Sliding Window)

### Algorithm

1. If `s.length() < p.length()` → return empty list.
2. Create two arrays:
   - `pcount[26]` → frequency of `p`
   - `scount[26]` → frequency of current window
3. Fill `pcount`.
4. Traverse `s` using index `i`:
   - Add current char → `scount[s[i]]++`
   - If window size exceeds `p.length()`:
     - Remove old char → `scount[s[i - x]]--`
5. Compare arrays:
   - If equal → add starting index `(i - x + 1)`
6. Return result.

### Code

    class Solution {
        public List<Integer> findAnagrams(String s, String p) {

            int n = s.length();
            int x = p.length();

            List<Integer> res = new ArrayList<>();

            if (n < x) return res;

            int[] pcount = new int[26];
            int[] scount = new int[26];

            for (char c : p.toCharArray()) {
                pcount[c - 'a']++;
            }

            for (int i = 0; i < n; i++) {

                scount[s.charAt(i) - 'a']++;

                if (i >= x) {
                    scount[s.charAt(i - x) - 'a']--;
                }

                if (Arrays.equals(scount, pcount)) {
                    res.add(i - x + 1);
                }
            }

            return res;
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`


