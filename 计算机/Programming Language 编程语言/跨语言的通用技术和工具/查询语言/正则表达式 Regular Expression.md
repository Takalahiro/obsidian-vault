正则表达式是一种用于匹配和操作文本的强大工具，它由普通字符和特殊字符（称为"元字符"）组成，用于描述要匹配的文本模式。

正则表达式可以在文本中查找、替换、提取和验证特定的模式。

例如：

- runoo+b，可以匹配 **runoob、runooob、runoooooob** 等，+ 号代表前面的字符必须至少出现一次（1 次或多次）
    
- runoo*b，可以匹配 **runob、runoob、runoooooob** 等，* 号代表前面的字符可以不出现，也可以出现一次或者多次（0 次、或 1 次、或多次）
    
- colou?r 可以匹配 **color** 或者 **colour**，? 问号代表前面的字符最多只可以出现一次（0 次或 1 次）
    

构造正则表达式的方法和创建数学表达式的方法一样——用多种元字符与运算符可以将小的表达式结合在一起，创建更大的表达式。正则表达式的组件可以是单个字符、字符集合、字符范围、字符间的选择或者所有这些组件的任意组合。

正则表达式作为一个模板，将某个字符模式与所搜索的字符串进行匹配。
[[Java 技术笔记]][[Python 技术文档]][[Javascript (ECMA-262 ) 技术文档]]
## 正则表达式（Regular Expression）

正则表达式是一种**通用的文本模式匹配工具**，几乎所有主流编程语言都支持，但它**不属于某个特定语言的语法**，而是一种**独立的文本处理技术**。

---

### 1. 正则表达式的定位

| 特性 | 说明 |
|-----|------|
| **独立性** | 正则表达式有自己的语法规则，独立于编程语言 |
| **通用性** | 几乎所有语言都支持（Java、Python、JavaScript、C++、Go 等） |
| **标准化** | 基于数学理论（有限状态自动机），有国际标准 |
| **应用场景** | 文本搜索、验证、替换、提取 |

**类比**：
- 正则表达式就像 **SQL**（数据库查询语言），是一种**领域特定语言（DSL）**
- 它不是编程语言的一部分，但可以在各种编程语言中使用

---

### 2. 正则表达式的基本语法

正则表达式的语法在各语言中**基本一致**，只有细微差异。


#### 基本元字符

| 符号      | 含义               | 示例                              |
| ------- | ---------------- | ------------------------------- |
| `.`     | 匹配任意单个字符（除换行符）   | `a.c` 匹配 `abc`, `a1c`           |
| `^`     | 匹配字符串开头          | `^Hello` 匹配以 Hello 开头           |
| `$`     | 匹配字符串结尾          | `world$` 匹配以 world 结尾           |
| `*`     | 匹配前面的字符 0 次或多次   | `ab*c` 匹配 `ac`, `abc`, `abbc`   |
| `+`     | 匹配前面的字符 1 次或多次   | `ab+c` 匹配 `abc`, `abbc`         |
| `?`     | 匹配前面的字符 0 次或 1 次 | `ab?c` 匹配 `ac`, `abc`           |
| `{n}`   | 匹配前面的字符恰好 n 次    | `a{3}` 匹配 `aaa`                 |
| `{n,}`  | 匹配前面的字符至少 n 次    | `a{2,}` 匹配 `aa`, `aaa`          |
| `{n,m}` | 匹配前面的字符 n 到 m 次  | `a{2,4}` 匹配 `aa`, `aaa`, `aaaa` |
| `[]`    | 字符集，匹配其中任意一个字符   | `[abc]` 匹配 `a`, `b`, `c`        |
| `[^]`   | 否定字符集            | `[^abc]` 匹配除 a, b, c 外的字符       |
| `\|`    | 或运算符             | `cat\|dog` 匹配 `cat` 或 `dog`     |
| `()`    | 分组               | `(ab)+` 匹配 `ab`, `abab`         |
| `\`     | 转义字符             | `\.` 匹配字面意义的点                   |

#### 预定义字符类

| 符号 | 含义 | 等价于 |
|-----|------|--------|
| `\d` | 数字 | `[0-9]` |
| `\D` | 非数字 | `[^0-9]` |
| `\w` | 单词字符（字母、数字、下划线） | `[a-zA-Z0-9_]` |
| `\W` | 非单词字符 | `[^a-zA-Z0-9_]` |
| `\s` | 空白字符（空格、制表符、换行符） | `[ \t\n\r\f]` |
| `\S` | 非空白字符 | `[^ \t\n\r\f]` |

---

### 3. 各语言中的正则表达式

虽然正则表达式语法基本一致，但各语言的**使用方式**略有不同。

#### Java 中的正则表达式

```java
import java.util.regex.*;

