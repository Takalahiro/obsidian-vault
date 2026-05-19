# JavaScript
JavaScript 是 Web 的编程语言。

所有现代的 HTML 页面都可以使用 JavaScript。

JavaScript 非常容易学。
![[Pasted image 20260511235328.png]]
## 为什么学习 JavaScript?

JavaScript 是 web 开发人员必须学习的 3 门语言中的一门：

1. **HTML** 定义了网页的内容
2. **CSS** 描述了网页的布局
3. **JavaScript** 控制了网页的行为
## 阅读本教程前，您需要了解的知识：

阅读本教程，您需要有以下基础：

- [[CSS 技术文档]]
- [[HyperText Markup Language (HTML) 技术文档]]
# JavaScript 简介

---

JavaScript 是互联网上最流行的脚本语言，这门语言可用于 HTML 和 web，更可广泛用于服务器、PC、笔记本电脑、平板电脑和智能手机等设备。

---

## JavaScript 是脚本语言

JavaScript 是一种轻量级的编程语言。

JavaScript 是可插入 HTML 页面的编程代码。

JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。



# JavaScript 基础笔记

## 1. 基础语法

### 1.1 变量声明

```javascript
// var - 函数作用域，可重复声明（不推荐）
var name = "张三";

// let - 块级作用域，不可重复声明
let age = 25;
age = 26; // 可以修改

// const - 块级作用域，不可重新赋值（常量）
const PI = 3.14159;
// PI = 3.14; // 报错

// const 对象的属性可以修改
const person = { name: "李四" };
person.name = "王五"; // 可以
// person = {}; // 报错
```

### 1.2 数据类型

#### 基本类型（Primitive Types）
```javascript
// 1. Number - 数字
let num = 42;
let float = 3.14;
let negative = -10;
let infinity = Infinity;
let notANumber = NaN;

// 2. String - 字符串
let str1 = "双引号";
let str2 = '单引号';
let str3 = `模板字符串 ${num}`; // 反引号，支持插值

// 3. Boolean - 布尔值
let isTrue = true;
let isFalse = false;

// 4. Undefined - 未定义
let x;
console.log(x); // undefined

// 5. Null - 空值
let empty = null;

// 6. Symbol - 唯一标识符（ES6）
let sym = Symbol("描述");

// 7. BigInt - 大整数（ES2020）
let bigNum = 9007199254740991n;
```

#### 引用类型（Reference Types）
```javascript
// Object - 对象
let obj = { name: "张三", age: 25 };

// Array - 数组
let arr = [1, 2, 3, 4, 5];

// Function - 函数
function greet() {
  console.log("Hello");
}

// Date - 日期
let now = new Date();

// RegExp - 正则表达式
let pattern = /abc/;
```

### 1.3 类型检查与转换

```javascript
// typeof 检查类型
typeof 42;          // "number"
typeof "hello";     // "string"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
typeof null;        // "object" (历史遗留bug)
typeof {};          // "object"
typeof [];          // "object"
typeof function(){}; // "function"

// 类型转换
String(123);        // "123"
Number("456");      // 456
Boolean(0);         // false
parseInt("42px");   // 42
parseFloat("3.14"); // 3.14

// 隐式转换
"5" + 3;           // "53" (字符串拼接)
"5" - 3;           // 2 (数字运算)
!!"hello";         // true (转布尔)
```

## 2. 运算符

### 2.1 算术运算符
```javascript
let a = 10, b = 3;

a + b;  // 13 加
a - b;  // 7  减
a * b;  // 30 乘
a / b;  // 3.333... 除
a % b;  // 1  取模（余数）
a ** b; // 1000 幂运算（ES2016）

// 自增自减
let x = 5;
x++;    // 后置自增，返回5，x变为6
++x;    // 前置自增，x变为7，返回7
x--;    // 后置自减
--x;    // 前置自减
```

### 2.2 比较运算符
```javascript
// 相等性
5 == "5";   // true  (宽松相等，会类型转换)
5 === "5";  // false (严格相等，不转换类型)
5 != "5";   // false
5 !== "5";  // true

// 大小比较
10 > 5;     // true
10 < 5;     // false
10 >= 10;   // true
10 <= 5;    // false
```

### 2.3 逻辑运算符
```javascript
// && 与（AND）
true && true;   // true
true && false;  // false

// || 或（OR）
true || false;  // true
false || false; // false

// ! 非（NOT）
!true;          // false
!false;         // true

// 短路求值
let result = null || "默认值";  // "默认值"
let value = true && "返回这个";  // "返回这个"

// 空值合并运算符（ES2020）
let count = 0;
count ?? 10;    // 0 (只有null/undefined才用默认值)
count || 10;    // 10 (0被视为假值)
```

