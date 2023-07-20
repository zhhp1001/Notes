**直接执行的模块的名字是__main__**

```python
def main():
    # Todo: Add your code here
    pass

if __name__ == '__main__':
    func()
```

## class



**下划线**



[**super()**](https://realpython.com/python-super/#an-overview-of-pythons-super-function)

`super()` alone returns a temporary object of the superclass that then allows you to call that superclass’s methods.



## 文件和异常

关键字`with`

```python
"""
格式
with context [as var]
	pass
"""
```

其中`context`是一个表达式，返回的是一个对象，var用来保存`context`表达式返回的对象，可以有单个或者多个返回值。

```python
with open('hello.txt') as f:
    print(f.read())
    
print(f.closed)  # True
```

执行完`with`这个结构后，f会自动关闭。相当于自带了一个`finally`



## print

`print`打印默认换行，是`end='\n'`在起作用，

```python
for elem in range(10)
	print(elem, end='')
# 输出 0123456789
```



## 正则表达式

正则表达式是用于记录**文本规则**的代码



`0\d{2}-\d{8}`



## 进程和线程

join() 表示等待进程执行结束















