---
title: INFO1110 Advance 练习
description: 正则表达式、密码校验、日志解析等练习题
---

# 主题 1：正则表达式

## 题 1.1 提取价格

```python
text = "苹果10元，香蕉5元，西瓜30元，榴莲298元"
# 期望输出: ['10', '5', '30', '298']
```

**要求**：用 `re.findall()` 提取所有价格数字。

---

## 题 1.2 验证密码强度

写一个函数 `check_password(pwd)`，判断密码是否合法：
- 长度 **8-16 位**
- 只能包含字母、数字、下划线

```python
check_password("abc123") # False（长度不够）
check_password("abc_12345") # True
check_password("hello world") # False（有空格）
check_password("a" * 20) # False（太长）
```

**提示**：`^[\w]{8,16}$`

---

## 题 1.3 提取并分组日志

```python
log = """
[2024-03-15 10:30:25] ERROR: 数据库连接失败
[2024-03-15 10:31:02] INFO: 用户登录
[2024-03-16 08:00:00] WARNING: 内存不足
"""
# 期望输出:
# [('2024-03-15', '10:30:25', 'ERROR'),
# ('2024-03-15', '10:31:02', 'INFO'),
# ('2024-03-16', '08:00:00', 'WARNING')]
```

**提示**：3 个分组 `()`

---

# 主题 2：递归 vs 迭代（同一函数两种写法）

> 每道题**用两种方式各写一遍**：递归 + 迭代（循环）

## 题 2.1 阶乘

`factorial(5)` → `120` （即 5×4×3×2×1）

```python
def factorial_recursive(n):
 # 递归实现
 pass

def factorial_iterative(n):
 # 用 for 循环实现
 pass

print(factorial_recursive(5)) # 120
print(factorial_iterative(5)) # 120
```

---

## 题 2.2 斐波那契数列

```
0, 1, 1, 2, 3, 5, 8, 13, 21, ...
fib(0) = 0
fib(1) = 1
fib(n) = fib(n-1) + fib(n-2)
```

```python
def fib_recursive(n):
 pass

def fib_iterative(n):
 pass

print(fib_recursive(10)) # 55
print(fib_iterative(10)) # 55
```

---

## 题 2.3 列表求和（不用 sum）

```python
def sum_recursive(lst):
 pass

def sum_iterative(lst):
 pass

print(sum_recursive([1, 2, 3, 4, 5])) # 15
print(sum_iterative([1, 2, 3, 4, 5])) # 15
```

**提示（递归）**：`sum([1,2,3]) = 1 + sum([2,3])`

---

# 主题 3：父类 / 子类（继承）

## 题 3.1 动物家族

写一个父类 `Animal` 和两个子类 `Dog`、`Cat`：

- `Animal` 有属性：`name`, `age`
- `Animal` 有方法：`speak()` → 打印 `"some sound"`
- `Dog` 重写 `speak()` → 打印 `"Woof!"`
- `Cat` 重写 `speak()` → 打印 `"Meow!"`

```python
d = Dog("Buddy", 3)
d.speak() # Woof!
print(d.name) # Buddy

c = Cat("Mimi", 2)
c.speak() # Meow!
```

---

## 题 3.2 员工工资

- 父类 `Employee`：`name`, `base_salary`，方法 `get_salary()` 返回基础工资
- 子类 `Manager`：多一个属性 `bonus`，`get_salary()` 返回 **基础工资 + 奖金**
- 子类 `Intern`：实习生工资是基础工资的 **50%**

```python
e = Employee("Alice", 5000)
print(e.get_salary()) # 5000

m = Manager("Bob", 8000, 3000)
print(m.get_salary()) # 11000

i = Intern("Charlie", 5000)
print(i.get_salary()) # 2500.0
```

**要求**：子类必须用 `super().__init__()`

---

## 题 3.3 形状面积

- 父类 `Shape`：方法 `area()` 抛异常 `NotImplementedError("子类必须实现")`
- 子类 `Rectangle`：属性 `width`, `height`，`area()` 返回 `width * height`
- 子类 `Circle`：属性 `radius`，`area()` 返回 `3.14 * radius ** 2`
- 子类 `Triangle`：属性 `base`, `height`，`area()` 返回 `0.5 * base * height`

```python
shapes = [Rectangle(3, 4), Circle(5), Triangle(6, 8)]
for s in shapes:
 print(s.area())
# 12
# 78.5
# 24.0
```

**核心考点**：多态（同一个 `area()` 方法名，不同实现）

---

# 主题 4：装饰器

## 装饰器速成（如果不熟）

