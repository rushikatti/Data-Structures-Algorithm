# 455. Assign Cookies

## Brute Force Solution

### Approach

- For every cookie, iterate through all children.
- Assign the cookie to the first unassigned child whose greed factor is less than or equal to the cookie size.
- Mark the child as assigned.
- Count the total number of satisfied children.

### Code

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {

        boolean[] assigned = new boolean[g.length];
        int count = 0;

        for (int cookie : s) {

            for (int i = 0; i < g.length; i++) {

                if (!assigned[i] && cookie >= g[i]) {
                    assigned[i] = true;
                    count++;
                    break;
                }
            }
        }

        return count;
    }
}
```

### Complexity

- Time: O(n × m)
- Space: O(n)

---

## Better Solution

### Approach

- Sort both the greed and cookie arrays.
- Start with the least greedy child.
- Traverse the cookies from smallest to largest.
- If a cookie satisfies the current child, assign it and move to the next child.
- Continue until all cookies are processed.

### Code

```java
class Solution {

    public int findContentChildren(int[] g, int[] s) {

        Arrays.sort(g);
        Arrays.sort(s);

        int child = 0;

        for (int cookie = 0; cookie < s.length && child < g.length; cookie++) {

            if (s[cookie] >= g[child]) {
                child++;
            }
        }

        return child;
    }
}
```

### Complexity

- Time: O(n log n + m log m)
- Space: O(1)

---

## Optimal Solution

### Approach

- Sort both arrays.
- Use two pointers:
  - One for children.
  - One for cookies.
- If the current cookie satisfies the current child, assign it and move both pointers.
- Otherwise, move only the cookie pointer to try a larger cookie.
- The number of assigned children is the answer.

### Code

```java
class Solution {

    public int findContentChildren(int[] g, int[] s) {

        Arrays.sort(g);
        Arrays.sort(s);

        int i = 0;
        int j = 0;

        while (i < g.length && j < s.length) {

            if (s[j] >= g[i]) {
                i++;
                j++;
            } else {
                j++;
            }
        }

        return i;
    }
}
```

### Complexity

- Time: O(n log n + m log m)
- Space: O(1)
