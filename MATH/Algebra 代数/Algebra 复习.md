# MATH1061 线性代数部分

## 1. 复数与旋转

### 1.1 复数基本概念

**核心定义：**

| 概念           | 公式                                               | 说明                                          |
| ------------ | ------------------------------------------------ | ------------------------------------------- |
| 标准形式         | $z = x + iy$                                     | $x = \text{Re}(z)$ 实部，$y = \text{Im}(z)$ 虚部 |
| 共轭 conjugate | $\bar{z} = x - iy$                               | 虚部取负                                        |
| 模 modulus    | $\|z\| = \sqrt{x^2 + y^2}$                       | 复数到原点的距离                                    |
| 极坐标形式        | $z = r(\cos\theta + i\sin\theta) = re^{i\theta}$ | $r = \|z\|$，$\theta$ 是辐角                    |
| Euler 公式     | $e^{i\theta} = \cos\theta + i\sin\theta$         | 连接指数和三角函数                                   |

### 1.2 复数运算

**加减法：** 实部和虚部分别相加减

$$
(a + ib) + (c + id) = (a+c) + i(b+d)
$$

**乘法：** 展开后用 $i^2 = -1$

$$
(a + ib)(c + id) = (ac - bd) + i(ad + bc)
$$

**极坐标乘法：**

$$
z_1 \cdot z_2 = r_1 e^{i\theta_1} \cdot r_2 e^{i\theta_2} = (r_1 r_2) e^{i(\theta_1 + \theta_2)}
$$

> **核心：** 模相乘，角度相加

**除法：** 分子分母同乘分母的共轭

$$
\frac{a + ib}{c + id} = \frac{(a + ib)(c - id)}{(c + id)(c - id)} = \frac{(ac + bd) + i(bc - ad)}{c^2 + d^2}
$$

**极坐标除法：**

$$
\frac{z_1}{z_2} = \frac{r_1}{r_2} e^{i(\theta_1 - \theta_2)}
$$

> **核心：** 模相除，角度相减

### 1.3 De Moivre 定理

$$
(\cos\theta + i\sin\theta)^n = \cos(n\theta) + i\sin(n\theta)
$$

或用指数形式：

$$
(e^{i\theta})^n = e^{in\theta}
$$

### 1.4 解方程 $z^n = \alpha$（核心题型）

**解题模板：**

| 步骤 | 操作 | 说明 |
|------|------|------|
| **Step 1** | 把 $\alpha$ 写成极坐标形式 | $\alpha = r(\cos\theta + i\sin\theta)$ |
| **Step 2** | 求模长 | $\|z\| = r^{1/n}$ |
| **Step 3** | 求辐角 | $\arg(z) = \frac{\theta + 2\pi k}{n}$，$k = 0,1,\ldots,n-1$ |
| **Step 4** | 写出所有根 | $z_k = r^{1/n} \cdot e^{i(\theta + 2\pi k)/n}$ |
| **结论** | $n$ 个根均匀分布在圆上 | 相邻根角度差 = $\frac{2\pi}{n}$ |

**例题：解 $z^3 = -8$**

**Step 1:** 把 $-8$ 写成极坐标形式

$$
-8 = 8(\cos\pi + i\sin\pi) = 8e^{i\pi}
$$

**Step 2:** 求模长

$$
|z| = 8^{1/3} = 2
$$

**Step 3:** 求辐角（$k = 0, 1, 2$）

$$
\arg(z) = \frac{\pi + 2\pi k}{3}
$$

$$
\begin{aligned}
k = 0: & \quad \theta_0 = \frac{\pi}{3} \\
k = 1: & \quad \theta_1 = \frac{\pi}{3} + \frac{2\pi}{3} = \pi \\
k = 2: & \quad \theta_2 = \frac{\pi}{3} + \frac{4\pi}{3} = \frac{5\pi}{3}
\end{aligned}
$$

**Step 4:** 写出三个根

$$
\begin{aligned}
z_0 &= 2e^{i\pi/3} = 2\left(\frac{1}{2} + i\frac{\sqrt{3}}{2}\right) = 1 + i\sqrt{3} \\
z_1 &= 2e^{i\pi} = 2(-1 + 0i) = -2 \\
z_2 &= 2e^{i5\pi/3} = 2\left(\frac{1}{2} - i\frac{\sqrt{3}}{2}\right) = 1 - i\sqrt{3}
\end{aligned}
$$

**答案：** $z = 1 + i\sqrt{3}, \; -2, \; 1 - i\sqrt{3}$

---

### 1.5 旋转 Rotation（核心考点）

#### 复平面中的旋转

| 操作 | 几何意义 | 例子 |
|------|----------|------|
| $z \times i$ | 逆时针旋转 $90°$（左旋） | $1 \to i$，$i \to -1$ |
| $z \times (-i)$ | 顺时针旋转 $90°$（右旋） | $1 \to -i$，$i \to 1$ |
| $z \times e^{i\theta}$ | 逆时针旋转 $\theta$ | 角度增加 $\theta$ |
| $z \times e^{-i\theta}$ | 顺时针旋转 $\theta$ | 角度减少 $\theta$ |

**核心理解：**
- 乘以 $e^{i\theta}$ → 模长不变（因为 $|e^{i\theta}| = 1$），角度增加 $\theta$
- 逆时针 = 左旋 = counterclockwise
- 顺时针 = 右旋 = clockwise

**例题：把复数 $z = 1 + i$ 逆时针旋转 $45°$**

旋转 $45°$ → 乘以 $e^{i\pi/4}$

$$
\begin{aligned}
z' &= (1 + i) \cdot e^{i\pi/4} \\
&= (1 + i) \cdot \left(\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2}\right) \\
&= \frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2} + i^2\frac{\sqrt{2}}{2} \\
&= \frac{\sqrt{2}}{2} + i\sqrt{2} - \frac{\sqrt{2}}{2} \\
&= i\sqrt{2}
\end{aligned}
$$

#### 旋转矩阵（$\mathbb{R}^2$ 中的旋转）

**逆时针旋转 $\theta$ 的矩阵：**

$$
R(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}
$$

**顺时针旋转 $\theta$ 的矩阵：**

$$
R(-\theta) = \begin{bmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{bmatrix}
$$

**特殊角度：**

| 旋转角度 | 矩阵 |
|----------|------|
| 逆时针 $90°$ | $\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$ |
| 顺时针 $90°$ | $\begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix}$ |
| $180°$ | $\begin{bmatrix} -1 & 0 \\ 0 & -1 \end{bmatrix}$ |

> ⚠️ **易错点：** $-\sin\theta$ 在右上角，$\sin\theta$ 在左下角，不要写反！

---

## 2. 向量、点积、叉积

### 2.1 向量基础

**向量表示：**

$$
\mathbf{v} = \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} \quad \text{或} \quad \mathbf{v} = v_1\mathbf{i} + v_2\mathbf{j} + v_3\mathbf{k}
$$

**由两点构造向量：**

$$
\overrightarrow{AB} = B - A = \begin{bmatrix} b_1 - a_1 \\ b_2 - a_2 \\ b_3 - a_3 \end{bmatrix}
$$

> **记忆：** 终点减起点

**向量长度（模）：**

$$
\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2 + v_3^2}
$$

**单位向量：**

$$
\hat{\mathbf{v}} = \frac{\mathbf{v}}{\|\mathbf{v}\|}
$$

**线性组合：**

$$
\mathbf{v} = c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \cdots + c_k\mathbf{v}_k
$$

### 2.2 点积 Dot Product（内积）

**代数定义：**

$$
\mathbf{u} \cdot \mathbf{v} = u_1v_1 + u_2v_2 + u_3v_3
$$

**几何定义：**

$$
\mathbf{u} \cdot \mathbf{v} = \|\mathbf{u}\| \cdot \|\mathbf{v}\| \cdot \cos\theta
$$

**性质：**
- 交换律：$\mathbf{u} \cdot \mathbf{v} = \mathbf{v} \cdot \mathbf{u}$
- 分配律：$\mathbf{u} \cdot (\mathbf{v} + \mathbf{w}) = \mathbf{u} \cdot \mathbf{v} + \mathbf{u} \cdot \mathbf{w}$
- 数乘：$(c\mathbf{u}) \cdot \mathbf{v} = c(\mathbf{u} \cdot \mathbf{v})$

