
# Advance_Assessment 2

---

##  目录

- [ 项目整体架构](#-项目整体架构)
- [ 模块依赖关系](#-模块依赖关系)
- [ 类继承体系](#️-类继承体系)
- [ 完整数据流水线](#-完整数据流水线)
- [ 模块 1：load_raw_records](#-模块-1load_raw_records)
- [ 模块 2：build_posts](#️-模块-2build_posts)
- [ 模块 3：count_embedded_likes](#-模块-3count_embedded_likes)
- [ 模块 4：descendants_of](#-模块-4descendants_of)
- [ 模块 5：solution_remover 装饰器](#-模块-5solution_remover-装饰器)
- [ 端到端调用示例](#-端到端调用示例)

---

## Structure

```mermaid
flowchart TB
    A[" 原始数据文件<br/>posts.txt"] -->|读取行| B[" load_raw_records<br/>解析 + fix_text 修复"]
    B -->|"records<br/>List[dict]"| C[" build_posts<br/>构造对象 + 合并"]
    C -->|"posts<br/>Dict[str, Post]"| D{"分析类操作"}
    D --> E[" count_embedded_likes<br/>统计点赞总数"]
    D --> F[" descendants_of<br/>查找所有后代"]
    F -.->|"被装饰"| G[" solution_remover<br/>过滤敏感帖子"]
    E --> H[" 整数: 总点赞数"]
    G --> I[" 列表: 过滤后的后代"]

    style A fill:#FFE4B5,color:#000
    style B fill:#B0E0E6,color:#000
    style C fill:#98FB98,color:#000
    style D fill:#FFD700,color:#000
    style E fill:#FFB6C1,color:#000
    style F fill:#FFB6C1,color:#000
    style G fill:#DDA0DD,color:#000
    style H fill:#F0E68C,color:#000
    style I fill:#F0E68C,color:#000
```

---

## 模块依赖关系

```mermaid
graph LR
    POST[" post.py<br/>Post / TextPost / StoryPost"]
    LOAD[" load_raw_records.py<br/>fix_text + 解析"]
    BUILD[" build_posts.py"]
    COUNT[" count_embedded_likes.py"]
    DESC[" descendants_of.py"]
    REM[" solution_remover.py"]

    BUILD -->|import| POST
    COUNT -->|import| POST
    DESC -->|import StoryPost| POST
    REM -->|import StoryPost| POST
    DESC -->|import @| REM

    style POST fill:#87CEEB,color:#000
    style LOAD fill:#FFA07A,color:#000
    style BUILD fill:#98FB98,color:#000
    style COUNT fill:#FFB6C1,color:#000
    style DESC fill:#FFB6C1,color:#000
    style REM fill:#DDA0DD,color:#000
```

>  **`load_raw_records.py` 不依赖任何项目内模块**，纯文本处理；其他文件都围绕 `post.py` 的类展开。

---

##  类继承体系

```mermaid
classDiagram
    class Post {
        +str post_id
        +str author
        +str text
        +str post_type
        +int likes
        +float timestamp
        +__init__(post_id, author, text, ...)
        +__str__()
        +__eq__(other) 比较 post_id
        +__hash__()
        +likesadd(n)
        +together(other)
        +merge_in(other) 合并 likes + 长文本
    }

    class TextPost {
        +__init__(post_id, author, text)
    }

    class StoryPost {
        +list children
        +__init__(post_id, author, text, children)
        +__str__()
    }

    Post <|-- TextPost : 继承
    Post <|-- StoryPost : 继承
```

###  三种类的核心区别

| 类 | 是否有 children | 角色 | 在树中的位置 |
|----|----------------|------|-------------|
| `Post` | ❌ | 抽象基类 | 不直接使用 |
| `TextPost` | ❌ | 普通文本帖 |  叶子节点 |
| `StoryPost` | ✅ | 故事帖（可包含其他帖） |  分支节点 |

---

##  完整数据流水线

```mermaid
flowchart LR
    subgraph S1 [" 阶段 1：原始读取"]
        A1["posts.txt<br/>(每行一条)"] --> A2["逐行 readlines<br/>或 yield"]
        A2 --> A3["剥离 # 注释 / 空行"]
    end
    
    subgraph S2 [" 阶段 2：字段解析"]
        B1["按 ; 分割"] --> B2["按 = 拆 key/value"]
        B2 --> B3["text 字段<br/>调用 fix_text"]
        B3 --> B4["dict 记录"]
    end
    
    subgraph S3 [" 阶段 3：对象构建"]
        C1["读 post_type"] --> C2{"类型?"}
        C2 -->|TextPost| C3["TextPost(...)"]
        C2 -->|StoryPost| C4["拆分 children<br/>StoryPost(...)"]
        C2 -->|其他| C5[" continue"]
        C3 --> C6["设置 likes/timestamp"]
        C4 --> C6
    end
    
    subgraph S4 ["阶段 4：去重合并"]
        D1{"post_id<br/>已存在?"} -->|是| D2["merge_in<br/>合并 likes<br/>保留长 text"]
        D1 -->|否| D3["直接放入字典"]
    end
    
    subgraph S5 ["阶段 5：分析"]
        E1["count_embedded_likes<br/>总点赞"]
        E2["descendants_of<br/> 后代列表"]
        E2 --> E3["solution_remover<br/> 过滤"]
    end

    A3 --> B1
    B4 --> C1
    C6 --> D1
    D2 --> S5
    D3 --> S5

    style S1 fill:#FFE4B5,color:#000
    style S2 fill:#B0E0E6,color:#000
    style S3 fill:#98FB98,color:#000
    style S4 fill:#FFD700,color:#000
    style S5 fill:#FFB6C1,color:#000
```

---

##  模块 1：load_raw_records

> **职责**：把 `posts.txt` 文件每一行原始字符串解析为 `dict`，并修复 `text` 字段。

 `fix_text` 字符修复算法

```mermaid
flowchart TD
    A["输入: 字符 ch"] --> B{"是英文字母?<br/>a-z 或 A-Z"}
    B -->|否| C["原样保留<br/>(数字/符号/空格)"]
    B -->|是| D["计算 ord(ch)"]
    D --> E{"code 是偶数?"}
    E -->|是| F["chr(code - 1)<br/> 退一位"]
    E -->|否| G["chr(code + 1)<br/> 进一位"]
    C --> H["拼接到 result"]
    F --> H
    G --> H

    style B fill:#FFD700,color:#000
    style E fill:#FFD700,color:#000
    style F fill:#FFB6C1,color:#000
    style G fill:#98FB98,color:#000
```

>  **示例**：`'b'`（ord=98，偶数）→ `'a'`；`'a'`（ord=97，奇数）→ `'b'`。这是个**对称变换**：fix_text(fix_text(x)) == x

###  `load_raw_records` 主流程

```mermaid
flowchart TD
    A[" 输入 filepath"] --> B["打开文件"]
    B --> C{"文件存在?"}
    C -->|否| D["FileNotFoundError"]
    C -->|是| E["逐行读取"]
    E --> F["line.strip()"]
    F --> G{"空行 or<br/>以 # 开头?"}
    G -->|是| H["跳过"]
    G -->|否| I["按 ; 分割成 parts"]
    I --> J["遍历每个 item"]
    J --> K{"含 '=' ?"}
    K -->|否| L["ValueError<br/>invalid pair"]
    K -->|是| M["按 = 拆成 key, value<br/>(只拆第一个)"]
    M --> N{"key == 'text'?"}
    N -->|是| O["fix_text(value)"]
    N -->|否| P["保留原值"]
    O --> Q["record[key] = value"]
    P --> Q
    Q --> R{"还有 item?"}
    R -->|是| J
    R -->|否| S["yield record<br/>一条记录完成"]
    S --> T{"还有行?"}
    T -->|是| E
    T -->|否| U["结束"]

    style D fill:#FF6B6B,color:#000
    style L fill:#FF6B6B,color:#000
    style S fill:#98FB98,color:#000
    style U fill:#98FB98,color:#000
```

### 文件中的两个版本对比

| 版本 | 实现方式 | 特点 |
|------|---------|------|
| 第 1 个（被覆盖） | `f.readlines()` 一次读完 → `return list` | 占内存  |
| 第 2 个（生效） | `for line in f` + `yield record` | **生成器**，省内存 |

>  **注意**：Python 中**后定义的函数会覆盖前面的同名函数**，所以实际生效的是第二个 `yield` 版本！

---

##  模块 2：build_posts

> **职责**：把 `dict` 列表转换为 `Post` 对象字典，处理重复 ID 时合并。

```mermaid
flowchart TD
    A["🚀 输入 records"] --> B["posts = {}"]
    B --> C["遍历每条 record"]
    C --> D["try 块开始"]
    D --> E["读取 post_type / post_id<br/>author / text"]
    E --> F{"post_type 是?"}
    F -->|TextPost| G["TextPost(post_id, author, text)"]
    F -->|StoryPost| H["children_str = record['children']<br/>按 ',' 分割并 strip"]
    H --> I["StoryPost(post_id, author,<br/>text, children)"]
    F -->|其他| J["⏭️ continue"]
    G --> K{"有 likes 字段?"}
    I --> K
    K -->|是| L["post.likes = int(...)"]
    K -->|否| M["likes"]
```

---

## 模块 3：`post.py`
[[Python 技术文档#第 7 章 面向对象编程]][[Computer science foundation note#第 18 章 面向对象核心概念]]
### `Post.__init__` 参数校验流程

```mermaid
flowchart TD
    A[" Post.__init__ 被调用"] --> B{"post_id 校验<br/>是 str? 长度=10? 全数字?"}
    B -->|任一不满足| B1["❌ ValueError<br/>invalid post id"]
    B -->|通过| C{"author 校验<br/>是 str? 长度 1-20? 全英文?"}
    C -->|任一不满足| C1["❌ ValueError<br/>invalid author"]
    C -->|通过| D{"text 校验<br/>是 str?"}
    D -->|否| D1["❌ ValueError<br/>invalid text"]
    D -->|通过| E{"post_type 校验<br/>是 str?"}
    E -->|否| E1["❌ ValueError<br/>invalid post type"]
    E -->|通过| F{"likes 校验<br/>是 int? 非负?"}
    F -->|否| F1["❌ ValueError<br/>invalid likes"]
    F -->|通过| G{"timestamp 校验<br/>是 int 或 float?"}
    G -->|否| G1["❌ ValueError<br/>invalid timestamp"]
    G -->|通过| H["赋值给 self.xxx"]
    H --> I["对象创建成功"]

    style B1 fill:#FF6B6B,color:#000
    style C1 fill:#FF6B6B,color:#000
    style D1 fill:#FF6B6B,color:#000
    style E1 fill:#FF6B6B,color:#000
    style F1 fill:#FF6B6B,color:#000
    style G1 fill:#FF6B6B,color:#000
    style I fill:#98FB98,color:#000
```

---

###  `StoryPost` 额外校验流程

```mermaid
flowchart TD
    A[" StoryPost.__init__"] --> B["调用 super().__init__()<br/>先做 Post 的 6 项校验"]
    B --> C{"children 是 list?"}
    C -->|否| C1["❌ ValueError"]
    C -->|是| D["遍历每个 child_id"]
    D --> E{"每个 child_id<br/>是 str? 长度=10? 全数字?"}
    E -->|否| E1["❌ ValueError<br/>invalid child id"]
    E -->|是| F{"child_id == self.post_id?<br/>(防止自引用)"}
    F -->|是| F1["❌ ValueError<br/>不能把自己当孩子"]
    F -->|否| G{"还有下一个?"}
    G -->|是| D
    G -->|否| H[" self.children = children"]
    H --> I["StoryPost 创建成功"]

    style C1 fill:#FF6B6B,color:#000
    style E1 fill:#FF6B6B,color:#000
    style F1 fill:#FF6B6B,color:#000
    style I fill:#98FB98,color:#000
```

---

### `Post.merge_in` 合并方法流程

```mermaid
flowchart TD
    A[" self.merge_in(other)"] --> B{"两者 post_id 相同?"}
    B -->|否| B1[" ValueError<br/>不能合并不同 ID 的帖子"]
    B -->|是| C[" self.likes += other.likes<br/>(点赞数累加)"]
    C --> D{"len(other.text) ><br/>len(self.text)?"}
    D -->|是| E[" self.text = other.text<br/>(保留更长的文本)"]
    D -->|否| F["保留 self.text"]
    E --> G["✅ 合并完成"]
    F --> G

    style B1 fill:#FF6B6B,color:#000
    style C fill:#FFB6C1,color:#000
    style E fill:#98FB98,color:#000
    style G fill:#98FB98,color:#000
```

> 💡 **设计哲学**：合并时**点赞累加**（数据汇总），但**文本保留较长版本**（信息更全）。

---

## 模块4：`count_embedded_likes` — 统计点赞总数
[[Python 技术文档#**第 15 章：递归函数（Recursive Functions）**]][[Computer science foundation note#13.7 递归 vs 迭代（互相转换）]]
> **职责**：递归统计某个帖子**自己 + 所有后代**的总点赞数。

### 函数主流程

````mermaid

flowchart TD
    A[" count_embedded_likes<br/>post_id, posts"] --> B["post = posts[post_id]"]
    B --> C[" total = post.likes"]
    C --> D{"post 是 StoryPost?"}
    D -->|"否 叶子节点"| E[" 无孩子可遍历"]
    D -->|是| F["遍历 post.children"]
    F --> G["取出 child_id"]
    G --> H[" 递归调用<br/>count_embedded_likes"]
    H --> I["接收返回值 sub_total"]
    I --> J["total += sub_total"]
    J --> K{"还有下个 child?"}
    K -->|是| G
    K -->|否| L["所有孩子处理完毕"]
    E --> M[" return total"]
    L --> M

    style C fill:#FFD700,color:#000
    style H fill:#FFB6C1,color:#000
    style J fill:#98FB98,color:#000
    style M fill:#87CEEB,color:#000
```

````

---

###  递归调用栈示意（树形展开）

```mermaid
flowchart TD
    A["🟦 count(A) likes=10"] --> B["🟨 count(B) likes=5"]
    A --> C["🟥 count(C) likes=2 TextPost 终止"]
    B --> D["🟩 count(D) likes=3 TextPost 终止"]
    
    D -.->|"return 3"| B
    B -.->|"return 5+3=8"| A
    C -.->|"return 2"| A
    A -.->|"return 10+8+2=20"| RESULT["最终: 20"]

    style A fill:#B0E0E6,color:#000
    style B fill:#FFD700,color:#000
    style C fill:#FFB6C1,color:#000
    style D fill:#98FB98,color:#000
    style RESULT fill:#FFE4B5,color:#000
```

---

## 模块5：`descendants_of` — 后代查询
[[Python 技术文档#**第 15 章：递归函数（Recursive Functions）**]][[Computer science foundation note#13.7 递归 vs 迭代（互相转换）]]
> **职责**：递归收集某个帖子的所有**后代**帖子（去重 + 过滤无点赞 + 排除 solution）。

###  函数主流程

```mermaid
flowchart TD
    A[" @solution_remover<br/>descendants_of post_id, posts"] --> B["result = [] 空列表"]
    B --> C["post = posts[post_id]"]
    C --> D{"post 是 StoryPost?"}
    D -->|否| Z[" return [] 空列表"]
    D -->|是| E["遍历 post.children"]
    E --> F["取出 child_id"]
    F --> G["child = posts[child_id]"]
    G --> H{"child.likes > 0<br/>且 child not in result?"}
    H -->| 满足| I[" result.append(child)<br/>加入直接子孩"]
    H -->|不满足| J[" 跳过添加"]
    I --> K[" 递归 descendants_of(child_id)"]
    J --> K
    K --> L[" 拿到 deeper 列表"]
    L --> M["遍历 deeper 中每个 d"]
    M --> N{"d not in result?"}
    N -->|是| O["result.append(d)"]
    N -->|否| P[" 跳过 (去重)"]
    O --> Q{"还有下个 d?"}
    P --> Q
    Q -->|是| M
    Q -->|否| R{"还有下个 child?"}
    R -->|是| F
    R -->|否| S[" return result"]
    S --> FILTER[" 经过 solution_remover<br/>过滤掉 solution 帖子"]
    FILTER --> END[" 最终列表返回给调用者"]

    style B fill:#FFE4B5,color:#000
    style I fill:#98FB98,color:#000
    style O fill:#98FB98,color:#000
    style K fill:#FFB6C1,color:#000
    style FILTER fill:#DDA0DD,color:#000
    style END fill:#87CEEB,color:#000
```

---

###  关键设计要点

```mermaid
flowchart LR
    A["三大过滤/去重机制"] --> B[" likes > 0<br/>过滤无人问津的帖子"]
    A --> C[" not in result<br/>列表去重"]
    A --> D[" @solution_remover<br/>外层过滤 solution 帖"]

    style B fill:#FFD700,color:#000
    style C fill:#98FB98,color:#000
    style D fill:#DDA0DD,color:#000
```

---

## 模块6： `solution_remover` — 装饰器过滤
[[Python 技术文档#**14.2 装饰器（Decorators）**]]

> **职责**：作为装饰器，**自动过滤掉返回列表中**任何 `text` 包含 "solution"（不区分大小写）的 `StoryPost`。

###  装饰器

```mermaid
flowchart TD
    A[" 用户调用<br/>descendants_of(post_id=X, posts=Y)"] --> B["实际执行的是<br/>wrapper(*args, **kwargs)"]
    B --> C["wrapper 内部:<br/>调用原始 func(*args, **kwargs)"]
    C --> D["原始 descendants_of 执行<br/>返回 result_list"]
    D --> E["wrapper 接收 result_list"]
    E --> F["filtered = [] 空列表"]
    F --> G["遍历 result_list 中每个 post"]
    G --> H{"post 是 StoryPost?"}
    H -->|否| I[" 直接保留<br/>filtered.append(post)"]
    H -->|是| J{"'solution' in post.text.lower()?"}
    J -->|否| K[" 不含 solution 保留<br/>filtered.append(post)"]
    J -->|是| L[" 跳过 (过滤掉)"]
    I --> M{"还有下个 post?"}
    K --> M
    L --> M
    M -->|是| G
    M -->|否| N[" return filtered"]

    style C fill:#FFB6C1,color:#000
    style J fill:#FFD700,color:#000
    style L fill:#FF6B6B,color:#000
    style N fill:#98FB98,color:#000
```

---

### 装饰器结构（洋葱模型）

```mermaid
flowchart LR
    USER["调用方"] -->|"传入 post_id, posts"| WRAPPER["wrapper 外层"]
    WRAPPER -->|"原样转发参数"| FUNC["原始 descendants_of"]
    FUNC -->|"返回原始列表"| WRAPPER
    WRAPPER -->|"过滤后返回"| USER

    style USER fill:#87CEEB,color:#000
    style WRAPPER fill:#DDA0DD,color:#000
    style FUNC fill:#FFB6C1,color:#000
```

