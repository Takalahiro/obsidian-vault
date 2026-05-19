超文本标记语言（英语：HyperText Markup Language，简称：HTML）是一种用于创建网页的标准标记语言。

您可以使用 HTML 来建立自己的 WEB 站点，HTML 运行在浏览器上，由浏览器来解析。

HTML 很容易学习！相信您能很快学会它！![[Pasted image 20260511232448.png]]

## 1. HTML 基础

### 1.1 什么是 HTML

HTML (HyperText Markup Language) 超文本标记语言，用于创建网页的标准标记语言。
#### HTML文档的后缀名

- .html
- .htm

以上两种后缀名没有区别，都可以使用
### 1.2 基本结构

![[Pasted image 20260511232649.png|697]]




---
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>页面标题</title>
</head>
<body>
    <!-- 页面内容 -->
</body>
</html>
```

### 1.3 标签语法

```html
<!-- 双标签 -->
<p>段落内容</p>

<!-- 单标签 -->
<br>
<img src="image.jpg" alt="图片">

<!-- 标签属性 -->
<a href="https://example.com" target="_blank">链接</a>

<!-- 注释 -->
<!-- 这是注释 -->
```

---


## 2. 文档头部 (head)

### 2.1 常用 meta 标签

```html
<head>
    <!-- 字符编码 -->
    <meta charset="UTF-8">
    
    <!-- 视口设置（响应式必备） -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- 页面描述 -->
    <meta name="description" content="网站描述">
    
    <!-- 关键词 -->
    <meta name="keywords" content="关键词1, 关键词2">
    
    <!-- 作者 -->
    <meta name="author" content="作者名">
    
    <!-- IE 兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    
    <!-- 页面标题 -->
    <title>网站标题</title>
    
    <!-- 引入 CSS -->
    <link rel="stylesheet" href="style.css">
    
    <!-- 网站图标 -->
    <link rel="icon" href="favicon.ico">
    
    <!-- 引入 JavaScript -->
    <script src="script.js"></script>
</head>
```

---

## 3. 文本标签

### 3.1 标题

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

### 3.2 段落和换行

```html
<!-- 段落 -->
<p>这是一个段落</p>

<!-- 换行 -->
第一行<br>第二行

<!-- 水平线 -->
<hr>
```

### 3.3 文本格式化

```html
<!-- 粗体 -->
<strong>重要文本</strong>
<b>粗体文本</b>

<!-- 斜体 -->
<em>强调文本</em>
<i>斜体文本</i>

<!-- 下划线 -->
<u>下划线文本</u>

<!-- 删除线 -->
<del>删除文本</del>
<s>删除文本</s>

<!-- 插入文本 -->
<ins>插入文本</ins>

<!-- 上标和下标 -->
x<sup>2</sup>  <!-- x² -->
H<sub>2</sub>O <!-- H₂O -->

<!-- 小号文本 -->
<small>小号文本</small>

<!-- 标记文本 -->
<mark>高亮文本</mark>

<!-- 引用 -->
<q>短引用</q>
<blockquote>长引用块</blockquote>

<!-- 代码 -->
<code>代码片段</code>
<pre>预格式化文本</pre>

<!-- 缩写 -->
<abbr title="HyperText Markup Language">HTML</abbr>
```

---

## 4. 链接

```html
<!-- 基本链接 -->
<a href="https://example.com">链接文本</a>

<!-- 新窗口打开 -->
<a href="https://example.com" target="_blank">新窗口打开</a>

<!-- 页面内锚点 -->
<a href="#section1">跳转到章节1</a>
<div id="section1">章节1内容</div>

<!-- 邮件链接 -->
<a href="mailto:email@example.com">发送邮件</a>

<!-- 电话链接 -->
<a href="tel:+8613800138000">拨打电话</a>

<!-- 下载链接 -->
<a href="file.pdf" download>下载文件</a>

