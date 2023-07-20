# 2's Complement

## Here is the best answer in my view:

> From https://stackoverflow.com/questions/1049722/what-is-2s-complement

I wonder if it could be explained any better than the Wikipedia article.

The basic problem that you are trying to solve with two's complement representation is the problem of storing negative integers.

First, consider an unsigned integer stored in 4 bits. You can have the following

```
0000 = 0
0001 = 1
0010 = 2
...
1111 = 15
```

These are unsigned because there is no indication of whether they are negative or positive.

### Sign Magnitude and Excess Notation

To store negative numbers you can try a number of things. First, you can use sign magnitude notation which assigns the first bit as a sign bit to represent +/- and the remaining bits to represent the magnitude. So using 4 bits again and assuming that 1 means - and 0 means + then you have

```
0000 = +0
0001 = +1
0010 = +2
...
1000 = -0
1001 = -1
1111 = -7
```

So, you see the problem there? We have positive and negative 0. The bigger problem is adding and subtracting binary numbers. The circuits to add and subtract using sign magnitude will be very complex.

What is

```
0010
1001 +
----
```

?

Another system is [excess notation](https://web.archive.org/web/20170223233445/http://www.cs.umd.edu/class/sum2003/cmsc311/Notes/Data/bias.html). You can store negative numbers, you get rid of the two zeros problem but addition and subtraction remains difficult.

So along comes two's complement. Now you can store positive and negative integers and perform arithmetic with relative ease. There are a number of methods to convert a number into two's complement. Here's one.

### Convert Decimal to Two's Complement

1. Convert the number to binary (ignore the sign for now) e.g. 5 is 0101 and -5 is 0101

2. If the number is a positive number then you are done. e.g. 5 is 0101 in binary using two's complement notation.

3. If the number is negative then

   3.1 find the complement (invert 0's and 1's) e.g. -5 is 0101 so finding the complement is 1010

   3.2 Add 1 to the complement 1010 + 1 = 1011. Therefore, -5 in two's complement is 1011.

So, what if you wanted to do 2 + (-3) in binary? 2 + (-3) is -1. What would you have to do if you were using sign magnitude to add these numbers? 0010 + 1101 = ?

Using two's complement consider how easy it would be.

```
 2  =  0010
 -3 =  1101 +
 -------------
 -1 =  1111
```

### Converting Two's Complement to Decimal

Converting 1111 to decimal:

1. The number starts with 1, so it's negative, so we find the complement of 1111, which is 0000.
2. Add 1 to 0000, and we obtain 0001.
3. Convert 0001 to decimal, which is 1.
4. Apply the sign = -1.

Tada!



### My Example



**Code**:

```C
int main(int argc, char *argv[]) {
    size_t a = 1;
    size_t b = 10;
    printf("HEX:\t\t%lu - %lu = 0x%08lx\n", a, b, a - b);
    printf("UNSIGNED:\t%lu - %lu = %lu\n", a, b, a - b);
    printf("SIGNED:\t\t%lu - %lu = %ld\n", a, b, a - b);
}
```



**Output**:

```bash
HEX:            1 - 10 = 0xfffffffffffffff7
UNSIGNED:       1 - 10 = 18446744073709551607
SIGNED:         1 - 10 = -9
```



`1 - 10` stored in computer as `0xfffffffffffffff7`, If you declare the result as *signed* number, then, the most significant bit is signed bit, you can convert this 2's complement to decimal:

1. The number starts with 1 (1111), so it's negative
2. Find the complement of `0xfffffffffffffff7` , which is `0x8`
3. Add 1 to `0x8`, and we obtain `0x9`
4. Convert `0x9` to decimal, which is 9
5. Apply the sign, and we get -9

If you declare the result as *unsigned* number, then you just convert `0xfffffffffffffff7` to decimal as normal. 

In a nutshell, the computer just store data, and don't care about it's type. It is you, the programmer,  give the data meaning. 

Decimal for man, Hex/Bin for machine.