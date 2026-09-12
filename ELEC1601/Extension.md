
## 一、精度与误差 · Precision & Rounding Error

**原理｜Principle**

小数点后 n 位，最小刻度（LSB 权重）为 $2^{-n}$。

| 存储方式 Storage | 最坏误差 Worst-case error |
|---|---|
| 截断 Truncate | $2^{-n}$（一个刻度） |
| 舍入 Round | $2^{-(n+1)}$（半个刻度） |

> 题目说 "rounding error" 用半刻度；只说"最多偏多少"按截断。

**例题｜Example**
> 4 个二进制小数位，最坏舍入误差是多少？
> *4 fractional bits, what's the worst-case rounding error?*

$$2^{-(4+1)} = 2^{-5} = 0.03125 \approx \boxed{0.0313}$$

---

## 二、整数范围需要几位 · Bits for an Integer Range

**原理｜Principle**

数区间内整数个数 $= b - a + 1$（含两端，别忘 +1），再找最小 N 使 $2^N \ge$ 个数。

**例题｜Example**
> 表示 [53, 100]，要几位？
> *Represent [53, 100], how many bits?*

$$100 - 53 + 1 = 48,\quad 2^5=32<48,\quad 2^6=64\ge48 \Rightarrow \boxed{6}$$

---

## 三、定标法 · Scaling

**原理｜Principle**

N 位只能存 $0 \sim 2^N-1$，乘一个 **2 的幂** $s$ 覆盖更大范围。取**能覆盖目标的、最小的 2 的幂**（越小误差越小）。误差 $= s/2$。

**例题｜Example**
> 4 位、范围 [0, 137]，最优缩放因子？
> *4 bits, range [0, 137], best scaling factor?*

$$15s \ge 137 \Rightarrow s \ge 9.13 \Rightarrow s = 2^4 = \boxed{16}$$

---

## 四、多量打包（混合基数）· Packing (Mixed-Radix)

**原理｜Principle**

每个量算取值个数 → **全部相乘**得组合总数 T → 最小 N 使 $2^N \ge T$。
**是乘法，不是把各自位数相加。**

**例题｜Example**
> 三个测量 [0,40]、[0,43]、[0,483] 打包，要几位？
> *Pack three measurements, how many bits?*

$$41 \times 44 \times 484 = 873{,}136,\quad 2^{19}=524{,}288 < T,\quad 2^{20}\ge T \Rightarrow \boxed{20}$$

---

## 五、定点补码所需位数 · Fixed-Point Two's Complement Bits

**原理｜Principle**

- **小数位 f**：由误差定，$2^{-f} \le \varepsilon$（截断）
- **整数位 i**：由范围定，补码 i 位范围 $[-2^{\,i-1},\ 2^{\,i-1}-1]$
- **总位数 = i + f**

**例题｜Example**
> 补码定点表示 [−10, 18]，误差 0.125，不用 bias，要几位？
> *Two's complement fixed-point, [−10, 18], error 0.125, no bias, how many bits?*

$$0.125 = 2^{-3} \Rightarrow f = 3;\quad 2^{\,i-1}-1 \ge 18 \Rightarrow 2^{\,i-1}\ge19 \Rightarrow i=6$$
$$i + f = 6 + 3 = \boxed{9}$$

---

## 六、负数转定点补码 · Negative → Two's Complement

**原理｜Principle**

铁律：**先 ×2ᶠ 变整数，再整体求补码**。求负数补码：正数**取反加一**。
**切勿**把整数部分、小数部分分开算再拼。

**例题｜Example**
> 用 6 整数位 + 2 小数位，把 −2.25 写成补码。
> *Convert −2.25, 6 integer + 2 fractional bits.*

$$-2.25 \times 4 = -9;\quad 9=00001001 \xrightarrow{\text{取反}} 11110110 \xrightarrow{+1} \boxed{11110111}$$

---

## 七、自定义浮点解码 · Custom Floating-Point Decode

**原理｜Principle**

切三段 `符号 | 指数 | 尾数`：符号定正负；尾数补上**隐含位**后转十进制；指数**减偏置**（$2^{k-1}-1$）后作 2 的幂相乘。

$$\text{值} = \text{符号} \times \text{尾数} \times 2^{\text{真实指数}}$$

**例题｜Example**
> `0 110 1011`，隐含位 1，求十进制值。
> *`0 110 1011`, implicit leading 1, decimal value?*

$$0.110\,1011:\quad 1.1011_2 = 1.6875;\quad E = 6 - 3 = 3$$
$$1.6875 \times 2^3 = \boxed{13.5}$$

---

