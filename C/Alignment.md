# Alignment

 chars can start on any byte address, but 2-byte shorts must start on an even address, 4-byte ints or floats must start on an address divisible by 4, and 8-byte longs or doubles must start on an address divisible by 8. Signed or unsigned makes no difference.



Here’s a last important detail: If your structure has structure members, the inner structs want to have the alignment of longest scalar too. Suppose you write this:

```
struct foo5 {
    char c;
    struct foo5_inner {
        char *p;
        short x;
    } inner;
};
```

The `char *p` member in the inner struct forces the outer struct to be **pointer-aligned** as well as the inner. Actual layout will be like this on a 64-bit machine:

```
struct foo5 {
    char c;           /* 1 byte*/
    char pad1[7];     /* 7 bytes */
    struct foo5_inner {
        char *p;      /* 8 bytes */
        short x;      /* 2 bytes */
        char pad2[6]; /* 6 bytes */
    } inner;
};
```



make all the pointer-aligned subfields come first, because on a 64-bit machine they will be 8 bytes. Then the 4-byte ints; then the 2-byte shorts; then the character fields.