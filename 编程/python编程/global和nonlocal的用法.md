# `global和nonlocal的用法`

### nonlocal 可以改变外部的定义的变量值

```python3

def myfunc1():
  x = "Bill"
  def myfunc2():
    nonlocal x
    x = "hello"
  myfunc2() 
  return x

print(myfunc1())

#1 2 3

```

### global global 关键字用于从非全局范围创建全局变量，例如在函数内部。

```python3
# 创建函数：
def myfunction():
  global x
  x = "hello"

# 执行函数：
myfunction()

# x 现在有关是全局变量，可以进行全局访问。
print(x)
```
