# Array and Pointer in C

Exercise code in **P208** *Expert C Programming*

```C
#include <stdio.h>

char ca[10] = "abcde";
void func(char ca[10]) {
    printf("In func\n");
    printf("ca = %p\n&ca = %p\n&(ca[0]) = %p\n&(ca[1]) = %p\n", ca, &ca, &(ca[0]), &(ca[1]));
}
void func_ptr(char pa[10]) {
    printf("In func_ptr\n");
    printf("pa = %p\n&pa = %p\n&(pa[0]) = %p\n&(pa[1]) = %p\n++pa = %p\n", pa, &pa, &(pa[0]), &(pa[1]), ++pa);
    printf("++pa = %p\n", ++pa);
}

int main (int argc, char *argv[]) {
    char *pa = "abcde";
    printf("ca = %p\n&ca = %p\n&(ca[0]) = %p\n&(ca[1]) = %p\n", ca, &ca, &(ca[0]), &(ca[1]));
    printf("pa = %p\n&pa = %p\n&(pa[0]) = %p\n&(pa[1]) = %p\n", pa, &pa, &(pa[0]), &(pa[1]));

    func(ca);
    func_ptr(pa);

    return 0;
}
```



**Output**

```C
ca = 0x55b7db946010
&ca = 0x55b7db946010
&(ca[0]) = 0x55b7db946010
&(ca[1]) = 0x55b7db946011
pa = 0x55b7db745993
&pa = 0x7ffd3ca51430
&(pa[0]) = 0x55b7db745993
&(pa[1]) = 0x55b7db745994
In func
ca = 0x55b7db946010
&ca = 0x7ffd3ca51408
&(ca[0]) = 0x55b7db946010
&(ca[1]) = 0x55b7db946011
In func_ptr
pa = 0x55b7db745994
&pa = 0x7ffd3ca51408
&(pa[0]) = 0x55b7db745994
&(pa[1]) = 0x55b7db745995
++pa = 0x55b7db745994
++pa = 0x55b7db745995
```

You may confused by the `&ca` ( output after `In func` ), actually, the array `ca` passed into `func` was **converted** into a pointer to the array.

Interestingly, there is no way to pass an array itself into a function, as **it is always automatically converted into a pointer to the array**. Of course, using the pointer inside the function, you can pretty much do most things you could have done with the original array. You won't get the right answer if you take the **size** of it, though.



`&pa` is the address of the pointer `pa` itself.

`pa` is the address of the first element of the string. 



> The last two lines `++pa` is related to the next topic.

# Execution of printf with ++ operators in C



**Example Code**

```C
#include<stdio.h>
int main() {
   volatile int x = 20;
   printf("%d %d\n", x, x++);
   x = 20;
   printf("%d %d\n", x++, x);
   x = 20;
   printf("%d %d %d ", x, x++, ++x);
   return 0;
}
```



Most of the compilers takes each parameter of `printf()` from right to left. So in the first `printf()` statement, the last parameter is `x++`, so this will be executed first, it will print 20, after that increase the value from 20 to 21. Now print the second last argument, and show 21. Like that other lines are also calculated in this manner. For `++x`, it will increase the value before printing, and for `x++`, it prints the value at first, then increase the value.

Please check the output to get the better understanding.

**Output**

```C
21 20
20 20
22 21 21
```



















