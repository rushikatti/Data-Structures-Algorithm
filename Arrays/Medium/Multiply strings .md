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
  
