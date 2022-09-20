# 8 kyu - Sort My Textbooks
## Instructions
HELP! Jason can't find his textbook! It is two days before the test date, and Jason's textbooks are all out of order! Help him sort a list (ArrayList in java) full of textbooks by subject, so he can study before the test.

The sorting should NOT be case sensitive.

## Examples
```
    {"Algebra", "history", "Geometry", "english"})
    {"Algebra", "english", "Geometry", "history"})
```

## My Solution #1 - 
```java
import java.util.List;
import java.util.stream.*;
class sorter {
  public static List<String> sort(List<String> textbooks) {
    // Key is String.CASE_INSENSITIVE_ORDER.
    List<String> sortedList = textbooks.stream().sorted(String.CASE_INSENSITIVE_ORDER).collect(Collectors.toList());
    return sortedList;
  }
}
```