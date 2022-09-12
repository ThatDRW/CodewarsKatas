# 6 kyu - Count the Photos
## Instructions
In a string we describe a road. There are cars that move to the right and we denote them with ">" and cars that move to the left and we denote them with "<". There are also cameras that are indicated by: " . ".
A camera takes a photo of a car if it moves to the direction of the camera.

Task
Your task is to write a function such that, for the input string that represents a road as described, returns the total number of photos that were taken by the cameras. The complexity should be strictly O(N) in order to pass all the tests. 

## Examples
```
For ">>." -> 2 photos were taken
For ".>>" -> 0 photos were taken
For ">.<." -> 3 photos were taken
For ".><.>>.<<" -> 11 photos were taken
```

## My Solution #1 - 
```python
def count_photos(road):
    count = 0
    cameras = road.count('.')
    cams_l, cams_r = cameras, cameras
    
    for i in range(len(road)):
        # Left to Right
        if road[i] == '>':
            count += cams_l
        elif road[i] == '.':
            cams_l -= 1
        
        # Right to Left
        if road[-(i+1)] == '<':
            count += cams_r
        elif road[-(i+1)] == '.':
            cams_r -= 1
    
    return count
```