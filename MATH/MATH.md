[[MATH/Algebra 代数/题型条件反射|题型条件反射]][[MATH/Calculus 微积分/题型条件反射|题型条件反射]][[Calculus复习]][[Algebra 复习]][[Statistics]][[Discrete]]

---

## 🔴 第一优先级：考试必用（两门课都要）

### 1. 求导公式

#### 基本求导

$$
\begin{aligned}
&(x^n)' = nx^{n-1} & &(e^x)' = e^x \\
&(\ln x)' = \frac{1}{x} & &(a^x)' = a^x \ln a \\
&(\sin x)' = \cos x & &(\cos x)' = -\sin x \\
&(\tan x)' = \sec^2 x & &(\cot x)' = -\csc^2 x \\
&(\sec x)' = \sec x \tan x & &(\csc x)' = -\csc x \cot x
\end{aligned}
$$

#### 双曲函数

$$
(\sinh x)' = \cosh x, \quad (\cosh x)' = \sinh x, \quad (\tanh x)' = \operatorname{sech}^2 x
$$

#### 反三角函数

$$
(\sin^{-1} x)' = \frac{1}{\sqrt{1-x^2}}, \quad (\cos^{-1} x)' = -\frac{1}{\sqrt{1-x^2}}, \quad (\tan^{-1} x)' = \frac{1}{1+x^2}
$$

#### 求导法则

$$
\begin{aligned}
\text{乘积法则：} & \quad (fg)' = f'g + fg' \\
\text{商法则：} & \quad \left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2} \\
\text{链式法则：} & \quad [f(g(x))]' = f'(g(x)) \cdot g'(x)
\end{aligned}
$$

---

### 2. 三角恒等式

#### 基本恒等式

$$
\sin^2 x + \cos^2 x = 1, \quad 1 + \tan^2 x = \sec^2 x, \quad 1 + \cot^2 x = \csc^2 x
$$

#### 倍角公式

$$
\begin{aligned}
\sin(2x) &= 2\sin x \cos x \\
\cos(2x) &= \cos^2 x - \sin^2 x = 1 - 2\sin^2 x = 2\cos^2 x - 1 \\
\tan(2x) &= \frac{2\tan x}{1 - \tan^2 x}
\end{aligned}
$$

####  降幂公式（积分常用！）

$$
\sin^2 x = \frac{1 - \cos 2x}{2}, \quad \cos^2 x = \frac{1 + \cos 2x}{2}
$$

#### 和差公式

$$
\sin(A \pm B) = \sin A \cos B \pm \cos A \sin B
$$

$$
\cos(A \pm B) = \cos A \cos B \mp \sin A \sin B
$$

---

### 3. 双曲函数

#### 定义

$$
\sinh x = \frac{e^x - e^{-x}}{2}, \quad \cosh x = \frac{e^x + e^{-x}}{2}, \quad \tanh x = \frac{\sinh x}{\cosh x}
$$

#### 关键恒等式

$$
\cosh^2 x - \sinh^2 x = 1
$$

$$
1 - \tanh^2 x = \operatorname{sech}^2 x
$$

$$
\cosh^2 x + \sinh^2 x = \cosh(2x), \quad 2\sinh x \cosh x = \sinh(2x)
$$

#### 值域

$$
\cosh x \geq 1 \text{（最小值在 } x=0 \text{ 处取 } 1\text{）}, \quad \sinh x \in \mathbb{R}
$$

---

### 4. 复数公式

#### 基本形式

$$
z = a + bi \quad \text{（直角坐标）}
$$

$$
z = r(\cos\theta + i\sin\theta) = re^{i\theta} \quad \text{（极坐标）}
$$

$$
r = |z| = \sqrt{a^2 + b^2}, \quad \theta = \arg(z) = \arctan\frac{b}{a}
$$

#### 共轭与模

$$
\bar{z} = a - bi, \quad |z|^2 = z\bar{z}
$$

#### 欧拉公式

$$
e^{i\theta} = \cos\theta + i\sin\theta
$$

$$
e^{i\pi} = -1, \quad e^{i\pi/2} = i
$$

#### 棣莫弗定理

$$
(\cos\theta + i\sin\theta)^n = \cos(n\theta) + i\sin(n\theta)
$$

#### 复指数形式的三角函数

