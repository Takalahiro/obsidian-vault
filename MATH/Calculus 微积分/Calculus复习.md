# MATH1061 微积分部分
## 第一部分：Functions 函数基础

### 1.1 Domain 定义域 - 保姆级判断法

**核心问题：什么样的 x 能放进这个函数？**

#### 判断流程（按顺序检查）：

**Step 1: 检查分母**
- 分母不能等于 0
- 例：$f(x) = \frac{1}{x-3}$ → $x \neq 3$
- 例：$f(x) = \frac{1}{x^2-4}$ → $x^2 \neq 4$ → $x \neq \pm 2$

**Step 2: 检查根号（偶次方根）**
- 根号里面必须 ≥ 0
- 例：$f(x) = \sqrt{x-5}$ → $x-5 \geq 0$ → $x \geq 5$
- 例：$f(x) = \sqrt{9-x^2}$ → $9-x^2 \geq 0$ → $x^2 \leq 9$ → $-3 \leq x \leq 3$

**Step 3: 检查对数**
- 对数里面必须 > 0（严格大于）
- 例：$f(x) = \ln(x+2)$ → $x+2 > 0$ → $x > -2$
- 例：$f(x) = \ln(4-x^2)$ → $4-x^2 > 0$ → $x^2 < 4$ → $-2 < x < 2$

**Step 4: 检查三角函数**
- $\tan x$：$\cos x \neq 0$ → $x \neq \frac{\pi}{2} + n\pi$
- $\sec x = \frac{1}{\cos x}$：$\cos x \neq 0$
- $\csc x = \frac{1}{\sin x}$：$\sin x \neq 0$ → $x \neq n\pi$

**Step 5: 复合函数（函数套函数）**
- 先算内层的 domain
- 再检查内层的输出能不能放进外层
- 例：$f(g(x)) = \ln(\sqrt{x-1})$
  - 内层：$\sqrt{x-1}$ 要求 $x \geq 1$
  - 外层：$\ln(u)$ 要求 $u > 0$，即 $\sqrt{x-1} > 0$ → $x > 1$
  - 最终：$x > 1$（注意不包括 1）

#### 完整例题：

**例 1：** $f(x) = \frac{\sqrt{x+3}}{x^2-9}$

**解题步骤：**
1. 根号：$x+3 \geq 0$ → $x \geq -3$
2. 分母：$x^2-9 \neq 0$ → $x \neq \pm 3$
3. 取交集：$x \geq -3$ 且 $x \neq 3$（$x=-3$ 时分母也不为 0，所以可以取）
4. **答案：** $[-3, 3) \cup (3, \infty)$

**例 2：** $f(x) = \ln\left(\frac{x-1}{x+2}\right)$

**解题步骤：**
1. 对数要求：$\frac{x-1}{x+2} > 0$
2. 分式大于 0 的条件：分子分母同号
   - 情况 1：都为正 → $x-1 > 0$ 且 $x+2 > 0$ → $x > 1$
   - 情况 2：都为负 → $x-1 < 0$ 且 $x+2 < 0$ → $x < -2$
3. **答案：** $(-\infty, -2) \cup (1, \infty)$

### 1.2 Inverse Function 反函数 - 完整流程

**什么时候有反函数？**
- 函数必须是 bijective（一一对应）
- 图像判断：horizontal line test（水平线最多交一次）

**求反函数的标准步骤：**

**例：** 求 $f(x) = \frac{2x+1}{x-3}$ 的反函数

**Step 1:** 写成 $y = \frac{2x+1}{x-3}$

**Step 2:** 解出 $x$（用 $y$ 表示）
y(x-3) = 2x+1
yx - 3y = 2x + 1
yx - 2x = 3y + 1
x(y-2) = 3y + 1
x = \frac{3y+1}{y-2}


**Step 3:** 交换 $x$ 和 $y$

y = \frac{3x+1}{x-2}

**Step 4:** 写成反函数记号

f^{-1}(x) = \frac{3x+1}{x-2}


**Step 5:** 确定 domain 和 range
- 原函数的 range = 反函数的 domain
- 原函数 $f(x) = \frac{2x+1}{x-3}$：
  - Domain: $x \neq 3$
  - Range: $y \neq 2$（通过 $y = \frac{2x+1}{x-3}$ 解出 $x$ 时分母不能为 0）
- 所以 $f^{-1}$ 的 domain 是 $x \neq 2$

---

## 第二部分：Limits and Continuity 极限与连续

### 2.1 Continuity 连续性 - 三步检查法

**函数在 $x=a$ 连续需要满足三个条件（缺一不可）：**

1. **$f(a)$ 存在**（函数在这点有定义）
2. **$\lim_{x \to a} f(x)$ 存在**（左右极限相等）
3. **$\lim_{x \to a} f(x) = f(a)$**（极限值等于函数值）

#### 分段函数连续性 - 完整例题

**例：** 求使下列函数在 $x=2$ 连续的 $k$ 值
$$f(x) = \begin{cases} 
x^2 + k & \text{if } x < 2 \\
3x - 1 & \text{if } x \geq 2
\end{cases}$$

**详细步骤：**

**Step 1:** 计算 $f(2)$（函数值）
- 因为 $x=2$ 时用第二个式子
- $f(2) = 3(2) - 1 = 5$

**Step 2:** 计算左极限 $\lim_{x \to 2^-} f(x)$
- $x < 2$ 时用第一个式子
- $\lim_{x \to 2^-} f(x) = \lim_{x \to 2^-} (x^2 + k) = 4 + k$

**Step 3:** 计算右极限 $\lim_{x \to 2^+} f(x)$
- $x > 2$ 时用第二个式子
- $\lim_{x \to 2^+} f(x) = \lim_{x \to 2^+} (3x-1) = 5$

**Step 4:** 令左极限 = 右极限 = 函数值
- $4 + k = 5$
- $k = 1$

**验证：** 当 $k=1$ 时，$\lim_{x \to 2^-} f(x) = 5 = f(2) = \lim_{x \to 2^+} f(x)$ ✓

### 2.2 Squeeze Theorem 夹逼定理 - 使用场景

**什么时候用夹逼定理？**
- 看到 $\sin(1/x)$ 或 $\cos(1/x)$
- 看到 $x^n \sin(\text{something})$ 或 $x^n \cos(\text{something})$

**核心思想：**
- $\sin$ 和 $\cos$ 的值域是 $[-1, 1]$
- 用不等式夹住目标函数

**标准模板：**

**例：** 求 $\lim_{x \to 0} x^2 \sin\left(\frac{1}{x}\right)$

**Step 1:** 写出 $\sin$ 的范围
$$-1 \leq \sin\left(\frac{1}{x}\right) \leq 1$$

**Step 2:** 两边同乘 $x^2$（注意 $x^2 \geq 0$，不等号方向不变）
$$-x^2 \leq x^2 \sin\left(\frac{1}{x}\right) \leq x^2$$

**Step 3:** 计算两边的极限
$$\lim_{x \to 0} (-x^2) = 0, \quad \lim_{x \to 0} x^2 = 0$$

**Step 4:** 应用夹逼定理
$$\lim_{x \to 0} x^2 \sin\left(\frac{1}{x}\right) = 0$$

**常见变形：**
- $\lim_{x \to 0} x \sin\left(\frac{1}{x}\right) = 0$
- $\lim_{x \to 0} x^3 \cos\left(\frac{1}{x^2}\right) = 0$
- $\lim_{x \to \infty} \frac{\sin x}{x} = 0$（因为 $-\frac{1}{x} \leq \frac{\sin x}{x} \leq \frac{1}{x}$）

---

## 第三部分：Derivatives 求导 - 完全拆解

### 3.1 求导第一步：识别函数类型

**看到一个函数，先问自己：**

| 问题 | 如果是 | 用什么方法 |
|------|--------|------------|
| 是加减吗？ | $f(x) + g(x)$ | 分别求导 |
| 是乘法吗？ | $f(x) \cdot g(x)$ | Product rule |
| 是除法吗？ | $\frac{f(x)}{g(x)}$ | Quotient rule |
| 有函数套函数吗？ | $f(g(x))$ | Chain rule |
| $y$ 和 $x$ 混在一起吗？ | $x^2 + xy + y^2 = 3$ | Implicit differentiation |
| 有积分号吗？ | $\frac{d}{dx} \int_0^x f(t) dt$ | FTC |

### 3.2 Chain Rule 链式法则 - 逐层拆解

**核心思想：从外到内，一层一层剥**

**公式：** $\frac{d}{dx}[f(g(x))] = f'(g(x)) \cdot g'(x)$

**记忆方法：** 外层导数（里面不动）× 里面的导数

#### 单层复合 - 基础例题

**例 1：** $\frac{d}{dx} \sin(x^2)$

**思考过程：**
1. 外层是 $\sin$，里面是 $x^2$
2. $\sin$ 的导数是 $\cos$
3. 里面 $x^2$ 保持不动：$\cos(x^2)$
4. 乘以里面的导数：$2x$
5. **答案：** $2x \cos(x^2)$

**例 2：** $\frac{d}{dx} e^{3x+1}$

**思考过程：**
1. 外层是 $e^u$，里面是 $3x+1$
2. $e^u$ 的导数还是 $e^u$
3. 里面保持不动：$e^{3x+1}$
4. 乘以里面的导数：$3$
5. **答案：** $3e^{3x+1}$

**例 3：** $\frac{d}{dx} \ln(x^2 + 1)$

**思考过程：**
1. 外层是 $\ln u$，里面是 $x^2+1$
2. $\ln u$ 的导数是 $\frac{1}{u}$
3. 代入里面：$\frac{1}{x^2+1}$
4. 乘以里面的导数：$2x$
5. **答案：** $\frac{2x}{x^2+1}$