<!-- target 属性 -->
<!-- _self: 当前窗口（默认） -->
<!-- _blank: 新窗口 -->
<!-- _parent: 父框架 -->
<!-- _top: 顶层框架 -->
```

---

## 5. 图片

```html
<!-- 基本图片 -->
<img src="image.jpg" alt="图片描述">

<!-- 设置尺寸 -->
<img src="image.jpg" alt="图片" width="300" height="200">

<!-- 图片链接 -->
<a href="https://example.com">
    <img src="image.jpg" alt="图片">
</a>

<!-- 响应式图片 -->
<img src="image.jpg" alt="图片" style="max-width: 100%; height: auto;">

<!-- 图片映射 -->
<img src="map.jpg" alt="地图" usemap="#map">
<map name="map">
    <area shape="rect" coords="0,0,100,100" href="link1.html" alt="区域1">
    <area shape="circle" coords="200,200,50" href="link2.html" alt="区域2">
</map>

<!-- picture 元素（响应式） -->
<picture>
    <source media="(min-width: 768px)" srcset="large.jpg">
    <source media="(min-width: 480px)" srcset="medium.jpg">
    <img src="small.jpg" alt="图片">
</picture>
```

---

## 6. 列表

### 6.1 无序列表

```html
<ul>
    <li>列表项1</li>
    <li>列表项2</li>
    <li>列表项3</li>
</ul>
```

### 6.2 有序列表

```html
<ol>
    <li>第一项</li>
    <li>第二项</li>
    <li>第三项</li>
</ol>

<!-- 指定起始数字 -->
<ol start="5">
    <li>第五项</li>
    <li>第六项</li>
</ol>

<!-- 类型 -->
<ol type="A">  <!-- A, a, I, i, 1 -->
    <li>A项</li>
    <li>B项</li>
</ol>
```

### 6.3 描述列表

```html
<dl>
    <dt>术语1</dt>
    <dd>术语1的描述</dd>
    
    <dt>术语2</dt>
    <dd>术语2的描述</dd>
</dl>
```

### 6.4 嵌套列表

```html
<ul>
    <li>项目1
        <ul>
            <li>子项目1.1</li>
            <li>子项目1.2</li>
        </ul>
    </li>
    <li>项目2</li>
</ul>
```

---

## 7. 表格

```html
<!-- 基本表格 -->
<table>
    <tr>
        <th>表头1</th>
        <th>表头2</th>
    </tr>
    <tr>
        <td>数据1</td>
        <td>数据2</td>
    </tr>
</table>

<!-- 完整表格结构 -->
<table border="1">
    <caption>表格标题</caption>
    <thead>
        <tr>
            <th>姓名</th>
            <th>年龄</th>
            <th>城市</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>张三</td>
            <td>25</td>
            <td>北京</td>
        </tr>
        <tr>
            <td>李四</td>
            <td>30</td>
            <td>上海</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">共2人</td>
        </tr>
    </tfoot>
</table>

<!-- 合并单元格 -->
<table>
    <tr>
        <td colspan="2">横跨2列</td>
    </tr>
    <tr>
        <td rowspan="2">纵跨2行</td>
        <td>数据</td>
    </tr>
    <tr>
        <td>数据</td>
    </tr>
</table>
```

---

## 8. 表单

### 8.1 基本表单

```html
<form action="/submit" method="post">
    <!-- 表单内容 -->
</form>

<!-- method: get 或 post -->
<!-- action: 提交地址 -->
<!-- enctype: 编码类型（上传文件时用 multipart/form-data） -->
```

### 8.2 输入框

```html
<!-- 文本输入 -->
<input type="text" name="username" placeholder="请输入用户名">

<!-- 密码输入 -->
<input type="password" name="password" placeholder="请输入密码">

<!-- 邮箱 -->
<input type="email" name="email" placeholder="请输入邮箱">

<!-- 数字 -->
<input type="number" name="age" min="0" max="120">