```python
def my_decorator(func):
 def wrapper(*args, **kwargs):
 print("函数执行前")
 result = func(*args, **kwargs)
 print("函数执行后")
 return result
 return wrapper

@my_decorator
def say_hello():
 print("Hello")

say_hello()
# 输出:
# 函数执行前
# Hello
# 函数执行后
```

> **核心**：装饰器 = 一个**接收函数、返回新函数**的函数

---

## 题 4.1 计时器装饰器

写一个 `@timer` 装饰器，计算函数运行时间：

```python
import time

@timer
def slow_function():
 time.sleep(1)
 print("做完了")

slow_function()
# 输出:
# 做完了
# slow_function 运行时间: 1.00 秒
```

**提示**：用 `time.time()`

---

## 题 4.2 日志装饰器

写一个 `@log` 装饰器，打印函数名、参数、返回值：

```python
@log
def add(a, b):
 return a + b

result = add(3, 5)
# 输出:
# 调用 add，参数: (3, 5), {}
# add 返回: 8
```

**提示**：`*args, **kwargs`

---

## 题 4.3 重试装饰器（带参数）

写一个 `@retry(times=3)` 装饰器，函数失败时**自动重试 N 次**：

```python
import random

@retry(times=3)
def unstable():
 if random.random() < 0.7:
 raise ValueError("失败了")
 return "成功！"

print(unstable())
# 可能输出:
# 第 1 次失败: 失败了
# 第 2 次失败: 失败了
# 第 3 次成功: 成功！
```

**进阶考点**：**带参数的装饰器** = 三层嵌套函数

```python
def retry(times): # 第 1 层：接收装饰器参数
 def decorator(func): # 第 2 层：接收函数
 def wrapper(*args, **kwargs): # 第 3 层：实际执行
 ...
 return wrapper
 return decorator
```

---

# 主题 5：ASCII 乱码修复

## 背景知识

ASCII 表里：
- `'A'` = 65, `'B'` = 66, ..., `'Z'` = 90
- `'a'` = 97, `'b'` = 98, ..., `'z'` = 122
- `'0'` = 48, ..., `'9'` = 57

```python
ord('A') # 65 字符 → 数字
chr(65) # 'A' 数字 → 字符
```

---

## 题 5.1 凯撒密码解密（位移 +3）

加密时：每个字母往后移 3 位（`A→D`, `B→E` ...）
**解密**：每个字母往前移 3 位

```python
encrypted = "Khoor Zruog" # 原文 "Hello World" 加密后
# 写函数 decrypt(s) 还原成 "Hello World"

print(decrypt("Khoor Zruog")) # Hello World
```

**提示**：
- 用 `ord()` 转数字 → `-3` → `chr()` 转回来
- **非字母（空格、标点）保持不变**
- 不要解密空格

---

## 题 5.2 修复大小写颠倒

某乱码把**大小写全反了**，写函数还原：

```python
fix("hELLO wORLD") # "Hello World"
fix("pYTHON iS fUN") # "Python Is Fun"
```

**提示**：
- 大写字母（65-90）→ 加 32 变小写
- 小写字母（97-122）→ 减 32 变大写
- 其他字符不动

> 不准用 `.swapcase()`！要手动操作 ASCII。

---

## 题 5.3 修复"偏移乱码"（自动检测偏移量）

文本被加密成奇怪的字符，但你**知道原文以 `"Hello"` 开头**，请：
1. 算出偏移量
2. 还原所有字母

```python
encrypted = "Mjqqt%|twqi" # 原文 "Hello world" 偏移了多少？

# 思路：
# 'H' (72) → 'M' (77) 偏移 +5
# 所以全部 -5 还原

print(fix_offset(encrypted, "Hello")) # Hello world
```

**进阶**：写一个 `auto_fix(encrypted, known_prefix)` 自动算偏移

---

# 题目总览

| 主题 | | | |
|------|------|------|------|
| 正则 | 提取价格 | 验证密码 | 提取日志 |
| 递归/迭代 | 阶乘 | 斐波那契 | 列表求和 |
| 父类子类 | 动物 | 员工 | 形状 |
| 装饰器 | 计时器 | 日志 | 重试 |
| ASCII | 凯撒 | 大小写颠倒 | 自动偏移 |

---

# 推荐练习顺序

```
第 1 天：1.1 + 2.1 + 3.1 + 4.1 + 5.1 (全部一星，热身)
第 2 天：1.2 + 2.2 + 3.2 + 4.2 + 5.2 (二星，主力)
第 3 天：1.3 + 2.3 + 3.3 + 4.3 + 5.3 (三星，挑战)
```

---

## 做题约定

1. **一次发一道题的代码**（不要 5 道一起发，太乱）
2. **写完跑一下，把输出也发我**
3. **报错就直接发报错信息**，不要硬调
4. **想思路时先用注释写步骤**，再写代码

---