public class RegexDemo {
    public static void main(String[] args) {
        // 1. 匹配验证
        String email = "test@example.com";
        boolean isValid = email.matches("^[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,}$");
        System.out.println("邮箱格式正确: " + isValid);  // true
        
        // 2. 查找匹配
        String text = "我的电话是 13812345678，备用电话 13987654321";
        Pattern pattern = Pattern.compile("1[3-9]\\d{9}");
        Matcher matcher = pattern.matcher(text);
        
        while (matcher.find()) {
            System.out.println("找到电话: " + matcher.group());
        }
        // 输出：
        // 找到电话: 13812345678
        // 找到电话: 13987654321
        
        // 3. 替换
        String str = "Hello123World456";
        String result = str.replaceAll("\\d+", "*");
        System.out.println(result);  // Hello*World*
        
        // 4. 分割
        String data = "apple,banana;orange:grape";
        String[] fruits = data.split("[,;:]");
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        // 输出：apple banana orange grape
        
        // 5. 提取分组
        String date = "2025-05-12";
        Pattern datePattern = Pattern.compile("(\\d{4})-(\\d{2})-(\\d{2})");
        Matcher dateMatcher = datePattern.matcher(date);
        
        if (dateMatcher.find()) {
            System.out.println("年: " + dateMatcher.group(1));  // 2025
            System.out.println("月: " + dateMatcher.group(2));  // 05
            System.out.println("日: " + dateMatcher.group(3));  // 12
        }
    }
}
```

#### Python 中的正则表达式

```python
import re

# 1. 匹配验证
email = "test@example.com"
is_valid = bool(re.match(r'^[\w.-]+@[\w.-]+\.[a-zA-Z]{2,}$', email))
print(f"邮箱格式正确: {is_valid}")  # True

# 2. 查找匹配
text = "我的电话是 13812345678，备用电话 13987654321"
phones = re.findall(r'1[3-9]\d{9}', text)
print(phones)  # ['13812345678', '13987654321']

# 3. 替换
str = "Hello123World456"
result = re.sub(r'\d+', '*', str)
print(result)  # Hello*World*

# 4. 分割
data = "apple,banana;orange:grape"
fruits = re.split(r'[,;:]', data)
print(fruits)  # ['apple', 'banana', 'orange', 'grape']

# 5. 提取分组
date = "2025-05-12"
match = re.match(r'(\d{4})-(\d{2})-(\d{2})', date)
if match:
    print(f"年: {match.group(1)}")  # 2025
    print(f"月: {match.group(2)}")  # 05
    print(f"日: {match.group(3)}")  # 12
```

#### JavaScript 中的正则表达式

```javascript
// 1. 匹配验证
let email = "test@example.com";
let isValid = /^[\w.-]+@[\w.-]+\.[a-zA-Z]{2,}$/.test(email);
console.log("邮箱格式正确:", isValid);  // true

// 2. 查找匹配
let text = "我的电话是 13812345678，备用电话 13987654321";
let phones = text.match(/1[3-9]\d{9}/g);
console.log(phones);  // ['13812345678', '13987654321']

// 3. 替换
let str = "Hello123World456";
let result = str.replace(/\d+/g, '*');
console.log(result);  // Hello*World*

// 4. 分割
let data = "apple,banana;orange:grape";
let fruits = data.split(/[,;:]/);
console.log(fruits);  // ['apple', 'banana', 'orange', 'grape']

// 5. 提取分组
let date = "2025-05-12";
let match = date.match(/(\d{4})-(\d{2})-(\d{2})/);
if (match) {
    console.log("年:", match[1]);  // 2025
    console.log("月:", match[2]);  // 05
    console.log("日:", match[3]);  // 12
}
```

---

### 4. 常见应用场景

#### 场景1：验证格式

```java
// 手机号验证（中国大陆）
public static boolean isValidPhone(String phone) {
    return phone.matches("^1[3-9]\\d{9}$");
}

// 邮箱验证
public static boolean isValidEmail(String email) {
    return email.matches("^[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,}$");
}

// 身份证号验证（18位）
public static boolean isValidIdCard(String idCard) {
    return idCard.matches("^[1-9]\\d{5}(19|20)\\d{2}(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01])\\d{3}[\\dXx]$");
}

// URL 验证
public static boolean isValidUrl(String url) {
    return url.matches("^https?://[\\w.-]+(:\\d+)?(/.*)?$");
}

// IP 地址验证
public static boolean isValidIp(String ip) {
    return ip.matches("^((25[0-5]|2[0-4]\\d|1\\d{2}|[1-9]?\\d)\\.){3}(25[0-5]|2[0-4]\\d|1\\d{2}|[1-9]?\\d)$");
}

// 测试
public static void main(String[] args) {
    System.out.println(isValidPhone("13812345678"));     // true
    System.out.println(isValidEmail("test@qq.com"));     // true
    System.out.println(isValidUrl("https://www.baidu.com")); // true
    System.out.println(isValidIp("192.168.1.1"));        // true
}
```

#### 场景2：提取信息

```java
// 提取所有数字
public static void extractNumbers() {
    String text = "订单号：12345，金额：99.99元，数量：3件";
    Pattern pattern = Pattern.compile("\\d+(\\.\\d+)?");
    Matcher matcher = pattern.matcher(text);
    
    while (matcher.find()) {
        System.out.println(matcher.group());
    }
    // 输出：12345  99.99  3
}

