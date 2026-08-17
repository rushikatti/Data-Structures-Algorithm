# 125. Valid Palindrome

## Solution Approach 1: Brute Force (Clean String + Reverse)

### Algorithm

1. Traverse the string character by character.
2. Keep only **alphanumeric characters**.
3. Convert each valid character to **lowercase**.
4. Store the cleaned characters in a `StringBuilder`.
5. Reverse the cleaned string.
6. Compare the cleaned string with the reversed string.
7. If both are equal, return `true`; otherwise, return `false`.

### Code

```java
class Solution {
    public boolean isPalindrome(String s) {

        StringBuilder sb = new StringBuilder();

        for (char c : s.toCharArray()) {

            if (Character.isLetterOrDigit(c)) {
                sb.append(Character.toLowerCase(c));
            }
        }

        String cleaned = sb.toString();
        String reversed = sb.reverse().toString();

        return cleaned.equals(reversed);
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Solution Approach 2: Clean String + Two Pointers

### Algorithm

1. Traverse the string character by character.
2. Keep only **alphanumeric characters**.
3. Convert each valid character to **lowercase**.
4. Store the cleaned characters in a `StringBuilder`.
5. Initialize two pointers:
   - `left = 0`
   - `right = length - 1`
6. Compare the characters at `left` and `right`.
7. If they are different, return `false`.
8. Move `left` forward and `right` backward.
9. Continue until `left >= right`.
10. Return `true`.

### Code

```java
class Solution {
    public boolean isPalindrome(String s) {

        StringBuilder sb = new StringBuilder();

        for (char c : s.toCharArray()) {

            if (Character.isLetterOrDigit(c)) {
                sb.append(Character.toLowerCase(c));
            }
        }

        int left = 0;
        int right = sb.length() - 1;

        while (left < right) {

            if (sb.charAt(left) != sb.charAt(right)) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Solution Approach 3: Regular Expression + Reverse

### Algorithm

1. Remove all non-alphanumeric characters using a regular expression.
2. Convert the resulting string to **lowercase**.
3. Reverse the cleaned string.
4. Compare the original cleaned string with its reverse.
5. If both are equal, return `true`; otherwise, return `false`.

### Code

```java
class Solution {
    public boolean isPalindrome(String s) {

        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();

        String reversed = new StringBuilder(s)
                .reverse()
                .toString();

        return s.equals(reversed);
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Solution Approach 4: Optimal (Two Pointers)

### Algorithm

1. Initialize two pointers:
   - `left = 0`
   - `right = n - 1`
2. If the character at `left` is not alphanumeric, move `left` forward.
3. If the character at `right` is not alphanumeric, move `right` backward.
4. If both characters are alphanumeric, convert them to lowercase.
5. Compare the two characters.
6. If they are different, return `false`.
7. Move both pointers:
   - `left++`
   - `right--`
8. Continue until `left >= right`.
9. Return `true`.

### Code

```java
class Solution {
    public boolean isPalindrome(String s) {

        int left = 0;
        int right = s.length() - 1;

        while (left < right) {

            if (!Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            else if (!Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            else {

                if (Character.toLowerCase(s.charAt(left)) !=
                    Character.toLowerCase(s.charAt(right))) {
                    return false;
                }

                left++;
                right--;
            }
        }

        return true;
    }
}
```

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---
