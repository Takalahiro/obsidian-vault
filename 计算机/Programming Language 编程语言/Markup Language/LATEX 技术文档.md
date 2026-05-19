[[Markdown 技术文档]]
LaTeX 是一个文档排版系统和标记语言，主要用于生成高质量的科技和学术文档。

具体来说：

**性质分类**

- 是一种标记语言（markup language），而不是所见即所得的编辑器
- 是基于 TeX 排版引擎的宏包系统
- 是开源软件

**主要用途**

- 学术论文、书籍排版
- 数学公式排版（这是它的强项）
- 科技文档、学位论文
- 演示文稿（通过 Beamer 等）

**特点**

- 内容与格式分离
- 对数学公式、参考文献、交叉引用等有出色支持
- 输出质量高，特别是印刷品质
- 学习曲线较陡
**工作方式**  
你用纯文本写带有 LaTeX 命令的源文件（.tex），然后编译生成 PDF 等格式的文档。

比如写数学公式：

Einstein's equation: $E = mc^2$
在学术界，特别是数学、物理、计算机科学等领域，LaTeX 是事实上的标准工具。
### 完整结构
```latex
\documentclass[12pt,a4paper]{article}  % 文档类

% 导言区 - 加载宏包
\usepackage[UTF8]{ctex}      % 中文支持
\usepackage{amsmath}         % 数学公式
\usepackage{graphicx}        % 插图

% 标题信息
\title{文档标题}
\author{作者名}
\date{\today}

% 正文区
\begin{document}

\maketitle                   % 生成标题
\tableofcontents            % 生成目录

\section{第一章}
正文内容...

\end{document}
```

### 常用文档类
- `article` - 文章（论文、报告）
- `book` - 书籍
- `beamer` - 演示文稿
- `report` - 长报告

---

## 文本格式

### 字体样式
```latex
\textbf{粗体}
\textit{斜体}
\underline{下划线}
\texttt{等宽字体}
\emph{强调}
```

### 字号
```latex
{\tiny 极小}
{\small 小号}
{\normalsize 正常}
{\large 大号}
{\Large 更大}
{\LARGE 很大}
{\huge 巨大}
{\Huge 最大}
```

### 对齐
```latex
\begin{center}
居中文本
\end{center}

\begin{flushleft}
左对齐
\end{flushleft}

\begin{flushright}
右对齐
\end{flushright}
```

### 段落和换行
- 空一行表示新段落
- `\\` 或 `\newline` 强制换行
- `\par` 开始新段落

---

## 数学公式

### 行内公式
```latex
这是行内公式 $E = mc^2$，继续文本。
```
效果：这是行内公式 E = mc² ，继续文本。

### 行间公式（不编号）
```latex
\[
    \int_{0}^{\infty} e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
\]
```
$$\[
    \int_{0}^{\infty} e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
\]$$
### 行间公式（带编号）
```latex
\begin{equation}
    \sum_{i=1}^{n} i = \frac{n(n+1)}{2}
    \label{eq:sum}
\end{equation}
```
$$\begin{equation}
    \sum_{i=1}^{n} i = \frac{n(n+1)}{2}
    \label{eq:sum}
\end{equation}$$
### 常用数学符号

#### 上下标
```latex
$x^2$           % 上标
$x_i$           % 下标
$x^{2y}$        % 多字符上标
$x_{i,j}$       % 多字符下标
```
$x^2$         
$x_i$           
$x^{2y}$      
$x_{i,j}$
#### 分数和根号
```latex
$\frac{a}{b}$           % 分数
$\sqrt{x}$              % 平方根
$\sqrt[n]{x}$           % n次方根
```
$\frac{a}{b}$        
$\sqrt{x}$           
$\sqrt[n]{x}$    
#### 求和、积分、极限
```latex
$\sum_{i=1}^{n} x_i$                    % 求和
$\int_{a}^{b} f(x) dx$                  % 积分
$\lim_{x \to \infty} f(x)$              % 极限
$\prod_{i=1}^{n} x_i$                   % 连乘
```
$\sum_{i=1}^{n} x_i$                    % 求和
$\int_{a}^{b} f(x) dx$                  
$\lim_{x \to \infty} f(x)$             
$\prod_{i=1}^{n} x_i$  
#### 希腊字母
```latex
$\alpha, \beta, \gamma, \delta$
$\epsilon, \theta, \lambda, \mu$
$\pi, \sigma, \phi, \omega$
$\Gamma, \Delta, \Theta, \Lambda$
```

$\alpha, \beta, \gamma, \delta$
$\epsilon, \theta, \lambda, \mu$
$\pi, \sigma, \phi, \omega$
$\Gamma, \Delta, \Theta, \Lambda$

#### 关系符号
```latex
$\leq$  $\geq$  $\neq$  $\approx$
$\equiv$  $\sim$  $\propto$
$\in$  $\notin$  $\subset$  $\subseteq$
```
$\leq$  $\geq$  $\neq$  $\approx$
$\equiv$  $\sim$  $\propto$
$\in$  $\notin$  $\subset$  $\subseteq$
#### 矩阵
```latex
\[
\begin{matrix}
a & b \\
c & d
\end{matrix}
\]

\[
\begin{pmatrix}  % 圆括号
a & b \\
c & d
\end{pmatrix}
\]

\[
\begin{bmatrix}  % 方括号
a & b \\
c & d
\end{bmatrix}
\]
```
$$\[
\begin{matrix}
a & b \\
c & d
\end{matrix}
\]

