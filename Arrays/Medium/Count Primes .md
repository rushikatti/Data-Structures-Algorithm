# 204. Count Primes

## Brute Force Solution

### Approach

- Iterate through every number from `2` to `n - 1`.
- For each number, check whether it is prime by trying all divisors from `2` to `num - 1`.
- If it is prime, increment the count.
- Return the total count.

### Code

```java
class Solution {

    public int countPrimes(int n) {

        int count = 0;

        for (int i = 2; i < n; i++) {

            if (isPrime(i))
                count++;
        }

        return count;
    }

    private boolean isPrime(int num) {

        if (num < 2)
            return false;

        for (int i = 2; i < num; i++) {

            if (num % i == 0)
                return false;
        }

        return true;
    }
}
```

### Complexity

- **Time:** O(n²)
- **Space:** O(1)

---

## Better Solution

### Approach

- Iterate through every number from `2` to `n - 1`.
- To check whether a number is prime, only test divisors up to `√num`.
- If no divisor is found, the number is prime.
- Count all prime numbers.

### Code

```java
class Solution {

    public int countPrimes(int n) {

        int count = 0;

        for (int i = 2; i < n; i++) {

            if (isPrime(i))
                count++;
        }

        return count;
    }

    private boolean isPrime(int num) {

        if (num < 2)
            return false;

        for (int i = 2; i * i <= num; i++) {

            if (num % i == 0)
                return false;
        }

        return true;
    }
}
```

### Complexity

- **Time:** O(n√n)
- **Space:** O(1)

---

## Optimal Solution (Sieve of Eratosthenes)

### Approach

- Create a boolean array `isPrime` of size `n`.
- Initially mark every number from `2` to `n - 1` as prime.
- Starting from `2`, if a number is prime, mark all of its multiples as non-prime.
- Start marking multiples from `i * i` because smaller multiples have already been processed.
- Count all remaining prime numbers.

### Code

```java
class Solution {

    public int countPrimes(int n) {

        if (n <= 2)
            return 0;

        boolean[] isPrime = new boolean[n];

        Arrays.fill(isPrime, true);

        isPrime[0] = false;
        isPrime[1] = false;

        for (int i = 2; i * i < n; i++) {

            if (isPrime[i]) {

                for (int j = i * i; j < n; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        int count = 0;

        for (int i = 2; i < n; i++) {

            if (isPrime[i])
                count++;
        }

        return count;
    }
}
```

### Complexity

- **Time:** O(n log log n)
- **Space:** O(n)
