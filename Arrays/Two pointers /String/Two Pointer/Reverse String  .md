# 344. Reverse String

## Solution Approach 1: Brute Force (Extra Array)

### Algorithm

1. Create a new character array of the same size as the input array.
2. Initialize an index `j` at the last position of the input array.
3. Traverse the input array from left to right.
4. Store each character in the new array from right to left.
5. Copy the reversed characters back into the original array.
6. The original array is now reversed.

### Code

    class Solution {
        public void reverseString(char[] s) {

            char[] reversed = new char[s.length];

            int j = s.length - 1;

            for (int i = 0; i < s.length; i++) {
                reversed[j] = s[i];
                j--;
            }

            for (int i = 0; i < s.length; i++) {
                s[i] = reversed[i];
            }
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Solution Approach 2: Using Stack

### Algorithm

1. Create a stack of characters.
2. Traverse the input array.
3. Push every character into the stack.
4. Traverse the array again.
5. Pop characters from the stack and store them back into the array.
6. Since a stack follows **LIFO (Last In, First Out)**, the characters are stored in reverse order.

### Code

    import java.util.Stack;

    class Solution {
        public void reverseString(char[] s) {

            Stack<Character> stack = new Stack<>();

            for (char c : s) {
                stack.push(c);
            }

            for (int i = 0; i < s.length; i++) {
                s[i] = stack.pop();
            }
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Solution Approach 3: Recursion

### Algorithm

1. Start with two pointers:
   - `left = 0`
   - `right = s.length - 1`
2. If `left >= right`, stop the recursion.
3. Swap the characters at `left` and `right`.
4. Recursively call the function with:
   - `left + 1`
   - `right - 1`
5. Continue until the pointers meet.
6. The array is reversed in-place.

### Code

    class Solution {
        public void reverseString(char[] s) {
            reverse(s, 0, s.length - 1);
        }

        private void reverse(char[] s, int left, int right) {

            if (left >= right) {
                return;
            }

            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;

            reverse(s, left + 1, right - 1);
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(n)` due to recursion stack

---

## Solution Approach 4: Optimal (Two Pointers)

### Algorithm

1. Initialize two pointers:
   - `left = 0`
   - `right = s.length - 1`
2. While `left < right`:
   - Store `s[left]` in a temporary variable.
   - Set `s[left] = s[right]`.
   - Set `s[right] = temporary`.
3. Move `left` forward.
4. Move `right` backward.
5. Continue until the two pointers meet.
6. The string is reversed in-place.

### Code

    class Solution {
        public void reverseString(char[] s) {

            int left = 0;
            int right = s.length - 1;

            while (left < right) {

                char temp = s[left];
                s[left] = s[right];
                s[right] = temp;

                left++;
                right--;
            }
        }
    }

### Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---