#### 多层复合 - 进阶例题

**例 4：** $\frac{d}{dx} \sin^3(2x)$

**注意：** $\sin^3(2x) = [\sin(2x)]^3$

**思考过程（从外到内）：**
1. **最外层：** 三次方 $u^3$ → 导数 $3u^2$
   - 里面保持：$3[\sin(2x)]^2$
2. **中间层：** $\sin(2x)$ → 导数 $\cos(2x)$
   - 现在是：$3[\sin(2x)]^2 \cdot \cos(2x)$
3. **最内层：** $2x$ → 导数 $2$
   - 最终：$3[\sin(2x)]^2 \cdot \cos(2x) \cdot 2$
4. **答案：** $6\sin^2(2x)\cos(2x)$

**例 5：** $\frac{d}{dx} e^{\sqrt{x^2+1}}$

**思考过程：**
1. **外层：** $e^u$ → $e^u$
   - $e^{\sqrt{x^2+1}}$
2. **中间层：** $\sqrt{u} = u^{1/2}$ → $\frac{1}{2}u^{-1/2} = \frac{1}{2\sqrt{u}}$
   - $e^{\sqrt{x^2+1}} \cdot \frac{1}{2\sqrt{x^2+1}}$
3. **内层：** $x^2+1$ → $2x$
   - $e^{\sqrt{x^2+1}} \cdot \frac{1}{2\sqrt{x^2+1}} \cdot 2x$
4. **化简：** $\frac{xe^{\sqrt{x^2+1}}}{\sqrt{x^2+1}}$

### 3.3 Product Rule 乘法法则 - 完整流程

**公式：** $(fg)' = f'g + fg'$

**记忆：** 前导后不导 + 前不导后导

#### 标准例题

**例 1：** $\frac{d}{dx}(x^2 \sin x)$

**Step 1:** 标记 $f$ 和 $g$
- $f = x^2$, $g = \sin x$

**Step 2:** 求各自的导数
- $f' = 2x$, $g' = \cos x$

**Step 3:** 套公式
- $(x^2 \sin x)' = (2x)(\sin x) + (x^2)(\cos x)$

**Step 4:** 化简（如果需要）
- $= 2x\sin x + x^2\cos x$

**例 2：** $\frac{d}{dx}(xe^x)$

- $f = x$, $f' = 1$
- $g = e^x$, $g' = e^x$
- $(xe^x)' = (1)(e^x) + (x)(e^x) = e^x + xe^x = e^x(1+x)$

#### 三个函数相乘

**例 3：** $\frac{d}{dx}(x \sin x \cos x)$

**方法：** 先把两个看成一组

**Step 1:** 令 $f = x$, $g = \sin x \cos x$

**Step 2:** 先求 $g'$（用 product rule）
- $g' = (\sin x)' \cos x + \sin x (\cos x)'$
- $g' = \cos x \cos x + \sin x (-\sin x)$
- $g' = \cos^2 x - \sin^2 x$

**Step 3:** 套 product rule
- $(x \sin x \cos x)' = (1)(\sin x \cos x) + (x)(\cos^2 x - \sin^2 x)$
- $= \sin x \cos x + x(\cos^2 x - \sin^2 x)$

### 3.4 Quotient Rule 除法法则 - 避免符号错误

**公式：** $\left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2}$

**记忆口诀：** 下导上不导 - 上导下不导，全部除以下平方

**符号陷阱：** 中间是减号！

#### 标准例题

**例 1：** $\frac{d}{dx}\left(\frac{x^2}{e^x}\right)$

**Step 1:** 标记分子分母
- 分子 $f = x^2$, $f' = 2x$
- 分母 $g = e^x$, $g' = e^x$

**Step 2:** 套公式（注意符号）
$$\frac{(2x)(e^x) - (x^2)(e^x)}{(e^x)^2}$$

**Step 3:** 化简
$$= \frac{e^x(2x - x^2)}{e^{2x}} = \frac{2x - x^2}{e^x} = \frac{x(2-x)}{e^x}$$

**例 2：** $\frac{d}{dx}\left(\frac{\sin x}{1+\cos x}\right)$

- 分子：$f = \sin x$, $f' = \cos x$
- 分母：$g = 1+\cos x$, $g' = -\sin x$

$$\frac{(\cos x)(1+\cos x) - (\sin x)(-\sin x)}{(1+\cos x)^2}$$

$$= \frac{\cos x + \cos^2 x + \sin^2 x}{(1+\cos x)^2}$$

$$= \frac{\cos x + 1}{(1+\cos x)^2} = \frac{1}{1+\cos x}$$

### 3.5 Implicit Differentiation 隐函数求导 - 完整模板

**什么时候用？**
- $y$ 和 $x$ 混在一起，无法解出 $y = f(x)$
- 例如：$x^2 + y^2 = 25$, $x^3 + xy + y^3 = 1$

**核心规则：**
- 对 $x$ 求导时，$x$ 的项正常求导
- 对 $y$ 求导时，要乘 $\frac{dy}{dx}$（或写成 $y'$）

#### 完整例题

**例 1：** 求 $x^2 + y^2 = 25$ 在点 $(3, 4)$ 的切线方程

**Step 1:** 两边对 $x$ 求导
$$\frac{d}{dx}(x^2) + \frac{d}{dx}(y^2) = \frac{d}{dx}(25)$$

**Step 2:** 逐项求导（$y$ 的项用 chain rule）
- $\frac{d}{dx}(x^2) = 2x$
- $\frac{d}{dx}(y^2) = 2y \cdot \frac{dy}{dx}$（外层 $2y$，里面 $y$ 对 $x$ 的导数）
- $\frac{d}{dx}(25) = 0$

$$2x + 2y\frac{dy}{dx} = 0$$

**Step 3:** 解出 $\frac{dy}{dx}$
$$2y\frac{dy}{dx} = -2x$$
$$\frac{dy}{dx} = -\frac{x}{y}$$

**Step 4:** 代入点 $(3, 4)$ 求斜率
$$\frac{dy}{dx}\bigg|_{(3,4)} = -\frac{3}{4}$$

**Step 5:** 写切线方程 $y - y_1 = m(x - x_1)$
$$y - 4 = -\frac{3}{4}(x - 3)$$
$$y = -\frac{3}{4}x + \frac{9}{4} + 4 = -\frac{3}{4}x + \frac{25}{4}$$

**例 2：** 求 $x^3 + xy + y^3 = 3$ 的 $\frac{dy}{dx}$

**Step 1:** 两边对 $x$ 求导
$$\frac{d}{dx}(x^3) + \frac{d}{dx}(xy) + \frac{d}{dx}(y^3) = 0$$

