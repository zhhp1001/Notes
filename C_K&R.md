## Exercise 1-7. 

**Write a program to print the value of EOF.**

`EOF` is an integer defined in `<stdio.h>` , but the specific numeric value doesn't matter as long as it is not the same as any `char` value. 

```C
printf("%d", EOF); // -1
```

## c - '0'

By definition `char`s are just small integers, so `char` variables and constants are identical to `int`s in arithmetic expressions. This is natural and convenient; for example `c - '0'` is an integer expression with a value between 0 and 9 corresponding to the character '0' to '9' stored in `c` , i.e. 

```C
'0'-'0' = 0
'1'-'0' = 1
'2'-'0' = 2
.
.
.
'9'-'0' = 9
```



