**应用 1：求夹角**

$$
\cos\theta = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \cdot \|\mathbf{v}\|}
$$

**应用 2：判断垂直**

$$
\mathbf{u} \perp \mathbf{v} \quad \Longleftrightarrow \quad \mathbf{u} \cdot \mathbf{v} = 0
$$

### 2.3 投影 Projection（高频考点）

**$\mathbf{v}$ 在 $\mathbf{u}$ 上的投影：**

$$
\text{proj}_{\mathbf{u}}(\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\mathbf{u} \cdot \mathbf{u}} \cdot \mathbf{u}
$$

**投影长度（标量投影）：**

$$
\text{comp}_{\mathbf{u}}(\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\|}
$$

**记忆方法：**
- 分子：两个向量点积
- 分母：被投影向量的自己点积
- 最后乘以被投影向量

> ⚠️ **易错点：** $\text{proj}_{\mathbf{u}}(\mathbf{v}) \neq \text{proj}_{\mathbf{v}}(\mathbf{u})$ 投影方向不同！

**例题：求 $\mathbf{v} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$ 在 $\mathbf{u} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ 上的投影**

$$
\begin{aligned}
\mathbf{u} \cdot \mathbf{v} &= 1 \times 3 + 0 \times 4 = 3 \\
\mathbf{u} \cdot \mathbf{u} &= 1 \times 1 + 0 \times 0 = 1 \\
\text{proj}_{\mathbf{u}}(\mathbf{v}) &= \frac{3}{1} \cdot \begin{bmatrix} 1 \\ 0 \end{bmatrix} = \begin{bmatrix} 3 \\ 0 \end{bmatrix}
\end{aligned}
$$

### 2.4 叉积 Cross Product（只在 $\mathbb{R}^3$）

**代数定义：**

$$
\mathbf{u} \times \mathbf{v} = \begin{bmatrix} u_2v_3 - u_3v_2 \\ u_3v_1 - u_1v_3 \\ u_1v_2 - u_2v_1 \end{bmatrix}
$$

**行列式记法：**

$$
\mathbf{u} \times \mathbf{v} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ u_1 & u_2 & u_3 \\ v_1 & v_2 & v_3 \end{vmatrix}
$$

**几何意义：**
- $\mathbf{u} \times \mathbf{v}$ 垂直于 $\mathbf{u}$ 和 $\mathbf{v}$
- 方向：右手法则
- 模长：$\|\mathbf{u} \times \mathbf{v}\| = \|\mathbf{u}\| \cdot \|\mathbf{v}\| \cdot \sin\theta$

**性质：**
- 反交换律：$\mathbf{u} \times \mathbf{v} = -(\mathbf{v} \times \mathbf{u})$
- $\mathbf{u} \times \mathbf{u} = \mathbf{0}$
- $\mathbf{u} \times \mathbf{v} = \mathbf{0} \Longleftrightarrow \mathbf{u}$ 和 $\mathbf{v}$ 平行

**应用：**
- **平行四边形面积：** $\text{Area} = \|\mathbf{u} \times \mathbf{v}\|$
- **三角形面积：** $\text{Area} = \frac{1}{2}\|\mathbf{u} \times \mathbf{v}\|$
- **求垂直向量：** 需要同时垂直于 $\mathbf{u}$ 和 $\mathbf{v}$ → 算 $\mathbf{u} \times \mathbf{v}$

**右手法则记忆：**

$$
\begin{aligned}
\mathbf{i} \times \mathbf{j} &= \mathbf{k}, \quad \mathbf{j} \times \mathbf{k} = \mathbf{i}, \quad \mathbf{k} \times \mathbf{i} = \mathbf{j} \\
\mathbf{j} \times \mathbf{i} &= -\mathbf{k}, \quad \mathbf{k} \times \mathbf{j} = -\mathbf{i}, \quad \mathbf{i} \times \mathbf{k} = -\mathbf{j}
\end{aligned}
$$

**例题：求 $\mathbf{u} = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$ 和 $\mathbf{v} = \begin{bmatrix} 4 \\ 5 \\ 6 \end{bmatrix}$ 的叉积**

$$
\begin{aligned}
\mathbf{u} \times \mathbf{v} &= \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ 1 & 2 & 3 \\ 4 & 5 & 6 \end{vmatrix} \\
&= \mathbf{i}(2 \times 6 - 3 \times 5) - \mathbf{j}(1 \times 6 - 3 \times 4) + \mathbf{k}(1 \times 5 - 2 \times 4) \\
&= \mathbf{i}(12 - 15) - \mathbf{j}(6 - 12) + \mathbf{k}(5 - 8) \\
&= -3\mathbf{i} + 6\mathbf{j} - 3\mathbf{k} \\
&= \begin{bmatrix} -3 \\ 6 \\ -3 \end{bmatrix}
\end{aligned}
$$

---

## 3. 直线与平面

### 3.1 $\mathbb{R}^3$ 中的直线

**向量形式：**

$$
\mathbf{x} = \mathbf{p} + t\mathbf{d}
$$

- $\mathbf{p}$：直线上一点（position vector）
- $\mathbf{d}$：方向向量（direction vector）
- $t \in \mathbb{R}$：参数

**参数方程：**

$$
\begin{cases}
x = p_1 + td_1 \\
y = p_2 + td_2 \\
z = p_3 + td_3
\end{cases}
$$

**由两点确定直线：**
- 已知点 $P$ 和 $Q$
- 方向向量：$\mathbf{d} = Q - P$
- 直线：$\mathbf{x} = P + t(Q - P)$

### 3.2 $\mathbb{R}^3$ 中的平面

**三种表示方式：**

**1. Normal form（法向量形式）：**

$$
\mathbf{n} \cdot (\mathbf{x} - \mathbf{p}) = 0
$$

- $\mathbf{n}$：法向量（垂直于平面）
- $\mathbf{p}$：平面上一点

**2. General equation（一般方程）：**

$$
ax + by + cz = d
$$

- $\mathbf{n} = \begin{bmatrix} a \\ b \\ c \end{bmatrix}$ 是法向量

**3. Vector form（向量形式）：**

$$
\mathbf{x} = \mathbf{p} + s\mathbf{u} + t\mathbf{v}
$$

- $\mathbf{u}, \mathbf{v}$：平面内两个不平行的向量

### 3.3 三点求平面（核心题型）

**模板步骤：**

已知三点 $P, Q, R$

| 步骤 | 操作 |
|------|------|
| **Step 1** | 取一点 $P$ |
| **Step 2** | 找两个方向向量：$\mathbf{u} = \overrightarrow{PQ} = Q - P$，$\mathbf{v} = \overrightarrow{PR} = R - P$ |
| **Step 3** | Vector form: $\mathbf{x} = P + s\mathbf{u} + t\mathbf{v}$ |
| **Step 4** | 求法向量：$\mathbf{n} = \mathbf{u} \times \mathbf{v}$ |
| **Step 5** | Normal form: $\mathbf{n} \cdot (\mathbf{x} - P) = 0$ |
| **Step 6** | 展开成 general equation: $ax + by + cz = d$ |

**例题：求过三点 $P(1,0,0)$，$Q(0,1,0)$，$R(0,0,1)$ 的平面方程**

**Step 1-2:** 找方向向量

$$
\mathbf{u} = Q - P = \begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix}, \quad \mathbf{v} = R - P = \begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix}
$$

**Step 3:** Vector form

$$
\mathbf{x} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} + s\begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix} + t\begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix}
$$

**Step 4:** 求法向量

$$
\mathbf{n} = \mathbf{u} \times \mathbf{v} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ -1 & 1 & 0 \\ -1 & 0 & 1 \end{vmatrix} = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}
$$

**Step 5:** Normal form

$$
\begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix} \cdot \left(\begin{bmatrix} x \\ y \\ z \end{bmatrix} - \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}\right) = 0
$$

**Step 6:** General equation