\[
\begin{pmatrix}  % 圆括号
a & b \\
c & d
\end{pmatrix}
\]

\[
\begin{bmatrix}  % 方括号
a & b \\
c & d
\end{bmatrix}
\]$$
#### 多行公式
```latex
\begin{align}
    f(x) &= x^2 + 2x + 1 \\
         &= (x+1)^2
\end{align}
```
$$\begin{align}
    f(x) &= x^2 + 2x + 1 \\
         &= (x+1)^2
\end{align}$$
---

## 列表和表格

### 无序列表
```latex
\begin{itemize}
    \item 第一项
    \item 第二项
    \item 第三项
\end{itemize}
```

### 有序列表
```latex
\begin{enumerate}
    \item 第一步
    \item 第二步
    \item 第三步
\end{enumerate}
```

### 描述列表
```latex
\begin{description}
    \item[LaTeX] 排版系统
    \item[Markdown] 轻量级标记语言
\end{description}
```

### 表格
```latex
\begin{table}[h]
\centering
\caption{成绩表}
\begin{tabular}{|c|c|c|}
\hline
姓名 & 科目 & 成绩 \\
\hline
张三 & 数学 & 95 \\
李四 & 物理 & 88 \\
\hline
\end{tabular}
\end{table}
```

表格说明：
- `|c|c|c|` - 三列居中，带竖线
- `l` 左对齐，`c` 居中，`r` 右对齐
- `\hline` - 横线
- `&` - 列分隔符
- `\\` - 行分隔符

---

## 图片和代码

### 插入图片
```latex
\usepackage{graphicx}  % 导言区加载

\begin{figure}[h]
\centering
\includegraphics[width=0.5\textwidth]{image.png}
\caption{图片标题}
\label{fig:example}
\end{figure}
```

位置参数：
- `h` - here (此处)
- `t` - top (页顶)
- `b` - bottom (页底)
- `p` - page (单独一页)

### 插入代码
```latex
\usepackage{listings}  % 导言区加载

% 行内代码
\verb|print("Hello")|

% 代码块
\begin{lstlisting}[language=Python]
def hello():
    print("Hello, World!")
\end{lstlisting}

% 从文件导入
\lstinputlisting[language=Python]{code.py}
```

---

## 常用技巧

### 交叉引用
```latex
\section{介绍}
\label{sec:intro}

如第 \ref{sec:intro} 节所述...
参见公式 \eqref{eq:sum}...
```

### 脚注
```latex
这是正文\footnote{这是脚注内容}。
```
$$这是正文\footnote{这是脚注内容}。$$
### 引用文献
```latex
\cite{author2020}

% 文档末尾
\begin{thebibliography}{99}
\bibitem{author2020} 作者名. 文章标题. 期刊名, 2020.
\end{thebibliography}
```

### 特殊字符
```latex
\%  \$  \&  \#  \_  \{  \}
\textbackslash  % 反斜杠
```

### 空格和换行
```latex
~           % 不可断空格
\,          % 小空格
\quad       % 1em 空格
\qquad      % 2em 空格
\\[2cm]     % 换行并增加垂直间距
\newpage    % 新页
```
$$$$
```latex
% 这是单行注释

\begin{comment}  % 需要 \usepackage{comment}
这是多行注释
可以注释多行
\end{comment}
```

---

## 常用宏包

| 宏包 | 功能 |
|------|------|
| `ctex` | 中文支持 |
| `amsmath` | 数学公式增强 |
| `graphicx` | 插图 |
| `geometry` | 页面设置 |
| `hyperref` | 超链接 |
| `listings` | 代码高亮 |
| `xcolor` | 颜色 |
| `tikz` | 绘图 |
| `biblatex` | 参考文献管理 |

---

## 编译命令

```bash
# 基本编译
pdflatex document.tex

# 中文文档
xelatex document.tex

# 带参考文献
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex
```

---

## 学习资源

- **官方文档**: [CTAN](https://www.ctan.org/)
- **在线教程**: [Overleaf Learn](https://www.overleaf.com/learn)
- **中文教程**: 《一份不太简短的 LaTeX 介绍》
- **符号查询**: [Detexify](http://detexify.kirelabs.org/classify.html) - 手写识别符号

---

## 快速参考

### 文档模板
```latex
\documentclass[12pt,a4paper]{article}
\usepackage[UTF8]{ctex}
\usepackage{amsmath,graphicx,hyperref}
\geometry{left=2.5cm,right=2.5cm,top=2.5cm,bottom=2.5cm}

\title{标题}
\author{作者}
\date{\today}

\begin{document}
\maketitle

\section{章节}
内容...

\end{document}
```

### 常见问题
1. **中文显示问题**: 使用 `xelatex` 编译，加载 `ctex` 宏包
2. **图片不显示**: 检查路径，使用相对路径
3. **公式编号**: 使用 `equation` 环境而非 `\[...\]`
4. **目录不更新**: 编译两次

---

**提示**: LaTeX 学习曲线较陡，但掌握基础后会非常高效。建议从简单文档开始，逐步学习高级功能。
```

这份笔记涵盖了 LaTeX 的核心内容，适合入门学习和日常查阅。