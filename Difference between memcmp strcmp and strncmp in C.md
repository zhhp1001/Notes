# Difference between memcmp strcmp and strncmp in C

[Reference](https://stackoverflow.com/questions/13095513/what-is-the-difference-between-memcmp-strcmp-and-strncmp-in-c) 



In short:

- [`strcmp`](http://linux.die.net/man/3/strcmp) compares null-terminated C strings
- [`strncmp`](http://linux.die.net/man/3/strcmp) compares at most N characters of null-terminated C strings
- [`memcmp`](http://linux.die.net/man/3/memcmp) compares binary byte buffers of N bytes

So, if you have these strings:

```c
// still remember \0 is NULL
const char s1[] = "atoms\0\0\0\0";  // extra null bytes at end
const char s2[] = "atoms\0abc";     // embedded null byte
const char s3[] = "atomsaaa";
```

Then these results hold true:

```c
strcmp(s1, s2) == 0      // strcmp stops at null terminator
strcmp(s1, s3) != 0      // Strings are different
strncmp(s1, s3, 5) == 0  // First 5 characters of strings are the same
memcmp(s1, s3, 5) == 0   // First 5 bytes are the same
strncmp(s1, s2, 8) == 0  // Strings are the same up through the null terminator
memcmp(s1, s2, 8) != 0   // First 8 bytes are different
```