$$
1(x-1) + 1(y-0) + 1(z-0) = 0 \quad \Rightarrow \quad x + y + z = 1
$$

### 3.4 两平面的交线

**已知两个平面：**

$$
\begin{aligned}
\Pi_1: & \quad \mathbf{n}_1 \cdot \mathbf{x} = d_1 \\
\Pi_2: & \quad \mathbf{n}_2 \cdot \mathbf{x} = d_2
\end{aligned}
$$

**交线的方向向量：**

$$
\mathbf{d} = \mathbf{n}_1 \times \mathbf{n}_2
$$

**求交线上一点：** 令某个坐标为 0（如 $z=0$），解方程组得到一点 $P$

**交线方程：**

$$
\mathbf{x} = P + t\mathbf{d}
$$

### 3.5 点到平面的距离

**平面：** $ax + by + cz = d$

**点：** $P_0(x_0, y_0, z_0)$

**距离公式：**

$$
\text{distance} = \frac{|ax_0 + by_0 + cz_0 - d|}{\sqrt{a^2 + b^2 + c^2}}
$$

---

## 4. 方程组与 Row Reduction

### 4.1 线性方程组

**一般形式：**

$$
\begin{cases}
a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1 \\
a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2 \\
\vdots \\
a_{m1}x_1 + a_{m2}x_2 + \cdots + a_{mn}x_n = b_m
\end{cases}
$$

**矩阵形式：**

$$
A\mathbf{x} = \mathbf{b}
$$

**增广矩阵 (Augmented Matrix)：**

$$ 510[A \mid \mathbf{b}] = \left[\begin{array}{cccc|c} 511a_{11}a_{11} & a_{12} & \cdots & a_{1n} & b_1 \\
a_{21} & a_{22} & \cdots & a_{2n} & b_2 \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn} & b_m
\end{array}\right]
$$

### 4.2 行化简 Row Reduction

**三种基本行操作（Elementary Row Operations）：**

1. **交换两行：** $R_i \leftrightarrow R_j$
2. **某行乘以非零常数：** $R_i \to kR_i$ （$k \neq 0$）
3. **某行加上另一行的倍数：** $R_i \to R_i + kR_j$

### 4.3 行阶梯形 Row Echelon Form (REF)

**定义：** 矩阵满足以下条件：

1. 所有零行在底部
2. 每行的首个非零元素（pivot）在上一行 pivot 的右边
3. Pivot 下方的元素都是 0

**例子：**

$$
\begin{bmatrix}
\boxed{2} & 1 & 3 & 4 \\
0 & \boxed{5} & 2 & 1 \\
0 & 0 & \boxed{1} & 7 \\
0 & 0 & 0 & 0
\end{bmatrix}
$$

### 4.4 简化行阶梯形 Reduced Row Echelon Form (RREF)

**定义：** 在 REF 基础上还满足：

1. 每个 pivot 都是 1
2. Pivot 所在列的其他元素都是 0

**例子：**

$$
\begin{bmatrix}
\boxed{1} & 0 & 0 & 3 \\
0 & \boxed{1} & 0 & 2 \\
0 & 0 & \boxed{1} & 7 \\
0 & 0 & 0 & 0
\end{bmatrix}
$$

### 4.5 Gauss-Jordan 消元法（核心算法）

**目标：** 把增广矩阵 $[A \mid \mathbf{b}]$ 化为 RREF

**步骤：**

| 步骤 | 操作 |
|------|------|
| **Step 1** | 找第一列的 pivot（非零元素），如果需要交换行使其在第一行 |
| **Step 2** | 把 pivot 化为 1（整行除以 pivot） |
| **Step 3** | 用行操作把 pivot 所在列的其他元素化为 0 |
| **Step 4** | 对下一列重复 Step 1-3 |
| **Step 5** | 继续直到得到 RREF |

**例题：解方程组**

$$
\begin{cases}
x + 2y + z = 3 \\
2x + 5y + 3z = 7 \\
x + 3y + 2z = 5
\end{cases}
$$

**Step 1:** 写增广矩阵

$$
\left[\begin{array}{ccc|c}
1 & 2 & 1 & 3 \\
2 & 5 & 3 & 7 \\
1 & 3 & 2 & 5
\end{array}\right]
$$

**Step 2:** $R_2 \to R_2 - 2R_1$，$R_3 \to R_3 - R_1$

$$
\left[\begin{array}{ccc|c}
1 & 2 & 1 & 3 \\
0 & 1 & 1 & 1 \\
0 & 1 & 1 & 2
\end{array}\right]
$$

**Step 3:** $R_3 \to R_3 - R_2$

$$
\left[\begin{array}{ccc|c}
1 & 2 & 1 & 3 \\
0 & 1 & 1 & 1 \\
0 & 0 & 0 & 1
\end{array}\right]
$$

**Step 4:** 最后一行表示 $0 = 1$，矛盾！

**结论：** 方程组无解（inconsistent）

### 4.6 解的类型

**判断方法（看 RREF）：**

| 情况 | RREF 特征 | 解的类型 |
|------|-----------|----------|
| **无解** | 出现 $[0 \; 0 \; \cdots \; 0 \mid c]$（$c \neq 0$） | Inconsistent |
| **唯一解** | 每个变量都有 pivot | Unique solution |
| **无穷多解** | 有自由变量（free variables） | Infinitely many solutions |

**自由变量：** 没有 pivot 的列对应的变量

### 4.7 齐次方程组 Homogeneous Systems

**定义：** $A\mathbf{x} = \mathbf{0}$（右边全是 0）

**性质：**
- 总有解（至少有零解 $\mathbf{x} = \mathbf{0}$）
- 如果有自由变量 → 有无穷多解
- 解空间是向量空间

**例题：求齐次方程组的通解**

$$
\begin{cases}
x_1 + 2x_2 - x_3 = 0 \\
2x_1 + 4x_2 - 2x_3 = 0
\end{cases}
$$

**Step 1:** 增广矩阵

$$
\left[\begin{array}{ccc|c}
1 & 2 & -1 & 0 \\
2 & 4 & -2 & 0
\end{array}\right]
$$

**Step 2:** $R_2 \to R_2 - 2R_1$

$$
\left[\begin{array}{ccc|c}
1 & 2 & -1 & 0 \\
0 & 0 & 0 & 0
\end{array}\right]
$$

**Step 3:** 从 RREF 读出方程

$$
x_1 + 2x_2 - x_3 = 0 \quad \Rightarrow \quad x_1 = -2x_2 + x_3
$$

**Step 4:** $x_2$ 和 $x_3$ 是自由变量，令 $x_2 = s$，$x_3 = t$

$$
\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} -2s + t \\ s \\ t \end{bmatrix} = s\begin{bmatrix} -2 \\ 1 \\ 0 \end{bmatrix} + t\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}
$$

**通解：**

$$
\mathbf{x} = s\begin{bmatrix} -2 \\ 1 \\ 0 \end{bmatrix} + t\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}, \quad s, t \in \mathbb{R}
$$

---

## 5. 矩阵代数

### 5.1 矩阵基本概念

**矩阵：** $m \times n$ 矩阵有 $m$ 行 $n$ 列

$$
A = \begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{bmatrix}
$$

**特殊矩阵：**

| 类型 | 定义 | 例子 |
|------|------|------|
| 方阵 | $m = n$ | $2 \times 2$，$3 \times 3$ |
| 零矩阵 | 所有元素都是 0 | $O$ 或 $0$ |
| 单位矩阵 | 对角线为 1，其余为 0 | $I_n$ |
| 对角矩阵 | 非对角线元素都是 0 | $\text{diag}(d_1, d_2, \ldots, d_n)$ |
| 上三角 | 对角线下方都是 0 | |
| 下三角 | 对角线上方都是 0 | |

**单位矩阵：**

$$
I_3 = \begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

### 5.2 矩阵运算

#### 矩阵加法

**条件：** 同型矩阵（相同的行数和列数）

$$
A + B = \begin{bmatrix}
a_{11} + b_{11} & a_{12} + b_{12} \\
a_{21} + b_{21} & a_{22} + b_{22}
\end{bmatrix}
$$

