# CSS 完整笔记
[[HyperText Markup Language (HTML) 技术文档]]
---

## 1. CSS 基础

### 什么是 CSS
CSS (Cascading Style Sheets) 层叠样式表，用于控制网页的外观和布局。

### 三种引入方式

#### 1.1 内联样式（不推荐）
```html
<p style="color: red; font-size: 16px;">这是一段文字</p>
```

#### 1.2 内部样式表
```html
<head>
    <style>
        p {
            color: red;
            font-size: 16px;
        }
    </style>
</head>
```

#### 1.3 外部样式表（推荐）
```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

```css
/* style.css */
p {
    color: red;
    font-size: 16px;
}
```

### CSS 语法结构
```css
选择器 {
    属性名: 属性值;
    属性名: 属性值;
}
```

### 注释
```css
/* 这是单行注释 */

/*
 * 这是
 * 多行注释
 */
```

---

## 2. 选择器

### 2.1 基础选择器

#### 元素选择器
```css
p {
    color: blue;
}

h1 {
    font-size: 32px;
}
```

#### 类选择器
```css
.container {
    width: 1200px;
    margin: 0 auto;
}

.btn {
    padding: 10px 20px;
    background: #007bff;
}
```

```html
<div class="container">
    <button class="btn">点击</button>
</div>
```

#### ID 选择器
```css
#header {
    background: #333;
    color: white;
}
```

```html
<header id="header">网站头部</header>
```

#### 通配符选择器
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

### 2.2 组合选择器

#### 后代选择器（空格）
```css
/* 选择 div 内所有的 p */
div p {
    color: red;
}
```

#### 子选择器（>）
```css
/* 只选择 div 的直接子元素 p */
div > p {
    color: blue;
}
```

#### 相邻兄弟选择器（+）
```css
/* 选择紧跟在 h1 后面的第一个 p */
h1 + p {
    font-weight: bold;
}
```

#### 通用兄弟选择器（~）
```css
/* 选择 h1 后面所有的 p */
h1 ~ p {
    color: gray;
}
```

### 2.3 属性选择器

```css
/* 存在 title 属性 */
[title] {
    cursor: help;
}

/* title 属性等于 "hello" */
[title="hello"] {
    color: red;
}

/* title 属性包含 "hello" */
[title*="hello"] {
    color: blue;
}

/* title 属性以 "hello" 开头 */
[title^="hello"] {
    color: green;
}

/* title 属性以 "hello" 结尾 */
[title$="hello"] {
    color: orange;
}

/* type 属性为 "text" 的 input */
input[type="text"] {
    border: 1px solid #ccc;
}
```

### 2.4 伪类选择器

#### 链接伪类
```css
a:link {
    color: blue;          /* 未访问的链接 */
}

a:visited {
    color: purple;        /* 已访问的链接 */
}

a:hover {
    color: red;           /* 鼠标悬停 */
}

a:active {
    color: orange;        /* 鼠标点击时 */
}
```

#### 结构伪类
```css
/* 第一个子元素 */
li:first-child {
    font-weight: bold;
}

/* 最后一个子元素 */
li:last-child {
    border-bottom: none;
}

/* 第 n 个子元素 */
li:nth-child(2) {
    color: red;
}

/* 奇数行 */
tr:nth-child(odd) {
    background: #f5f5f5;
}

/* 偶数行 */
tr:nth-child(even) {
    background: white;
}

/* 每 3 个 */
li:nth-child(3n) {
    color: blue;
}

/* 唯一子元素 */
p:only-child {
    margin: 0;
}

/* 空元素 */
div:empty {
    display: none;
}
```

#### 表单伪类
```css
input:focus {
    border-color: #007bff;
    outline: none;
}

input:disabled {
    background: #e9ecef;
    cursor: not-allowed;
}

input:checked {
    /* 选中的复选框/单选框 */
}

input:valid {
    border-color: green;
}

input:invalid {
    border-color: red;
}
```

#### 其他伪类
```css
/* 非某个选择器 */
p:not(.special) {
    color: gray;
}

/* 目标元素（URL 锚点） */
:target {
    background: yellow;
}
```

### 2.5 伪元素选择器

```css
/* 第一行 */
p::first-line {
    font-weight: bold;
}

/* 第一个字母 */
p::first-letter {
    font-size: 2em;
    float: left;
}

/* 在元素前插入内容 */
.icon::before {
    content: "★ ";
    color: gold;
}

/* 在元素后插入内容 */
.required::after {
    content: " *";
    color: red;
}

/* 选中的文本 */
::selection {
    background: #007bff;
    color: white;
}

/* 占位符文本 */
input::placeholder {
    color: #999;
}
```

### 2.6 选择器优先级

**优先级从高到低：**
1. `!important`
2. 内联样式 (1000)
3. ID 选择器 (100)
4. 类/属性/伪类选择器 (10)
5. 元素/伪元素选择器 (1)
6. 通配符 (0)

```css
/* 优先级计算示例 */
p { color: black; }                    /* 1 */
.text { color: blue; }                 /* 10 */
#title { color: red; }                 /* 100 */
div p { color: green; }                /* 1 + 1 = 2 */
.container .text { color: purple; }    /* 10 + 10 = 20 */
#header .nav li { color: orange; }     /* 100 + 10 + 1 = 111 */

/* 强制最高优先级（慎用） */
p {
    color: pink !important;
}
```

---

## 3. 盒模型

### 3.1 盒模型组成

```
┌─────────────────────────────────┐
│         margin (外边距)          │
│  ┌───────────────────────────┐  │
│  │    border (边框)          │  │
│  │  ┌─────────────────────┐  │  │
│  │  │  padding (内边距)   │  │  │
│  │  │  ┌───────────────┐  │  │  │
│  │  │  │   content     │  │  │  │
│  │  │  │   (内容)      │  │  │  │
│  │  │  └───────────────┘  │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### 3.2 盒模型属性

