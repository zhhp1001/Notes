# Dynamic Memory Allocation



## External Fragmentation

Occurs when there is enough aggregate heap memory, but no single free block is large enough.



## Macros in mm.c

Why use `~0x7` instead of `0x8`

```C
#define GET_SIZE(p) (GET(p) & ~0x7)
#define GET_ALLOC(p) (GET(p) & 0x1)
```









TBD

https://condor.depaul.edu/glancast/374class/docs/lecFeb04.html

http://www.cs.cmu.edu/afs/cs/academic/class/15213-f14/www/recitations/rec11_shailind.pdf