**Step 2:** 逐项求导
- $\frac{d}{dx}(x^3) = 3x^2$
- $\frac{d}{dx}(xy)$ 用 product rule：$(1)(y) + (x)(y') = y + xy'$
- $\frac{d}{dx}(y^3) = 3y^2 y'$

$$3x^2 + y + xy' + 3y^2y' = 0$$

**Step 3:** 把含 $y'$ 的项放一边
$$xy' + 3y^2y' = -3x^2 - y$$

**Step 4:** 提取 $y'$
$$y'(x + 3y^2) = -3x^2 - y$$

**Step 5:** 解出 $y'$
$$y' = \frac{-3x^2 - y}{x + 3y^2}$$

---

## 第四部分：L'Hopital's Rule 洛必达法则

### 4.1 使用条件（必须检查！）

**只能用于以下两种情况：**
1. $\frac{0}{0}$ 型
2. $\frac{\infty}{\infty}$ 型

**不能用的情况：**
- $\frac{1}{0}$（这是无穷大，不是不定式）
- $\frac{0}{\infty}$（这等于 0）
- $\frac{\infty}{1}$（这是无穷大）

### 4.2 标准流程

**例 1：** $\lim_{x \to 0} \frac{\sin x}{x}$

**Step 1:** 代入检查类型
- 分子：$\sin 0 = 0$
- 分母：$0$
- 类型：$\frac{0}{0}$ ✓ 可以用

**Step 2:** 分子分母分别求导
$$\lim_{x \to 0} \frac{\sin x}{x} = \lim_{x \to 0} \frac{(\sin x)'}{(x)'} = \lim_{x \to 0} \frac{\cos x}{1}$$

**Step 3:** 代入
$$= \frac{\cos 0}{1} = 1$$

**例 2：** $\lim_{x \to \infty} \frac{e^x}{x^2}$

**Step 1:** 代入检查
- 分子：$e^\infty = \infty$
- 分母：$\infty^2 = \infty$
- 类型：$\frac{\infty}{\infty}$ ✓

**Step 2:** 第一次 L'Hopital
$$\lim_{x \to \infty} \frac{e^x}{x^2} = \lim_{x \to \infty} \frac{e^x}{2x}$$

**Step 3:** 还是 $\frac{\infty}{\infty}$，再用一次
$$= \lim_{x \to \infty} \frac{e^x}{2} = \infty$$

**例 3：** $\lim_{x \to 0} \frac{1 - \cos x}{x^2}$

**Step 1:** $\frac{0}{0}$ ✓

**Step 2:** 第一次
$$\lim_{x \to 0} \frac{\sin x}{2x}$$

**Step 3:** 还是 $\frac{0}{0}$，再用
$$\lim_{x \to 0} \frac{\cos x}{2} = \frac{1}{2}$$

### 4.3 其他不定式类型的转化

**$0 \cdot \infty$ 型 → 转化为 $\frac{0}{0}$ 或 $\frac{\infty}{\infty}$**

**例：** $\lim_{x \to 0^+} x \ln x$

- 这是 $0 \cdot (-\infty)$ 型
- 改写：$x \ln x = \frac{\ln x}{1/x}$（变成 $\frac{-\infty}{\infty}$）
- 用 L'Hopital：$\lim_{x \to 0^+} \frac{1/x}{-1/x^2} = \lim_{x \to 0^+} \frac{-x^2}{x} = \lim_{x \to 0^+} (-x) = 0$

**$\infty - \infty$ 型 → 通分**

**例：** $\lim_{x \to 0} \left(\frac{1}{x} - \frac{1}{\sin x}\right)$

- 通分：$\frac{\sin x - x}{x \sin x}$
- 这是 $\frac{0}{0}$ 型
- 用 L'Hopital：$\lim_{x \to 0} \frac{\cos x - 1}{(\sin x) + x\cos x}$
- 还是 $\frac{0}{0}$，再用：$\lim_{x \to 0} \frac{-\sin x}{2\cos x - x\sin x} = \frac{0}{2} = 0$

---

## 第五部分：Optimization 优化问题

### 5.1 完整解题模板（9步法）

**例题：** 要做一个无盖的长方体盒子，底面是正方形，体积为 32 立方米。求使表面积最小的盒子尺寸。

**Step 1: Define variables（定义变量）**
- 设底面边长为 $x$ 米
- 设高为 $h$ 米

**Step 2: Write target function（写目标函数）**
- 要最小化的是表面积
- 表面积 = 底面积 + 四个侧面积
- $S = x^2 + 4xh$（无盖，所以只有一个底面）

**Step 3: Write constraint（写约束条件）**
- 体积 = 32
- $V = x^2 h = 32$

**Step 4: Use constraint to reduce variables（用约束减少变量）**
- 从约束解出 $h$：$h = \frac{32}{x^2}$
- 代入目标函数：
$$S(x) = x^2 + 4x \cdot \frac{32}{x^2} = x^2 + \frac{128}{x}$$

**Step 5: Determine domain（确定定义域）**
- $x > 0$（边长必须为正）
- Domain: $(0, \infty)$

**Step 6: Differentiate（求导）**
$$S'(x) = 2x - \frac{128}{x^2}$$

**Step 7: Find critical points（求临界点）**
- 令 $S'(x) = 0$：
$$2x - \frac{128}{x^2} = 0$$
$$2x = \frac{128}{x^2}$$
$$2x^3 = 128$$
$$x^3 = 64$$
$$x = 4$$

**Step 8: Check endpoints and critical points（检查端点和临界点）**
- 端点：$x \to 0^+$ 时 $S \to \infty$；$x \to \infty$ 时 $S \to \infty$
- 临界点：$x = 4$
- 用二阶导数检验：
$$S''(x) = 2 + \frac{256}{x^3}$$
$$S''(4) = 2 + \frac{256}{64} = 2 + 4 = 6 > 0$$
- 所以 $x=4$ 是最小值点 ✓

**Step 9: Write final answer with units（写最终答案，带单位）**
- $x = 4$ 米
- $h = \frac{32}{16} = 2$ 米
- 最小表面积：$S = 16 + 32 = 48$ 平方米

**答案：底面边长 4 米，高 2 米，最小表面积 48 平方米。**

### 5.2 常见优化问题类型

#### 类型 1：几何问题（面积、体积、距离）

**例：** 用 100 米篱笆围一个矩形菜园，一边靠墙（不需要篱笆）。求最大面积。

**快速解法：**
- 设平行于墙的边长为 $x$，垂直于墙的边长为 $y$
- 约束：$x + 2y = 100$（只有三边需要篱笆）
- 目标：$A = xy$
- 消元：$y = \frac{100-x}{2}$，所以 $A(x) = x \cdot \frac{100-x}{2} = \frac{100x - x^2}{2}$
- 求导：$A'(x) = \frac{100 - 2x}{2} = 0$ → $x = 50$
- $y = 25$
- **答案：** $x = 50$ 米，$y = 25$ 米，最大面积 1250 平方米

#### 类型 2：距离最小化

**例：** 求点 $(1, 2)$ 到抛物线 $y = x^2$ 的最短距离。

**方法：** 最小化距离的平方（避免根号）

- 抛物线上的点：$(x, x^2)$
- 距离平方：$D^2 = (x-1)^2 + (x^2-2)^2$
- 令 $f(x) = (x-1)^2 + (x^2-2)^2$
- 展开：$f(x) = x^2 - 2x + 1 + x^4 - 4x^2 + 4 = x^4 - 3x^2 - 2x + 5$
- 求导：$f'(x) = 4x^3 - 6x - 2$
- 令 $f'(x) = 0$：$4x^3 - 6x - 2 = 0$ → $2x^3 - 3x - 1 = 0$
- 试根：$x = 1$ 时 $2 - 3 - 1 = -2 \neq 0$
- 试 $x = -0.5$：$2(-0.125) - 3(-0.5) - 1 = -0.25 + 1.5 - 1 = 0.25 \neq 0$
- （实际需要数值方法或图形计算器求解）

**简化方法：** 用几何直觉
- 最短距离是垂直于切线的
- 切线斜率 $= 2x$
- 从 $(1,2)$ 到 $(x, x^2)$ 的斜率 $= \frac{x^2-2}{x-1}$
- 垂直条件：$2x \cdot \frac{x^2-2}{x-1} = -1$

#### 类型 3：时间/成本优化

**例：** 一艘船在离海岸 6 公里的海上，要到海岸线上 10 公里外的城镇。船速 5 km/h，陆地速度 13 km/h。求最短时间路径。

**设置：**
- 设船在距离城镇 $x$ 公里处靠岸
- 海上距离：$\sqrt{36 + (10-x)^2}$
- 陆地距离：$x$
- 总时间：$T(x) = \frac{\sqrt{36 + (10-x)^2}}{5} + \frac{x}{13}$

**求导：**
$$T'(x) = \frac{1}{5} \cdot \frac{-(10-x)}{\sqrt{36+(10-x)^2}} + \frac{1}{13}$$

**令 $T'(x) = 0$：**
$$\frac{1}{13} = \frac{10-x}{5\sqrt{36+(10-x)^2}}$$
$$5\sqrt{36+(10-x)^2} = 13(10-x)$$
$$25[36+(10-x)^2] = 169(10-x)^2$$
$$900 + 25(10-x)^2 = 169(10-x)^2$$
$$900 = 144(10-x)^2$$
$$(10-x)^2 = 6.25$$
$$10-x = 2.5$$
$$x = 7.5$$

**答案：** 在距离城镇 7.5 公里处靠岸。

---

## 第六部分：Curve Sketching 曲线草图

### 6.1 完整 12 步流程

**例题：** 画出 $f(x) = \frac{x^2}{x^2-4}$ 的草图

**Step 1: Domain（定义域）**
- 分母 $x^2 - 4 \neq 0$
- $x \neq \pm 2$
- **Domain:** $(-\infty, -2) \cup (-2, 2) \cup (2, \infty)$

**Step 2: Intercepts（截距）**
- $y$-intercept: $f(0) = \frac{0}{-4} = 0$ → 点 $(0, 0)$
- $x$-intercept: $f(x) = 0$ → $x^2 = 0$ → $x = 0$ → 点 $(0, 0)$

**Step 3: Symmetry（对称性）**
- 检查 $f(-x)$：
$$f(-x) = \frac{(-x)^2}{(-x)^2-4} = \frac{x^2}{x^2-4} = f(x)$$
- **偶函数，关于 $y$ 轴对称**

**Step 4: Vertical asymptotes（垂直渐近线）**
- 分母为 0 的点：$x = \pm 2$
- 检查左右极限：
  - $\lim_{x \to 2^-} f(x) = \frac{4}{0^-} = -\infty$
  - $\lim_{x \to 2^+} f(x) = \frac{4}{0^+} = +\infty$
  - $\lim_{x \to -2^-} f(x) = +\infty$
  - $\lim_{x \to -2^+} f(x) = -\infty$
- **垂直渐近线：** $x = 2$ 和 $x = -2$

**Step 5: Horizontal asymptotes（水平渐近线）**
- $\lim_{x \to \infty} \frac{x^2}{x^2-4}$
- 分子分母同除 $x^2$：
$$\lim_{x \to \infty} \frac{1}{1 - 4/x^2} = \frac{1}{1-0} = 1$$
- **水平渐近线：** $y = 1$

**Step 6: First derivative（一阶导数）**
- 用 quotient rule：
$$f'(x) = \frac{(2x)(x^2-4) - (x^2)(2x)}{(x^2-4)^2}$$
$$= \frac{2x^3 - 8x - 2x^3}{(x^2-4)^2} = \frac{-8x}{(x^2-4)^2}$$

**Step 7: Critical points（临界点）**
- $f'(x) = 0$ → $-8x = 0$ → $x = 0$
- $f'(x)$ 不存在的点：$x = \pm 2$（但这些不在 domain 内）
- **临界点：** $x = 0$

**Step 8: Increasing/Decreasing intervals（增减区间）**
- 测试点：

| 区间 | 测试点 | $f'(x)$ 符号 | 结论 |
|------|--------|--------------|------|
| $(-\infty, -2)$ | $x = -3$ | $\frac{-8(-3)}{25} = \frac{24}{25} > 0$ | 递增 ↗ |
| $(-2, 0)$ | $x = -1$ | $\frac{-8(-1)}{9} = \frac{8}{9} > 0$ | 递增 ↗ |
| $(0, 2)$ | $x = 1$ | $\frac{-8(1)}{9} = -\frac{8}{9} < 0$ | 递减 ↘ |
| $(2, \infty)$ | $x = 3$ | $\frac{-8(3)}{25} = -\frac{24}{25} < 0$ | 递减 ↘ |

- **$x = 0$ 是局部最大值点**，$f(0) = 0$

**Step 9: Second derivative（二阶导数）**
$$f''(x) = \frac{d}{dx}\left[\frac{-8x}{(x^2-4)^2}\right]$$

用 quotient rule：
$$f''(x) = \frac{(-8)(x^2-4)^2 - (-8x) \cdot 2(x^2-4)(2x)}{(x^2-4)^4}$$
$$= \frac{-8(x^2-4) + 32x^2}{(x^2-4)^3} = \frac{-8x^2 + 32 + 32x^2}{(x^2-4)^3}$$
$$= \frac{24x^2 + 32}{(x^2-4)^3} = \frac{8(3x^2+4)}{(x^2-4)^3}$$

**Step 10: Concavity（凹凸性）**
- 分子 $8(3x^2+4) > 0$ 恒成立
- 符号由分母 $(x^2-4)^3$ 决定：

| 区间 | $(x^2-4)^3$ 符号 | $f''(x)$ 符号 | 凹凸性 |
|------|------------------|---------------|--------|
| $(-\infty, -2)$ | $+$ | $+$ | 凹向上 ∪ |
| $(-2, 2)$ | $-$ | $-$ | 凹向下 ∩ |
| $(2, \infty)$ | $+$ | $+$ | 凹向上 ∪ |

**Step 11: Inflection points（拐点）**
- $f''(x) = 0$ → $3x^2 + 4 = 0$ → 无实数解
- $f''(x)$ 不存在：$x = \pm 2$（不在 domain 内）
- **无拐点**

**Step 12: Sketch（画图）**

关键信息总结：
- 截距：$(0, 0)$
- 垂直渐近线：$x = -2, x = 2$
- 水平渐近线：$y = 1$
- 局部最大值：$(0, 0)$
- 对称性：关于 $y$ 轴对称
- 在 $(-\infty, -2)$ 和 $(-2, 0)$ 递增，凹向上和凹向下
- 在 $(0, 2)$ 和 $(2, \infty)$ 递减，凹向下和凹向上

### 6.2 快速判断表

| 条件 | 图像特征 |
|------|----------|
| $f'(x) > 0$ | 函数递增 ↗ |
| $f'(x) < 0$ | 函数递减 ↘ |
| $f'(c) = 0$ 且 $f''(c) > 0$ | 局部最小值 ∪ |
| $f'(c) = 0$ 且 $f''(c) < 0$ | 局部最大值 ∩ |
| $f''(x) > 0$ | 凹向上（笑脸）∪ |
| $f''(x) < 0$ | 凹向下（哭脸）∩ |
| $f''$ 变号 | 拐点（凹凸性改变）|

---

## 第七部分：Taylor Series 泰勒级数

### 7.1 Taylor Polynomial 泰勒多项式

**公式：** 在 $x = a$ 处展开到 $n$ 阶
$$T_n(x) = \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!}(x-a)^k$$