```css
.box {
    /* 宽度和高度 */
    width: 300px;
    height: 200px;
    
    /* 内边距 */
    padding: 20px;                    /* 四边相同 */
    padding: 10px 20px;               /* 上下 左右 */
    padding: 10px 20px 30px;          /* 上 左右 下 */
    padding: 10px 20px 30px 40px;     /* 上 右 下 左（顺时针） */
    
    /* 单独设置 */
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 30px;
    padding-left: 40px;
    
    /* 边框 */
    border: 1px solid #ccc;           /* 宽度 样式 颜色 */
    border-width: 2px;
    border-style: solid;              /* solid, dashed, dotted, double */
    border-color: #333;
    
    /* 单独设置某一边 */
    border-top: 2px solid red;
    border-right: 1px dashed blue;
    border-bottom: 3px dotted green;
    border-left: 1px solid black;
    
    /* 圆角 */
    border-radius: 10px;              /* 四角相同 */
    border-radius: 10px 20px;         /* 左上右下 右上左下 */
    border-radius: 10px 20px 30px 40px; /* 左上 右上 右下 左下 */
    border-radius: 50%;               /* 圆形 */
    
    /* 外边距 */
    margin: 20px;
    margin: 10px 20px;
    margin: 10px 20px 30px 40px;
    
    /* 单独设置 */
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 30px;
    margin-left: 40px;
    
    /* 水平居中 */
    margin: 0 auto;
}
```

### 3.3 盒模型类型

```css
/* 标准盒模型（默认） */
.box1 {
    box-sizing: content-box;
    width: 300px;              /* 只包含 content */
    padding: 20px;
    border: 1px solid #ccc;
    /* 实际宽度 = 300 + 20*2 + 1*2 = 342px */
}

/* IE 盒模型（推荐） */
.box2 {
    box-sizing: border-box;
    width: 300px;              /* 包含 content + padding + border */
    padding: 20px;
    border: 1px solid #ccc;
    /* 实际宽度 = 300px */
}

/* 全局设置（推荐） */
* {
    box-sizing: border-box;
}
```

### 3.4 外边距合并

```css
/* 垂直方向外边距会合并 */
.box1 {
    margin-bottom: 30px;
}

.box2 {
    margin-top: 20px;
}
/* 实际间距是 30px，不是 50px */

/* 解决方案 */
.box1 {
    margin-bottom: 30px;
}

.box2 {
    margin-top: 0;
    padding-top: 20px;  /* 用 padding 代替 */
}
```

---

## 4. 布局

### 4.1 Display 属性

```css
/* 块级元素 */
div {
    display: block;
    /* 独占一行，可设置宽高 */
}

/* 行内元素 */
span {
    display: inline;
    /* 不独占一行，不可设置宽高 */
}

/* 行内块元素 */
img {
    display: inline-block;
    /* 不独占一行，可设置宽高 */
}

/* 隐藏元素 */
.hidden {
    display: none;          /* 不占空间 */
}

.invisible {
    visibility: hidden;     /* 占空间但不可见 */
}

/* Flex 容器 */
.flex-container {
    display: flex;
}

/* Grid 容器 */
.grid-container {
    display: grid;
}
```

### 4.2 浮动布局

```css
/* 浮动 */
.left {
    float: left;
    width: 200px;
}

.right {
    float: right;
    width: 200px;
}

/* 清除浮动 */
.clearfix::after {
    content: "";
    display: block;
    clear: both;
}

/* 或者 */
.parent {
    overflow: hidden;  /* 触发 BFC */
}
```

```html
<div class="clearfix">
    <div class="left">左侧</div>
    <div class="right">右侧</div>
</div>
```

### 4.3 多列布局

```css
/* 两列布局 */
.container {
    width: 100%;
}

.sidebar {
    float: left;
    width: 200px;
}

.main {
    margin-left: 220px;  /* 留出侧边栏空间 */
}

/* 三列布局 */
.left {
    float: left;
    width: 200px;
}

.right {
    float: right;
    width: 200px;
}

.center {
    margin: 0 220px;  /* 左右留空 */
}
```

---

## 5. 定位

### 5.1 Position 属性

```css
/* 静态定位（默认） */
.static {
    position: static;
}

/* 相对定位 */
.relative {
    position: relative;
    top: 10px;      /* 相对于原位置偏移 */
    left: 20px;
    /* 原位置仍占空间 */
}

/* 绝对定位 */
.absolute {
    position: absolute;
    top: 0;         /* 相对于最近的非 static 祖先元素 */
    right: 0;
    /* 脱离文档流，不占空间 */
}

/* 固定定位 */
.fixed {
    position: fixed;
    bottom: 20px;   /* 相对于浏览器窗口 */
    right: 20px;
    /* 滚动时位置不变 */
}

/* 粘性定位 */
.sticky {
    position: sticky;
    top: 0;         /* 滚动到顶部时固定 */
}
```

### 5.2 层级控制

```css
.layer1 {
    position: relative;
    z-index: 1;     /* 数值越大越在上层 */
}

.layer2 {
    position: absolute;
    z-index: 10;
}

.layer3 {
    position: fixed;
    z-index: 999;   /* 最上层 */
}
```

### 5.3 居中定位

```css
/* 水平垂直居中 - 方法1 */
.center1 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* 水平垂直居中 - 方法2 */
.center2 {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    width: 200px;
    height: 200px;
}

/* 水平垂直居中 - 方法3（已知宽高） */
.center3 {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 200px;
    height: 200px;
    margin-top: -100px;  /* 高度的一半 */
    margin-left: -100px; /* 宽度的一半 */
}
```

---

## 6. Flexbox

### 6.1 Flex 容器属性

