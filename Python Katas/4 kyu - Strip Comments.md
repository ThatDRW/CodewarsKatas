# 4 kyu - Strip Comments
## Instructions
Complete the solution so that it strips all text that follows any of a set of comment markers passed in. Any whitespace at the end of the line should also be stripped out.

Example:

Given an input string of:
```
apples, pears # and bananas
grapes
bananas !apples
```

The output expected would be:
```
apples, pears
grapes
bananas
```

The code would be called like so:
```python
result = solution("apples, pears # and bananas\ngrapes\nbananas !apples", ["#", "!"])
# result should == "apples, pears\ngrapes\nbananas"
```

## Examples
```python
test.assert_equals(solution('apples, pears # and bananas\ngrapes\nbananas !apples', ['#', '!']), 'apples, pears\ngrapes\nbananas')
test.assert_equals(solution('a #b\nc\nd $e f g', ['#', '$']), 'a\nc\nd')
test.assert_equals(solution(' a #b\nc\nd $e f g', ['#', '$']), ' a\nc\nd')
```

## My Solution #1 - 
```python
def strip_comments(strng, markers):
    # Split input strng to seperate lines.
    lines = strng.split('\n')
    
    # Store each line after stripping here.
    out = []
    
    if lines:
        for line in lines:
            for marker in markers:
                # Check if any of the markers appear in the string.
                if line.find(marker) > -1:
                    # If so, cut the line from the marker.
                    line = line[:line.find(marker)]
                    
            # Add the (stripped) line to our output buffer.
            # Note that we are removing any -trailing- spaces only.
            out.append(line.rstrip())
                    
    # Return our solution.
    return '\n'.join(out)
```