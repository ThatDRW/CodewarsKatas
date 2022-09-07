# 5 kyu - Simple Pig Latin
## Instructions
Move the first letter of each word to the end of it, then add "ay" to the end of the word. Leave punctuation marks untouched.

## Examples
```
pig_it('Pig latin is cool') # igPay atinlay siay oolcay
pig_it('Hello world !')     # elloHay orldway !
```

## My Solution #1 - Split and Splice
```python
def pig_it(text):
    # Create an array of words in text.
    words = text.split(' ')

    # Array to store our output.
    latin = []

    # Punctuation to ignore.
    symbols = ['!','?',',','.']
    
    # Loop over the words array.
    for word in words:
        if word not in symbols:
            # Pigify our word if it's not a symbol.
            word = word[1:] + word[0] + 'ay'
        
        # Store to our output.
        latin.append(word)
        
    # Return the pigified string by joining the words with a space inbetween each of them.
    return " ".join(latin)
```