**展开式：**
$$T_n(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + \cdots$$

**Maclaurin series（$a=0$ 的特殊情况）：**
$$T_n(x) = f(0) + f'(0)x + \frac{f''(0)}{2!}x^2 + \frac{f'''(0)}{3!}x^3 + \cdots$$

### 7.2 必背的 Maclaurin Series

| 函数 | Maclaurin series | 收敛域 |
|------|------------------|--------|
| $e^x$ | $1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \frac{x^4}{4!} + \cdots$ | 所有 $x$ |
| $\sin x$ | $x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots$ | 所有 $x$ |
| $\cos x$ | $1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \cdots$ | 所有 $x$ |
| $\sinh x$ | $x + \frac{x^3}{3!} + \frac{x^5}{5!} + \frac{x^7}{7!} + \cdots$ | 所有 $x$ |
| $\cosh x$ | $1 + \frac{x^2}{2!} + \frac{x^4}{4!} + \frac{x^6}{6!} + \cdots$ | 所有 $x$ |
| $\ln(1+x)$ | $x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} + \cdots$ | $-1 < x \leq 1$ |
| $\frac{1}{1-x}$ | $1 + x + x^2 + x^3 + x^4 + \cdots$ | $\|x\| < 1$ |
| $(1+x)^p$ | $1 + px + \frac{p(p-1)}{2!}x^2 + \frac{p(p-1)(p-2)}{3!}x^3 + \cdots$ | $\|x\| < 1$ |

**记忆技巧：**
- $e^x$：所有项都是正的，分母是阶乘
- $\sin x$：只有奇数次幂，正负交替
- $\cos x$：只有偶数次幂，正负交替
- $\sinh x$：像 $\sin x$ 但全是正的
- $\cosh x$：像 $\cos x$ 但全是正的

### 7.3 从定义求 Taylor Polynomial - 完整例题

**例 1：** 求 $f(x) = e^{2x}$ 在 $x=0$ 处的 4 阶 Maclaurin polynomial

**Step 1:** 求各阶导数在 $x=0$ 的值

| 阶数 | 导数 | 在 $x=0$ 的值 |
|------|------|---------------|
| 0 | $f(x) = e^{2x}$ | $f(0) = 1$ |
| 1 | $f'(x) = 2e^{2x}$ | $f'(0) = 2$ |
| 2 | $f''(x) = 4e^{2x}$ | $f''(0) = 4$ |
| 3 | $f'''(x) = 8e^{2x}$ | $f'''(0) = 8$ |
| 4 | $f^{(4)}(x) = 16e^{2x}$ | $f^{(4)}(0) = 16$ |

**Step 2:** 代入公式
$$T_4(x) = 1 + \frac{2}{1!}x + \frac{4}{2!}x^2 + \frac{8}{3!}x^3 + \frac{16}{4!}x^4$$

**Step 3:** 化简
$$T_4(x) = 1 + 2x + 2x^2 + \frac{4}{3}x^3 + \frac{2}{3}x^4$$

**例 2：** 求 $f(x) = \sin(2x)$ 在 $x=0$ 处的 5 阶 Maclaurin polynomial

**Step 1:** 求导数（找规律）

| 阶数 | 导数 | 在 $x=0$ 的值 |
|------|------|---------------|
| 0 | $\sin(2x)$ | $0$ |
| 1 | $2\cos(2x)$ | $2$ |
| 2 | $-4\sin(2x)$ | $0$ |
| 3 | $-8\cos(2x)$ | $-8$ |
| 4 | $16\sin(2x)$ | $0$ |
| 5 | $32\cos(2x)$ | $32$ |

**Step 2:** 代入（偶数阶都是 0）
$$T_5(x) = 2x - \frac{8}{3!}x^3 + \frac{32}{5!}x^5$$

**Step 3:** 化简
$$T_5(x) = 2x - \frac{4}{3}x^3 + \frac{4}{15}x^5$$

### 7.4 用已知级数构造新级数

**技巧：替换、求导、积分**

**例 1：** 求 $e^{-x^2}$ 的 Maclaurin series

**方法：** 从 $e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots$ 出发

**Step 1:** 用 $-x^2$ 替换 $x$
$$e^{-x^2} = 1 + (-x^2) + \frac{(-x^2)^2}{2!} + \frac{(-x^2)^3}{3!} + \cdots$$

**Step 2:** 化简
$$= 1 - x^2 + \frac{x^4}{2!} - \frac{x^6}{3!} + \frac{x^8}{4!} - \cdots$$

**例 2：** 求 $\frac{1}{1+x^2}$ 的 Maclaurin series

**方法：** 从 $\frac{1}{1-x} = 1 + x + x^2 + x^3 + \cdots$ 出发

**Step 1:** 用 $-x^2$ 替换 $x$
$$\frac{1}{1-(-x^2)} = \frac{1}{1+x^2} = 1 + (-x^2) + (-x^2)^2 + (-x^2)^3 + \cdots$$

**Step 2:** 化简
$$= 1 - x^2 + x^4 - x^6 + x^8 - \cdots$$

**例 3：** 求 $\arctan x$ 的 Maclaurin series

**方法：** 利用 $\frac{d}{dx}(\arctan x) = \frac{1}{1+x^2}$

**Step 1:** 从例 2 知道
$$\frac{1}{1+x^2} = 1 - x^2 + x^4 - x^6 + \cdots$$

**Step 2:** 两边积分
$$\arctan x = \int (1 - x^2 + x^4 - x^6 + \cdots) dx$$
$$= x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \cdots$$

### 7.5 Lagrange Remainder 拉格朗日余项

**误差估计公式：**
$$R_n(x) = \frac{f^{(n+1)}(c)}{(n+1)!}(x-a)^{n+1}$$

其中 $c$ 在 $a$ 和 $x$ 之间。

**如何估计误差：**

**例：** 用 $T_3(x) = x - \frac{x^3}{6}$ 近似 $\sin(0.1)$，估计误差。

**Step 1:** 确定 $n$, $a$, $x$
- $n = 3$（用到 3 阶）
- $a = 0$（Maclaurin）
- $x = 0.1$

**Step 2:** 求 $f^{(4)}(x)$
- $f(x) = \sin x$
- $f^{(4)}(x) = \sin x$

**Step 3:** 找 $|f^{(4)}(c)|$ 的最大值（$c$ 在 0 和 0.1 之间）
- $|\sin c| \leq \sin(0.1) < 0.1$（实际上 $|\sin c| \leq 1$，但这里可以更精确）
- 保守估计：$|f^{(4)}(c)| \leq 1$

**Step 4:** 计算误差上界
$$|R_3(0.1)| \leq \frac{1}{4!} |0.1|^4 = \frac{0.0001}{24} \approx 0.0000042$$