<!-- 电话 -->
<input type="tel" name="phone">

<!-- URL -->
<input type="url" name="website">

<!-- 搜索 -->
<input type="search" name="search">

<!-- 日期 -->
<input type="date" name="birthday">

<!-- 时间 -->
<input type="time" name="time">

<!-- 日期时间 -->
<input type="datetime-local" name="datetime">

<!-- 颜色选择器 -->
<input type="color" name="color">

<!-- 范围滑块 -->
<input type="range" name="volume" min="0" max="100">

<!-- 文件上传 -->
<input type="file" name="file">
<input type="file" name="files" multiple>  <!-- 多文件 -->

<!-- 隐藏域 -->
<input type="hidden" name="id" value="123">
```

### 8.3 单选和复选

```html
<!-- 单选按钮 -->
<input type="radio" name="gender" value="male" id="male">
<label for="male">男</label>

<input type="radio" name="gender" value="female" id="female">
<label for="female">女</label>

<!-- 复选框 -->
<input type="checkbox" name="hobby" value="reading" id="reading">
<label for="reading">阅读</label>

<input type="checkbox" name="hobby" value="music" id="music">
<label for="music">音乐</label>

<!-- 默认选中 -->
<input type="checkbox" name="agree" checked>
```

### 8.4 下拉列表

```html
<!-- 单选下拉 -->
<select name="city">
    <option value="">请选择</option>
    <option value="beijing">北京</option>
    <option value="shanghai">上海</option>
    <option value="guangzhou" selected>广州</option>
</select>

<!-- 多选下拉 -->
<select name="cities" multiple>
    <option value="beijing">北京</option>
    <option value="shanghai">上海</option>
</select>

<!-- 分组 -->
<select name="country">
    <optgroup label="亚洲">
        <option value="china">中国</option>
        <option value="japan">日本</option>
    </optgroup>
    <optgroup label="欧洲">
        <option value="uk">英国</option>
        <option value="france">法国</option>
    </optgroup>
</select>
```

### 8.5 文本域

```html
<textarea name="message" rows="5" cols="30" placeholder="请输入内容"></textarea>
```

### 8.6 按钮

```html
<!-- 提交按钮 -->
<input type="submit" value="提交">
<button type="submit">提交</button>

<!-- 重置按钮 -->
<input type="reset" value="重置">
<button type="reset">重置</button>

<!-- 普通按钮 -->
<input type="button" value="按钮">
<button type="button">按钮</button>
```

### 8.7 标签和字段集

```html
<!-- label 关联 -->
<label for="username">用户名：</label>
<input type="text" id="username" name="username">

<!-- 或者包裹 -->
<label>
    用户名：
    <input type="text" name="username">
</label>

<!-- 字段集分组 -->
<fieldset>
    <legend>个人信息</legend>
    <label>姓名：<input type="text" name="name"></label>
    <label>年龄：<input type="number" name="age"></label>
</fieldset>
```

### 8.8 表单属性

```html
<!-- 必填 -->
<input type="text" name="username" required>

<!-- 只读 -->
<input type="text" name="username" readonly value="只读">

<!-- 禁用 -->
<input type="text" name="username" disabled>

<!-- 自动聚焦 -->
<input type="text" name="username" autofocus>

<!-- 自动完成 -->
<input type="text" name="username" autocomplete="off">

<!-- 模式验证 -->
<input type="text" name="phone" pattern="[0-9]{11}" title="请输入11位手机号">

<!-- 最大最小长度 -->
<input type="text" name="username" minlength="3" maxlength="20">

<!-- 数据列表 -->
<input type="text" name="browser" list="browsers">
<datalist id="browsers">
    <option value="Chrome">
    <option value="Firefox">
    <option value="Safari">