```css
.container {
    display: flex;
    
    /* 主轴方向 */
    flex-direction: row;            /* 水平（默认） */
    flex-direction: row-reverse;    /* 水平反向 */
    flex-direction: column;         /* 垂直 */
    flex-direction: column-reverse; /* 垂直反向 */
    
    /* 换行 */
    flex-wrap: nowrap;    /* 不换行（默认） */
    flex-wrap: wrap;      /* 换行 */
    flex-wrap: wrap-reverse; /* 反向换行 */
    
    /* 简写 */
    flex-flow: row wrap;  /* direction + wrap */
    
    /* 主轴对齐 */
    justify-content: flex-start;    /* 起点对齐（默认） */
    justify-content: flex-end;      /* 终点对齐 */
    justify-content: center;        /* 居中 */
    justify-content: space-between; /* 两端对齐，项目间隔相等 */
    justify-content: space-around;  /* 项目两侧间隔相等 */
    justify-content: space-evenly;  /* 所有间隔相等 */
    
    /* 交叉轴对齐 */
    align-items: stretch;     /* 拉伸（默认） */
    align-items: flex-start;  /* 起点对齐 */
    align-items: flex-end;    /* 终点对齐 */
    align-items: center;      /* 居中 */
    align-items: baseline;    /* 基线对齐 */
    
    /* 多行对齐 */
    align-content: stretch;        /* 拉伸（默认） */
    align-content: flex-start;     /* 起点对齐 */
    align-content: flex-end;       /* 终点对齐 */
    align-content: center;         /* 居中 */
    align-content: space-between;  /* 两端对齐 */
    align-content: space-around;   /* 间隔相等 */
    
    /* 间距（新特性） */
    gap: 20px;           /* 行列间距 */
    row-gap: 20px;       /* 行间距 */
    column-gap: 10px;    /* 列间距 */
}
```

### 6.2 Flex 项目属性