**答案：** 误差小于 $4.2 \times 10^{-6}$

---
## 第八部分：Integration 积分

### 8.1 Fundamental Theorem of Calculus (FTC)

**Part 1：** 如果 $F'(x) = f(x)$，则
$$\int_a^b f(x) dx = F(b) - F(a)$$

**Part 2：** 
$$\frac{d}{dx}\left[\int_a^x f(t) dt\right] = f(x)$$

### 8.2 FTC with Variable Limits - 完整分类

**情况 1：上限是 $x$，下限是常数**

$$\frac{d}{dx}\left[\int_a^x f(t) dt\right] = f(x)$$

**例：** $\frac{d}{dx}\left[\int_0^x \sin(t^2) dt\right] = \sin(x^2)$

**情况 2：上限是 $g(x)$，下限是常数**

$$\frac{d}{dx}\left[\int_a^{g(x)} f(t) dt\right] = f(g(x)) \cdot g'(x)$$

**例：** $\frac{d}{dx}\left[\int_0^{x^2} \sin(t^2) dt\right]$

**Step 1:** 上限是 $x^2$，所以代入 $x^2$
$$= \sin((x^2)^2) \cdot \frac{d}{dx}(x^2)$$

**Step 2:** 化简
$$= \sin(x^4) \cdot 2x = 2x\sin(x^4)$$

**情况 3：上下限都是变量**

$$\frac{d}{dx}\left[\int_{a(x)}^{b(x)} f(t) dt\right] = f(b(x)) \cdot b'(x) - f(a(x)) \cdot a'(x)$$

**例：** $\frac{d}{dx}\left[\int_{\sin x}^{x^2} e^{t^2} dt\right]$

**Step 1:** 上限部分
$$f(x^2) \cdot (x^2)' = e^{(x^2)^2} \cdot 2x = 2xe^{x^4}$$

**Step 2:** 下限部分
$$f(\sin x) \cdot (\sin x)' = e^{(\sin x)^2} \cdot \cos x = \cos x \cdot e^{\sin^2 x}$$

**Step 3:** 相减
$$= 2xe^{x^4} - \cos x \cdot e^{\sin^2 x}$$

**情况 4：积分里面还有 $x$**

**例：** $\frac{d}{dx}\left[\int_0^x t^2 x dt\right]$

**注意：** 这里 $x$ 不是积分变量，可以提出来

**Step 1:** 提出 $x$
$$\frac{d}{dx}\left[x \int_0^x t^2 dt\right]$$


**Step 2:** 先算积分
$$\int_0^x t^2 dt = \left[\frac{t^3}{3}\right]_0^x = \frac{x^3}{3}$$

**Step 3:** 代入
$$\frac{d}{dx}\left[x \cdot \frac{x^3}{3}\right] = \frac{d}{dx}\left[\frac{x^4}{3}\right] = \frac{4x^3}{3}$$

**或者用 product rule：**
$$\frac{d}{dx}\left[x \int_0^x t^2 dt\right] = (1) \cdot \int_0^x t^2 dt + x \cdot \frac{d}{dx}\left[\int_0^x t^2 dt\right]$$
$$= \int_0^x t^2 dt + x \cdot x^2 = \frac{x^3}{3} + x^3 = \frac{4x^3}{3}$$

### 8.3 Integration by Substitution 换元积分法

**核心思想：** 找到 inside function 和它的导数

**识别模式：** 如果被积函数可以写成 $f(g(x)) \cdot g'(x)$ 的形式，就用 substitution

#### 不定积分 substitution 模板

**例 1：** $\int x \cos(x^2) dx$

**Step 1:** 识别 inside function
- 看到 $\cos(x^2)$，里面是 $x^2$
- 令 $u = x^2$

**Step 2:** 求 $du$
$$du = 2x dx \quad \Rightarrow \quad x dx = \frac{1}{2}du$$

**Step 3:** 替换
$$\int x \cos(x^2) dx = \int \cos(u) \cdot \frac{1}{2} du = \frac{1}{2}\int \cos(u) du$$

**Step 4:** 积分
$$= \frac{1}{2}\sin(u) + C$$

**Step 5:** 换回 $x$
$$= \frac{1}{2}\sin(x^2) + C$$

**例 2：** $\int \frac{x^2}{\sqrt{x^3+1}} dx$

**Step 1:** 令 $u = x^3 + 1$

**Step 2:** $du = 3x^2 dx$ → $x^2 dx = \frac{1}{3}du$

**Step 3:** 替换
$$\int \frac{x^2}{\sqrt{x^3+1}} dx = \int \frac{1}{\sqrt{u}} \cdot \frac{1}{3} du = \frac{1}{3}\int u^{-1/2} du$$

**Step 4:** 积分
$$= \frac{1}{3} \cdot \frac{u^{1/2}}{1/2} + C = \frac{2}{3}u^{1/2} + C$$

**Step 5:** 换回
$$= \frac{2}{3}\sqrt{x^3+1} + C$$

#### 定积分 substitution 模板（改变上下限）

**例 3：** $\int_0^1 x e^{x^2} dx$

**Step 1:** 令 $u = x^2$，$du = 2x dx$

**Step 2:** 改变上下限
- 当 $x = 0$ 时，$u = 0^2 = 0$
- 当 $x = 1$ 时，$u = 1^2 = 1$

**Step 3:** 替换（包括上下限）
$$\int_0^1 x e^{x^2} dx = \int_0^1 e^u \cdot \frac{1}{2} du = \frac{1}{2}\int_0^1 e^u du$$

**Step 4:** 积分并代入上下限
$$= \frac{1}{2}[e^u]_0^1 = \frac{1}{2}(e^1 - e^0) = \frac{1}{2}(e - 1)$$

**注意：** 定积分换元后，直接用新的上下限，不需要换回 $x$

**例 4：** $\int_0^{\pi/2} \sin x \cos^7 x dx$

**Step 1:** 令 $u = \cos x$，$du = -\sin x dx$

**Step 2:** 改变上下限
- 当 $x = 0$ 时，$u = \cos 0 = 1$
- 当 $x = \pi/2$ 时，$u = \cos(\pi/2) = 0$

**Step 3:** 替换（注意负号和上下限交换）
$$\int_0^{\pi/2} \sin x \cos^7 x dx = \int_1^0 u^7 (-du) = -\int_1^0 u^7 du = \int_0^1 u^7 du$$

**Step 4:** 积分
$$= \left[\frac{u^8}{8}\right]_0^1 = \frac{1}{8} - 0 = \frac{1}{8}$$

### 8.4 常见 substitution 模式识别表

