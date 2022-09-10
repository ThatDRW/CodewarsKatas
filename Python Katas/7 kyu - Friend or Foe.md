# 7 kyu - Friend or Foe
## Instructions
Make a program that filters a list of strings and returns a list with only your friends name in it.

If a name has exactly 4 letters in it, you can be sure that it has to be a friend of yours! Otherwise, you can be sure he's not...

Note: keep the original order of the names in the output.

## Examples
```
Ex: Input = ["Ryan", "Kieran", "Jason", "Yous"], Output = ["Ryan", "Yous"]

Ex: friend ["Ryan", "Kieran", "Mark"] `shouldBe` ["Ryan", "Mark"]
```

## My Solution #1 - 
```python
def friend(x):
    return [y for y in x if len(y) == 4]
```