**性质：**
- 交换律：$A + B = B + A$
- 结合律：$(A + B) + C = A + (B + C)$

#### 数乘

$$
cA = \begin{bmatrix}
ca_{11} & ca_{12} \\
ca_{21} & ca_{22}
\end{bmatrix}
$$

#### 矩阵乘法

**条件：** $A$ 是 $m \times n$，$B$ 是 $n \times p$ → $AB$ 是 $m \times p$

> **记忆：** A 的列数 = B 的行数

**定义：**

$$
(AB)_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj} = a_{i1}b_{1j} + a_{i2}b_{2j} + \cdots + a_{in}b_{nj}
$$

**例子：**

$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
=
\begin{bmatrix}
1 \cdot 5 + 2 \cdot 7 & 1 \cdot 6 + 2 \cdot 8 \\
3 \cdot 5 + 4 \cdot 7 & 3 \cdot 6 + 4 \cdot 8
\end{bmatrix}
=
\begin{bmatrix}
19 & 22 \\
43 & 50
\end{bmatrix}
$$

**性质：**
- **不满足交换律：** $AB \neq BA$（一般情况）
- 结合律：$(AB)C = A(BC)$
- 分配律：$A(B + C) = AB + AC$
- $(AB)^T = B^T A^T$
- $AI = IA = A$

> ⚠️ **易错点：** 矩阵乘法不可交换！

### 5.3 矩阵转置 Transpose

**定义：** $A^T$ 的第 $i$ 行第 $j$ 列元素 = $A$ 的第 $j$ 行第 $i$ 列元素

$$
A = \begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}
\quad \Rightarrow \quad
A^T = \begin{bmatrix}
1 & 4 \\
2 & 5 \\
3 & 6
\end{bmatrix}
$$

**性质：**
- $(A^T)^T = A$
- $(A + B)^T = A^T + B^T$
- $(cA)^T = cA^T$
- $(AB)^T = B^T A^T$（顺序颠倒！）

**对称矩阵：** $A^T = A$

### 5.4 矩阵的幂

**定义：** $A^n = \underbrace{A \cdot A \cdot \cdots \cdot A}_{n \text{ 次}}$

**性质：**
- $A^m A^n = A^{m+n}$
- $(A^m)^n = A^{mn}$
- $A^0 = I$

> ⚠️ **注意：** $(AB)^n \neq A^n B^n$（除非 $AB = BA$）

### 5.5 分块矩阵 Block Matrices

**定义：** 把矩阵分成若干子矩阵

$$
A = \begin{bmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{bmatrix}
$$

**分块乘法：** 按照矩阵乘法规则，但元素是子矩阵

$$
\begin{bmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{bmatrix}
\begin{bmatrix}
B_{11} & B_{12} \\
B_{21} & B_{22}
\end{bmatrix}
=
\begin{bmatrix}
A_{11}B_{11} + A_{12}B_{21} & A_{11}B_{12} + A_{12}B_{22} \\
A_{21}B_{11} + A_{22}B_{21} & A_{21}B_{12} + A_{22}B_{22}
\end{bmatrix}
$$

---

## 6. 逆矩阵

### 6.1 逆矩阵定义

**定义：** 如果存在矩阵 $B$ 使得

$$
AB = BA = I
$$

则称 $B$ 是 $A$ 的逆矩阵，记作 $A^{-1}$

**可逆矩阵（Invertible Matrix）：** 有逆矩阵的矩阵

**奇异矩阵（Singular Matrix）：** 没有逆矩阵的矩阵

### 6.2 $2 \times 2$ 矩阵的逆

**公式：**

$$
A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}
\quad \Rightarrow \quad
A^{-1} = \frac{1}{ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}
$$

**条件：** $\det(A) = ad - bc \neq 0$

**记忆方法：**
1. 算行列式 $\det(A) = ad - bc$
2. 交换对角线元素 $a \leftrightarrow d$
3. 副对角线元素取负 $b \to -b$，$c \to -c$
4. 除以行列式

**例题：求 $A = \begin{bmatrix} 3 & 1 \\ 5 & 2 \end{bmatrix}$ 的逆矩阵**

$$
\begin{aligned}
\det(A) &= 3 \cdot 2 - 1 \cdot 5 = 6 - 5 = 1 \\
A^{-1} &= \frac{1}{1} \begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix} = \begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix}
\end{aligned}
$$

**验证：**

$$
AA^{-1} = \begin{bmatrix} 3 & 1 \\ 5 & 2 \end{bmatrix} \begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = I
$$

### 6.3 用 Gauss-Jordan 求逆矩阵（核心方法）

**步骤：**

| 步骤 | 操作 |
|------|------|
| **Step 1** | 构造增广矩阵 $[A \mid I]$ |
| **Step 2** | 用行操作把左边化为 $I$ |
| **Step 3** | 如果成功，右边就是 $A^{-1}$ |
| **Step 4** | 如果左边无法化为 $I$，则 $A$ 不可逆 |

**例题：求 $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$ 的逆矩阵**

**Step 1:** 构造 $[A \mid I]$

$$
\left[\begin{array}{cc|cc}
1 & 2 & 1 & 0 \\
3 & 4 & 0 & 1
\end{array}\right]
$$

**Step 2:** $R_2 \to R_2 - 3R_1$

$$
\left[\begin{array}{cc|cc}
1 & 2 & 1 & 0 \\
0 & -2 & -3 & 1
\end{array}\right]
$$

**Step 3:** $R_2 \to -\frac{1}{2}R_2$

$$
\left[\begin{array}{cc|cc}
1 & 2 & 1 & 0 \\
0 & 1 & \frac{3}{2} & -\frac{1}{2}
\end{array}\right]
$$

**Step 4:** $R_1 \to R_1 - 2R_2$

$$
\left[\begin{array}{cc|cc}
1 & 0 & -2 & 1 \\
0 & 1 & \frac{3}{2} & -\frac{1}{2}
\end{array}\right]
$$

**答案：**

$$
A^{-1} = \begin{bmatrix} -2 & 1 \\ \frac{3}{2} & -\frac{1}{2} \end{bmatrix}
$$

### 6.4 逆矩阵的性质

**基本性质：**

1. $(A^{-1})^{-1} = A$
2. $(AB)^{-1} = B^{-1}A^{-1}$（顺序颠倒！）
3. $(A^T)^{-1} = (A^{-1})^T$
4. $(cA)^{-1} = \frac{1}{c}A^{-1}$（$c \neq 0$）
5. $(A^n)^{-1} = (A^{-1})^n$

> ⚠️ **易错点：** $(AB)^{-1} = B^{-1}A^{-1}$，顺序要颠倒！

### 6.5 用逆矩阵解方程组

**方程组：** $A\mathbf{x} = \mathbf{b}$

**如果 $A$ 可逆：**

$$
\mathbf{x} = A^{-1}\mathbf{b}
$$

**例题：解方程组**

$$
\begin{cases}
x + 2y = 5 \\
3x + 4y = 11
\end{cases}
$$

**Step 1:** 写成矩阵形式

$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 5 \\ 11 \end{bmatrix}
$$

**Step 2:** 从前面知道

$$
A^{-1} = \begin{bmatrix} -2 & 1 \\ \frac{3}{2} & -\frac{1}{2} \end{bmatrix}
$$

**Step 3:** 计算

$$
\begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} -2 & 1 \\ \frac{3}{2} & -\frac{1}{2} \end{bmatrix} \begin{bmatrix} 5 \\ 11 \end{bmatrix} = \begin{bmatrix} -10 + 11 \\ \frac{15}{2} - \frac{11}{2} \end{bmatrix} = \begin{bmatrix} 1 \\ 2 \end{bmatrix}
$$

**答案：** $x = 1$，$y = 2$

### 6.6 可逆性判断

**矩阵 $A$ 可逆 $\Longleftrightarrow$ 以下任一条件成立：**

1. $\det(A) \neq 0$
2. $A$ 的 RREF 是 $I$
3. $A\mathbf{x} = \mathbf{0}$ 只有零解
4. $A$ 的列向量线性无关
5. $A$ 的行向量线性无关

---

## 7. 题型反射表

### 7.1 复数题型