| 被积函数特征 | 令 $u =$ | 例子 |
|-------------|----------|------|
| $f(ax+b)$ | $ax+b$ | $\int \sin(3x+2) dx$ → $u = 3x+2$ |
| $x^n f(x^{n+1})$ | $x^{n+1}$ | $\int x^2 e^{x^3} dx$ → $u = x^3$ |
| $\frac{f'(x)}{f(x)}$ | $f(x)$ | $\int \frac{2x}{x^2+1} dx$ → $u = x^2+1$ |
| $f'(x) \cdot [f(x)]^n$ | $f(x)$ | $\int 2x(x^2+1)^5 dx$ → $u = x^2+1$ |
| $\tan x$ 或 $\sec^2 x$ | $\tan x$ 或 $\cos x$ | $\int \tan x \sec^2 x dx$ → $u = \tan x$ |
| $\sin x \cos^n x$ | $\cos x$ | $\int \sin x \cos^3 x dx$ → $u = \cos x$ |
| $\cos x \sin^n x$ | $\sin x$ | $\int \cos x \sin^5 x dx$ → $u = \sin x$ |
| $e^x f(e^x)$ | $e^x$ | $\int e^x \sin(e^x) dx$ → $u = e^x$ |
| $\frac{1}{x} f(\ln x)$ | $\ln x$ | $\int \frac{(\ln x)^2}{x} dx$ → $u = \ln x$ |

### 8.5 Substitution 常见错误

**错误 1：忘记调整 $dx$**

❌ **错误：** $\int x \cos(x^2) dx$，令 $u = x^2$，得 $\int x \cos(u) dx$

✓ **正确：** $du = 2x dx$，所以 $x dx = \frac{1}{2}du$，得 $\int \cos(u) \cdot \frac{1}{2} du$

**错误 2：定积分换元后忘记改上下限**

❌ **错误：** $\int_0^1 x e^{x^2} dx$，令 $u = x^2$，得 $\frac{1}{2}\int_0^1 e^u du$

✓ **正确：** 上下限也要换：$x=0 \to u=0$，$x=1 \to u=1$，所以是 $\frac{1}{2}\int_0^1 e^u du$（这个例子碰巧上下限一样，但必须检查）

**错误 3：$du$ 和被积函数不匹配**

❌ **错误：** $\int x^2 e^{x^3} dx$，令 $u = x^3$，$du = 3x^2 dx$，得 $\int e^u du$（漏了系数）

✓ **正确：** $x^2 dx = \frac{1}{3}du$，所以是 $\frac{1}{3}\int e^u du$

---

## 第九部分：Riemann Sums 黎曼和

### 9.1 基本概念

**定义：** 用矩形面积之和近似曲线下面积

$$\Delta x = \frac{b-a}{n}$$

**Left Riemann Sum（左端点）：**
$$L_n = \sum_{i=0}^{n-1} f(x_i) \Delta x = \Delta x [f(x_0) + f(x_1) + \cdots + f(x_{n-1})]$$

**Right Riemann Sum（右端点）：**
$$R_n = \sum_{i=1}^{n} f(x_i) \Delta x = \Delta x [f(x_1) + f(x_2) + \cdots + f(x_n)]$$

**Midpoint Riemann Sum（中点）：**
$$M_n = \sum_{i=1}^{n} f\left(\frac{x_{i-1}+x_i}{2}\right) \Delta x$$

### 9.2 单调函数的上下界

| 函数性质 | Lower sum（下和） | Upper sum（上和） |
|----------|-------------------|-------------------|
| 递增函数 | Left endpoints | Right endpoints |
| 递减函数 | Right endpoints | Left endpoints |

**记忆方法：**
- 递增函数：左边低，右边高 → 左端点是下界
- 递减函数：左边高，右边低 → 右端点是下界

### 9.3 完整例题

**例：** 用 $n=4$ 个矩形估计 $\int_0^2 x^2 dx$，分别用左端点、右端点和中点。

**Step 1:** 计算 $\Delta x$
$$\Delta x = \frac{2-0}{4} = 0.5$$

**Step 2:** 确定分点
$$x_0 = 0, \quad x_1 = 0.5, \quad x_2 = 1, \quad x_3 = 1.5, \quad x_4 = 2$$

**Step 3:** 计算函数值

| $i$ | $x_i$ | $f(x_i) = x_i^2$ |
|-----|-------|------------------|
| 0 | 0 | 0 |
| 1 | 0.5 | 0.25 |
| 2 | 1 | 1 |
| 3 | 1.5 | 2.25 |
| 4 | 2 | 4 |

**Step 4:** Left Riemann Sum
$$L_4 = 0.5[f(0) + f(0.5) + f(1) + f(1.5)]$$
$$= 0.5[0 + 0.25 + 1 + 2.25] = 0.5 \times 3.5 = 1.75$$

**Step 5:** Right Riemann Sum
$$R_4 = 0.5[f(0.5) + f(1) + f(1.5) + f(2)]$$
$$= 0.5[0.25 + 1 + 2.25 + 4] = 0.5 \times 7.5 = 3.75$$

**Step 6:** Midpoint Riemann Sum
- 中点：$0.25, 0.75, 1.25, 1.75$
$$M_4 = 0.5[f(0.25) + f(0.75) + f(1.25) + f(1.75)]$$
$$= 0.5[0.0625 + 0.5625 + 1.5625 + 3.0625]$$
$$= 0.5 \times 5.25 = 2.625$$

**Step 7:** 比较精确值
$$\int_0^2 x^2 dx = \left[\frac{x^3}{3}\right]_0^2 = \frac{8}{3} \approx 2.667$$

**分析：**
- $f(x) = x^2$ 是递增函数，所以 $L_4 < \text{真实值} < R_4$ ✓
- $1.75 < 2.667 < 3.75$ ✓
- 中点法 $M_4 = 2.625$ 最接近真实值

---

## 第十部分：常见错误诊断清单

### 10.1 Domain 相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| 根号忘记 $\geq 0$ | $\sqrt{x-5}$ 的 domain 是 $x > 5$ | 应该是 $x \geq 5$ |
| 对数写成 $\geq 0$ | $\ln(x+1)$ 要求 $x+1 \geq 0$ | 应该是 $x+1 > 0$（严格大于）|
| 复合函数只看外层 | $\ln(\sqrt{x-1})$ 只要求 $x > 1$ | 要先 $x \geq 1$（根号），再 $x > 1$（对数）|
| 分式不等式符号错误 | $\frac{x-1}{x+2} > 0$ 直接得 $x > 1$ | 要分情况：同号分析 |

### 10.2 求导相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| Chain rule 漏乘内层导数 | $\frac{d}{dx}\sin(x^2) = \cos(x^2)$ | 应该是 $2x\cos(x^2)$ |
| Product rule 符号错误 | $(fg)' = f'g' + fg$ | 应该是 $f'g + fg'$ |
| Quotient rule 符号错误 | $\left(\frac{f}{g}\right)' = \frac{f'g + fg'}{g^2}$ | 中间是减号：$\frac{f'g - fg'}{g^2}$ |
| 隐函数求导忘记 $y'$ | $\frac{d}{dx}(y^2) = 2y$ | 应该是 $2y \cdot y'$ |
| 常数的导数 | $\frac{d}{dx}(5) = 5$ | 常数导数是 0 |

### 10.3 L'Hopital 相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| 不检查类型就用 | $\lim_{x \to 0} \frac{x+1}{x}$ 用 L'Hopital | 这是 $\frac{1}{0}$，不能用 |
| 整体求导 | $\lim \frac{f(x)}{g(x)}$ 变成 $\lim \frac{[f(x)/g(x)]'}{1}$ | 应该分子分母分别求导 |
| 一次不够就放弃 | $\lim_{x \to 0} \frac{1-\cos x}{x^2}$ 用一次还是 $\frac{0}{0}$ | 可以继续用第二次 |

### 10.4 Optimization 相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| 忘记检查端点 | 只检查 $f'(x)=0$ 的点 | 闭区间必须检查端点 |
| 没有确定 domain | 直接求导解方程 | 先确定变量的合理范围 |
| 忘记写单位 | 答案：$x = 5$ | 答案：$x = 5$ 米 |
| 没有验证是最大还是最小 | 找到临界点就结束 | 用二阶导数或比较函数值 |

### 10.5 Taylor Series 相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| 阶乘位置错误 | $T_n(x) = \sum \frac{f^{(k)}(a) (x-a)^k}{k!}$ | 阶乘在分母：$\frac{f^{(k)}(a)}{k!}(x-a)^k$ |
| $\sin$ 和 $\cos$ 混淆 | $\sin x = 1 - \frac{x^2}{2!} + \cdots$ | $\sin x$ 只有奇数次幂 |
| 替换时符号错误 | $e^{-x}$ 用 $e^x$ 替换，忘记负号 | 每一项都要带负号 |
| 收敛域不写 | $\ln(1+x) = x - \frac{x^2}{2} + \cdots$ | 要注明 $-1 < x \leq 1$ |

### 10.6 Integration 相关错误

| 错误类型 | 错误示例 | 正确做法 |
|----------|----------|----------|
| Substitution 忘记调整 $dx$ | 令 $u=x^2$，$\int x\cos(x^2)dx = \int x\cos(u)dx$ | $du=2xdx$，要写成 $\int \cos(u) \frac{1}{2}du$ |
| 定积分换元不改上下限 | 换元后还用原来的 $x$ 的上下限 | 必须把上下限也换成 $u$ 的 |
| FTC 上下限搞反 | $\int_a^b f(x)dx = F(a) - F(b)$ | 应该是 $F(b) - F(a)$ |
| 不定积分忘记 $+C$ | $\int x dx = \frac{x^2}{2}$ | 应该是 $\frac{x^2}{2} + C$ |

---

## 第十一部分：考前速查公式表

### 11.1 基础导数

$$\begin{align}
\frac{d}{dx}(x^n) &= nx^{n-1} \\
\frac{d}{dx}(e^x) &= e^x \\
\frac{d}{dx}(\ln x) &= \frac{1}{x} \\
\frac{d}{dx}(\sin x) &= \cos x \\
\frac{d}{dx}(\cos x) &= -\sin x \\
\frac{d}{dx}(\tan x) &= \sec^2 x \\
\frac{d}{dx}(\sinh x) &= \cosh x \\
\frac{d}{dx}(\cosh x) &= \sinh x
\end{align}$$

### 11.2 求导法则

$$\begin{align}
(f+g)' &= f' + g' \\
(cf)' &= cf' \\
(fg)' &= f'g + fg' \\
\left(\frac{f}{g}\right)' &= \frac{f'g - fg'}{g^2} \\
(f \circ g)' &= f'(g(x)) \cdot g'(x)
\end{align}$$

### 11.3 积分公式

$$\begin{align}
\int x^n dx &= \frac{x^{n+1}}{n+1} + C \quad (n \neq -1) \\
\int \frac{1}{x} dx &= \ln|x| + C \\
\int e^x dx &= e^x + C \\
\int \sin x dx &= -\cos x + C \\
\int \cos x dx &= \sin x + C \\
\int \sec^2 x dx &= \tan x + C \\
\int \frac{1}{1+x^2} dx &= \arctan x + C \\
\int \frac{1}{\sqrt{1-x^2}} dx &= \arcsin x + C
\end{align}$$

### 11.4 Taylor Series（Maclaurin）

$$\begin{align}
e^x &= \sum_{n=0}^{\infty} \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots \\
\sin x &= \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n+1}}{(2n+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots \\
\cos x &= \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n}}{(2n)!} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots \\
\frac{1}{1-x} &= \sum_{n=0}^{\infty} x^n = 1 + x + x^2 + x^3 + \cdots \quad (|x|<1) \\
\ln(1+x) &= \sum_{n=1}^{\infty} \frac{(-1)^{n+1} x^n}{n} = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots \quad (-1<x \leq 1)
\end{align}$$

---

## 第十二部分：题型快速识别训练

### 12.1 看到题目第一眼应该想到什么

**练习：快速判断下列题目用什么方法**

1. 求 $f(x) = \frac{x+1}{x^2-4}$ 的 domain
   - **答案：** 分母不为 0 → $x \neq \pm 2$

2. 求 $\lim_{x \to 0} \frac{\sin(3x)}{x}$
   - **答案：** $\frac{0}{0}$ 型 → L'Hopital 或用 $\lim_{x \to 0} \frac{\sin x}{x} = 1$

3. 求 $\frac{d}{dx}[\sin(x^2)]$
   - **答案：** 复合函数 → Chain rule → $2x\cos(x^2)$

