
# Java 与 Python 基础语法对比

## Program Structure（程序结构）

### Python
```python
# 直接写代码即可运行
print("Hello World")
```

### Java
```java
// 必须有 class 和 main method
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

**区别**：Java 是纯 object-oriented 语言，所有代码必须写在 class 里；Python 可以直接写 script。

---

## Statement Terminator & Code Block（语句结束符与代码块）

| 特性 | Python | Java |
|------|--------|------|
| Statement 结束 | 换行 | 必须用 `;` (semicolon) |
| Code block | Indentation（缩进 4 空格） | Curly braces `{ }` |
| Comment | `#` 或 `""" """` | `//` 或 `/* */` |

---

## Variable Declaration（变量声明）

### Python（Dynamic Typing 动态类型）
```python
x = 10          # 自动推断为 int
name = "Alice"  # 自动推断为 str
x = "hello"     # 可以随意改变 type
```

### Java（Static Typing 静态类型，必须声明 type）
```java
int x = 10;
String name = "Alice";
// x = "hello";  // 错误！type 不能改变

// Java 10+ 可用 var 让 compiler 推断
var y = 10;     // 仍然是 static typing
```

---

## Primitive Data Types（基本数据类型）

| 类型 | Python | Java |
|------|--------|------|
| Integer | `int`（无限大） | `byte`, `short`, `int`, `long` |
| Floating-point | `float` | `float`, `double` |
| Boolean | `True`, `False` | `true`, `false`（小写） |
| Character | 无单独 char 类型 | `char`（单引号 `'A'`） |
| String | `str`（单/双引号） | `String`（**只能双引号** `"A"`） |
| Null value | `None` | `null` |

---

## Input & Output（输入输出）

### Python
```python
name = input("请输入姓名: ")
print(f"你好, {name}")
```

### Java
```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
System.out.print("请输入姓名: ");
String name = sc.nextLine();
System.out.println("你好, " + name);
// 或使用 printf
System.out.printf("你好, %s%n", name);
```

---

## Operators（运算符差异）

| 操作 | Python | Java |
|------|--------|------|
| Integer division | `//` | `/`（两个 integer 相除自动为整除） |
| Exponentiation | `**` | `Math.pow(a, b)` |
| Logical AND/OR/NOT | `and`, `or`, `not` | `&&`, `\|\|`, `!` |
| Equality | `==`（值）, `is`（reference） | `==`（reference）, `.equals()`（值） |

**注意**：Java 中比较 String **必须**用 `.equals()`：
```java
String a = "hello";
if (a.equals("hello")) { ... }   // 正确
if (a == "hello") { ... }        // 错误！比较的是 reference
```

---

## Conditional Statement（条件语句）

### Python
```python
if x > 0:
    print("正数")
elif x == 0:
    print("零")
else:
    print("负数")
```

### Java
```java
if (x > 0) {
    System.out.println("正数");
} else if (x == 0) {
    System.out.println("零");
} else {
    System.out.println("负数");
}
```

**区别**：Java 条件必须用 parentheses `()`，用 `else if` 而不是 `elif`。

---

## Loops（循环）

### Python
```python
# for loop
for i in range(10):
    print(i)

# while loop
while x > 0:
    x -= 1
```

### Java
```java
// 传统 for loop
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}

// Enhanced for loop（类似 Python 的 for-in）
int[] arr = {1, 2, 3};
for (int n : arr) {
    System.out.println(n);
}

// while loop
while (x > 0) {
    x--;
}
```

---

## Array vs List（数组与列表）

### Python（List 长度可变）
```python
lst = [1, 2, 3]
lst.append(4)
lst.remove(2)
```

### Java（Array 长度固定）
```java
int[] arr = {1, 2, 3};
int[] arr2 = new int[5];   // 固定 length 5
// arr.length 获取长度（不是 method，是 field）

// 需要动态数组用 ArrayList
import java.util.ArrayList;
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.remove(Integer.valueOf(2));
```

---

## Function / Method（函数 / 方法）

### Python
```python
def add(a, b):
    return a + b

def greet(name="World"):  # Default parameter 默认参数
    return f"Hello, {name}"
```

### Java
```java
// 必须声明 return type 和 parameter type
public static int add(int a, int b) {
    return a + b;
}

// Java 没有 default parameter，需要用 method overloading 实现
public static String greet() {
    return greet("World");
}
public static String greet(String name) {
    return "Hello, " + name;
}
```

---

## Type Casting / Conversion（类型转换）

### Python
```python
x = int("123")
y = str(456)
z = float("3.14")
```

### Java
```java
int x = Integer.parseInt("123");
String y = String.valueOf(456);
double z = Double.parseDouble("3.14");

// Primitive type 间的强制转换 (casting)
int a = (int) 3.14;   // a = 3
```

---

## Class & Object（类与对象）

### Python
```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def greet(self):
        print(f"Hi, {self.name}")

p = Person("Alice")
p.greet()
```

### Java
```java
public class Person {
    private String name;   // 需声明 field
    
    public Person(String name) {   // Constructor 名 = class 名
        this.name = name;
    }
    
    public void greet() {
        System.out.println("Hi, " + name);
    }
}

Person p = new Person("Alice");   // 必须用 new 关键字
p.greet();
```

---

## Other Important Differences（其他重要区别）

| 特性 | Python | Java |
|------|--------|------|
| Compiled / Interpreted | Interpreted 解释型 | Compiled 编译型（编译成 bytecode） |
| Entry point | `if __name__ == "__main__":` | `public static void main(String[] args)` |
| Package manager | `pip` | `Maven` / `Gradle` |
| Exception syntax | `try/except/finally` | `try/catch/finally` |
| Import | `import module` | `import package.Class;` |
| Null check | `if x is None:` | `if (x == null)` |
| Multiple inheritance | 支持 | 不支持（但可 implement 多个 interface） |

---

## Exception Handling（异常处理对比）

### Python
```python
try:
    x = 10 / 0
except ZeroDivisionError as e:
    print(e)
finally:
    print("结束")
```

### Java
```java
try {
    int x = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println(e.getMessage());
} finally {
    System.out.println("结束");
}
```

---

## Access Modifiers（访问修饰符 —— Java 特有）

Python 用命名约定表示访问级别，Java 有严格的 keyword：

| Modifier | 作用范围 |
|----------|---------|
| `public` | 任何地方可访问 |
| `private` | 仅 class 内部 |
| `protected` | 同 package + 子类 |
| 默认（无修饰符） | 同 package 内 |

Python 对比：
- `name` → public
- `_name` → protected（约定）
- `__name` → private（name mangling）

---