```css
.item {
    /* 排序 */
    order: 0;  /* 数值越小越靠前，默认 0 */
    
    /* 放大比例 */
    flex-grow: 0;   /* 默认 0，不放大 */
    flex-grow: 1;   /* 平分剩余空间 */
    
    /* 缩小比例 */
    flex-shrink: 1; /* 默认 1，空间不足时缩小 */
    flex-shrink: 0; /* 不缩小 */
    
    /* 初始大小 */
    flex-basis: auto;  /* 默认，根据内容 */
    flex-basi```css
    flex-basis: 200px;  /* 固定初始大小 */
    flex-basis: 50%;    /* 百分比 */
    
    /* 简写 */
    flex: 1;              /* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
    flex: 0 0 200px;      /* grow shrink basis */
    flex: auto;           /* 1 1 auto */
    flex: none;           /* 0 0 auto */
    
    /* 单独对齐 */
    align-self: auto;       /* 继承父元素（默认） */
    align-self: flex-start;
    align-self: flex-end;
    align-self: center;
    align-self: stretch;
}
```

### 6.3 Flex 常用布局

#### 水平垂直居中
```css
.center {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
```

#### 等分布局
```css
.equal-layout {
    display: flex;
}

.equal-layout .item {
    flex: 1;  /* 每个项目平分空间 */
}
```

#### 固定侧边栏
```css
.layout {
    display: flex;
    height: 100vh;
}

.sidebar {
    flex: 0 0 200px;  /* 固定 200px */
}

.main {
    flex: 1;  /* 占满剩余空间 */
}
```

#### 底部固定
```css
.page {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.header {
    flex: 0 0 auto;
}

.content {
    flex: 1;  /* 占满中间空间 */
}

.footer {
    flex: 0 0 auto;
}
```

#### 响应式网格
```css
.grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.grid-item {
    flex: 1 1 300px;  /* 最小 300px，自动换行 */
}
```

---

## 7. Grid

### 7.1 Grid 容器属性

```css
.container {
    display: grid;
    
    /* 定义列 */
    grid-template-columns: 100px 200px 100px;  /* 3列固定宽度 */
    grid-template-columns: 1fr 2fr 1fr;        /* 比例分配 */
    grid-template-columns: repeat(3, 1fr);     /* 3列等宽 */
    grid-template-columns: repeat(auto-fill, 200px); /* 自动填充 */
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* 响应式 */
    
    /* 定义行 */
    grid-template-rows: 100px 200px;
    grid-template-rows: repeat(3, 100px);
    grid-template-rows: auto 1fr auto;  /* 头部自动，内容占满，底部自动 */
    
    /* 间距 */
    gap: 20px;              /* 行列间距 */
    row-gap: 20px;          /* 行间距 */
    column-gap: 10px;       /* 列间距 */
    
    /* 对齐 */
    justify-items: start;   /* 水平对齐：start, end, center, stretch */
    align-items: start;     /* 垂直对齐：start, end, center, stretch */
    place-items: center;    /* align-items + justify-items 简写 */
    
    /* 整体对齐 */
    justify-content: start; /* 水平：start, end, center, space-between, space-around, space-evenly */
    align-content: start;   /* 垂直：start, end, center, space-between, space-around, space-evenly */
    place-content: center;  /* align-content + justify-content 简写 */
    
    /* 自动行高 */
    grid-auto-rows: 100px;
    grid-auto-rows: minmax(100px, auto);
    
    /* 自动列宽 */
    grid-auto-columns: 100px;
    
    /* 自动放置 */
    grid-auto-flow: row;      /* 按行填充（默认） */
    grid-auto-flow: column;   /* 按列填充 */
    grid-auto-flow: dense;    /* 紧密填充 */
}
```

### 7.2 Grid 项目属性

```css
.item {
    /* 列位置 */
    grid-column-start: 1;
    grid-column-end: 3;
    grid-column: 1 / 3;        /* 简写：从第1列到第3列 */
    grid-column: 1 / span 2;   /* 从第1列开始，跨2列 */
    
    /* 行位置 */
    grid-row-start: 1;
    grid-row-end: 3;
    grid-row: 1 / 3;
    grid-row: 1 / span 2;
    
    /* 区域简写 */
    grid-area: 1 / 1 / 3 / 3;  /* row-start / col-start / row-end / col-end */
    
    /* 单独对齐 */
    justify-self: start;  /* 水平：start, end, center, stretch */
    align-self: start;    /* 垂直：start, end, center, stretch */
    place-self: center;   /* 简写 */
}
```

### 7.3 Grid 命名区域

```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header header"
        "sidebar main aside"
        "footer footer footer";
    gap: 20px;
}

.header {
    grid-area: header;
}

.sidebar {
    grid-area: sidebar;
}

.main {
    grid-area: main;
}

.aside {
    grid-area: aside;
}

.footer {
    grid-area: footer;
}
```

### 7.4 Grid 常用布局

#### 响应式卡片网格
```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
```

#### 圣杯布局
```css
.holy-grail {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
    gap: 20px;
}

.header {
    grid-column: 1 / 4;
}

.footer {
    grid-column: 1 / 4;
}
```

#### 瀑布流布局
```css
.masonry {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-auto-rows: 20px;
    gap: 10px;
}

.masonry-item {
    grid-row: span 10;  /* 根据内容调整 */
}
```

#### 12列网格系统
```css
.grid-12 {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    gap: 20px;
}

.col-6 {
    grid-column: span 6;  /* 占6列 */
}

.col-4 {
    grid-column: span 4;  /* 占4列 */
}

.col-3 {
    grid-column: span 3;  /* 占3列 */
}
```

---

## 8. 文本与字体

### 8.1 字体属性

```css
.text {
    /* 字体族 */
    font-family: "Helvetica Neue", Arial, sans-serif;
    font-family: "Microsoft YaHei", "微软雅黑", sans-serif;
    
    /* 字体大小 */
    font-size: 16px;
    font-size: 1rem;      /* 相对于根元素 */
    font-size: 1.2em;     /* 相对于父元素 */
    font-size: 100%;
    
    /* 字体粗细 */
    font-weight: normal;  /* 400 */
    font-weight: bold;    /* 700 */
    font-weight: 100;     /* 100-900 */
    
    /* 字体样式 */
    font-style: normal;
    font-style: italic;   /* 斜体 */
    font-style: oblique;  /* 倾斜 */
    
    /* 字体变体 */
    font-variant: normal;
    font-variant: small-caps;  /* 小型大写字母 */
    
    /* 简写 */
    font: italic bold 16px/1.5 Arial, sans-serif;
    /* style weight size/line-height family */
}
```

### 8.2 文本属性

```css
.text {
    /* 文本颜色 */
    color: #333;
    color: rgb(51, 51, 51);
    color: rgba(51, 51, 51, 0.8);
    
    /* 文本对齐 */
    text-align: left;
    text-align: right;
    text-align: center;
    text-align: justify;  /* 两端对齐 */
    
    /* 文本装饰 */
    text-decoration: none;
    text-decoration: underline;      /* 下划线 */
    text-decoration: overline;       /* 上划线 */
    text-decoration: line-through;   /* 删除线 */
    text-decoration: underline wavy red;  /* 样式 */
    
    /* 文本转换 */
    text-transform: none;
    text-transform: uppercase;   /* 大写 */
    text-transform: lowercase;   /* 小写 */
    text-transform: capitalize;  /* 首字母大写 */
    
    /* 文本缩进 */
    text-indent: 2em;  /* 首行缩进 */
    
    /* 行高 */
    line-height: 1.5;
    line-height: 24px;
    line-height: 150%;
    
    /* 字母间距 */
    letter-spacing: 1px;
    letter-spacing: 0.1em;
    
    /* 单词间距 */
    word-spacing: 5px;
    
    /* 文本阴影 */
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    text-shadow: 0 0 10px #fff, 0 0 20px #fff;  /* 发光效果 */
    
    /* 垂直对齐 */
    vertical-align: baseline;
    vertical-align: top;
    vertical-align: middle;
    vertical-align: bottom;
    vertical-align: text-top;
    
    /* 空白处理 */
    white-space: normal;    /* 默认 */
    white-space: nowrap;    /* 不换行 */
    white-space: pre;       /* 保留空白 */
    white-space: pre-wrap;  /* 保留空白，自动换行 */
    white-space: pre-line;  /* 合并空白，保留换行 */
    
    /* 文本溢出 */
    overflow: hidden;
    text-overflow: ellipsis;  /* 省略号 */
    white-space: nowrap;
    
    /* 多行省略 */
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
    
    /* 换行 */
    word-wrap: break-word;      /* 长单词换行 */
    word-break: break-all;      /* 任意位置换行 */
    word-break: keep-all;       /* 只在空格处换行 */
    
    /* 书写方向 */
    direction: ltr;  /* 从左到右 */
    direction: rtl;  /* 从右到左 */
    
    /* 用户选择 */
    user-select: none;  /* 禁止选择 */
    user-select: text;  /* 可选择 */
}
```

### 8.3 Web 字体

```css
/* 引入字体 */
@font-face {
    font-family: 'MyFont';
    src: url('fonts/myfont.woff2') format('woff2'),
         url('fonts/myfont.woff') format('woff'),
         url('fonts/myfont.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-display: swap;  /* 字体加载策略 */
}

/* 使用字体 */
.custom-font {
    font-family: 'MyFont', sans-serif;
}

/* Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.google-font {
    font-family: 'Roboto', sans-serif;
}
```

---

## 9. 颜色与背景

### 9.1 颜色表示

```css
.color-demo {
    /* 颜色名 */
    color: red;
    color: blue;
    color: transparent;
    
    /* 十六进制 */
    color: #ff0000;
    color: #f00;      /* 简写 */
    
    /* RGB */
    color: rgb(255, 0, 0);
    color: rgba(255, 0, 0, 0.5);  /* 带透明度 */
    
    /* HSL */
    color: hsl(0, 100%, 50%);     /* 色相, 饱和度, 亮度 */
    color: hsla(0, 100%, 50%, 0.5);
    
    /* 当前颜色 */
    border-color: currentColor;
}
```

### 9.2 背景属性

```css
.background {
    /* 背景颜色 */
    background-color: #f5f5f5;
    background-color: rgba(0, 0, 0, 0.1);
    
    /* 背景图片 */
    background-image: url('image.jpg');
    background-image: linear-gradient(to right, red, blue);
    
    /* 背景重复 */
    background-repeat: repeat;      /* 默认 */
    background-repeat: no-repeat;
    background-repeat: repeat-x;    /* 水平重复 */
    background-repeat: repeat-y;    /* 垂直重复 */
    
    /* 背景位置 */
    background-position: center;
    background-position: top left;
    background-position: 50% 50%;
    background-position: 10px 20px;
    
    /* 背景大小 */
    background-size: auto;
    background-size: cover;         /* 覆盖整个容器 */
    background-size: contain;       /* 完整显示图片 */
    background-size: 100% 100%;
    background-size: 200px 150px;
    
    /* 背景固定 */
    background-attachment: scroll;  /* 默认 */
    background-attachment: fixed;   /* 固定背景 */
    
    /* 背景裁剪 */
    background-clip: border-box;    /* 默认 */
    background-clip: padding-box;
    background-clip: content-box;
    background-clip: text;          /* 文字裁剪 */
    
    /* 背景原点 */
    background-origin: padding-box; /* 默认 */
    background-origin: border-box;
    background-origin: content-box;
    
    /* 简写 */
    background: #f5f5f5 url('image.jpg') no-repeat center/cover;
    /* color image repeat position/size */
}
```

### 9.3 渐变

#### 线性渐变
```css
.linear-gradient {
    /* 基础渐变 */
    background: linear-gradient(red, blue);
    
    /* 指定方向 */
    background: linear-gradient(to right, red, blue);
    background: linear-gradient(to bottom right, red, blue);
    background: linear-gradient(45deg, red, blue);
    
    /* 多个颜色 */
    background: linear-gradient(red, yellow, green, blue);
    
    /* 颜色位置 */
    background: linear-gradient(red 0%, yellow 50%, blue 100%);
    background: linear-gradient(red 20%, blue 80%);
    
    /* 透明渐变 */
    background: linear-gradient(to right, 
        rgba(255, 0, 0, 0), 
        rgba(255, 0, 0, 1)
    );
    
    /* 条纹效果 */
    background: linear-gradient(
        90deg,
        #f5f5f5 0%,
        #f5f5f5 50%,
        #e0e0e0 50%,
        #e0e0e0 100%
    );
    background-size: 40px 40px;
}
```

#### 径向渐变
```css
.radial-gradient {
    /* 基础渐变 */
    background: radial-gradient(red, blue);
    
    /* 指定形状 */
    background: radial-gradient(circle, red, blue);
    background: radial-gradient(ellipse, red, blue);
    
    /* 指定大小 */
    background: radial-gradient(circle 100px, red, blue);
    background: radial-gradient(closest-side, red, blue);
    background: radial-gradient(farthest-corner, red, blue);
    
    /* 指定位置 */
    background: radial-gradient(circle at center, red, blue);
    background: radial-gradient(circle at top left, red, blue);
    background: radial-gradient(circle at 30% 40%, red, blue);
    
    /* 多个颜色 */
    background: radial-gradient(circle, r```css
    background: radial-gradient(circle, red, yellow, green, blue);
    
    /* 颜色位置 */
    background: radial-gradient(circle, red 0%, yellow 30%, blue 100%);
}
```

#### 圆锥渐变
```css
.conic-gradient {
    /* 基础渐变 */
    background: conic-gradient(red, yellow, green, blue, red);
    
    /* 指定起始角度 */
    background: conic-gradient(from 45deg, red, blue);
    
    /* 指定中心点 */
    background: conic-gradient(at 30% 40%, red, blue);
    
    /* 颜色位置 */
    background: conic-gradient(
        red 0deg,
        yellow 90deg,
        green 180deg,
        blue 270deg,
        red 360deg
    );
    
    /* 饼图效果 */
    background: conic-gradient(
        #4CAF50 0deg 120deg,
        #2196F3 120deg 240deg,
        #FF9800 240deg 360deg
    );
}
```

#### 重复渐变
```css
.repeating-gradient {
    /* 重复线性渐变 */
    background: repeating-linear-gradient(
        45deg,
        #f5f5f5 0px,
        #f5f5f5 10px,
        #e0e0e0 10px,
        #e0e0e0 20px
    );
    
    /* 重复径向渐变 */
    background: repeating-radial-gradient(
        circle,
        red 0px,
        red 10px,
        blue 10px,
        blue 20px
    );
    
    /* 重复圆锥渐变 */
    background: repeating-conic-gradient(
        red 0deg 15deg,
        blue 15deg 30deg
    );
}
```

### 9.4 多重背景

```css
.multiple-backgrounds {
    background-image: 
        url('front.png'),
        url('middle.png'),
        url('back.png');
    background-position: 
        center,
        left top,
        right bottom;
    background-repeat: 
        no-repeat,
        repeat-x,
        no-repeat;
    background-size: 
        cover,
        auto,
        contain;
    
    /* 或者简写 */
    background: 
        url('front.png') center/cover no-repeat,
        url('middle.png') left top/auto repeat-x,
        url('back.png') right bottom/contain no-repeat;
}
```

### 9.5 背景混合模式

```css
.blend-mode {
    background: url('image.jpg'), linear-gradient(red, blue);
    background-blend-mode: multiply;
    /* normal, multiply, screen, overlay, darken, lighten, 
       color-dodge, color-burn, hard-light, soft-light, 
       difference, exclusion, hue, saturation, color, luminosity */
}
```

---

## 10. 过渡与动画

### 10.1 过渡 (Transition)

```css
.transition {
    /* 基础过渡 */
    transition: all 0.3s;
    
    /* 指定属性 */
    transition: width 0.3s;
    transition: width 0.3s, height 0.5s;
    
    /* 完整语法 */
    transition-property: width;           /* 属性 */
    transition-duration: 0.3s;            /* 持续时间 */
    transition-timing-function: ease;     /* 速度曲线 */
    transition-delay: 0.1s;               /* 延迟 */
    
    /* 简写 */
    transition: width 0.3s ease 0.1s;
    /* property duration timing-function delay */
}

/* 速度曲线 */
.timing-functions {
    transition-timing-function: linear;        /* 匀速 */
    transition-timing-function: ease;          /* 慢-快-慢（默认） */
    transition-timing-function: ease-in;       /* 慢-快 */
    transition-timing-function: ease-out;      /* 快-慢 */
    transition-timing-function: ease-in-out;   /* 慢-快-慢 */
    
    /* 贝塞尔曲线 */
    transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1);
    
    /* 步进 */
    transition-timing-function: steps(4, end);
}

/* 实例：按钮悬停 */
.button {
    background: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    transition: all 0.3s ease;
}

.button:hover {
    background: #0056b3;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
```

### 10.2 变换 (Transform)

#### 2D 变换
```css
.transform-2d {
    /* 平移 */
    transform: translate(50px, 100px);
    transform: translateX(50px);
    transform: translateY(100px);
    
    /* 缩放 */
    transform: scale(1.5);           /* 放大1.5倍 */
    transform: scale(2, 0.5);        /* 宽2倍，高0.5倍 */
    transform: scaleX(2);
    transform: scaleY(0.5);
    
    /* 旋转 */
    transform: rotate(45deg);        /* 顺时针45度 */
    transform: rotate(-45deg);       /* 逆时针45度 */
    
    /* 倾斜 */
    transform: skew(10deg, 20deg);
    transform: skewX(10deg);
    transform: skewY(20deg);
    
    /* 组合变换 */
    transform: translate(50px, 100px) rotate(45deg) scale(1.5);
    
    /* 变换原点 */
    transform-origin: center;        /* 默认 */
    transform-origin: top left;
    transform-origin: 50% 50%;
    transform-origin: 10px 20px;
}
```

#### 3D 变换
```css
.transform-3d {
    /* 透视 */
    perspective: 1000px;
    
    /* 3D 平移 */
    transform: translate3d(50px, 100px, 200px);
    transform: translateZ(200px);
    
    /* 3D 缩放 */
    transform: scale3d(2, 2, 2);
    transform: scaleZ(2);
    
    /* 3D 旋转 */
    transform: rotateX(45deg);
    transform: rotateY(45deg);
    transform: rotateZ(45deg);
    transform: rotate3d(1, 1, 1, 45deg);
    
    /* 保留3D */
    transform-style: preserve-3d;
    
    /* 背面可见性 */
    backface-visibility: hidden;
}

/* 3D 卡片翻转效果 */
.card {
    width: 300px;
    height: 200px;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.6s;
}

.card:hover {
    transform: rotateY(180deg);
}

.card-front,
.card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
}

.card-back {
    transform: rotateY(180deg);
}
```

### 10.3 动画 (Animation)

```css
/* 定义关键帧 */
@keyframes slide-in {
    from {
        transform: translateX(-100%);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

/* 或者使用百分比 */
@keyframes bounce {
    0% {
        transform: translateY(0);
    }
    50% {
        transform: translateY(-50px);
    }
    100% {
        transform: translateY(0);
    }
}

/* 应用动画 */
.animated {
    /* 完整语法 */
    animation-name: slide-in;              /* 动画名称 */
    animation-duration: 1s;                /* 持续时间 */
    animation-timing-function: ease;       /* 速度曲线 */
    animation-delay: 0.5s;                 /* 延迟 */
    animation-iteration-count: infinite;   /* 次数：数字或infinite */
    animation-direction: normal;           /* 方向 */
    animation-fill-mode: forwards;         /* 填充模式 */
    animation-play-state: running;         /* 播放状态 */
    
    /* 简写 */
    animation: slide-in 1s ease 0.5s infinite normal forwards;
    /* name duration timing-function delay iteration-count direction fill-mode */
}

/* 动画方向 */
.direction {
    animation-direction: normal;           /* 正常播放 */
    animation-direction: reverse;          /* 反向播放 */
    animation-direction: alternate;        /* 交替播放 */
    animation-direction: alternate-reverse; /* 反向交替 */
}

/* 填充模式 */
.fill-mode {
    animation-fill-mode: none;             /* 默认 */
    animation-fill-mode: forwards;         /* 保持最后状态 */
    animation-fill-mode: backwards;        /* 应用第一帧 */
    animation-fill-mode: both;             /* 两者都应用 */
}
```

### 10.4 常用动画示例

#### 淡入淡出
```css
@keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
}

@keyframes fade-out {
    from { opacity: 1; }
    to { opacity: 0; }
}

.fade-in {
    animation: fade-in 0.5s ease;
}
```

#### 弹跳
```css
@keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
        transform: translateY(0);
    }
    40% {
        transform: translateY(-30px);
    }
    60% {
        transform: translateY(-15px);
    }
}

.bounce {
    animation: bounce 2s infinite;
}
```

#### 旋转加载
```css
@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

.spinner {
    width: 50px;
    height: 50px;
    border: 5px solid #f3f3f3;
    border-top: 5px solid #007bff;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}
```

#### 脉冲
```css
@keyframes pulse {
    0% {
        transform: scale(1);
        opacity: 1;
    }
    50% {
        transform: scale(1.1);
        opacity: 0.8;
    }
    100% {
        transform: scale(1);
        opacity: 1;
    }
}

.pulse {
    animation: pulse 2s ease-in-out infinite;
}
```

#### 摇晃
```css
@keyframes shake {
    0%, 100% {
        transform: translateX(0);
    }
    10%, 30%, 50%, 70%, 90% {
        transform: translateX(-10px);
    }
    20%, 40%, 60%, 80% {
        transform: translateX(10px);
    }
}

.shake {
    animation: shake 0.5s;
}
```

#### 打字效果
```css
@keyframes typing {
    from {
        width: 0;
    }
    to {
        width: 100%;
    }
}

@keyframes blink {
    50% {
        border-color: transparent;
    }
}

.typewriter {
    overflow: hidden;
    border-right: 2px solid;
    white-space: nowrap;
    animation: 
        typing 3s steps(30) 1s forwards,
        blink 0.5s step-end infinite;
}
```

---

## 11. 响应式设计

### 11.1 媒体查询

```css
/* 基础语法 */
@media screen and (max-width: 768px) {
    /* 屏幕宽度 ≤ 768px 时应用 */
    .container {
        width: 100%;
        padding: 10px;
    }
}

/* 常用断点 */
/* 超小屏幕（手机） */
@media (max-width: 575px) {
    .container { width: 100%; }
}

/* 小屏幕（平板竖屏） */
@media (min-width: 576px) and (max-width: 767px) {
    .container { width: 540px; }
}

/* 中等屏幕（平板横屏） */
@media (min-width: 768px) and (max-width: 991px) {
    .container { width: 720px; }
}

/* 大屏幕（桌面） */
@media (min-width: 992px) and (max-width: 1199px) {
    .container { width: 960px; }
}

/* 超大屏幕 */
@media (min-width: 1200px) {
    .container { width: 1140px; }
}
```

### 11.2 媒体类型和特性

```css
/* 媒体类型 */
@media screen { }          /* 屏幕 */
@media print { }           /* 打印 */
@media all { }             /* 所有设备 */

/* 宽度和高度 */
@media (min-width: 768px) { }
@media (max-width: 1200px) { }
@media (min-height: 600px) { }
@media (max-height: 800px) { }

/* 方向 */
@media (orientation: portrait) { }   /* 竖屏 */
@media (orientation: landscape) { }  /* 横屏 */

/* 分辨率 */
@media (min-resolution: 2dppx) { }   /* 高清屏 */
@media (-webkit-min-device-pixel-ratio: 2) { }

/* 宽高比 */
@media (aspect-ratio: 16/9) { }
@media (min-aspect-ratio: 16/9) { }

/* 颜色 */
@media (color) { }                   /* 彩色设备 */
@media (min-color: 8) { }            /* 至少8位色深 */

/* 悬停能力 */
@media (hover: hover) { }            /* 支持悬停 */
@media (hover: none) { }             /* 不支持悬停（触摸屏） */

/* 指针精度 */
@media (pointer: fine) { }           /* 精确指针（鼠标） */
@media (pointer: coarse) { }         /* 粗糙指针（触摸） */

/* 深色模式 */
@media (prefers-color-scheme: dark) {
    body {
        background: #1a1a1a;
        color: #ffffff;
    }
}

@media (prefers-color-scheme: light) {
    body {
        background: #ffffff;
        color: #000000;
    }
}

/* 减少动画 */
@media (prefers-reduced-motion: reduce) {
    * {
        animation: none !important;
        transition: none !important;
    }
}
```

### 11.3 逻辑运算符

```css
/* and - 且 */
@media screen and (min-width: 768px) and (max-width: 1200px) { }

/* or - 或（用逗号） */
@media (max-width: 768px), (orientation: portrait) { }

/* not - 非 */
@media not screen and (color) { }

/* only - 仅（防止旧浏览器应用样式） */
@media only screen and (min-width: 768px) { }
```

### 11.4 响应式单位

```css
.responsive-units {
    /* 相对单位 */
    font-size: 1rem;        /* 相对于根元素 */
    font-size: 1em;         /* 相对于父元素 */
    
    /* 视口单位 */
    width: 100vw;           /* 视口宽度的100% */
    height: 100vh;          /* 视口高度的100% */
    font-size: 5vw;         /* 视口宽度的5% */
    font-size: 5vh;         /* 视口高度的5% */
    font-size: 5vmin;       /* vw和vh中较小的值 */
    font-size: 5vmax;       /* vw和vh中较大的值*/
    
    /* 百分比 */
    width: 50%;             /* 相对于父元素 */
    
    /* 计算 */
    width: calc(100% - 200px);
    font-size: calc(16px + 1vw);
}
```

### 11.5 响应式图片

```css
/* 基础响应式图片 */
img {
    max-width: 100%;
    height: auto;
}

/* 背景图片 */
.hero {
    backg```css
.hero {
    background-image: url('small.jpg');
    background-size: cover;
    background-position: center;
}

@media (min-width: 768px) {
    .hero {
        background-image: url('large.jpg');
    }
}
```

### 11.6 容器查询（新特性）

```css
.container {
    container-type: inline-size;
    container-name: card;
}

@container card (min-width: 400px) {
    .card-content {
        display: flex;
    }
}
```

---

## 12. CSS 变量

### 12.1 定义和使用

```css
/* 全局变量（:root 伪类） */
:root {
    --primary-color: #007bff;
    --secondary-color: #6c757d;
    --font-size: 16px;
    --spacing: 20px;
    --border-radius: 5px;
}

/* 使用变量 */
.button {
    background: var(--primary-color);
    font-size: var(--font-size);
    padding: var(--spacing);
    border-radius: var(--border-radius);
}

/* 局部变量 */
.card {
    --card-padding: 15px;
    padding: var(--card-padding);
}

/* 默认值 */
.element {
    color: var(--text-color, #333);  /* 如果变量不存在，使用 #333 */
}

/* 计算 */
.box {
    padding: calc(var(--spacing) * 2);
}
```

### 12.2 JavaScript 操作变量

```javascript
// 获取变量
const root = document.documentElement;
const primaryColor = getComputedStyle(root).getPropertyValue('--primary-color');

// 设置变量
root.style.setProperty('--primary-color', '#ff0000');

// 删除变量
root.style.removeProperty('--primary-color');
```

### 12.3 主题切换示例

```css
/* 亮色主题 */
:root {
    --bg-color: #ffffff;
    --text-color: #333333;
    --border-color: #dddddd;
}

/* 暗色主题 */
[data-theme="dark"] {
    --bg-color: #1a1a1a;
    --text-color: #ffffff;
    --border-color: #444444;
}

body {
    background: var(--bg-color);
    color: var(--text-color);
}

.card {
    border: 1px solid var(--border-color);
}
```

---

## 13. 常用技巧

### 13.1 清除浮动

```css
/* 方法1：clearfix */
.clearfix::after {
    content: "";
    display: block;
    clear: both;
}

/* 方法2：overflow */
.parent {
    overflow: hidden;
}

/* 方法3：Flex */
.parent {
    display: flex;
}
```

### 13.2 水平垂直居中

```css
/* 方法1：Flex */
.center-flex {
    display: flex;
    justify-content: center;
    align-items: center;
}

/* 方法2：Grid */
.center-grid {
    display: grid;
    place-items: center;
}

/* 方法3：绝对定位 + transform */
.center-absolute {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* 方法4：margin auto */
.center-margin {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    width: 200px;
    height: 200px;
}
```

### 13.3 单行/多行文本省略

```css
/* 单行省略 */
.ellipsis {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

/* 多行省略 */
.ellipsis-multi {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
}
```

### 13.4 三角形

```css
.triangle {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid #007bff;
}

/* 向右三角 */
.triangle-right {
    width: 0;
    height: 0;
    border-top: 50px solid transparent;
    border-bottom: 50px solid transparent;
    border-left: 100px solid #007bff;
}
```

### 13.5 隐藏滚动条

```css
/* 隐藏但保留功能 */
.hide-scrollbar {
    overflow: auto;
    scrollbar-width: none;  /* Firefox */
    -ms-overflow-style: none;  /* IE/Edge */
}

.hide-scrollbar::-webkit-scrollbar {
    display: none;  /* Chrome/Safari */
}
```

### 13.6 自定义滚动条

```css
/* Webkit 浏览器 */
.custom-scrollbar::-webkit-scrollbar {
    width: 10px;
}

.custom-scrollbar::-webkit-scrollbar-track {
    background: #f1f1f1;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 5px;
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
    background: #555;
}
```

### 13.7 禁止选择

```css
.no-select {
    user-select: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
}
```

### 13.8 平滑滚动

```css
html {
    scroll-behavior: smooth;
}
```

### 13.9 宽高比

```css
/* 方法1：padding-top */
.aspect-ratio {
    width: 100%;
    padding-top: 56.25%;  /* 16:9 = 9/16 = 56.25% */
    position: relative;
}

.aspect-ratio > * {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

/* 方法2：aspect-ratio（新特性） */
.aspect-ratio-new {
    aspect-ratio: 16 / 9;
}
```

### 13.10 毛玻璃效果

```css
.glass {
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.3);
}
```

### 13.11 阴影效果

```css
/* 盒阴影 */
.shadow {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

/* 多重阴影 */
.shadow-multiple {
    box-shadow: 
        0 2px 4px rgba(0, 0, 0, 0.1),
        0 8px 16px rgba(0, 0, 0, 0.1);
}

/* 内阴影 */
.shadow-inset {
    box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* 文字阴影 */
.text-shadow {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
```

### 13.12 渐变边框

```css
.gradient-border {
    border: 2px solid transparent;
    background: 
        linear-gradient(white, white) padding-box,
        linear-gradient(45deg, red, blue) border-box;
}
```

### 13.13 重置样式

```css
/* 简单重置 */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* 常用重置 */
body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    line-height: 1.6;
    color: #333;
}

a {
    text-decoration: none;
    color: inherit;
}

ul, ol {
    list-style: none;
}

img {
    max-width: 100%;
    height: auto;
    display: block;
}

button {
    border: none;
    background: none;
    cursor: pointer;
    font: inherit;
}
```

### 13.14 性能优化

```css
/* 硬件加速 */
.accelerated {
    transform: translateZ(0);
    will-change: transform;
}

/* 避免重排 */
.optimized {
    /* 使用 transform 代替 top/left */
    transform: translate(10px, 20px);
    
    /* 使用 opacity 代替 visibility */
    opacity: 0;
}

/* 字体渲染优化 */
body {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```

---

## 附录：常用属性速查

### 尺寸
- `width`, `height`, `max-width`, `min-width`, `max-height`, `min-height`

### 间距
- `margin`, `padding`

### 边框
- `border`, `border-radius`, `outline`

### 背景
- `background`, `background-color`, `background-image`, `background-size`, `background-position`

### 文本
- `color`, `font-size`, `font-weight`, `font-family`, `line-height`, `text-align`, `text-decoration`

### 布局
- `display`, `position`, `float`, `clear`, `overflow`, `z-index`

### Flex
- `flex`, `flex-direction`, `justify-content`, `align-items`, `flex-wrap`

### Grid
- `grid-template-columns`, `grid-template-rows`, `gap`, `grid-column`, `grid-row`

### 变换
- `transform`, `transition`, `animation`

### 其他
- `opacity`, `visibility`, `cursor`, `box-shadow`, `filter`

---