// 提取所有邮箱
public static void extractEmails() {
    String text = "联系方式：admin@example.com 或 support@test.org";
    Pattern pattern = Pattern.compile("[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,}");
    Matcher matcher = pattern.matcher(text);
    
    while (matcher.find()) {
        System.out.println(matcher.group());
    }
    // 输出：admin@example.com  support@test.org
}

// 提取 HTML 标签内容
public static void extractHtmlContent() {
    String html = "<div>Hello</div><p>World</p>";
    Pattern pattern = Pattern.compile("<(\\w+)>(.*?)</\\1>");
    Matcher matcher = pattern.matcher(html);
    
    while (matcher.find()) {
        System.out.println("标签: " + matcher.group(1) + ", 内容: " + matcher.group(2));
    }
    // 输出：
    // 标签: div, 内容: Hello
    // 标签: p, 内容: World
}
```

#### 场景3：文本替换

```java
// 隐藏手机号中间4位
public static String hidePhone(String phone) {
    return phone.replaceAll("(\\d{3})\\d{4}(\\d{4})", "$1****$2");
}

// 隐藏邮箱用户名
public static String hideEmail(String email) {
    return email.replaceAll("(\\w{1,3})\\w*(@.*)", "$1***$2");
}

// 删除 HTML 标签
public static String removeHtmlTags(String html) {
    return html.replaceAll("<[^>]+>", "");
}

// 统一空白字符
public static String normalizeWhitespace(String text) {
    return text.replaceAll("\\s+", " ").trim();
}

// 测试
public static void main(String[] args) {
    System.out.println(hidePhone("13812345678"));        // 138****5678
    System.out.println(hideEmail("admin@example.com"));  // adm***@example.com
    System.out.println(removeHtmlTags("<p>Hello</p>"));  // Hello
    System.out.println(normalizeWhitespace("a  b\tc\nd")); // a b c d
}
```

#### 场景4：数据清洗

```java
// 提取纯数字
public static String extractDigits(String text) {
    return text.replaceAll("\\D", "");
}

// 提取纯字母
public static String extractLetters(String text) {
    return text.replaceAll("[^a-zA-Z]", "");
}

// 提取中文
public static String extractChinese(String text) {
    return text.replaceAll("[^\\u4e00-\\u9fa5]", "");
}

// 测试
public static void main(String[] args) {
    String text = "订单号：Order123，金额：99元";
    System.out.println(extractDigits(text));   // 12399
    System.out.println(extractLetters(text));  // Order
    System.out.println(extractChinese(text));  // 订单号金额元
}
```

---

### 5. 正则表达式的性能注意事项

```java
//  错误：每次都编译正则表达式
public static void badExample(String[] texts) {
    for (String text : texts) {
        // 每次循环都会编译正则表达式，性能差
        boolean match = text.matches("\\d+");
    }
}

//  正确：预编译正则表达式
public static void goodExample(String[] texts) {
    Pattern pattern = Pattern.compile("\\d+");  // 只编译一次
    for (String text : texts) {
        Matcher matcher = pattern.matcher(text);
        boolean match = matcher.matches();
    }
}

//  危险：回溯陷阱（可能导致性能问题）
// 示例：匹配重复的 a
String text = "aaaaaaaaaaaaaaaaaaaaaaaaaaab";
// 这个正则会导致大量回溯，性能极差
boolean match = text.matches("(a+)+b");

//  优化：避免嵌套量词
boolean match = text.matches("a+b");
```

---

### 6. 正则表达式的学习建议

**学习路径**：
1. **掌握基本语法**：元字符、字符类、量词
2. **练习常见场景**：验证、提取、替换
3. **使用在线工具**：
   - [regex101.com](https://regex101.com/) - 在线测试和学习
   - [regexr.com](https://regexr.com/) - 可视化正则表达式
4. **避免过度使用**：简单的字符串操作不需要正则

**常见误区**：
```java
//  过度使用正则
String result = text.replaceAll("a", "b");  // 简单替换不需要正则

//  使用普通方法
String result = text.replace("a", "b");  // 更快

//  正则表达式过于复杂
String regex = "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@$!%*?&])[A-Za-z\\d@$!%*?&]{8,}$";

//  分步验证更清晰
boolean hasLower = text.matches(".*[a-z].*");
boolean hasUpper = text.matches(".*[A-Z].*");
boolean hasDigit = text.matches(".*\\d.*");
boolean hasSpecial = text.matches(".*[@$!%*?&].*");
boolean isLongEnough = text.length() >= 8;
```

---

### 7. 总结

| 特性 | 说明 |
|-----|------|
| **定位** | 独立的文本处理工具，不属于某个编程语言 |
| **通用性** | 几乎所有语言都支持，语法基本一致 |
| **应用场景** | 验证、提取、替换、分割文本 |
| **学习难度** | 入门简单，精通需要大量练习 |
| **性能** | 复杂正则可能有性能问题，需要优化 |

**正则表达式是程序员的必备技能**，就像 SQL 一样，是一种**跨语言的通用工具**。掌握正则表达式可以大大提高文本处理效率。