#  Convert hex string (begin with 0x) to int



[Reference](https://stackoverflow.com/questions/10156409/convert-hex-string-char-to-int)



Example:

```c
const char *hexstring = "abcdef0";
int number = (int)strtol(hexstring, NULL, 16);
```

In case the string representation of the number begins with a `0x` prefix, one must should use 0 as base:

```c
const char *hexstring = "0xabcdef0";
int number = (int)strtol(hexstring, NULL, 0);
```

(It's as well possible to specify an explicit base such as 16, but I wouldn't recommend introducing redundancy.)