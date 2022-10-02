# 8 kyu - Aspect Ratio Cropping Part 1
## Instructions
The aspect ratio of an image describes the proportional relationship between its width and its height. Most video shown on the internet uses a 16:9 aspect ratio, which means that for every pixel in the Y, there are roughly 1.77 pixels in the X (where 1.77 ~= 16/9). As an example, 1080p video with an aspect ratio of 16:9 would have an X resolution of 1920, however 1080p video with an aspect ratio of 4:3 would have an X resolution of 1440.

Write a function that accepts arbitrary X and Y resolutions and converts them into resolutions with a 16:9 aspect ratio that maintain equal height. Round your answers up to the nearest integer.

This kata is part of a series with Aspect Ratio Cropping - Part 2.

## Examples
```

```

## My Solution #1 - 
```cobol
       identification division.
       program-id. AspectRatio.
       author. ThatDRW.

       data division.
       working-storage section.
       01  ratio            pic 9(5).9(5).
      
       linkage section.
       01  x                pic 9(4).
       01  y                pic 9(4).
       01  result.
           05 res-x         pic 9(4).
           05 res-y         pic 9(4).
      
       procedure division using x y result.
           initialize result
      
           move y to res-y
           multiply y by 1.77777 giving ratio
           move ratio to res-x
           add 1 to res-x
      
           goback.
       end program AspectRatio.
      
```