### 2.4 其他运算符
```javascript
// 三元运算符
let age = 18;
let status = age >= 18 ? "成年" : "未成年";

// 可选链（ES2020）
let user = { address: { city: "北京" } };
user?.address?.city;     // "北京"
user?.contact?.phone;    // undefined (不报错)

// 展开运算符
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }
```

## 3. 控制流程

### 3.1 条件语句
```javascript
// if...else
let score = 85;
if (score >= 90) {
  console.log("优秀");
} else if (score >= 60) {
  console.log("及格");
} else {
  console.log("不及格");
}

// switch
let day = 3;
switch (day) {
  case 1:
    console.log("星期一");
    break;
  case 2:
    console.log("星期二");
    break;
  case 3:
    console.log("星期三");
    break;
  default:
    console.log("其他");
}
```

### 3.2 循环语句
```javascript
// for 循环
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}

// while 循环
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

// do...while 循环（至少执行一次）
let j = 0;
do {
  console.log(j);
  j++;
} while (j < 5);

// for...of 遍历数组
let arr = [10, 20, 30];
for (let value of arr) {
  console.log(value); // 10, 20, 30
}

// for...in 遍历对象属性
let obj = { a: 1, b: 2, c: 3 };
for (let key in obj) {
  console.log(key, obj[key]); // a 1, b 2, c 3
}

// break 和 continue
for (let i = 0; i < 10; i++) {
  if (i === 3) continue; // 跳过本次循环
  if (i === 7) break;    // 终止循环
  console.log(i);
}
```

## 4. 函数

### 4.1 函数声明
```javascript
// 函数声明（会提升）
function add(a, b) {
  return a + b;
}

// 函数表达式（不会提升）
const subtract = function(a, b) {
  return a - b;
};

// 箭头函数（ES6）
const multiply = (a, b) => a * b;

// 箭头函数多行
const divide = (a, b) => {
  if (b === 0) return "除数不能为0";
  return a / b;
};

// 单参数可省略括号
const square = x => x * x;

// 无参数
const greet = () => console.log("Hello");
```

### 4.2 函数参数
```javascript
// 默认参数
function greet(name = "访客") {
  return `你好，${name}`;
}

// 剩余参数
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3, 4); // 10

// 解构参数
function printUser({ name, age }) {
  console.log(`${name}, ${age}岁`);
}
printUser({ name: "张三", age: 25 });
```

### 4.3 作用域与闭包
```javascript
// 作用域
let global = "全局变量";

function outer() {
  let outerVar = "外部变量";
  
  function inner() {
    let innerVar = "内部变量";
    console.log(global);    // 可访问
    console.log(outerVar);  // 可访问
    console.log(innerVar);  // 可访问
  }
  
  inner();
  // console.log(innerVar); // 报错，无法访问
}

// 闭包
function createCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

### 4.4 this 关键字
```javascript
// 普通函数中的 this
function showThis() {
  console.log(this); // 浏览器中是 window，严格模式下是 undefined
}

// 对象方法中的 this
const person = {
  name: "张三",
  greet: function() {
    console.log(this.name); // "张三"
  }
};

// 箭头函数没有自己的 this，继承外层
const obj = {
  name: "李四",
  greet: () => {
    console.log(this.name); // undefined（继承全局）
  },
  sayHi: function() {
    const inner = () => {
      console.log(this.name); // "李四"（继承 sayHi 的 this）
    };
    inner();
  }
};

// call, apply, bind 改变 this
function introduce(greeting) {
  console.log(`${greeting}, 我是${this.name}`);
}

const user = { name: "王五" };
introduce.call(user, "你好");      // "你好, 我是王五"
introduce.apply(user, ["嗨"]);     // "嗨, 我是王五"
const boundFunc = introduce.bind(user, "Hello");
boundFunc();                        // "Hello, 我是王五"
```

## 5. 数组

### 5.1 数组基础
```javascript
// 创建数组
let arr1 = [1, 2, 3, 4, 5];
let arr2 = new Array(5);        // 长度为5的空数组
let arr3 = Array.of(1, 2, 3);   // [1, 2, 3]

// 访问元素
arr1[0];        // 1
arr1[arr1.length - 1]; // 5

// 修改元素
arr1[0] = 10;

// 数组长度
arr1.length;    // 5
```

### 5.2 数组方法
```javascript
let arr = [1, 2, 3, 4, 5];

