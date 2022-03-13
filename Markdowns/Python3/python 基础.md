## Python3 print 不换行
在 Python 3.x 中，我们可以在 print() 函数中添加 end="" 参数，这样就可以实现不换行效果。

在 Python3 中， print 函数的参数 end 默认值为 "\n"，即end="\n"，表示换行，给 end 赋值为空, 即end=""，就不会换行了

```python
print('12345', end=" ")  # 设置空格
```

## 标准数据类型
Python3 中有六个标准的数据类型：

- Number（数字）
    - int、float、bool、complex（复数）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- 不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）；
- 可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。

## Python 推导式
Python 推导式是一种独特的数据处理方式，可以从一个数据序列构建另一个新的数据序列的结构体。
```python
# 列表
[out_exp_res for out_exp in input_list if condition]
# 字典
{ key_expr: value_expr for value in collection if condition }
# 集合
{ expression for item in Sequence if conditional }
# 元组
(expression for item in Sequence if conditional )

>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
>>> new_names = [name.upper()for name in names if len(name)>3]
>>> print(new_names)
['ALICE', 'JERRY', 'WENDY', 'SMITH']
```