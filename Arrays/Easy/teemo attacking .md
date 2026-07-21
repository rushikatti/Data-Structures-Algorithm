# 495. Teemo Attacking

## Brute Force Solution

### Approach

- Mark every second during which Ashe is poisoned.
- For each attack at time `t`, mark all seconds from `t` to `t + duration - 1`.
- Use a `HashSet` to avoid counting overlapping seconds multiple times.
- Return the size of the set.

### Code

```java
class Solution {

    public int findPoisonedDuration(int[] timeSeries, int duration) {

        HashSet<Integer> poisoned = new HashSet<>();

        for (int attack : timeSeries) {

            for (int t = attack; t < attack + duration; t++) {
                poisoned.add(t);
            }
        }

        return poisoned.size();
    }
}
```

### Complexity

- **Time:** O(n × duration)
- **Space:** O(n × duration)

---

## Better Solution

### Approach

- Traverse consecutive attack times.
- For each attack except the last:
  - Compute the gap between the current attack and the next attack.
  - If the gap is smaller than `duration`, only the gap contributes because the poison overlaps.
  - Otherwise, the full `duration` contributes.
- Add the full duration for the last attack.

### Code

```java
class Solution {

    public int findPoisonedDuration(int[] timeSeries, int duration) {

        if (timeSeries.length == 0)
            return 0;

        int total = 0;

        for (int i = 0; i < timeSeries.length - 1; i++) {

            total += Math.min(duration, timeSeries[i + 1] - timeSeries[i]);
        }

        total += duration;

        return total;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Optimal Solution

### Approach

- Initialize the answer with `duration` for the first attack.
- Traverse from the second attack onward.
- Calculate the time gap between consecutive attacks.
- If the gap is greater than or equal to `duration`, add the full `duration`.
- Otherwise, add only the gap since the remaining poison time overlaps.
- Return the accumulated poison duration.

### Code

```java
class Solution {

    public int findPoisonedDuration(int[] timeSeries, int duration) {

        if (timeSeries.length == 0)
            return 0;

        int total = duration;

        for (int i = 1; i < timeSeries.length; i++) {

            int gap = timeSeries[i] - timeSeries[i - 1];

            total += Math.min(gap, duration);
        }

        return total;
    }
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)