</datalist>
```

### 8.9 完整表单示例

```html
<form action="/register" method="post">
    <fieldset>
        <legend>注册信息</legend>
        
        <label for="username">用户名：</label>
        <input type="text" id="username" name="username" required minlength="3">
        <br><br>
        
        <label for="email">邮箱：</label>
        <input type="email" id="email" name="email" required>
        <br><br>
        
        <label for="password">密码：</label>
        <input type="password" id="password" name="password" required minlength="6">
        <br><br>
        
        <label>性别：</label>
        <input type="radio" name="gender" value="male" id="male">
        <label for="male">男</label>
        <input type="radio" name="gender" value="female" id="female">
        <label for="female">女</label>
        <br><br>
        
        <label for="city">城市：</label>
        <select id="city" name="city">
            <option value="">请选择</option>
            <option value="beijing">北京</option>
            <option value="shanghai">上海</option>
        </select>
        <br><br>
        
        <label>
            <input type="checkbox" name="agree" required>
            同意用户协议
        </label>
        <br><br>
        
        <button type="submit">注册</button>
        <button type="reset">重置</button>
    </fieldset>
</form>
```

---

## 9. 语义化标签

### 9.1 页面结构

```html
<header>
    <!-- 页头：logo、导航等 -->
</header>

<nav>
    <!-- 导航链接 -->
    <ul>
        <li><a href="#home">首页</a></li>
        <li><a href="#about">关于</a></li>
    </ul>
</nav>

<main>
    <!-- 主要内容 -->
    <article>
        <!-- 独立文章 -->
        <h2>文章标题</h2>
        <p>文章内容</p>
    </article>
    
    <section>
        <!-- 章节 -->
        <h2>章节标题</h2>
        <p>章节内容</p>
    </section>
</main>

<aside>
    <!-- 侧边栏 -->
</aside>

<footer>
    <!-- 页脚：版权信息等 -->
</footer>
```

### 9.2 内容标签

```html
<!-- 文章 -->
<article>
    <header>
        <h2>文章标题</h2>
        <time datetime="2024-01-01">2024年1月1日</time>
    </header>
    <p>文章内容</p>
    <footer>作者信息</footer>
</article>

<!-- 章节 -->
<section>
    <h2>章节标题</h2>
    <p>章节内容</p>
</section>

<!-- 独立内容 -->
<figure>
    <img src="image.jpg" alt="图片">
    <figcaption>图片说明</figcaption>
</figure>

<!-- 详情/摘要 -->
<details>
    <summary>点击展开</summary>
    <p>详细内容</p>
</details>

<!-- 时间 -->
<time datetime="2024-01-01">2024年1月1日</time>

<!-- 进度条 -->
<progress value="70" max="100">70%</progress>

<!-- 度量 -->
<meter value="0.7" min="0" max="1">70%</meter>
```

---

## 10. 多媒体

### 10.1 音频

```html
<!-- 基本音```html
<!-- 基本音频 -->
<audio src="audio.mp3" controls></audio>

<!-- 多格式兼容 -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    您的浏览器不支持音频播放
</audio>

<!-- 音频属性 -->
<audio 
    src="audio.mp3" 
    controls          <!-- 显示控制条 -->
    autoplay          <!-- 自动播放 -->
    loop              <!-- 循环播放 -->
    muted             <!-- 静音 -->
    preload="auto">   <!-- 预加载：auto/metadata/none -->
</audio>
```

### 10.2 视频

```html
<!-- 基本视频 -->
<video src="video.mp4" controls width="640" height="360"></video>

<!-- 多格式兼容 -->
<video controls width="640" height="360">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    <source src="video.ogg" type="video/ogg">
    您的浏览器不支持视频播放
</video>

<!-- 视频属性 -->
<video 
    src="video.mp4" 
    controls          <!-- 显示控制条 -->
    autoplay          <!-- 自动播放 -->
    loop              <!-- 循环播放 -->
    muted             <!-- 静音 -->
    poster="cover.jpg" <!-- 封面图 -->
    preload="auto"    <!-- 预加载 -->
    width="640" 
    height="360">
</video>

<!-- 带字幕 -->
<video controls>
    <source src="video.mp4" type="video/mp4">
    <track src="subtitles.vtt" kind="subtitles" srclang="zh" label="中文">
</video>
```

