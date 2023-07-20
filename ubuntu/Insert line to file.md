# Insert line to file

 

https://unix.stackexchange.com/questions/99350/how-to-insert-text-before-the-first-line-of-a-file



`1i`  means insert `text` to first line of filename

```
sed  -i '1i text' filename
```