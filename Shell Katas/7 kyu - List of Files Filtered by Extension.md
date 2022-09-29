# 7 kyu - List of Files Filtered by Extension
## Instructions
For this challenge you will write a script that takes the first argument passed in and returns a list of files in the current directory, filtered by file extension.

    Note: The files will be in the current directory.

## Examples
For example, if the following files are in a directory:
```
cat.png
cow.jpg
zebra.png
```
and png is passed in as the argument then the following should be returned:
```
cat.png
zebra.png
```

## My Solution #1 - 
```shell
# add your shell script here. Expect the file extension to be passed in as the first argument
ls *".$1"
```