### 10.3 嵌入内容

```html
<!-- iframe 嵌入网页 -->
<iframe 
    src="https://example.com" 
    width="800" 
    height="600"
    frameborder="0"
    allowfullscreen>
</iframe>

<!-- 嵌入 YouTube 视频 -->
<iframe 
    width="560" 
    height="315" 
    src="https://www.youtube.com/embed/VIDEO_ID"
    frameborder="0" 
    allowfullscreen>
</iframe>

<!-- embed（嵌入插件内容） -->
<embed src="file.pdf" type="application/pdf" width="800" height="600">

<!-- object（嵌入对象） -->
<object data="file.pdf" type="application/pdf" width="800" height="600">
    <p>您的浏览器不支持 PDF 预览</p>
</object>
```

---

## 11. 容器标签

```html
<!-- div：块级容器 -->
<div class="container">
    <p>内容</p>
</div>

<!-- span：行内容器 -->
<p>这是<span class="highlight">重点</span>内容</p>

<!-- 语义化容器 -->
<header>页头</header>
<nav>导航</nav>
<main>主内容</main>
<section>章节</section>
<article>文章</article>
<aside>侧边栏</aside>
<footer>页脚</footer>
```

---

## 12. 特殊字符

```html
<!-- HTML 实体 -->
&lt;      <!-- < -->
&gt;      <!-- > -->
&amp;     <!-- & -->
&quot;    <!-- " -->
&apos;    <!-- ' -->
&nbsp;    <!-- 空格 -->
&copy;    <!-- © -->
&reg;     <!-- ® -->
&trade;   <!-- ™ -->
&times;   <!-- × -->
&divide;  <!-- ÷ -->
&plusmn;  <!-- ± -->
&deg;     <!-- ° -->
&para;    <!-- ¶ -->
&sect;    <!-- § -->

<!-- 数字实体 -->
&#60;     <!-- < -->
&#62;     <!-- > -->
&#38;     <!-- & -->
```

---

## 13. 全局属性

```html
<!-- id：唯一标识 -->
<div id="header"></div>

<!-- class：类名（可多个） -->
<div class="container main"></div>

<!-- style：内联样式 -->
<p style="color: red; font-size: 16px;">文本</p>

<!-- title：提示文本 -->
<p title="这是提示">鼠标悬停查看</p>

<!-- data-* 自定义属性 -->
<div data-id="123" data-name="test"></div>

<!-- hidden：隐藏元素 -->
<div hidden>隐藏内容</div>

<!-- contenteditable：可编辑 -->
<div contenteditable="true">可编辑内容</div>

<!-- draggable：可拖拽 -->
<div draggable="true">可拖拽</div>

<!-- lang：语言 -->
<p lang="en">English text</p>

<!-- dir：文本方向 -->
<p dir="rtl">从右到左</p>

<!-- tabindex：Tab 键顺序 -->
<input type="text" tabindex="1">
<input type="text" tabindex="2">

<!-- accesskey：快捷键 -->
<button accesskey="s">保存 (Alt+S)</button>

<!-- spellcheck：拼写检查 -->
<textarea spellcheck="true"></textarea>
```

---

## 14. 页面布局示例

### 14.1 基础布局

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>网站标题</title>
</head>
<body>
    <header>
        <h1>网站 Logo</h1>
        <nav>
            <ul>
                <li><a href="#home">首页</a></li>
                <li><a href="#about">关于</a></li>
                <li><a href="#contact">联系</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section id="home">
            <h2>首页</h2>
            <p>欢迎来到我的网站</p>
        </section>
        
        <section id="about">
            <h2>关于我们</h2>
            <article>
                <h3>公司介绍</h3>
                <p>公司简介内容</p>
            </article>
        </section>
    </main>
    
    <aside>
        <h3>侧边栏</h3>
        <ul>
            <li>链接1</li>
            <li>链接2</li>
        </ul>
    </aside>
    
    <footer>
        <p>&copy; 2024 版权所有</p>
    </footer>
