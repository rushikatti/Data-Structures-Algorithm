# 202. Happy Number

## Brute Force Solution

### Approach

- Repeatedly replace the number with the sum of the squares of its digits.
- Stop if the number becomes `1`.
- To avoid an infinite loop, run the process for a fixed number of iterations.
- If `1` is not reached within the limit, return `false`.

> This approach is not guaranteed to be correct because the iteration limit is arbitrary.

### Code

```java
class Solution {

    public boolean isHappy(int n) {

        int limit = 1000;

        while (limit-- > 0) {

            if (n == 1)
                return true;

            n = getNext(n);
        }

        return false;
    }

    private int getNext(int n) {

        int sum = 0;

        while (n > 0) {
            int digit = n % 10;
            sum += digit * digit;
            n /= 10;
        }

        return sum;
    }
}
```

### Complexity

- **Time:** O(k × log n)
- **Space:** O(1)

---

## Better Solution

### Approach

- Store every generated number in a `HashSet`.
- If the number becomes `1`, return `true`.
- If a number repeats, a cycle is detected, so return `false`.

### Code

```java
class Solution {

    public boolean isHappy(int n) {

        HashSet<Integer> visited = new HashSet<>();

        while (n != 1 && !visited.contains(n)) {
            visited.add(n);
            n = getNext(n);
        }

        return n == 1;
    }

    private int getNext(int n) {

        int sum = 0;

        while (n > 0) {
            int digit = n % 10;
            sum += digit * digit;
            n /= 10;
        }

        return sum;
    }
}
```

### Complexity

- **Time:** O(log n)
- **Space:** O(log n)

---

## Optimal Solution

### Approach

- Treat the generated numbers as a linked list.
- Use Floyd's Cycle Detection.
- Slow moves one step.
- Fast moves two steps.
- If they meet before reaching `1`, a cycle exists.
- If they meet at `1`, the number is happy.

### Code

```java
class Solution {

    public boolean isHappy(int n) {

        int slow = n;
        int fast = n;

        do {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        } while (slow != fast);

        return slow == 1;
    }

    private int getNext(int n) {

        int sum = 0;

        while (n > 0) {
            int digit = n % 10;
            sum += digit * digit;
            n /= 10;
        }

        return sum;
    }
}
```

### Complexity

- **Time:** O(log n)
- **Space:** O(1)
