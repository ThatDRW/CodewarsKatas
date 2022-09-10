# 4 kyu - Text Align Justify
## Instructions
Your task in this Kata is to emulate text justification in monospace font. You will be given a single-lined text and the expected justification width. The longest word will never be greater than this width.

Here are the rules:

    Use spaces to fill in the gaps between words.
    Each line should contain as many words as possible.
    Use '\n' to separate lines.
    Gap between words can't differ by more than one space.
    Lines should end with a word not a space.
    '\n' is not included in the length of a line.
    Large gaps go first, then smaller ones ('Lorem--ipsum--dolor--sit-amet,' (2, 2, 2, 1 spaces)).
    Last line should not be justified, use only one space between words.
    Last line should not contain '\n'
    Strings with one word do not need gaps ('somelongword\n').

Also you can always take a look at how justification works in your text editor or directly in HTML (css: text-align: justify).

Have fun :)

## Examples
```
Example with width=30:

Lorem  ipsum  dolor  sit amet,
consectetur  adipiscing  elit.
Vestibulum    sagittis   dolor
mauris,  at  elementum  ligula
tempor  eget.  In quis rhoncus
nunc,  at  aliquet orci. Fusce
at   dolor   sit   amet  felis
suscipit   tristique.   Nam  a
imperdiet   tellus.  Nulla  eu
vestibulum    urna.    Vivamus
tincidunt  suscipit  enim, nec
ultrices   nisi  volutpat  ac.
Maecenas   sit   amet  lacinia
arcu,  non dictum justo. Donec
sed  quam  vel  risus faucibus
euismod.  Suspendisse  rhoncus
rhoncus  felis  at  fermentum.
Donec lorem magna, ultricies a
nunc    sit    amet,   blandit
fringilla  nunc. In vestibulum
velit    ac    felis   rhoncus
pellentesque. Mauris at tellus
enim.  Aliquam eleifend tempus
dapibus. Pellentesque commodo,
nisi    sit   amet   hendrerit
fringilla,   ante  odio  porta
lacus,   ut   elementum  justo
nulla et dolor.
```

## My Solution #1 - 
```python
def justify(text, width):
    words = text.split(' ')
    lengs = [len(x) for x in words]
    
    # Store all our justified lines.
    lines = []
    
    # Store the line we are working on.
    curl = []   # Holds words we want to put on this line.
    llen = 0    # Length of the current line excl. spaces.
    
    # Divide the words over the new lines.
    for word, length in zip(words, lengs):
        # Check curl length + spaces.
        # Check if we can fit the next word.
        if (llen + len(curl)) + length > width:
            # We should finish this line and start a new one.
            lines.append(curl[:])
            curl = []
            llen = 0
        
        # Add our word to the current line.
        curl.append(word)
        llen += length
        
    # Add our last line.
    if curl: lines.append(curl[:])
                           
    # Check if divided properly.
    # for line in lines: print(line)
    
    # Add the proper spacing to all but the last lines.
    outlines = []
    for line in lines[:-1]:
        # Find how many spaces and how many per space.
        length = sum([len(x) for x in line])
        spaces = len(line) - 1
        tofill = width-length
        if spaces > 0:
            spacer = tofill // spaces
            spacel = tofill % spacer
        else:
            spacer = spacel = 1
        
        # print('Length:', length, ' Spaces:', spaces, ' To Fill:', tofill)
        # print('SpaceRegular:', spacer, ' SpaceLast:', spacel)
    
        # Construct our justifies lines.
        wordcount = len(line)
        if wordcount == 1:
            outlines.append(line[0] + '\n')
        elif wordcount == 2:
            outlines.append(line[0] + (' '*spacer) + line[1] + '\n')
        else:
            joiner = ' '*spacer
            joined = joiner.join(line)
            
            # Final spacing check.
            if len(joined) < width:
                joined = joined.replace(joiner,(joiner+' '),width-len(joined))
                
            outlines.append(joined + '\n')
    
    # If there was more that 1 line, we need to process our last line still.
    if len(lines) > 1:
        outlines.append(' '.join(lines[-1]))
                        
    for line in outlines: print(len(line), line)
    
    return ''.join(outlines)
```