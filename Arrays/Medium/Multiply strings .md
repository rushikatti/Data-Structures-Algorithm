## Brute Force (Not Accepted for Large Inputs)

* Convert both strings to integers.
* Multiply them.
* Convert the result back to a string

### code :

```java
long n1 = Long.parseLong(num1);
long n2 = Long.parseLong(num2);

return String.valueOf(n1 * n2);
```

### complexity :

* time complexity : o(n + m)
* space complexity : o(1)
  
## Optimal (School Multiplication)


```

Suppose

num1 = "123"
num2 = "45"

Multiply exactly like on paper.

        1 2 3
      ×   4 5
      --------
        6 1 5      (123 × 5)
    4 9 2          (123 × 4, shifted left)
      --------
      5 5 3 5

Instead of storing partial strings, we directly store digits in an integer array.

```

### code :

```java
class Solution {

    public String multiply(String num1, String num2) {

        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }

        int n = num1.length();
        int m = num2.length();

        int[] result = new int[n + m];

        for (int i = n - 1; i >= 0; i--) {

            for (int j = m - 1; j >= 0; j--) {

                int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');

                int p1 = i + j;
                int p2 = i + j + 1;

                int sum = mul + result[p2];

                result[p2] = sum % 10;
                result[p1] += sum / 10;
            }
        }

        StringBuilder ans = new StringBuilder();

        for (int num : result) {

            if (!(ans.length() == 0 && num == 0)) {
                ans.append(num);
            }
        }

        return ans.toString();
    }
}
```

### complexity :

* time complexity : o(n * m)
* space complexity : O(n+m)
