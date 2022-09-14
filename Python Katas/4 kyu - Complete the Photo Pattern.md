# 4 kyu - Complete the Photo Pattern
## Instructions
"All the people hurry up! We need to take a picture. The tallest standing in the middle, and then left and right descending...All the people, hand in hand..."

Give you an array legs. It recorded the length of the legs of all the people(we assume that their upper body is the same height), please follow the above rules to arrange these people, and then complete and return the photo.

Note:

    The length of array legs always be a positive odd integer, all elements are positive integers.
    The order is tallest in the middle, then left, then right, then left, then right..
    If necessary, please add some spaces on both sides.
    Please pay attention to "hand in hand". You can assume that their arms are retractable ;-)


## Examples
```
legs = [1,2,3]
After arrange --> [2,3,1]

The photo should be:
             + +   
   + +      +o o+  
  +o o+    +  u  +      + +     
 +  u  +    + ~ +      +o o+  
  + ~ +       |       +  u  + 
    |       +-o-+      + ~ +  
  +-o-+    /| o |\       |    
_/| o |\__/ +-o-+ \    +-o-+  
  +-o-+      | |   \__/| o |\_
   | |       | |       +-o-+  
   I I       I I        I I   
 
 
 
legs = [1,1,1,2,3]
After arrange --> [1,2,3,1,1]

The photo should be:
                       + +   
             + +      +o o+  
   + +      +o o+    +  u  +      + +      + +     
  +o o+    +  u  +    + ~ +      +o o+    +o o+  
 +  u  +    + ~ +       |       +  u  +  +  u  + 
  + ~ +       |       +-o-+      + ~ +    + ~ +  
    |       +-o-+    /| o |\       |        |    
  +-o-+    /| o |\__/ +-o-+ \    +-o-+    +-o-+  
_/| o |\__/ +-o-+      | |   \__/| o |\__/| o |\_
  +-o-+      | |       | |       +-o-+    +-o-+  
   I I       I I       I I        I I      I I   
```

## My Solution #1 - 
```python
def sort_legs(legs):
    """Sort the legs for the photo."""
    out = []
    for leg in sorted(legs, reverse=True):
        if len(out) % 2 == 0: out.append(leg)
        else: out.insert(0, leg)
    return out

def person(left, height, right, maxh):
    """Returns one person."""
    ext_head = maxh - height            # Number of blank layers above head
    ext_legs = height - 1               # Number of extra leg layers
    ext_larm = max(height-left+1, 1)    # Number of left arm parts
    ext_rarm = max(height-right+1, 1)   # Number of extra right arm parts
    
    person = [  ' + + ', # 0
                '+o o+', # 1
               '+  u  +', # 2
                '+ ~ +', # 3
                '  |  ', # 4
                '+-o-+', # 5 <- Stitch Arms Here
                '| o |',
                '+-o-+',
                ' I I ']
    
    e_legs =    ' | | '

    # Stretch those legs.
    for e in range(ext_legs): person.insert(-1, e_legs)
    
    # Generate right arm.
    arm_r = right_arm(ext_larm)
    arm_r.extend([' '*len(arm_r[0])] * (len(person) - len(arm_r)))
    
    # Generate left arm.
    arm_l = left_arm(ext_rarm)
    arm_l.extend([' '*len(arm_l[0])] * (len(person) - len(arm_l)))

    # Stitch em up.
    complete = []
    for a, b, c in zip(arm_r, person, arm_l):
        complete.append(a + b + c)
        
    # Fill headroom.
    if ext_head > 0:
        air = ' ' * len(complete[0])
        for i in range(ext_head): complete.insert(0,air)
    
    return '\n'.join(complete)

def right_arm(length):
    larm =  ['_/']
    
    for i in range(length-1):
        new = '  ' + ' ' * (i) + '/'
        for i in range(len(larm)):
            larm[i] += ' '
        larm.insert(0, new)
    
    # Pad so arm can be stitched to person.
    padding = [' '*len(larm[0])] * 6
    padding[2] = padding[2][:-1] # Space for Cheek
    padding.extend(larm)
    
    return padding
    
def left_arm(length):
    larm =  ['\_']
    
    for i in range(length-1):
        new = '\\' + ' ' * (i) + '  '
        for i in range(len(larm)):
            larm[i] = ' ' + larm[i]
        larm.insert(0, new)
    
    # Pad so arm can be stitched to person.
    padding = [' '*len(larm[0])] * 6
    padding[2] = padding[2][:-1]
    padding.extend(larm)
    
    
    # for p in padding: print(p)
    return padding

def pattern(legs):
    # Sort legs in the correct order for the photo.
    legs = sort_legs(legs)
    
    # Store the tallest persons leg-length.
    maxh = max(legs)
    
    persons = []
    
    for i, height in enumerate(legs):
        # Get Left person height except for first.
        if i > 0: left = legs[i-1]
        else: left = height
        
        # Get Right person height except for last.
        if i < len(legs)-1: right = legs[i+1]
        else: right = height
        
        # Generate new person.
        persons.append(person(left, height, right, maxh))
    
    # Generate the picture from the individual persons.
    picture = [''] * len(persons[0].split('\n'))
    
    for p in persons:
        for i, line in enumerate(p.split('\n')):
            picture[i] += line
            
    return '\n'.join(picture)
```