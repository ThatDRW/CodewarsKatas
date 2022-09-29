# 7 kyu - Return the Latest Modified File
## Instructions
Write a script which return the latest modified file.

For example, if the following files are in the current directory:
```
poem.txt
article.txt
quotes.txt
```
and the latest edited file was `article.txt` then the following should be returned:
```
article.txt
```
Note: The files will be in the current directory.

## Examples
```

```

## My Solution #1 - 
```shell
ls -Art | tail -n 1
```