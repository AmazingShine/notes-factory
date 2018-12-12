# Python

## Notes

### 迭代器

- 遍历迭代器时不能在内部再次调用迭代器
```python
a = (x for x in range(10))
b = (x for x in range(10))
for x in a:
    print(a.__next__())
    print(b.__next__())

# 结果 a 和 b 不同
```

### 内置函数

- python3 filter返回 filter 对象,需要用list()转换