4. 求 $x^2 + xy + y^2 = 3$ 的 $\frac{dy}{dx}$
   - **答案：** 隐函数 → Implicit differentiation

5. 求 $\frac{d}{dx}\left[\int_0^{x^2} \sin(t) dt\right]$
   - **答案：** FTC + Chain rule → $\sin(x^2) \cdot 2x$

6. 求 $\int x e^{x^2} dx$
   - **答案：** Substitution，$u = x^2$

7. 用 100 米篱笆围最大矩形面积
   - **答案：** Optimization 问题

8. 画 $f(x) = \frac{x^2}{x-1}$ 的图
   - **答案：** Curve sketching（domain, asymptotes, $f'$, $f''$）

9. 求 $e^{-x^2}$ 的 Maclaurin series
   - **答案：** 用 $e^x$ 的级数，替换 $x \to -x^2$

10. 判断 $f(x) = \begin{cases} x^2 & x < 1 \\ 2x-1 & x \geq 1 \end{cases}$ 在 $x=1$ 是否连续
    - **答案：** 检查左极限、右极限、函数值是否相等

### 12.2 多步骤问题的思路链

**例：** 求曲线 $y = x^3 - 3x + 2$ 在 $x=1$ 处的切线方程，并求该切线与曲线的其他交点。

**思路链：**
1. 求切线 → 需要点和斜率
2. 点：$f(1) = 1 - 3 + 2 = 0$ → $(1, 0)$
3. 斜率：$f'(x) = 3x^2 - 3$ → $f'(1) = 0$
4. 切线方程：$y - 0 = 0(x-1)$ → $y = 0$
5. 交点：解 $x^3 - 3x + 2 = 0$
6. 因式分解：$(x-1)^2(x+2) = 0$
7. 其他交点：$x = -2$ → $(-2, 0)$

---

## 第十三部分：考试策略

### 13.1 时间分配建议

假设考试 2 小时，题目分布：

| 题型 | 建议时间 | 策略 |
|------|----------|------|
| 选择题/填空题 | 30-40 分钟 | 快速判断，不会的先跳过 |
| 求导/积分计算 | 20-30 分钟 | 步骤清晰，检查符号 |
| 应用题（optimization, curve sketching） | 30-40 分钟 | 画图辅助，写清楚变量定义 |
| Taylor series / FTC | 20-30 分钟 | 公式要准确，展开要完整 |
| 检查 | 10-15 分钟 | 重点检查计算和符号 |

### 13.2 答题顺序建议

1. **先做会做的**：快速浏览全卷，标记难度
2. **先易后难**：从最有把握的开始
3. **计算题写步骤**：即使答案不对，步骤分也很重要
4. **不要在一道题上卡太久**：超过 10 分钟没思路就跳过

### 13.3 检查重点

**高频错误检查清单：**
- [ ] Chain rule 有没有乘内层导数？
- [ ] Product rule 和 Quotient rule 的符号对不对？
- [ ] 隐函数求导有没有漏 $y'$ 或 $\frac{dy}{dx}$？
- [ ] Substitution 有没有调整 $dx$？
- [ ] 定积分换元有没有改上下限？
- [ ] L'Hopital 用之前检查过类型了吗？
- [ ] Optimization 有没有检查端点？
- [ ] Domain 的不等号是 $>$ 还是 $\geq$？
- [ ] 不定积分有没有写 $+C$？
- [ ] 最终答案有没有化简？有没有单位？

### 13.4 遇到不会的题怎么办

**策略 1：部分分数法**
- 即使不会做完，也要写出你知道的步骤
- 例如：Optimization 问题
  - 至少写出变量定义
  - 至少写出目标函数
  - 至少写出约束条件
  - 即使求不出答案，这些步骤也有分

**策略 2：特殊值检验法**
- 选择题可以代入特殊值排除错误选项
- 例如：$x=0, x=1, x=-1$ 通常是好的测试点

**策略 3：图像辅助法**
- 不确定的时候画个草图
- 特别是 curve sketching、optimization、极限问题

**策略 4：公式反推法**
- 忘记公式时，从简单情况推导
- 例如：忘记 $\int \sec^2 x dx$
  - 想：什么函数的导数是 $\sec^2 x$？
  - 回忆：$(\tan x)' = \sec^2 x$
  - 所以：$\int \sec^2 x dx = \tan x + C$

---

## 第十四部分：综合练习题（带完整解答）

### 练习 1：Domain 综合

**题目：** 求 $f(x) = \frac{\sqrt{4-x^2}}{\ln(x+3)}$ 的 domain

**完整解答：**

**Step 1:** 根号要求
$$4 - x^2 \geq 0$$
$$x^2 \leq 4$$
$$-2 \leq x \leq 2$$

**Step 2:** 对数要求
$$x + 3 > 0$$
$$x > -3$$

**Step 3:** 分母不为 0
$$\ln(x+3) \neq 0$$
$$x + 3 \neq 1$$
$$x \neq -2$$

**Step 4:** 取交集
- 从 Step 1：$[-2, 2]$
- 从 Step 2：$(-3, \infty)$
- 从 Step 3：$x \neq -2$
- 交集：$(-2, 2]$

**答案：** $(-2, 2]$

---

### 练习 2：Implicit Differentiation 综合

**题目：** 求 $e^{xy} + x^2y = 2$ 的 $\frac{dy}{dx}$

**完整解答：**

**Step 1:** 两边对 $x$ 求导
$$\frac{d}{dx}(e^{xy}) + \frac{d}{dx}(x^2y) = \frac{d}{dx}(2)$$

