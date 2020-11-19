# `yield`

```python3
def fun1(a):
    l = [1,2,3,4,5]
    for i in l:
        yield i
    yield 'fuck'
# yield 作用是生成一个生成器，fun1(),每次执行next的时候返回yield的值，中断。下一个next执行下一个yield.
l = [1,2,3,4,5]
iter = fun1(l)
for i in range(6):
    print(iter.__next__())

# 1
# 2
# 3
# 4
# 5
# fuck

# 生成器根据一定的规律算法生成的，当我们去遍历它的时候，它可以通过特定的算法不断的推算出相应的元素，
# 边运行边推算结果，从而节省了很多空间。
```
