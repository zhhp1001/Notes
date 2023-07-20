## Typedef 函数指针



## Tips

https://www.geeksforgeeks.org/function-pointer-in-c/

Many object oriented features in C++ are implemented using function pointers in C. For example [virtual functions](https://www.geeksforgeeks.org/virtual-functions-and-runtime-polymorphism-in-c-set-1-introduction/). Class methods are another example implemented using function pointers. Refer [this book](http://www.cs.rit.edu/~ats/books/ooc.pdf) for more details.

C语言的struct没用成员函数，但是可以使用函数指针来实现类似功能



## Basic

```C
typedef char (*PTRFUN)(int); 
PTRFUN pFun; 
char glFun(int a){ return;} 
void main() 
{ 
    pFun = glFun; 
    (*pFun)(2);  //pFun(2)
} 
```

typedef的功能是定义新的类型。第一句就是定义了一种PTRFUN的类型，并定义这种类型为指向某种函数的指针，这种函数以一个int为参数并返回char类型。后面就可以像使用int,char一样使用PTRFUN了。

第二行的代码便使用这个新类型定义了变量pFun，此时就可以像使用形式1一样使用这个变量了。



```C
#include <stdio.h>
#include <assert.h>
 
typedef int (*FP_CALC)(int,int);//定义一个函数指针类型
 
int add(int a, int b)
{
    return a + b;
}
 
int sub(int a, int b)
{
    return a - b;
}
 
int mul(int a, int b)
{
    return a * b;
}
 
int div(int a, int b)
{
    return b ? a/b : -1;
}
 
//定义一个函数，参数为op，返回一个指针,该指针类型为拥有两个int参数、
//返回类型为int的函数指针。它的作用是根据操作符返回相应函数的地址
FP_CALC calc_func(char op)
{
    switch( op )
    {
    case '+':
        return add;
    case '-':
        return sub;
    case '*':
        return mul;
    case '/':
        return div;
    default:
        return NULL;
    }
    return NULL;
}
 
//s_calc_func为函数，它的参数是 op，   
//返回值为一个拥有两个int参数、返回类型为int的函数指针  
int (*s_calc_func(char op)) (int , int)
{
    return calc_func(op);
}
 
//最终用户直接调用的函数，该函数接收两个int整数，
//和一个算术运算符，返回两数的运算结果
int calc(int a, int b, char op)
{
    FP_CALC fp = calc_func(op);
    int (*s_fp)(int,int) = s_calc_func(op);//用于测试
 
    assert(fp == s_fp);// 可以断言这两个是相等的
 
    if(fp)
        return fp(a,b);
    else
        return -1;
}
 
void main()
{
    int a = 100, b = 20;
 
    printf("calc(%d, %d, %c) = %d\n", a, b, '+', calc(a, b, '+'));
    printf("calc(%d, %d, %c) = %d\n", a, b, '-', calc(a, b, '-'));   
    printf("calc(%d, %d, %c) = %d\n", a, b, '*', calc(a, b, '*'));   
    printf("calc(%d, %d, %c) = %d\n", a, b, '/', calc(a, b, '/')); 
}
```





**Reference:**

**[1]** https://www.jianshu.com/p/75bc0e75cda2

**[2]** https://stackoverflow.com/questions/11038430/how-to-create-a-typedef-for-function-pointers