// 添加/删除元素
arr.push(6);           // 末尾添加，返回新长度
arr.pop();             // 末尾删除，返回删除的元素
arr.unshift(0);        // 开头添加
arr.shift();           // 开头删除
arr.splice(2, 1, 99);  // 从索引2删除1个，插入99

// 查找元素
arr.indexOf(3);        // 2（索引）
arr.includes(3);       // true
arr.find(x => x > 3);  // 4（第一个满足条件的元素）
arr.findIndex(x => x > 3); // 3（索引）

// 数组转换
arr.slice(1, 3);       // [2, 3]（截取，不改变原数组）
arr.concat([6, 7]);    // [1,2,3,4,5,6,7]（合并）
arr.join("-");         // "1-2-3-4-5"（转字符串）
arr.reverse();         // 反转（改变原数组）
arr.sort();            // 排序（改变原数组）
arr.sort((a, b) => a - b); // 数字升序

// 高阶方法
arr.forEach(x => console.log(x));           // 遍历
arr.map(x => x * 2);                        // [2,4,6,8,10]
arr.filter(x => x > 2);                     // [3,4,5]
arr.reduce((sum, x) => sum + x, 0);         // 15（累加）
arr.every(x => x > 0);                      // true（所有元素满足）
arr.some(x => x > 4);                       // true（至少一个满足）

// ES6+ 方法
arr.flat();            // 数组扁平化
arr.flatMap(x => [x, x * 2]); // map + flat
Array.from("hello");   // ["h","e","l","l","o"]
```

### 5.3 数组解构
```javascript
let [a, b, c] = [1, 2, 3];
console.log(a, b, c); // 1 2 3

// 跳过元素
let [first, , third] = [1, 2, 3];

// 剩余元素
let [head, ...tail] = [1, 2, 3, 4];
console.log(head, tail); // 1 [2,3,4]

// 默认值
let [x = 10, y = 20] = [5];
console.log(x, y); // 5 20
```

## 6. 对象

### 6.1 对象基础
```javascript
// 创建对象
let obj1 = { name: "张三", age: 25 };
let obj2 = new Object();
obj2.name = "李四";

// 访问属性
obj1.name;          // "张三"（点表示法）
obj1["age"];        // 25（方括号表示法）

// 添加/修改属性
obj1.city = "北京";
obj1.age = 26;

// 删除属性
delete obj1.city;

// 检查属性
"name" in obj1;           // true
obj1.hasOwnProperty("name"); // true

// 属性简写（ES6）
let name = "王五", age = 30;
let person = { name, age }; // { name: "王五", age: 30 }

// 计算属性名
let key = "score";
let student = { [key]: 95 }; // { score: 95 }

// 方法简写
let obj = {
  greet() {
    console.log("Hello");
  }
};
```

### 6.2 对象方法
```javascript
let obj = { a: 1, b: 2, c: 3 };

// 获取键/值/键值对
Object.keys(obj);      // ["a", "b", "c"]
Object.values(obj);    // [1, 2, 3]
Object.entries(obj);   // [["a",1], ["b",2], ["c",3]]

// 合并对象
Object.assign({}, obj, { d: 4 }); // { a:1, b:2, c:3, d:4 }
let merged = { ...obj, d: 4 };    // 展开运算符（推荐）

// 冻结对象
Object.freeze(obj);    // 不可修改
Object.seal(obj);      // 不可添加/删除属性，可修改现有属性

// 对象转换
JSON.stringify(obj);   // '{"a":1,"b":2,"c":3}'
JSON.parse('{"a":1}'); // { a: 1 }
```

### 6.3 对象解构
```javascript
let person = { name: "张三", age: 25, city: "北京" };

// 基本解构
let { name, age } = person;

// 重命名
let { name: userName, age: userAge } = person;

// 默认值
let { name, country = "中国" } = person;

// 剩余属性
let { name, ...rest } = person;
console.log(rest); // { age: 25, city: "北京" }

// 嵌套解构
let user = {
  info: { name: "李四", age: 30 },
  address: { city: "上海" }
};
let { info: { name }, address: { city } } = user;
```

## 7. 字符串

### 7.1 字符串方法
```javascript
let str = "Hello World";

// 长度
str.length;            // 11

// 访问字符
str[0];                // "H"
str.charAt(0);         // "H"
str.charCodeAt(0);     // 72（字符编码）

// 查找
str.indexOf("o");      // 4
str.lastIndexOf("o");  // 7
str.includes("World"); // true
str.startsWith("Hello"); // true
str.endsWith("World"); // true