$$
\sin\theta = \frac{e^{i\theta} - e^{-i\theta}}{2i}, \quad \cos\theta = \frac{e^{i\theta} + e^{-i\theta}}{2}
$$

---


### 5. 泰勒级数

#### 通用公式

$$
f(x) \approx \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!} (x-a)^k
$$

#### 常见函数泰勒级数（在 $x = 0$ 处）

$$
e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots
$$

$$
\sin x = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots
$$

$$
\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots
$$

$$
\ln(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots \quad (|x| < 1)
$$

$$
\frac{1}{1-x} = 1 + x + x^2 + x^3 + \cdots \quad (|x| < 1)
$$

$$
(1+x)^n = 1 + nx + \frac{n(n-1)}{2!}x^2 + \cdots
$$

#### 泰勒余项（拉格朗日形式）

$$
R_n(x) = \frac{f^{(n+1)}(c)}{(n+1)!}(x-a)^{n+1}, \quad c \in (a, x)
$$

$$
|R_n(x)| \leq \frac{M}{(n+1)!}|x-a|^{n+1}, \quad M = \max|f^{(n+1)}|
$$

---

### 6. 几何应用公式

#### 旋转体体积

$$
\text{绕 } x \text{ 轴：} \quad V = \pi \int_a^b [f(x)]^2 \, dx
$$

$$
\text{绕 } y \text{ 轴（壳层法）：} \quad V = 2\pi \int_a^b x \cdot f(x) \, dx
$$

#### 弧长公式

$$
L = \int_a^b \sqrt{1 + \left(\frac{dy}{dx}\right)^2} \, dx
$$

#### 平面区域面积

$$
A = \int_a^b |f(x) - g(x)| \, dx
$$

---

### 7. 黎曼和

区间 $[a,b]$ 分 $n$ 等份，$\Delta x = \frac{b-a}{n}$：

$$
\text{左黎曼和：} \quad L_n = \sum_{k=0}^{n-1} f(a + k\Delta x) \cdot \Delta x
$$

$$
\text{右黎曼和：} \quad R_n = \sum_{k=1}^{n} f(a + k\Delta x) \cdot \Delta x
$$

**单调函数：** $\min(L_n, R_n) \leq \int_a^b f(x)\,dx \leq \max(L_n, R_n)$

---

### 8. 微积分基本定理 (FTC)

#### Part I

> 若 $f$ 在 $[a,b]$ 连续，定义 $F(x) = \int_a^x f(t)\,dt$，  
> 则 $F$ 在 $[a,b]$ 可导，且 $F'(x) = f(x)$。

#### Part II（牛顿-莱布尼茨）

$$
\int_a^b f(x) \, dx = F(b) - F(a), \quad \text{其中 } F'(x) = f(x)
$$

#### 链式法则结合 FTC（重要！）

$$
\frac{d}{dx}\left[\int_a^{g(x)} f(t)\,dt\right] = f(g(x)) \cdot g'(x)
$$

---

## 第三优先级：MATH1061 专属

### 9. 矩阵公式

#### 行列式

$$
\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc
$$

$$
\det(A_{3\times 3}) = a_{11}M_{11} - a_{12}M_{12} + a_{13}M_{13} \quad \text{（按第一行展开）}
$$

#### 2×2 求逆

$$
A^{-1} = \frac{1}{\det(A)} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}
$$

#### 行列式性质

$$
\det(AB) = \det(A) \cdot \det(B)
$$

$$
\det(A^T) = \det(A), \quad \det(A^{-1}) = \frac{1}{\det(A)}
$$

$$
\det(kA) = k^n \det(A) \quad (n \text{ 是阶数})
$$

$$
A \text{ 可逆} \iff \det(A) \neq 0
$$

#### 伴随矩阵法求逆

$$
A^{-1} = \frac{1}{\det(A)} \cdot \operatorname{adj}(A), \quad \operatorname{adj}(A) = (\operatorname{cof}(A))^T
$$

---

### 10. 向量公式

#### 点积

$$
\vec{u} \cdot \vec{v} = u_1 v_1 + u_2 v_2 + u_3 v_3 = |\vec{u}||\vec{v}|\cos\theta
$$

$$
\cos\theta = \frac{\vec{u} \cdot \vec{v}}{|\vec{u}||\vec{v}|}, \quad \vec{u} \perp \vec{v} \iff \vec{u} \cdot \vec{v} = 0
$$