</body>
</html>
```

### 14.2 博客文章页面

```html
<article>
    <header>
        <h1>文章标题</h1>
        <p>
            作者：<span>张三</span> | 
            发布时间：<time datetime="2024-01-01">2024年1月1日</time>
        </p>
    </header>
    
    <section>
        <h2>章节1</h2>
        <p>内容...</p>
        
        <figure>
            <img src="image.jpg" alt="配图">
            <figcaption>图片说明</figcaption>
        </figure>
    </section>
    
    <section>
        <h2>章节2</h2>
        <p>内容...</p>
    </section>
    
    <footer>
        <p>标签：<a href="#">HTML</a> <a href="#">CSS</a></p>
    </footer>
</article>
```

---

## 15. SEO 优化要点

```html
<head>
    <!-- 标题（50-60字符） -->
    <title>页面标题 - 网站名称</title>
    
    <!-- 描述（150-160字符） -->
    <meta name="description" content="页面描述，简洁明了">
    
    <!-- 关键词 -->
    <meta name="keywords" content="关键词1, 关键词2, 关键词3">
    
    <!-- 作者 -->
    <meta name="author" content="作者名">
    
    <!-- 规范链接 -->
    <link rel="canonical" href="https://example.com/page">
    
    <!-- Open Graph（社交分享） -->
    <meta property="og:title" content="页面标题">
    <meta property="og:description" content="页面描述">
    <meta property="og:image" content="https://example.com/image.jpg">
    <meta property="og:url" content="https://example.com/page">
    
    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="页面标题">
    <meta name="twitter:description" content="页面描述">
    <meta name="twitter:image" content="https://example.com/image.jpg">
</head>

<body>
    <!-- 语义化标签 -->
    <header>
        <h1>主标题（每页只有一个 h1）</h1>
    </header>
    
    <!-- 图片 alt 属性 -->
    <img src="image.jpg" alt="描述性文字">
    
    <!-- 链接 title 属性 -->
    <a href="page.html" title="链接说明">链接文本</a>
    
    <!-- 结构化数据 -->
    <script type="application/ld+json">
    {
        "@context": "https://schema.org",
        "@type": "Article",
        "headline": "文章标题",
        "author": "作者名",
        "datePublished": "2024-01-01"
    }
    </script>
</body>
```

---

## 16. 无障碍访问 (Accessibility)

```html
<!-- 语义化标签 -->
<nav aria-label="主导航">
    <ul>
        <li><a href="#home">首页</a></li>
    </ul>
</nav>

<!-- alt 属性 -->
<img src="logo.png" alt="公司 Logo">

<!-- 装饰性图片 -->
<img src="decoration.png" alt="" role="presentation">

<!-- 表单标签关联 -->
<label for="email">邮箱：</label>
<input type="email" id="email" name="email" aria-required="true">

<!-- ARIA 属性 -->
<button aria-label="关闭对话框">×</button>

<div role="alert" aria-live="polite">
    提示信息
</div>

<!-- 跳过导航链接 -->
<a href="#main-content" class="skip-link">跳到主内容</a>

<!-- 键盘可访问 -->
<div tabindex="0" role="button" aria-pressed="false">
    自定义按钮
</div>

<!-- 语言标记 -->
<html lang="zh-CN">
<p lang="en">English text</p>
```

---

## 17. 常用代码片段

### 17.1 导航菜单

```html
<nav>
    <ul>
        <li><a href="#home" class="active">首页</a></li>
        <li><a href="#about">关于</a></li>
        <li><a href="#services">服务</a></li>
        <li><a href="#contact">联系</a></li>
    </ul>