// 提取
str.slice(0, 5);       // "Hello"
str.substring(0, 5);   // "Hello"
str.substr(0, 5);      // "Hello"（已废弃）

// 替换
str.replace("World", "JS");     // "Hello JS"
str.replaceAll("o", "0");       // "Hell0 W0rld"

// 大小写
str.toLowerCase();     // "hello world"
str.toUpperCase();     // "HELLO WORLD"

// 去空格
"  hello  ".trim();    // "hello"
"  hello  ".trimStart(); // "hello  "
"  hello  ".trimEnd(); // "  hello"

// 分割/连接
str.split(" ");        // ["Hello", "World"]
["Hello", "World"].join(" "); // "Hello World"

// 重复/填充
"abc".repeat(3);       // "abcabcabc"
"5".padStart(3, "0");  // "005"
"5".padEnd(3, "0");    // "500"
```

### 7.2 模板字符串
```javascript
let name = "张三";
let age = 25;

// 基本用法
let message = `你好，${name}！你今年${age}岁。`;

// 多行字符串
let html = `
  <div>
    <h1>${name}</h1>
    <p>年龄：${age}</p>
  </div>
`;

// 表达式
let result = `1 + 1 = ${1 + 1}`;

// 标签模板
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return result + str + (values[i] ? `<strong>${values[i]}</strong>` : "");
  }, "");
}

let output = highlight`姓名：${name}，年龄：${age}`;
```

## 8. ES6+ 新特性

### 8.1 解构赋值
```javascript
// 数组解构
let [a, b] = [1, 2];

// 对象```markdown
// 对象解构
let { name, age } = { name: "张三", age: 25 };

// 函数参数解构
function greet({ name, age }) {
  console.log(`${name}, ${age}岁`);
}
```

### 8.2 展开运算符
```javascript
// 数组展开
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

// 对象展开
let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }

// 函数参数展开
Math.max(...[1, 5, 3]); // 5

// 复制数组/对象（浅拷贝）
let arrCopy = [...arr1];
let objCopy = { ...obj1 };
```

### 8.3 Promise 与异步
```javascript
// Promise 基础
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("成功");
    // reject("失败");
  }, 1000);
});

promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("完成"));

// Promise 链式调用
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Promise 静态方法
Promise.all([promise1, promise2])      // 全部成功才成功
  .then(results => console.log(results));

Promise.race([promise1, promise2])     // 第一个完成的结果
  .then(result => console.log(result));

Promise.allSettled([promise1, promise2]) // 等待全部完成
  .then(results => console.log(results));

Promise.any([promise1, promise2])      // 第一个成功的结果
  .then(result => console.log(result));

// async/await（ES2017）
async function fetchData() {
  try {
    let response = await fetch("https://api.example.com/data");
    let data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error("错误：", error);
  }
}

// 并行执行
async function parallel() {
  let [result1, result2] = await Promise.all([
    fetch("/api/1").then(r => r.json()),
    fetch("/api/2").then(r => r.json())
  ]);
}
```

### 8.4 Class 类
```javascript
// 类定义
class Person {
  // 构造函数
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  // 实例方法
  greet() {
    console.log(`你好，我是${this.name}`);
  }
  
  // 静态方法
  static create(name, age) {
    return new Person(name, age);
  }
  
  // Getter
  get info() {
    return `${this.name}, ${this.age}岁`;
  }
  
  // Setter
  set info(value) {
    [this.name, this.age] = value.split(",");
  }
}

// 使用类
let person = new Person("张三", 25);
person.greet();
console.log(person.info);

// 继承
class Student extends Person {
  constructor(name, age, grade) {
    super(name, age); // 调用父类构造函数
    this.grade = grade;
  }
  
  // 重写方法
  greet() {
    super.greet(); // 调用父类方法
    console.log(`我是${this.grade}年级学生`);
  }
}

let student = new Student("李四", 18, 12);
student.greet();

// 私有字段（ES2022）
class BankAccount {
  #balance = 0; // 私有字段
  
  deposit(amount) {
    this.#balance += amount;
  }
  
  getBalance() {
    return this.#balance;
  }
}
```

### 8.5 模块化
```javascript
// 导出（export）
// math.js
export const PI = 3.14159;
export function add(a, b) {
  return a + b;
}
export default function multiply(a, b) {
  return a * b;
}

// 导入（import）
// main.js
import multiply, { PI, add } from "./math.js";
import * as math from "./math.js"; // 导入全部