#### 叉积（仅 3D）

$$
\vec{u} \times \vec{v} = \begin{vmatrix} \vec{i} & \vec{j} & \vec{k} \\ u_1 & u_2 & u_3 \\ v_1 & v_2 & v_3 \end{vmatrix}
$$

$$
|\vec{u} \times \vec{v}| = |\vec{u}||\vec{v}|\sin\theta, \quad \vec{u} \parallel \vec{v} \iff \vec{u} \times \vec{v} = \vec{0}
$$

#### 投影

$$
\operatorname{proj}_{\vec{u}}(\vec{v}) = \frac{\vec{u} \cdot \vec{v}}{|\vec{u}|^2} \vec{u}
$$

#### 直线参数方程

$$
\vec{r} = \vec{r_0} + t\vec{d} \quad (\vec{d} \text{ 是方向向量})
$$

#### 平面方程

$$
\vec{n} \cdot (\vec{r} - \vec{r_0}) = 0
$$

$$
\vec{n} \cdot (\vec{r} - \vec{r_0}) = 0
$$

$$
a(x - x_0) + b(y - y_0) + c(z - z_0) = 0, \quad \vec{n} = (a, b, c)
$$

---

### 11. 特征值与对角化

#### 特征方程

$$
\det(A - \lambda I) = 0 \quad \Rightarrow \quad \text{解出特征值 } \lambda
$$

#### 特征向量

对每个特征值 $\lambda$，解齐次方程组：

$$
(A - \lambda I)\vec{v} = \vec{0}
$$

#### 对角化

若 $A$ 有 $n$ 个线性无关的特征向量 $\vec{v_1}, \ldots, \vec{v_n}$：

$$
A = PDP^{-1}
$$

$$
P = [\vec{v_1} \; \vec{v_2} \; \cdots \; \vec{v_n}], \quad D = \operatorname{diag}(\lambda_1, \lambda_2, \ldots, \lambda_n)
$$

#### 矩阵幂

$$
A^n = PD^nP^{-1}, \quad D^n = \operatorname{diag}(\lambda_1^n, \lambda_2^n, \ldots, \lambda_k^n)
$$

#### 可对角化判定

- **充分条件：** $n$ 个不同特征值 $\Rightarrow$ 必可对角化
- **一般条件：** 每个特征值的几何重数 = 代数重数

#### 实用结论

$$
A \text{ 可逆} \iff 0 \text{ 不是 } A \text{ 的特征值}
$$

$$
\det(A) = \lambda_1 \cdot \lambda_2 \cdots \lambda_n
$$

$$
\operatorname{tr}(A) = \lambda_1 + \lambda_2 + \cdots + \lambda_n
$$

---

##  通用必背（两门课都要）

### 12. 极限与连续性

#### 重要极限

$$
\lim_{x \to 0} \frac{\sin x}{x} = 1
$$

$$
\lim_{x \to 0} \frac{1 - \cos x}{x^2} = \frac{1}{2}
$$

$$
\lim_{x \to 0} \frac{e^x - 1}{x} = 1
$$

$$
\lim_{x \to 0} \frac{\ln(1+x)}{x} = 1
$$

$$
\lim_{x \to \infty} \left(1 + \frac{1}{x}\right)^x = e, \quad \lim_{x \to 0}(1 + x)^{1/x} = e
$$

#### 洛必达法则（$\frac{0}{0}$ 或 $\frac{\infty}{\infty}$ 型）

$$
\lim_{x \to a} \frac{f(x)}{g(x)} = \lim_{x \to a} \frac{f'(x)}{g'(x)}
$$

#### 连续性定义

$$
f \text{ 在 } a \text{ 连续} \iff \lim_{x \to a} f(x) = f(a)
$$

需要满足三个条件：
1. $f(a)$ 存在
2. $\lim_{x \to a} f(x)$ 存在
3. $\lim_{x \to a} f(x) = f(a)$

---

### 13. 中值定理类

#### Rolle 定理

> 若 $f$ 在 $[a, b]$ 连续，在 $(a, b)$ 可导，且 $f(a) = f(b)$，  
> 则存在 $c \in (a, b)$ 使得 $f'(c) = 0$。

#### 均值定理 (MVT)

> 若 $f$ 在 $[a, b]$ 连续，在 $(a, b)$ 可导，  
> 则存在 $c \in (a, b)$ 使得：

