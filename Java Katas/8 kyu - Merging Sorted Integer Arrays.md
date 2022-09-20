# 8 kyu - Merging Sorted Integer Arrays
## Instructions
Write a function that merges two sorted arrays into a single one. The arrays only contain integers. Also, the final outcome must be sorted and not have any duplicate.

## Examples
```

```

## My Solution #1 - 
```java
import java.util.*;
import java.util.stream.*;

public class Kata {
  public static int[] mergeArrays(int[] first, int[] second) {
    int[] result = IntStream.concat(IntStream.of(first), IntStream.of(second))
                          .distinct()    // filter duplicates
                          .sorted()      // sort
                          .toArray();
    return result;
  }
}
```