| 题型 | 关键词 | 方法 |
|------|--------|------|
| 求 $z^n = \alpha$ 的所有根 | "solve", "find all solutions" | 极坐标 + De Moivre |
| 复数旋转 | "rotate", "counterclockwise" | 乘以 $e^{i\theta}$ |
| 复数模长 | "modulus", "$\|z\|$" | $\sqrt{x^2 + y^2}$ |
| 复数辐角 | "argument", "$\arg(z)$" | $\theta = \arctan(y/x)$ |
| 极坐标转换 | "polar form" | $z = re^{i\theta}$ |

### 7.2 向量题型

| 题型 | 关键词 | 方法 |
|------|--------|------|
| 求夹角 | "angle between" | $\cos\theta = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\|\|\mathbf{v}\|}$ |
| 判断垂直 | "perpendicular", "orthogonal" | 检查 $\mathbf{u} \cdot \mathbf{v} = 0$ |
| 判断平行 | "parallel" | 检查 $\mathbf{u} \times \mathbf{v} = \mathbf{0}$ 或 $\mathbf{u} = k\mathbf{v}$ |
| 投影 | "projection of $\mathbf{v}$ onto $\mathbf{u}$" | $\text{proj}_{\mathbf{u}}(\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\mathbf{u} \cdot \mathbf{u}} \mathbf{u}$ |
| 求垂直向量 | "perpendicular to both" | 叉积 $\mathbf{u} \times \mathbf{v}$ |
| 平行四边形面积 | "area of parallelogram" | $\|\mathbf{u} \times \mathbf{v}\|$ |
| 三角形面积 | "area of triangle" | $\frac{1}{2}\|\mathbf{u} \times \mathbf{v}\|$ |

### 7.3 直线与平面题型

| 题型 | 关键词 | 方法 |
|------|--------|------|
| 两点确定直线 | "line through $P$ and $Q$" | $\mathbf{x} = P + t(Q - P)$ |
| 三点确定平面 | "plane through $P$, $Q$, $R$" | 求 $\mathbf{u} \times \mathbf{v}$ 得法向量 |
| 点到平面距离 | "distance from point to plane" | $\frac{\|ax_0 + by_0 + cz_0 - d\|}{\sqrt{a^2 + b^2 + c^2}}$ |
| 两平面交线 | "intersection of two planes" | 方向向量 = $\mathbf{n}_1 \times \mathbf{n}_2$ |
| 直线与平面交点 | "intersection of line and plane" | 代入参数方程求 $t$ |

### 7.4 矩阵题型

| 题型 | 关键词 | 方法 |
|------|--------|------|
| 解方程组 | "solve the system" | Gauss-Jordan 消元 |
| 求逆矩阵 | "find $A^{-1}$" | $[A \mid I] \to [I \mid A^{-1}]$ |
| 判断可逆性 | "is $A$ invertible?" | 化为 RREF 看是否为 $I$ |
| 矩阵乘法 | "compute $AB$" | 行乘列 |
| 齐次方程组 | "$A\mathbf{x} = \mathbf{0}$" | 找自由变量，写通解 |

---

## 8. 综合示例题

### 题目 1：复数方程

**题目：** 求方程 $z^4 = 16i$ 的所有复数解。

**解答：**

**Step 1:** 把 $16i$ 写成极坐标形式

$$
16i = 16(\cos\frac{\pi}{2} + i\sin\frac{\pi}{2}) = 16e^{i\pi/2}
$$

**Step 2:** 求模长

$$
|z| = 16^{1/4} = 2
$$

**Step 3:** 求辐角（$k = 0, 1, 2, 3$）

$$
\arg(z) = \frac{\pi/2 + 2\pi k}{4} = \frac{\pi(1 + 4k)}{8}
$$

$$
\begin{aligned}
k = 0: & \quad \theta_0 = \frac{\pi}{8} \\
k = 1: & \quad \tk = 1: & \quad \theta_1 = \frac{\pi}{8} + \frac{\pi}{2} = \frac{5\pi}{8} \\
k = 2: & \quad \theta_2 = \frac{\pi}{8} + \pi = \frac{9\pi}{8} \\
k = 3: & \quad \theta_3 = \frac{\pi}{8} + \frac{3\pi}{2} = \frac{13\pi}{8}
\end{aligned}
$$

**Step 4:** 写出四个根

$$
\begin{aligned}
z_0 &= 2e^{i\pi/8} = 2\left(\cos\frac{\pi}{8} + i\sin\frac{\pi}{8}\right) \\
z_1 &= 2e^{i5\pi/8} = 2\left(\cos\frac{5\pi}{8} + i\sin\frac{5\pi}{8}\right) \\
z_2 &= 2e^{i9\pi/8} = 2\left(\cos\frac{9\pi}{8} + i\sin\frac{9\pi}{8}\right) \\
z_3 &= 2e^{i13\pi/8} = 2\left(\cos\frac{13\pi}{8} + i\sin\frac{13\pi}{8}\right)
\end{aligned}
$$

**答案：** 四个根均匀分布在半径为 2 的圆上，相邻根角度差 $90°$

---

### 题目 2：复数旋转

**题目：** 把复数 $z = 3 + 4i$ 绕原点逆时针旋转 $60°$，求旋转后的复数。

**解答：**

**方法 1：极坐标法**

**Step 1:** 把 $z$ 转换为极坐标

$$
\begin{aligned}
r &= |z| = \sqrt{3^2 + 4^2} = 5 \\
\theta &= \arctan\frac{4}{3} \approx 53.13°
\end{aligned}
$$

**Step 2:** 旋转 $60°$ → 角度增加 $60°$

$$
\theta' = \theta + 60°
$$

**Step 3:** 新复数

$$
z' = 5e^{i(\theta + \pi/3)}
$$

**方法 2：直接乘法**

$$
\begin{aligned}
z' &= z \cdot e^{i\pi/3} \\
&= (3 + 4i) \cdot \left(\cos\frac{\pi}{3} + i\sin\frac{\pi}{3}\right) \\
&= (3 + 4i) \cdot \left(\frac{1}{2} + i\frac{\sqrt{3}}{2}\right) \\
&= 3 \cdot \frac{1}{2} + 3 \cdot i\frac{\sqrt{3}}{2} + 4i \cdot \frac{1}{2} + 4i \cdot i\frac{\sqrt{3}}{2} \\
&= \frac{3}{2} + i\frac{3\sqrt{3}}{2} + 2i - 2\sqrt{3} \\
&= \left(\frac{3}{2} - 2\sqrt{3}\right) + i\left(\frac{3\sqrt{3}}{2} + 2\right) \\
&= \left(\frac{3 - 4\sqrt{3}}{2}\right) + i\left(\frac{3\sqrt{3} + 4}{2}\right)
\end{aligned}
$$

**答案：** $z' = \frac{3 - 4\sqrt{3}}{2} + i\frac{3\sqrt{3} + 4}{2}$

---

### 题目 3：向量投影

**题目：** 已知 $\mathbf{u} = \begin{bmatrix} 2 \\ 1 \\ -1 \end{bmatrix}$，$\mathbf{v} = \begin{bmatrix} 1 \\ 3 \\ 2 \end{bmatrix}$

(a) 求 $\mathbf{v}$ 在 $\mathbf{u}$ 上的投影

(b) 求 $\mathbf{u}$ 和 $\mathbf{v}$ 的夹角

**解答：**

**(a) 投影**

**Step 1:** 计算点积

$$
\mathbf{u} \cdot \mathbf{v} = 2 \cdot 1 + 1 \cdot 3 + (-1) \cdot 2 = 2 + 3 - 2 = 3
$$

**Step 2:** 计算 $\mathbf{u} \cdot \mathbf{u}$

$$
\mathbf{u} \cdot \mathbf{u} = 2^2 + 1^2 + (-1)^2 = 4 + 1 + 1 = 6
$$

**Step 3:** 投影公式

$$
\text{proj}_{\mathbf{u}}(\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\mathbf{u} \cdot \mathbf{u}} \mathbf{u} = \frac{3}{6} \begin{bmatrix} 2 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} 1 \\ 0.5 \\ -0.5 \end{bmatrix}
$$