</nav>
```

### 17.2 卡片组件

```html
<div class="card">
    <img src="image.jpg" alt="卡片图片">
    <div class="card-body">
        <h3>卡片标题</h3>
        <p>卡片描述文字</p>
        <a href="#" class="btn">了解更多</a>
    </div>
</div>
```

### 17.3 模态框

```html
<div class="modal" id="myModal">
    <div class="modal-content">
        <span class="close">&times;</span>
        <h2>模态框标题</h2>
        <p>模态框内容</p>
    </div>
</div>
```

### 17.4 面包屑导航

```html
<nav aria-label="面包屑">
    <ol>
        <li><a href="/">首页</a></li>
        <li><a href="/category">分类</a></li>
        <li aria-current="page">当前页面</li>
    </ol>
</nav>
```

### 17.5 分页

```html
<nav aria-label="分页">
    <ul class="pagination">
        <li><a href="#" aria-label="上一页">&laquo;</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#" aria-current="page">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#" aria-label="下一页">&raquo;</a></li>
    </ul>
</nav>
```

---

## 18. 最佳实践

### 18.1 代码规范

```html
<!-- 使用小写标签名 -->
<div></div>  ✓
<DIV></DIV>  ✗

<!-- 属性使用双引号 -->
<img src="image.jpg" alt="图片">  ✓
<img src='image.jpg' alt='图片'>  ✗

<!-- 关闭所有标签 -->
<p>段落</p>  ✓
<p>段落      ✗

<!-- 单标签自闭合（可选） -->
<br>   ✓
<br/>  ✓

<!-- 属性值不省略 -->
<input type="checkbox" checked="checked">  ✓
<input type="checkbox" checked>            ✓

<!-- 合理缩进 -->
<div>
    <p>段落</p>
</div>
```

### 18.2 性能优化

```html
<!-- 延迟加载图片 -->
<img src="image.jpg" alt="图片" loading="lazy">

<!-- 异步加载脚本 -->
<script src="script.js" async></script>
<script src="script.js" defer></script>

<!-- 预加载资源 -->
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
<link rel="prefetch" href="next-page.html">
<link rel="dns-prefetch" href="https://example.com">

<!-- 压缩和优化图片 -->
<picture>
    <source srcset="image.webp" type="image/webp">
    <img src="image.jpg" alt="图片">
</picture>
```

### 18.3 安全性

```html
<!-- 外部链接添加 rel -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
    外部链接
</a>

<!-- 用户生成内容转义 -->
<!-- 避免 XSS 攻击，使用服务器端转义 -->

<!-- 表单 CSRF 保护 -->
<form method="post">
    <input type="hidden" name="csrf_token" value="TOKEN">
</form>
```

---

## 附录：常用标签速查

### 文档结构
- `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`

### 元数据
- `<title>`, `<meta>`, `<link>`, `<style>`, `<script>`

### 文本
- `<h1>`-`<h6>`, `<p>`, `<br>`, `<hr>`, `<strong>`, `<em>`, `<span>`

### 链接和媒体
- `<a>`, `<img>`, `<audio>`, `<video>`, `<iframe>`

### 列表
- `<ul>`, `<ol>`, `<li>`, `<dl>`, `<dt>`, `<dd>`

### 表格
- `<table>`, `<tr>`, `<td>`, `<th>`, `<thead>`, `<tbody>`, `<tfoot>`

### 表单
- `<form>`, `<input>`, `<textarea>`, `<select>`, `<option>`, `<button>`, `<label>`

### 语义化
- `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`

### 容器
- `<div>`, `<span>`

---

**学习建议：**
1. 掌握基本标签和文档结构
2. 理解语义化标签的使用
3. 熟练使用表单元素
4. 注重代码规范和可访问性
5. 多实践，多写代码
6. 结合 CSS 和 JavaScript 学习