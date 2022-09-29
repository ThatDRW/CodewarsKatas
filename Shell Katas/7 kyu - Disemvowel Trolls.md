# 7 kyu - Disemvowel Trolls
## Instructions
Trolls are attacking your comment section!

A common way to deal with this situation is to remove all of the vowels from the trolls' comments, neutralizing the threat.

Your task is to write a function that takes a string and return a new string with all vowels removed.

Note: for this kata y isn't considered a vowel.

## Examples
For example, the string `"This website is for losers LOL!"` would become `"Ths wbst s fr lsrs LL!"`.

## My Solution #1 - 
```shell
#!/bin/bash
# s Enter Match and Replace
# /
# To Match Regex
# /
# Replace Match With (in this case nothing)
# /
# g Replace all matches instead of just the first.
echo $1 | sed 's/[aeiouAEIOU]//g'
```