# How to calculate size of memory by given a range of address



https://stackoverflow.com/questions/14113051/how-to-calculate-size-of-memory-by-given-a-range-of-address



**Step**

```
1. second_add - first_add + 1
2. convert to dec
```

**Example**

```
fdff ffff - fd00 0000 + 1 = 0100 0000 = 2^24 = 2^4 * 2^20 = 16Mbyte [2^20 byte = 1 Mbyte] 
```