**Step 2:** 第一项用 chain rule
- 外层：$e^u$ → $e^u$
- 内层：$xy$ → 用 product rule → $y + xy'$
$$\frac{d}{dx}(e^{xy}) = e^{xy}(y + xy')$$

**Step 3:** 第二项用 product rule
$$\frac{d}{dx}(x^2y) = 2xy + x^2y'$$

**Step 4:** 右边
$$\frac{d}{dx}(2) = 0$$

**Step 5:** 合并
$$e^{xy}(y + xy') + 2xy + x^2y' = 0$$

**Step 6:** 展开
$$ye^{xy} + xye^{xy} + 2xy + x^2y' = 0$$

**Step 7:** 把含 $y'$ 的项移到左边
$$xy'e^{xy} + x^2y' = -ye^{xy} - 2xy$$

**Step 8:** 提取 $y'$
$$y'(xe^{xy} + x^2) = -ye^{xy} - 2xy$$

**Step 9:** 解出 $y'$
$$y' = \frac{-ye^{xy} - 2xy}{xe^{xy} + x^2} = \frac{-y(e^{xy} + 2x)}{x(e^{xy} + x)}$$

**答案：** $\frac{dy}{dx} = \frac{-y(e^{xy} + 2x)}{x(e^{xy} + x)}$

---

### 练习 3：L'Hopital 综合

**题目：** 求 $\lim_{x \to 0} \frac{e^x - 1 - x}{x^2}$

**完整解答：**

**Step 1:** 检查类型
- 分子：$e^0 - 1 - 0 = 0$
- 分母：$0$
- 类型：$\frac{0}{0}$ ✓ 可以用 L'Hopital

**Step 2:** 第一次 L'Hopital
$$\lim_{x \to 0} \frac{e^x - 1 - x}{x^2} = \lim_{x \to 0} \frac{e^x - 1}{2x}$$

**Step 3:** 检查类型
- 分子：$e^0 - 1 = 0$
- 分母：$0$
- 还是 $\frac{0}{0}$，继续用

**Step 4:** 第二次 L'Hopital
$$\lim_{x \to 0} \frac{e^x - 1}{2x} = \lim_{x \to 0} \frac{e^x}{2}$$

**Step 5:** 代入
$$= \frac{e^0}{2} = \frac{1}{2}$$

**答案：** $\frac{1}{2}$

---

### 练习 4：Optimization 综合

**题目：** 一个圆柱形罐子（有盖），体积为 $1000\pi$ 立方厘米。求使表面积最小的半径和高。

**完整解答：**

**Step 1:** 定义变量
- 设半径为 $r$ cm
- 设高为 $h$ cm

**Step 2:** 写目标函数（表面积）
- 两个圆形底面：$2\pi r^2$
- 侧面：$2\pi rh$
- 总表面积：$S = 2\pi r^2 + 2\pi rh$

**Step 3:** 写约束条件（体积）
$$V = \pi r^2 h = 1000\pi$$

**Step 4:** 用约束消元
$$h = \frac{1000\pi}{\pi r^2} = \frac{1000}{r^2}$$

**Step 5:** 代入目标函数
$$S(r) = 2\pi r^2 + 2\pi r \cdot \frac{1000}{r^2} = 2\pi r^2 + \frac{2000\pi}{r}$$

**Step 6:** 确定 domain
$$r > 0$$

**Step 7:** 求导
$$S'(r) = 4\pi r - \frac{2000\pi}{r^2}$$

**Step 8:** 求临界点
$$4\pi r - \frac{2000\pi}{r^2} = 0$$
$$4\pi r = \frac{2000\pi}{r^2}$$
$$4r^3 = 2000$$
$$r^3 = 500$$
$$r = \sqrt[3]{500} = 5\sqrt[3]{4} \approx 7.94 \text{ cm}$$

**Step 9:** 验证是最小值（二阶导数）
$$S''(r) = 4\pi + \frac{4000\pi}{r^3}$$
$$S''(5\sqrt[3]{4}) = 4\pi + \frac{4000\pi}{500} = 4\pi + 8\pi = 12\pi > 0$$
所以是最小值 ✓

**Step 10:** 求对应的 $h$
$$h = \frac{1000}{r^2} = \frac{1000}{(5\sqrt[3]{4})^2} = \frac{1000}{25\sqrt[3]{16}} = \frac{40}{\sqrt[3]{16}} = 10\sqrt[3]{4} \approx 15.87 \text{ cm}$$

**Step 11:** 观察关系
$$h = 10\sqrt[3]{4} = 2 \times 5\sqrt[3]{4} = 2r$$

**答案：** 
- 半径 $r = 5\sqrt[3]{4} \approx 7.94$ cm
- 高 $h = 10\sqrt[3]{4} \approx 15.87$ cm
- 关系：$h = 2r$（高是直径）

---

### 练习 5：FTC 综合

**题目：** 求 $\frac{d}{dx}\left[\int_{\sin x}^{x^3} e^{t^2} dt\right]$

**完整解答：**

**Step 1:** 识别类型
- 上下限都是变量 → 用公式
$$\frac{d}{dx}\left[\int_{a(x)}^{b(x)} f(t) dt\right] = f(b(x)) \cdot b'(x) - f(a(x)) \cdot a'(x)$$

**Step 2:** 确定各部分
- $f(t) = e^{t^2}$
- $b(x) = x^3$，$b'(x) = 3x^2$
- $a(x) = \sin x$，$a'(x) = \cos x$

**Step 3:** 上限部分
$$f(b(x)) \cdot b'(x) = e^{(x^3)^2} \cdot 3x^2 = 3x^2 e^{x^6}$$

**Step 4:** 下限部分
$$f(a(x)) \cdot a'(x) = e^{(\sin x)^2} \cdot \cos x = \cos x \cdot e^{\sin^2 x}$$

**Step 5:** 相减
$$\frac{d}{dx}\left[\int_{\sin x}^{x^3} e^{t^2} dt\right] = 3x^2 e^{x^6} - \cos x \cdot e^{\sin^2 x}$$

**答案：** $3x^2 e^{x^6} - \cos x \cdot e^{\sin^2 x}$

---

### 练习 6：Taylor Series 综合

**题目：** 求 $f(x) = x\cos(x^2)$ 在 $x=0$ 处的 5 阶 Maclaurin polynomial

**完整解答：**

**方法 1：从定义求导**

**Step 1:** 求各阶导数

| 阶数 | 导数 | 在 $x=0$ 的值 |
|------|------|---------------|
| 0 | $x\cos(x^2)$ | $0$ |
| 1 | $\cos(x^2) + x(-\sin(x^2))(2x) = \cos(x^2) - 2x^2\sin(x^2)$ | $1$ |
| 2 | $-2x\sin(x^2) - [4x\sin(x^2) + 2x^2\cos(x^2)(2x)]$ | $0$ |
| 3 | （计算复杂）| $-4$ |
| 4 | （计算复杂）| $0$ |
| 5 | （计算复杂）| $16$ |

这个方法太复杂了！

**方法 2：用已知级数（推荐）**

**Step 1:** 回忆 $\cos u$ 的级数
$$\cos u = 1 - \frac{u^2}{2!} + \frac{u^4}{4!} - \frac{u^6}{6!} + \cdots$$

**Step 2:** 用 $u = x^2$ 替换
$$\cos(x^2) = 1 - \frac{(x^2)^2}{2!} + \frac{(x^2)^4}{4!} - \cdots = 1 - \frac{x^4}{2} + \frac{x^8}{24} - \cdots$$

**Step 3:** 乘以 $x$
$$x\cos(x^2) = x\left(1 - \frac{x^4}{2} + \frac{x^8}{24} - \cdots\right)$$
$$= x - \frac{x^5}{2} + \frac{x^9}{24} - \cdots$$

**Step 4:** 取到 5 阶
$$T_5(x) = x - \frac{x^5}{2}$$

**答案：** $T_5(x) = x - \frac{x^5}{2}$

---

### 练习 7：Curve Sketching 综合

**题目：** 画出 $f(x) = xe^{-x}$ 的草图

**完整解答：**

**Step 1:** Domain
- 没有限制
- **Domain:** $(-\infty, \infty)$

**Step 2:** Intercepts
- $y$-intercept: $f(0) = 0$
- $x$-intercept: $xe^{-x} = 0$ → $x = 0$
- **截距：** $(0, 0)$

**Step 3:** Asymptotes
- 垂直渐近线：无（函数处处有定义）
- 水平渐近线：
  - $\lim_{x \to \infty} xe^{-x} = \lim_{x \to \infty} \frac{x}{e^x} \stackrel{L'H}{=} \lim_{x \to \infty} \frac{1}{e^x} = 0$
  - $\lim_{x \to -\infty} xe^{-x} = \lim_{x \to -\infty} \frac{x}{e^x} = -\infty \cdot 0 = -\infty$
- **水平渐近线：** $y = 0$（当 $x \to \infty$）

**Step 4:** First derivative
$$f'(x) = (1)(e^{-x}) + (x)(-e^{-x}) = e^{-x}(1-x)$$

**Step 5:** Critical points
$$f'(x) = 0$$
$$e^{-x}(1-x) = 0$$
$$1 - x = 0$$（因为 $e^{-x} \neq 0$）
$$x = 1$$

**Step 6:** Increasing/Decreasing

| 区间 | 测试点 | $f'(x)$ 符号 | 结论 |
|------|--------|--------------|------|
| $(-\infty, 1)$ | $x=0$ | $e^0(1-0) = 1 > 0$ | 递增 ↗ |
| $(1, \infty)$ | $x=2$ | $e^{-2}(1-2) < 0$ | 递减 ↘ |

- **$x=1$ 是局部最大值**
- $f(1) = 1 \cdot e^{-1} = \frac{1}{e} \approx 0.368$

**Step 7:** Second derivative
$$f''(x) = \frac{d}{dx}[e^{-x}(1-x)]$$
$$= (-e^{-x})(1-x) + e^{-x}(-1)$$
$$= e^{-x}[-(1-x) - 1]$$
$$= e^{-x}(-1+x-1)$$
$$= e^{-x}(x-2)$$

**Step 8:** Inflection points
$$f''(x) = 0$$
$$e^{-x}(x-2) = 0$$
$$x = 2$$

**Step 9:** Concavity

| 区间 | 测试点 | $f''(x)$ 符号 | 凹凸性 |
|------|--------|---------------|--------|
| $(-\infty, 2)$ | $x=0$ | $e^0(0-2) = -2 < 0$ | 凹向下 ∩ |
| $(2, \infty)$ | $x=3$ | $e^{-3}(3-2) > 0$ | 凹向上 ∪ |

- **拐点：** $x=2$，$f(2) = 2e^{-2} \approx 0.271$

**Step 10:** 关键信息总结
- 截距：$(0, 0)$
- 局部最大值：$(1, 1/e)$
- 拐点：$(2, 2/e^2)$
- 水平渐近线：$y=0$（右侧）
- $(-\infty, 1)$ 递增凹向下
- $(1, 2)$ 递减凹向下
- $(2, \infty)$ 递减凹向上

**草图特征：**
- 从左下方上升
- 在 $(1, 1/e)$ 达到最高点
- 然后下降
- 在 $(2, 2/e^2)$ 改变凹凸性
- 最后趋近于 $x$ 轴

---

### 练习 8：Integration 综合

**题目：** 求 $\int_0^{\pi/4} \tan x \sec^2 x dx$

**完整解答：**

**Step 1:** 识别 substitution
- 看到 $\tan x$ 和 $\sec^2 x$
- 回忆：$\frac{d}{dx}(\tan x) = \sec^2 x$
- 令 $u = \tan x$

**Step 2:** 求 $du$
$$du = \sec^2 x dx$$

**Step 3:** 改变上下限
- 当 $x = 0$ 时，$u = \tan 0 = 0$
- 当 $x = \pi/4$ 时，$u = \tan(\pi/4) = 1$

**Step 4:** 替换
$$\int_0^{\pi/4} \tan x \sec^2 x dx = \int_0^1 u \, du$$

**Step 5:** 积分
$$= \left[\frac{u^2}{2}\right]_0^1 = \frac{1}{2} - 0 = \frac{1}{2}$$

**答案：** $\frac{1}{2}$

---
## 附录：快速自测清单

**考前 30 分钟自测（每题 30 秒内回答）：**

1. $\frac{d}{dx}(\sin(x^2)) = ?$
   - **答案：** $2x\cos(x^2)$

2. $(fg)' = ?$
   - **答案：** $f'g + fg'$

3. $\left(\frac{f}{g}\right)' = ?$
   - **答案：** $\frac{f'g - fg'}{g^2}$

4. $\int x^n dx = ?$ ($n \neq -1$)
   - **答案：** $\frac{x^{n+1}}{n+1} + C$

5. $e^x$ 的 Maclaurin series 前 4 项？
   - **答案：** $1 + x + \frac{x^2}{2} + \frac{x^3}{6}$

6. $\sin x$ 的 Maclaurin series 前 3 项？
   - **答案：** $x - \frac{x^3}{6} + \frac{x^5}{120}$

7. $\frac{d}{dx}\left[\int_0^x f(t) dt\right] = ?$
   - **答案：** $f(x)$

8. L'Hopital 适用于哪两种类型？
   - **答案：** $\frac{0}{0}$ 和 $\frac{\infty}{\infty}$

9. 隐函数求导 $\frac{d}{dx}(y^2) = ?$
   - **答案：** $2y \cdot y'$ 或 $2y \frac{dy}{dx}$

10. $\ln(x+1)$ 的 domain？
    - **答案：** $x > -1$

**如果这 10 题你都能快速答对，你已经准备好了！**

---

---

**文档完成时间：** 2026-05-22  
**适用课程：** MATH1061 Calculus  