**答案 (a)：** $\text{proj}_{\mathbf{u}}(\mathbf{v}) = \begin{bmatrix} 1 \\ 1/2 \\ -1/2 \end{bmatrix}$

**(b) 夹角**

**Step 1:** 计算模长

$$
\begin{aligned}
\|\mathbf{u}\| &= \sqrt{6} \\
\|\mathbf{v}\| &= \sqrt{1^2 + 3^2 + 2^2} = \sqrt{14}
\end{aligned}
$$

**Step 2:** 夹角公式

$$
\cos\theta = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|} = \frac{3}{\sqrt{6} \cdot \sqrt{14}} = \frac{3}{\sqrt{84}} = \frac{3}{2\sqrt{21}} = \frac{\sqrt{21}}{14}
$$

**Step 3:** 求角度

$$
\theta = \arccos\left(\frac{\sqrt{21}}{14}\right) \approx 71.07°
$$

**答案 (b)：** $\theta = \arccos\left(\frac{\sqrt{21}}{14}\right) \approx 71.07°$

---

### 题目 4：叉积与面积

**题目：** 已知三角形的三个顶点为 $A(1, 0, 0)$，$B(0, 2, 0)$，$C(0, 0, 3)$

(a) 求三角形的面积

(b) 求垂直于三角形平面的单位向量

**解答：**

**(a) 面积**

**Step 1:** 构造两个边向量

$$
\begin{aligned}
\overrightarrow{AB} &= B - A = \begin{bmatrix} -1 \\ 2 \\ 0 \end{bmatrix} \\
\overrightarrow{AC} &= C - A = \begin{bmatrix} -1 \\ 0 \\ 3 \end{bmatrix}
\end{aligned}
$$

**Step 2:** 计算叉积

$$
\begin{aligned}
\overrightarrow{AB} \times \overrightarrow{AC} &= \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ -1 & 2 & 0 \\ -1 & 0 & 3 \end{vmatrix} \\
&= \mathbf{i}(2 \cdot 3 - 0 \cdot 0) - \mathbf{j}((-1) \cdot 3 - 0 \cdot (-1)) + \mathbf{k}((-1) \cdot 0 - 2 \cdot (-1)) \\
&= \mathbf{i}(6) - \mathbf{j}(-3) + \mathbf{k}(2) \\
&= \begin{bmatrix} 6 \\ 3 \\ 2 \end{bmatrix}
\end{aligned}
$$

**Step 3:** 计算模长

$$
\|\overrightarrow{AB} \times \overrightarrow{AC}\| = \sqrt{6^2 + 3^2 + 2^2} = \sqrt{36 + 9 + 4} = \sqrt{49} = 7
$$

**Step 4:** 三角形面积

$$
\text{Area} = \frac{1}{2}\|\overrightarrow{AB} \times \overrightarrow{AC}\| = \frac{7}{2}
$$

**答案 (a)：** 面积 = $\frac{7}{2}$ 平方单位

**(b) 单位法向量**

$$
\hat{\mathbf{n}} = \frac{\overrightarrow{AB} \times \overrightarrow{AC}}{\|\overrightarrow{AB} \times \overrightarrow{AC}\|} = \frac{1}{7}\begin{bmatrix} 6 \\ 3 \\ 2 \end{bmatrix} = \begin{bmatrix} 6/7 \\ 3/7 \\ 2/7 \end{bmatrix}
$$

**答案 (b)：** $\hat{\mathbf{n}} = \begin{bmatrix} 6/7 \\ 3/7 \\ 2/7 \end{bmatrix}$ 或 $-\hat{\mathbf{n}}$

---

### 题目 5：三点求平面方程

**题目：** 求过三点 $P(1, 2, 3)$，$Q(2, 1, 4)$，$R(3, 3, 2)$ 的平面方程。

**解答：**

**Step 1:** 找两个方向向量

$$
\begin{aligned}
\mathbf{u} &= \overrightarrow{PQ} = Q - P = \begin{bmatrix} 1 \\ -1 \\ 1 \end{bmatrix} \\
\mathbf{v} &= \overrightarrow{PR} = R - P = \begin{bmatrix} 2 \\ 1 \\ -1 \end{bmatrix}
\end{aligned}
$$

**Step 2:** 求法向量（叉积）

$$
\begin{aligned}
\mathbf{n} &= \mathbf{u} \times \mathbf{v} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ 1 & -1 & 1 \\ 2 & 1 & -1 \end{vmatrix} \\
&= \mathbf{i}((-1)(-1) - 1 \cdot 1) - \mathbf{j}(1 \cdot (-1) - 1 \cdot 2) + \mathbf{k}(1 \cdot 1 - (-1) \cdot 2) \\
&= \mathbf{i}(1 - 1) - \mathbf{j}(-1 - 2) + \mathbf{k}(1 + 2) \\
&= \mathbf{i}(0) - \mathbf{j}(-3) + \mathbf{k}(3) \\
&= \begin{bmatrix} 0 \\ 3 \\ 3 \end{bmatrix}
\end{aligned}
$$

简化：$\mathbf{n} = \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}$（除以 3）

**Step 3:** Normal form

$$
\mathbf{n} \cdot (\mathbf{x} - P) = 0
$$

$$
\begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix} \cdot \left(\begin{bmatrix} x \\ y \\ z \end{bmatrix} - \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}\right) = 0
$$

**Step 4:** 展开

$$
0(x - 1) + 1(y - 2) + 1(z - 3) = 0
$$

$$
y - 2 + z - 3 = 0
$$

$$
y + z = 5
$$

**答案：** 平面方程为 $y + z = 5$

---

### 题目 6：两平面的交线

**题目：** 求平面 $\Pi_1: x + y + z = 1$ 和 $\Pi_2: 2x - y + z = 3$ 的交线。

**解答：**

**Step 1:** 找法向量

$$
\mathbf{n}_1 = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}, \quad \mathbf{n}_2 = \begin{bmatrix} 2 \\ -1 \\ 1 \end{bmatrix}
$$

**Step 2:** 交线的方向向量

$$
\begin{aligned}
\mathbf{d} &= \mathbf{n}_1 \times \mathbf{n}_2 = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ 1 & 1 & 1 \\ 2 & -1 & 1 \end{vmatrix} \\
&= \mathbf{i}(1 \cdot 1 - 1 \cdot (-1)) - \mathbf{j}(1 \cdot 1 - 1 \cdot 2) + \mathbf{k}(1 \cdot (-1) - 1 \cdot 2) \\
&= \mathbf{i}(2) - \mathbf{j}(-1) + \mathbf{k}(-3) \\
&= \begin{bmatrix} 2 \\ 1 \\ -3 \end{bmatrix}
\end{aligned}
$$

**Step 3:** 找交线上一点（令 $z = 0$）

$$
\begin{cases}
x + y = 1 \\
2x - y = 3
\end{cases}
$$

从第一个方程：$y = 1 - x$

代入第二个：$2x - (1 - x) = 3 \Rightarrow 3x = 4 \Rightarrow x = \frac{4}{3}$

$$
y = 1 - \frac{4}{3} = -\frac{1}{3}
$$

所以一点为 $P\left(\frac{4}{3}, -\frac{1}{3}, 0\right)$

**Step 4:** 交线方程

$$
\mathbf{x} = \begin{bmatrix} 4/3 \\ -1/3 \\ 0 \end{bmatrix} + t\begin{bmatrix} 2 \\ 1 \\ -3 \end{bmatrix}
$$

**参数方程：**

$$
\begin{cases}
x = \frac{4}{3} + 2t \\
y = -\frac{1}{3} + t \\
z = -3t
\end{cases}
$$

**答案：** $\mathbf{x} = \begin{bmatrix} 4/3 \\ -1/3 \\ 0 \end{bmatrix} + t\begin{bmatrix} 2 \\ 1 \\ -3 \end{bmatrix}$

---

### 题目 7：点到平面的距离

**题目：** 求点 $P(2, 3, 1)$ 到平面 $2x - y + 2z = 5$ 的距离。

**解答：**

**公式：**