console.log(PI);
console.log(add(2, 3));
console.log(multiply(2, 3));
console.log(math.PI);

// 动态导入
async function loadModule() {
  const module = await import("./math.js");
  console.log(module.PI);
}
```

### 8.6 其他新特性
```javascript
// Map 和 Set
let map = new Map();
map.set("name", "张三");
map.set("age", 25);
map.get("name");        // "张三"
map.has("age");         // true
map.delete("age");
map.size;               // 1

let set = new Set([1, 2, 3, 3, 4]);
console.log(set);       // Set {1, 2, 3, 4}
set.add(5);
set.has(3);             // true
set.delete(3);
set.size;               // 4

// Symbol
let sym1 = Symbol("描述");
let sym2 = Symbol("描述");
sym1 === sym2;          // false（每个Symbol都是唯一的）

let obj = {
  [sym1]: "值"
};

// 迭代器和生成器
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

let gen = generator();
gen.next();             // { value: 1, done: false }
gen.next();             // { value: 2, done: false }
gen.next();             // { value: 3, done: false }
gen.next();             // { value: undefined, done: true }

// for...of 遍历生成器
for (let value of generator()) {
  console.log(value);   // 1, 2, 3
}

// Proxy 代理
let target = { name: "张三" };
let proxy = new Proxy(target, {
  get(target, prop) {
    console.log(`读取 ${prop}`);
    return target[prop];
  },
  set(target, prop, value) {
    console.log(`设置 ${prop} = ${value}`);
    target[prop] = value;
    return true;
  }
});

proxy.name;             // 读取 name
proxy.age = 25;         // 设置 age = 25

// Reflect
Reflect.get(target, "name");
Reflect.set(target, "age", 25);
Reflect.has(target, "name");
Reflect.deleteProperty(target, "age");
```

## 9. DOM 操作

### 9.1 选择元素
```javascript
// 单个元素
document.getElementById("myId");
document.querySelector(".myClass");
document.querySelector("#myId");

// 多个元素
document.getElementsByClassName("myClass");
document.getElementsByTagName("div");
document.querySelectorAll(".myClass");
```

### 9.2 修改元素
```javascript
let element = document.querySelector("#myDiv");

// 修改内容
element.textContent = "纯文本";
element.innerHTML = "<strong>HTML内容</strong>";

// 修改属性
element.setAttribute("data-id", "123");
element.getAttribute("data-id");
element.removeAttribute("data-id");

// 修改样式
element.style.color = "red";
element.style.backgroundColor = "blue";
element.classList.add("active");
element.classList.remove("hidden");
element.classList.toggle("visible");
element.classList.contains("active");

// 修改数据属性
element.dataset.userId = "123";
console.log(element.dataset.userId);
```

### 9.3 创建和删除元素
```javascript
// 创建元素
let newDiv = document.createElement("div");
newDiv.textContent = "新元素";
newDiv.className = "box";

// 添加元素
let parent = document.querySelector("#parent");
parent.appendChild(newDiv);           // 末尾添加
parent.insertBefore(newDiv, parent.firstChild); // 开头添加
parent.append(newDiv);                // 末尾添加（可添加多个）
parent.prepend(newDiv);               // 开头添加

// 删除元素
newDiv.remove();                      // 删除自己
parent.removeChild(newDiv);           // 父元素删除子元素

// 替换元素
parent.replaceChild(newDiv, oldDiv);
```

### 9.4 事件处理
```javascript
let button = document.querySelector("#myButton");

// 添加事件监听
button.addEventListener("click", function(event) {
  console.log("按钮被点击");
  console.log(event.target);          // 触发事件的元素
  event.preventDefault();             // 阻止默认行为
  event.stopPropagation();            // 阻止事件冒泡
});

// 移除事件监听
function handleClick(event) {
  console.log("点击");
}
button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);

// 常见事件
element.addEventListener("click", handler);      // 点击
element.addEventListener("dblclick", handler);   // 双击
element.addEventListener("mouseenter", handler); // 鼠标进入
element.addEventListener("mouseleave", handler); // 鼠标离开
element.addEventListener("keydown", handler);    // 键盘按下
element.addEventListener("keyup", handler);      // 键盘抬起
element.addEventListener("submit", handler);     // 表单提交
element.addEventListener("input", handler);      // 输入变化
element.addEventListener("change", handler);     // 值改变
element.addEventListener("focus", handler);      // 获得焦点
element.addEventListener("blur", handler);       // 失去焦点

