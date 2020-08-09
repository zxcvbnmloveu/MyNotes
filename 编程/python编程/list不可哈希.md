# `list不可哈希`


想给列表做个去重，想当然用哈希。

```python3
if __name__ == '__main__':
    a = [[1,2],[1,2],[3,4]]
    dic = set()
    for v in a:
        if v not in dic:
            dic.add(v)
```
结果遇到列表不能哈希。
#### 原因
Python不支持dict的key为list或dict类型，因为list和dict类型是unhashable（不可哈希）的。

```  File "/home/hzw/tmp/CDAN/pytorch/tes3.py", line 36, in <module>
    if v not in dic:
TypeError: unhashable type: 'list'
```
正确做法是把列表转为元组。

```python3
if __name__ == '__main__':

    a = [[1,2],[1,2],[3,4]]
    dic = set()
    for v in a:
        if tuple(v) not in dic:
            dic.add(tuple(v))
    print(list(map(list,dic)))
```

面试忙乎半天没弄出来。
