# 7 kyu - Series of Integers from m to n
## Instructions
Write a function that accepts two arguments and generates a sequence containing the integers from the first argument to the second inclusive.
Input

Pair of integers greater than or equal to 0. The second argument will always be greater than or equal to the first. 

## Examples
```
generate_integers(2, 5) # --> [2, 3, 4, 5]
```

## My Solution #1 - 
```java
public class Kata {
    public static int[] generateIntegers(final int m, final int n) {
      int[] series = new int[n-m+1];
      for (int i = 0; i < n-m+1; i++) {
        series[i] = i + m;
      }
      return series;
    }
}
```