// 事件委托
document.querySelector("#list").addEventListener("click", function(event) {
  if (event.target.tagName === "LI") {
    console.log("点击了列表项：", event.target.textContent);
  }
});
```

## 10. 常见操作

### 10.1 定时器
```javascript
// setTimeout - 延迟执行一次
let timeoutId = setTimeout(() => {
  console.log("3秒后执行");
}, 3000);

// 取消定时器
clearTimeout(timeoutId);

// setInterval - 重复执行
let intervalId = setInterval(() => {
  console.log("每2秒执行一次");
}, 2000);

// 取消定时器
clearInterval(intervalId);

// 倒计时示例
let count = 10;
let countdown = setInterval(() => {
  console.log(count);
  count--;
  if (count < 0) {
    clearInterval(countdown);
    console.log("倒计时结束");
  }
}, 1000);
```

### 10.2 本地存储
```javascript
// localStorage - 永久存储
localStorage.setItem("username", "张三");
localStorage.getItem("username");     // "张三"
localStorage.removeItem("username");
localStorage.clear();                 // 清空所有

// 存储对象
let user = { name: "张三", age: 25 };
localStorage.setItem("user", JSON.stringify(user));
let savedUser = JSON.parse(localStorage.getItem("user"));

// sessionStorage - 会话存储（关闭标签页后清除）
sessionStorage.setItem("token", "abc123");
sessionStorage.getItem("token");
```

### 10.3 错误处理
```javascript
// try...catch
try {
  let result = riskyOperation();
  console.log(result);
} catch (error) {
  console.error("发生错误：", error.message);
} finally {
  console.log("无论如何都会执行");
}

// 抛出错误
function divide(a, b) {
  if (b === 0) {
    throw new Error("除数不能为0");
  }
  return a / b;
}

// 自定义错误
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

throw new ValidationError("验证失败");

// 全局错误处理
window.addEventListener("error", function(event) {
  console.error("全局错误：", event.error);
});

// Promise 错误处理
window.addEventListener("unhandledrejection", function(event) {
  console.error("未处理的Promise拒绝：", event.reason);
});
```

### 10.4 正则表达式
[[正则表达式 Regular Expression]]
```javascript
// 创建正则
let regex1 = /abc/;
let regex2 = new RegExp("abc");

// 测试匹配
/hello/.test("hello world");          // true

// 查找匹配
"hello world".match(/o/g);            // ["o", "o"]
"hello world".search(/world/);        // 6（索引）

// 替换
"hello world".replace(/o/g, "0");     // "hell0 w0rld"

// 分割
"a,b,c".split(/,/);                   // ["a", "b", "c"]

// 常用模式
let email = /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/;
let phone = /^1[3-9]\d{9}$/;
let url = /^https?:\/\/.+/;
let number = /^\d+$/;

// 捕获组
let dateRegex = /(\d{4})-(\d{2})-(\d{2})/;
let match = "2024-01-15".match(dateRegex);
console.log(match[1], match[2], match[3]); // 2024 01 15

// 命名捕获组
let regex = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
let result = "2024-01-15".match(regex);
console.log(result.groups.year);      // 2024
```

### 10.5 常用工具函数
```javascript
// 防抖（debounce）
function debounce(func, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

// 使用
let search = debounce(function(query) {
  console.log("搜索：", query);
}, 500);

// 节流（throttle）
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// 深拷贝
function deepClone(obj) {
  if (obj === null || typeof obj !== "object") return obj;
  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof Array) return obj.map(item => deepClone(item));
  
  let cloned = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      cloned[key] = deepClone(obj[key]);
    }
  }
  return cloned;
}

// 简单版（不处理特殊情况）
let deepCopy = JSON.parse(JSON.stringify(obj));

// 数组去重
let unique1 = [...new Set(array)];
let unique2 = array.filter((item, index) => array.indexOf(item) === index);

// 数组扁平化
let flat1 = array.flat(Infinity);
let flat2 = array.reduce((acc, val) => 
  Array.isArray(val) ? acc.concat(flat2(val)) : acc.concat(val), []);

