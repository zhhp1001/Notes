POSIX 是一个操作系统标准

```C
i = 1, 2;
```

逗号运算符在所有运算符中优先级最低，所以上面的语句相当于`(i = 1), 2`，`i`赋值为1，接着执行逗号右侧的运算，计算结果被丢弃，最终`i`为1。



```C
struct 结构标签(可选) {
    类型1 标识符1;
    类型2 标识符2;
    ...
}变量定义(可选);
```

加上结构标签后，我们就可以在将来的声明中用`struct 结构标签`作为`struct {内容...}`的简写形式了。

我们只编写一次代码，但在以后的维护过程中将多次阅读这些代码，所以我们应该关心代码是否容易阅读。

**C是一种弱类型语言**

**P65** 如何解析C语言的声明

`const`是只读，不能理解为常量

**P85** 数组与指针

`%p` is for printing a pointer address

我们使用**内存泄漏**这个词是因为一种稀有的资源正被一个进程榨干。

**P199**定义是声明的一种特殊情况，它分配内存空间，并可能提供一个初始值。

**P200**  只限于作为函数定义的形式参数时， `char s[];` 和 `char *s;`是一样的