$$
d = \frac{|ax_0 + by_0 + cz_0 - d|}{\sqrt{a^2 + b^2 + c^2}}
$$

**代入：**

$$
\begin{aligned}
d &= \frac{|2(2) + (-1)(3) + 2(1) - 5|}{\sqrt{2^2 + (-1)^2 + 2^2}} \\
&= \frac{|4 - 3 + 2 - 5|}{\sqrt{4 + 1 + 4}} \\
&= \frac{|-2|}{\sqrt{9}} \\
&= \frac{2}{3}
\end{aligned}
$$

**答案：** 距离 = $\frac{2}{3}$

---

### 题目 8：解线性方程组

**题目：** 解方程组

$$
\begin{cases}
x + 2y - z = 3 \\
2x + 5y - 2z = 7 \\
3x + 7y - 3z = 10
\end{cases}
$$

**解答：**

**Step 1:** 写增广矩阵

$$
\left[\begin{array}{ccc|c}
1 & 2 & -1 & 3 \\
2 & 5 & -2 & 7 \\
3 & 7 & -3 & 10
\end{array}\right]
$$

**Step 2:** $R_2 \to R_2 - 2R_1$，$R_3 \to R_3 - 3R_1$

$$
\left[\begin{array}{ccc|c}
1 & 2 & -1 & 3 \\
0 & 1 & 0 & 1 \\
0 & 1 & 0 & 1
\end{array}\right]
$$

**Step 3:** $R_3 \to R_3 - R_2$

$$
\left[\begin{array}{ccc|c}
1 & 2 & -1 & 3 \\
0 & 1 & 0 & 1 \\
0 & 0 & 0 & 0
\end{array}\right]
$$

**Step 4:** $R_1 \to R_1 - 2R_2$

$$
\left[\begin{array}{ccc|c}
1 & 0 & -1 & 1 \\
0 & 1 & 0 & 1 \\
0 & 0 & 0 & 0
\end{array}\right]
$$

**Step 5:** 从 RREF 读出方程

$$
\begin{cases}
x - z = 1 \\
y = 1
\end{cases}
$$

**Step 6:** $z$ 是自由变量，令 $z = t$

$$
\begin{cases}
x = 1 + t \\
y = 1 \\
z = t
\end{cases}
$$

**通解：**

$$
\mathbf{x} = \begin{bmatrix} 1 + t \\ 1 \\ t \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} + t\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}, \quad t \in \mathbb{R}
$$

**答案：** 无穷多解，通解为 $\mathbf{x} = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} + t\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}$

---

### 题目 9：求逆矩阵

**题目：** 求矩阵 $A = \begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 5 & 6 & 0 \end{bmatrix}$ 的逆矩阵。

**解答：**

**Step 1:** 构造 $[A \mid I]$

$$
\left[\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 4 & 0 & 1 & 0 \\
5 & 6 & 0 & 0 & 0 & 1
\end{array}\right]
$$

**Step 2:** $R_3 \to R_3 - 5R_1$

$$
\left[\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 4 & 0 & 1 & 0 \\
0 & -4 & -15 & -5 & 0 & 1
\end{array}\right]
$$

**Step 3:** $R_3 \to R_3 + 4R_2$

$$
\left[\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 4 & 0 & 1 & 0 \\
0 & 0 & 1 & -5 & 4 & 1
\end{array}\right]
$$

**Step 4:** $R_2 \to R_2 - 4R_3$

$$
\left[\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 0 & 20 & -15 & -4 \\
0 & 0 & 1 & -5 & 4 & 1
\end{array}\right]
$$

**Step 5:** $R_1 \to R_1 - 3R_3$

$$
\left[\begin{array}{ccc|ccc}
1 & 2 & 0 & 16 & -12 & -3 \\
0 & 1 & 0 & 20 & -15 & -4 \\
0 & 0 & 1 & -5 & 4 & 1
\end{array}\right]
$$

**Step 6:** $R_1 \to R_1 - 2R_2$

$$
\left[\begin{array}{ccc|ccc}
1 & 0 & 0 & -24 & 18 & 5 \\
0 & 1 & 0 & 20 & -15 & -4 \\
0 & 0 & 1 & -5 & 4 & 1
\end{array}\right]
$$

**答案：**

$$
A^{-1} = \begin{bmatrix} -24 & 18 & 5 \\ 20 & -15 & -4 \\ -5 & 4 & 1 \end{bmatrix}
$$

---

### 题目 10：综合应用题

**题目：** 已知向量 $\mathbf{a} = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$，$\mathbf{b} = \begin{bmatrix} 2 \\ -1 \\ 1 \end{bmatrix}$

(a) 求 $\mathbf{a}$ 和 $\mathbf{b}$ 的夹角

(b) 求垂直于 $\mathbf{a}$ 和 $\mathbf{b}$ 的单位向量

(c) 求过原点且包含 $\mathbf{a}$ 和 $\mathbf{b}$ 的平面方程

(d) 求点 $P(1, 1, 1)$ 到该平面的距离

**解答：**

**(a) 夹角**

**Step 1:** 计算点积

$$
\mathbf{a} \cdot \mathbf{b} = 1(2) + 2(-1) + 3(1) = 2 - 2 + 3 = 3
$$

**Step 2:** 计算模长

$$
\begin{aligned}
\|\mathbf{a}\| &= \sqrt{1^2 + 2^2 + 3^2} = \sqrt{14} \\
\|\mathbf{b}\| &= \sqrt{2^2 + (-1)^2 + 1^2} = \sqrt{6}
\end{aligned}
$$

**Step 3:** 夹角

$$
\cos\theta = \frac{3}{\sqrt{14} \cdot \sqrt{6}} = \frac{3}{\sqrt{84}} = \frac{3}{2\sqrt{21}} = \frac{\sqrt{21}}{14}
$$

$$
\theta = \arccos\left(\frac{\sqrt{21}}{14}\right) \approx 71.07°
$$

**答案 (a)：** $\theta \approx 71.07°$

**(b) 垂直单位向量**

**Step 1:** 叉积

$$
\begin{aligned}
\mathbf{n} &= \mathbf{a} \times \mathbf{b} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ 1 & 2 & 3 \\ 2 & -1 & 1 \end{vmatrix} \\
&= \mathbf{i}(2 \cdot 1 - 3 \cdot (-1)) - \mathbf{j}(1 \cdot 1 - 3 \cdot 2) + \mathbf{k}(1 \cdot (-1) - 2 \cdot 2) \\
&= \mathbf{i}(2 + 3) - \mathbf{j}(1 - 6) + \mathbf{k}(-1 - 4) \\
&= 5\mathbf{i} + 5\mathbf{j} - 5\mathbf{k} \\
&= \begin{bmatrix} 5 \\ 5 \\ -5 \end{bmatrix}
\end{aligned}
$$

**Step 2:** 单位化

$$
\|\mathbf{n}\| = \sqrt{5^2 + 5^2 + (-5)^2} = \sqrt{75} = 5\sqrt{3}
$$

$$
\hat{\mathbf{n}} = \frac{1}{5\sqrt{3}}\begin{bmatrix} 5 \\ 5 \\ -5 \end{bmatrix} = \frac{1}{\sqrt{3}}\begin{bmatrix} 1 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} \frac{\sqrt{3}}{3} \\ \frac{\sqrt{3}}{3} \\ -\frac{\sqrt{3}}{3} \end{bmatrix}
$$

**答案 (b)：** $\hat{\mathbf{n}} = \frac{1}{\sqrt{3}}\begin{bmatrix} 1 \\ 1 \\ -1 \end{bmatrix}$ 或 $-\hat{\mathbf{n}}$

**(c) 平面方程**
平面过原点，法向量为 $\mathbf{n} = \begin{bmatrix} 1 \\ 1 \\ -1 \end{bmatrix}$（简化后）

**Normal form:**

$$
\mathbf{n} \cdot \mathbf{x} = 0
$$

$$
\begin{bmatrix} 1 \\ 1 \\ -1 \end{bmatrix} \cdot \begin{bmatrix} x \\ y \\ z \end{bmatrix} = 0
$$

**General equation:**

$$
x + y - z = 0
$$

**答案 (c)：** 平面方程为 $x + y - z = 0$