// 随机数
function random(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// 格式化日期
function formatDate(date) {
  let year = date.getFullYear();
  let month = String(d```markdown
  let month = String(date.getMonth() + 1).padStart(2, "0");
  let day = String(date.getDate()).padStart(2, "0");
  return `${year}-${month}-${day}`;
}

// 判断数据类型
function getType(value) {
  return Object.prototype.toString.call(value).slice(8, -1).toLowerCase();
}
getType([]);        // "array"
getType({});        // "object"
getType(null);      // "null"
```

## 11. 常见概念

### 11.1 变量提升
```javascript
// var 会提升
console.log(x);     // undefined（不报错）
var x = 5;

// 等价于
var x;
console.log(x);
x = 5;

// let/const 不会提升（暂时性死区）
console.log(y);     // 报错：Cannot access 'y' before initialization
let y = 10;

// 函数声明会提升
greet();            // "Hello"（可以调用）
function greet() {
  console.log("Hello");
}

// 函数表达式不会提升
sayHi();            // 报错
const sayHi = function() {
  console.log("Hi");
};
```

### 11.2 值类型 vs 引用类型
```javascript
// 值类型（基本类型）- 复制值
let a = 10;
let b = a;
b = 20;
console.log(a);     // 10（a 不变）

// 引用类型 - 复制引用（地址）
let obj1 = { name: "张三" };
let obj2 = obj1;
obj2.name = "李四";
console.log(obj1.name); // "李四"（obj1 也变了）

// 比较
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
arr1 == arr2;       // false（比较引用地址）
arr1 === arr2;      // false

// 函数参数
function change(num, obj) {
  num = 100;        // 不影响外部
  obj.name = "王五"; // 影响外部
}

let n = 10;
let person = { name: "张三" };
change(n, person);
console.log(n);           // 10
console.log(person.name); // "王五"
```

### 11.3 作用域链
```javascript
let global = "全局";

function outer() {
  let outerVar = "外层";
  
  function inner() {
    let innerVar = "内层";
    console.log(innerVar);  // 找到：内层
    console.log(outerVar);  // 向上找：外层
    console.log(global);    // 继续向上：全局
  }
  
  inner();
}

outer();
```

### 11.4 事件循环（Event Loop）
```javascript
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");

// 输出顺序：1, 4, 3, 2
// 解释：
// 1. 同步代码先执行：1, 4
// 2. 微任务（Promise）：3
// 3. 宏任务（setTimeout）：2
```

### 11.5 严格模式
```javascript
"use strict";

// 严格模式下的限制：
// 1. 变量必须声明
x = 10;             // 报错

// 2. 禁止删除变量
let y = 20;
delete y;           // 报错

// 3. 函数参数不能重名
function test(a, a) {} // 报错

// 4. this 不会指向全局对象
function show() {
  console.log(this); // undefined（非严格模式是 window）
}

// 5. 禁止八进制字面量
let num = 010;      // 报错
```

## 12. 常见面试题

### 12.1 数据类型判断
```javascript
// typeof 的局限性
typeof null;        // "object"（bug）
typeof [];          // "object"
typeof function(){}; // "function"

// 准确判断
Object.prototype.toString.call([]);     // "[object Array]"
Object.prototype.toString.call(null);   // "[object Null]"
Array.isArray([]);                      // true
```

### 12.2 == vs ===
```javascript
// == 会类型转换
5 == "5";           // true
0 == false;         // true
null == undefined;  // true

// === 严格相等
5 === "5";          // false
0 === false;        // false
null === undefined; // false

// 推荐使用 ===
```

### 12.3 浅拷贝 vs 深拷贝
```javascript
let original = { a: 1, b: { c: 2 } };

// 浅拷贝 - 只复制第一层
let shallow1 = { ...original };
let shallow2 = Object.assign({}, original);

shallow1.a = 10;           // 不影响 original
shallow1.b.c = 20;         // 影响 original（嵌套对象共享引用）

// 深拷贝 - 完全独立
let deep1 = JSON.parse(JSON.stringify(original));
// 注意：无法处理函数、undefined、Symbol、循环引用

// 手动深拷贝
function deepClone(obj) {
  if (obj === null || typeof obj !== "object") return obj;
  let clone = Array.isArray(obj) ? [] : {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      clone[key] = deepClone(obj[key]);
    }
  }
  return clone;
}
```

### 12.4 闭包应用
```javascript
// 1. 数据私有化
function createCounter() {
  let count = 0;
  return {
    increment() { return ++count; },
    decrement() { return --count; },
    getCount() { return count; }
  };
}

let counter = createCounter();
counter.increment(); // 1
counter.increment(); // 2
// count 无法直接访问

// 2. 循环中的闭包问题
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 输出：3, 3, 3（var 是函数作用域）

// 解决方法1：使用 let
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 输出：0, 1, 2

// 解决方法2：立即执行函数
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(() => console.log(j), 100);
  })(i);
}
```

### 12.5 数组常见操作
```javascript
let arr = [1, 2, 3, 4, 5];

// 求和
let sum = arr.reduce((acc, val) => acc + val, 0);

// 求最大值
let max = Math.max(...arr);

// 数组去重
let unique = [...new Set(arr)];

// 数组扁平化
let nested = [1, [2, [3, [4]]]];
let flat = nested.flat(Infinity);

// 数组分组
let numbers = [1, 2, 3, 4, 5, 6];
let grouped = numbers.reduce((acc, num) => {
  let key = num % 2 === 0 ? "even" : "odd";
  (acc[key] = acc[key] || []).push(num);
  return acc;
}, {});
// { odd: [1,3,5], even: [2,4,6] }

// 数组交集
let arr1 = [1, 2, 3];
let arr2 = [2, 3, 4];
let intersection = arr1.filter(x => arr2.includes(x));

// 数组差集
let difference = arr1.filter(x => !arr2.includes(x));
```

### 12.6 对象常见操作
```javascript
let obj = { a: 1, b: 2, c: 3 };

// 对象遍历
for (let key in obj) {
  console.log(key, obj[key]);
}

Object.keys(obj).forEach(key => {
  console.log(key, obj[key]);
});

// 对象过滤
let filtered = Object.fromEntries(
  Object.entries(obj).filter(([key, value]) => value > 1)
);
// { b: 2, c: 3 }

// 对象映射
let mapped = Object.fromEntries(
  Object.entries(obj).map(([key, value]) => [key, value * 2])
);
// { a: 2, b: 4, c: 6 }

// 合并对象
let obj1 = { a: 1, b: 2 };
let obj2 = { b: 3, c: 4 };
let merged = { ...obj1, ...obj2 }; // { a: 1, b: 3, c: 4 }
```

## 13. 最佳实践

### 13.1 命名规范
```javascript
// 变量和函数：小驼峰
let userName = "张三";
function getUserInfo() {}

// 常量：全大写下划线
const MAX_COUNT = 100;
const API_URL = "https://api.example.com";

// 类：大驼峰
class UserService {}

// 私有变量：下划线开头（约定）
let _privateVar = "私有";

// 布尔值：is/has/can 开头
let isActive = true;
let hasPermission = false;
let canEdit = true;
```

### 13.2 代码风格
```javascript
// 使用 const/let，避免 var
const name = "张三";
let age = 25;

// 使用 === 而不是 ==
if (value === 10) {}

// 使用模板字符串
let message = `你好，${name}`;

// 使用箭头函数
let double = x => x * 2;

// 使用解构
let { name, age } = user;
let [first, second] = array;

// 使用展开运算符
let newArr = [...oldArr, newItem];
let newObj = { ...oldObj, newProp: value };

// 提前返回，减少嵌套
function process(data) {
  if (!data) return;
  if (!data.valid) return;
  // 处理逻辑
}
```

### 13.3 性能优化
```javascript
// 1. 避免全局变量
(function() {
  let localVar = "局部变量";
})();

// 2. 缓存 DOM 查询
let element = document.querySelector("#myDiv");
// 多次使用 element，而不是重复查询

// 3. 事件委托
document.querySelector("#list").addEventListener("click", function(e) {
  if (e.target.tagName === "LI") {
    // 处理点击
  }
});

// 4. 防抖和节流
let search = debounce(searchFunction, 300);

// 5. 使用文档片段
let fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  let li = document.createElement("li");
  fragment.appendChild(li);
}
list.appendChild(fragment); // 一次性添加

// 6. 避免内存泄漏
// 移除事件监听
element.removeEventListener("click", handler);
// 清除定时器
clearInterval(intervalId);
```

---

## 总结

JavaScript 基础知识点：
1. **变量与数据类型**：let/const、7种基本类型、引用类型
2. **运算符**：算术、比较、逻辑、三元
3. **控制流程**：if/else、switch、for/while
4. **函数**：声明、表达式、箭头函数、作用域、闭包
5. **数组**：创建、方法、遍历、高阶函数
6. **对象**：创建、属性、方法、解构
7. **字符串**：方法、模板字符串
8. **ES6+**：解构、展开、Promise、async/await、Class、模块化
9. **DOM 操作**：选择、修改、创建、事件
10. **常用工具**：定时器、存储、错误处理、正则

**学习建议**：
- 多写代码，多练习
- 理解概念，不要死记硬背
- 从简单到复杂，循序渐进
- 查阅 MDN 文档深入学习
- 做小项目巩固知识
```

这份笔记涵盖了 JavaScript 的核心基础知识，适合初学者系统学习和快速查阅！