**(d) 点到平面距离**

**公式：**

$$
d = \frac{|ax_0 + by_0 + cz_0 - d|}{\sqrt{a^2 + b^2 + c^2}}
$$

**代入** $P(1, 1, 1)$，平面 $x + y - z = 0$：

$$
\begin{aligned}
d &= \frac{|1(1) + 1(1) + (-1)(1) - 0|}{\sqrt{1^2 + 1^2 + (-1)^2}} \\
&= \frac{|1 + 1 - 1|}{\sqrt{3}} \\
&= \frac{1}{\sqrt{3}} \\
&= \frac{\sqrt{3}}{3}
\end{aligned}
$$

**答案 (d)：** 距离 = $\frac{\sqrt{3}}{3}$

---

## 9. 易错点总结

### 9.1 复数

| 错误 | 正确 |
|------|------|
| 算 $z^n$ 的根时忘记加 $2\pi k$ | 必须考虑所有 $k = 0, 1, \ldots, n-1$ |
| 混淆顺时针和逆时针 | 乘 $e^{i\theta}$ 是逆时针，乘 $e^{-i\theta}$ 是顺时针 |
| 辐角范围搞错 | 通常取 $\theta \in [0, 2\pi)$ 或 $(-\pi, \pi]$ |

### 9.2 向量

| 错误 | 正确 |
|------|------|
| 投影方向搞反 | $\text{proj}_{\mathbf{u}}(\mathbf{v}) \neq \text{proj}_{\mathbf{v}}(\mathbf{u})$ |
| 叉积顺序写反 | $\mathbf{u} \times \mathbf{v} = -(\mathbf{v} \times \mathbf{u})$ |
| 叉积行列式 $\mathbf{j}$ 项忘了取负 | 中间一项是 $-\mathbf{j}(\cdots)$ |
| 三角形面积忘了 $\frac{1}{2}$ | $\text{Area}_{\triangle} = \frac{1}{2}\|\mathbf{u} \times \mathbf{v}\|$ |

### 9.3 平面与直线

| 错误 | 正确 |
|------|------|
| 三点求平面用了三个向量 | 只需两个方向向量 $\overrightarrow{PQ}$ 和 $\overrightarrow{PR}$ |
| 点到平面距离忘了取绝对值 | 必须 $|ax_0 + by_0 + cz_0 - d|$ |
| 两平面交线方向用了点积 | 用叉积 $\mathbf{n}_1 \times \mathbf{n}_2$ |

### 9.4 矩阵

| 错误 | 正确 |
|------|------|
| 矩阵乘法当成可交换 | 一般 $AB \neq BA$ |
| $(AB)^{-1} = A^{-1}B^{-1}$ | 应为 $(AB)^{-1} = B^{-1}A^{-1}$ |
| $(AB)^T = A^T B^T$ | 应为 $(AB)^T = B^T A^T$ |
| RREF 没化彻底 | Pivot 必须为 1 且该列其他元素必须为 0 |
| 求逆矩阵忘了除以行列式 | $2\times 2$ 公式必须乘 $\frac{1}{ad-bc}$ |

---

## 10. 重要公式速查表

### 复数

$$
\boxed{
\begin{aligned}
& z = x + iy = re^{i\theta} \\
& |z| = \sqrt{x^2 + y^2} \\
& e^{i\theta} = \cos\theta + i\sin\theta \\
& (e^{i\theta})^n = e^{in\theta} \\
& z^n = \alpha \Rightarrow z_k = |\alpha|^{1/n} e^{i(\arg\alpha + 2\pi k)/n}
\end{aligned}
}
$$

### 向量

$$
\boxed{
\begin{aligned}
& \mathbf{u} \cdot \mathbf{v} = u_1v_1 + u_2v_2 + u_3v_3 = \|\mathbf{u}\|\|\mathbf{v}\|\cos\theta \\
& \|\mathbf{u} \times \mathbf{v}\| = \|\mathbf{u}\|\|\mathbf{v}\|\sin\theta \\
& \text{proj}_{\mathbf{u}}(\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\mathbf{u} \cdot \mathbf{u}} \mathbf{u} \\
& \text{Area}_{\parallel} = \|\mathbf{u} \times \mathbf{v}\|, \quad \text{Area}_{\triangle} = \frac{1}{2}\|\mathbf{u} \times \mathbf{v}\|
\end{aligned}
}
$$

### 直线与平面

$$
\boxed{
\begin{aligned}
& \text{直线: } \mathbf{x} = \mathbf{p} + t\mathbf{d} \\
& \text{平面: } \mathbf{n} \cdot (\mathbf{x} - \mathbf{p}) = 0 \quad \text{或} \quad ax + by + cz = d \\
& \text{三点求平面: } \mathbf{n} = (Q-P) \times (R-P) \\
& \text{点到平面距离: } d = \frac{|ax_0 + by_0 + cz_0 - d|}{\sqrt{a^2 + b^2 + c^2}}
\end{aligned}
}
$$

### 矩阵

$$
\boxed{
\begin{aligned}
& (AB)^T = B^T A^T \\
& (AB)^{-1} = B^{-1}A^{-1} \\
& A^{-1} = \frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix} \quad (2\times 2) \\
& [A \mid I] \xrightarrow{\text{Row Reduce}} [I \mid A^{-1}] \\
& A\mathbf{x} = \mathbf{b} \Rightarrow \mathbf{x} = A^{-1}\mathbf{b}
\end{aligned}
}
$$

### 旋转矩阵

$$
\boxed{
R(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}
}
$$

---

## 11. 考前检查清单

### 复数部分 ✅

- [ ] 能把复数在三种形式间互转（$a+bi$、极坐标、$re^{i\theta}$）
- [ ] 会用 De Moivre 公式求 $z^n = \alpha$ 的所有根
- [ ] 理解乘以 $e^{i\theta}$ 等于旋转
- [ ] 会写旋转矩阵（注意 $-\sin\theta$ 的位置）

### 向量部分 ✅

- [ ] 会计算点积、叉积
- [ ] 会用点积判断垂直、求夹角
- [ ] 会用叉积求垂直向量、求面积
- [ ] 会算投影（注意分母是哪个向量自己点积）

### 直线平面部分 ✅

- [ ] 会用两点写直线方程
- [ ] 会用三点求平面方程（叉积求法向量）
- [ ] 会求两平面交线
- [ ] 会求点到平面距离

### 矩阵部分 ✅

- [ ] 会做矩阵加减乘
- [ ] 会用 Gauss-Jordan 解方程组
- [ ] 会判断方程组解的类型（唯一/无穷多/无解）
- [ ] 会写齐次方程组的通解（自由变量法）
- [ ] 会用 $[A|I] \to [I|A^{-1}]$ 求逆矩阵
- [ ] 会用 $2\times 2$ 公式快速求逆
- [ ] 记住 $(AB)^{-1} = B^{-1}A^{-1}$、$(AB)^T = B^T A^T$

---

## 12. 学习建议

### 12.1 复习顺序

**第一阶段（基础）：**
1. 复数的运算和极坐标
2. 向量的点积、叉积
3. 矩阵的基本运算

**第二阶段（核心方法）：**
1. Gauss-Jordan 消元法
2. 求逆矩阵
3. 三点求平面

**第三阶段（综合应用）：**
1. 用矩阵解方程组
2. 几何应用（距离、面积、角度）
3. 综合题练习

### 12.2 做题策略

1. **先看题目要求什么**，再决定用哪个公式
2. **画图辅助理解**，尤其是向量和复数题
3. **检查答案合理性**：模长是否为正、角度是否在合理范围
4. **多写几步**，行操作清楚标注 $R_2 \to R_2 - 2R_1$

### 12.3 时间分配建议

- 复数旋转：每天 15 分钟练习
- Row Reduction：每天 2 道题
- 求逆矩阵：每天 1 道 $3\times 3$
- 综合题：每周 3-5 道

---

**🎯 复习完成！祝考试顺利！**

> 📌 **重点回顾：** 复数极坐标 + 旋转 → 向量点积叉积投影 → 三点求平面 → Gauss-Jordan 解方程 + 求逆矩阵

