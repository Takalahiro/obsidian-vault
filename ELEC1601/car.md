先回答你的问题:**你贴的这段文字,是"Essential(基础必做)"部分的完整要求。** 它从 Overview 一直写到场景 9/10,覆盖了:硬件、LED 编码规则、每个场景的判据和动作、时间约束。但要提醒你两点:

- 这是项目说明,不是**评分细则(rubric)**。打分点(每个场景各占多少分、动作精度怎么判)不在这段文字里。
- Extension 和 Advanced 的迷宫要求**只提了一句**(要 nav 整个迷宫 + 挑战性起始位置),具体规则没在这段里。所以别以为"做完这 11 个场景就完事了"。

下面把我从这段文字里抽出的**完整要求清单**给出来,再给你一份可以直接贴到笔记本上、喂给另一个 AI 的**交接文档(文字段 + 代码段)**。

---

## 一、要求清单(从你贴的文字抽取)

**通用规则(每个场景都适用)**
1. 用 3 个 LED 显示二进制场景号,再执行动作。
2. 显示后必须**静止至少 5 秒**,让老师看清编码。
3. 5 秒后 LED 可随意。
4. 完成一套舵机动作,脱离该位置。
5. 可逐个场景验收;但建议合成一份代码。
6. 场景 0/1 的 LED 是"关灯"表示,别漏。

**LED 编码表**(R=A0, M=A1, L=A2)

| 场景 | R(A0) | M(A1) | L(A2) | 判据 | 动作 |
|---|---|---|---|---|---|
| 0 未知 | 灭 | 灭 | 灭 | 都不是 | **完全不动** |
| 1 走廊 | 亮 | 灭 | 灭 | 左≈右,前≥10cm或无墙 | 前进5cm,保持平行居中(偏差<3cm),停 |
| 2 右转位 | 灭 | 亮 | 灭 | 右无墙,左有墙,前有墙 | 转90°,前进,回走廊,停 |
| 3 左转位 | 亮 | 亮 | 灭 | 左无墙,右有墙,前有墙 | 转90°,前进,回走廊,停 |
| 4 死路 | 灭 | 灭 | 亮 | 左+前+右都有墙 | 转180°,前进≥5cm,停 |
| 5 贴左墙平行 | 亮 | 灭 | 亮 | 左右都有墙,右侧更近,前远 | 微右转→前进→微左转回平行→后退归位 |
| 6 贴右墙平行 | 灭 | 亮 | 亮 | 左右都有墙,左侧更近,前远 | 微左转→前进→微右转回平行→后退归位 |
| 7 贴左墙~30° | 亮 | 亮 | 亮 | 左近+前近,右远墙 | 微右转至平行 |
| 8 贴右墙~30° | R闪1s | 灭 | 灭 | 右近+前近,左远墙 | 微左转至平行 |
| 9 自定义 | 灭 | M闪1s | 灭 | 你定 | 你定 |
| 10 自定义 | R闪1s | M闪1s | 灭 | 你定 | 你定 |

**必须达到的关键难点**
- 场景 7/8 必须能和 1/2 **区分开**(斜对墙时前传感器也变近)。
- 场景 5/6 要能判断"哪一侧明显更近"。
- 所有动作后:居中偏差 <3cm,约平行。

**约束**
- 走廊宽 20cm,车轮每侧超出机体约 2cm。
- take-home board 传感器**水平**排列,机器人上**垂直**排列 → 读数不同,实验室要重校。
- 第 12 周完成,第 13 周验收;达不到 essential 会挂科。

---

## 二、交接文档 · 文字段(整段复制,贴给另一个 AI)

```
【项目背景】
我正在做 ELEC1601 的机器人迷宫项目(Essential 部分)。
机器人有 3 个 IR 传感器:左、前、右。我目前只有"take-home board"
(没有舵机和轮子),所以现阶段只能开发和验证"传感器感知/场景识别"部分,
舵机动作留到实验室再调。

【硬件引脚】(以 shield 顶部表格为准,以下是当前代码所用)
左: IR-LED=10, 接收=11, 红LED=A2
右: IR-LED=2,  接收=3,  红LED=A0
前: IR-LED=6,  接收=7,  红LED=A1
LED 语义: A0=右, A1=中(前), A2=左

【红外频率】
左 41300, 右 42300, 前 44300 (单位 Hz)

【检测原理】
tone()发射IR -> digitalRead 接收脚,接收=LOW 视为"被反射回来"(有墙)。
采样 N 次,统计 LOW 次数 = strength(0~N),strength 越大表示墙越近。

【LED 编码】(R=A0, M=A1, L=A2) 0=灭,1=亮,FLASH=1秒间隔闪烁
场景0: 000   场景1: 100   场景2: 010   场景3: 110
场景4: 001   场景5: 101   场景6: 011   场景7: 111
场景8: R闪,M灭,L灭   场景9: M闪   场景10: R闪+M闪

【每个场景通用流程】
1) 识别场景 -> 2) 显示对应LED -> 3) 静止>=5秒 -> 4) 执行脱离动作 -> 5) 停

【场景判据与动作】(精简)
0 未知: 都不匹配 -> 不动
1 走廊: 左≈右 且 前方远/无墙 -> 前进5cm,保持平行居中(偏差<3cm)
2 右转位: 右无墙, 左有墙, 前有墙 -> 右转90°,前进,回走廊
3 左转位: 左无墙, 右有墙, 前有墙 -> 左转90°,前进,回走廊
4 死路: 左+前+右都有墙 -> 转180°,前进>=5cm
5 贴左墙平行: 左右都有墙且右侧更近, 前远 -> 微调+前进+回正
6 贴右墙平行: 左右都有墙且左侧更近, 前远 -> 微调+前进+回正
7 贴左墙30度: 左近+前近, 右远 -> 微右转至平行
8 贴右墙30度: 右近+前近, 左远 -> 微左转至平行

【难点】7/8 必须能和 1/2 区分(斜对墙时前方传感器也变近)。

【我当前的需求】
帮我完善"传感器校准 + 场景识别"这部分代码。我现在不想用厘米做绝对
校准,想用"检测边缘 + 相对比较(谁更近/有没有墙)"来实现判断。
代码里请留出阈值常量,方便我实测后填。
```

---

## 三、交接文档 · 代码段(整段复制,贴给另一个 AI 当基础)

```cpp
// ============================================================
// ELEC1601 迷宫项目 - 传感器感知 / 场景识别 骨架
// 现阶段：只用 take-home board 验证"识别 + LED 显示"
// 舵机动作暂用桩函数，到实验室再填
// ============================================================

// ---- 引脚 ----
const int leftIrLedPin       = 10;
const int leftIrReceiverPin  = 11;
const int leftRedLedPin      = A2;

const int rightIrLedPin      = 2;
const int rightIrReceiverPin = 3;
const int rightRedLedPin     = A0;

const int frontIrLedPin      = 6;
const int frontIrReceiverPin = 7;
const int frontRedLedPin     = A1;

// ---- 红外频率 ----
const long LEFT_FREQ  = 41300;
const long RIGHT_FREQ = 42300;
const long FRONT_FREQ = 44300;

// ---- 采样 ----
const int sampleCount = 30;      // 可调，越大越稳

// ---- 阈值（占位：必须用实测值填！）----
// EDGE  = “有墙”的下限（strength 超过它就认为有墙）
// MARGIN= 抗抖余量，用于判断“明显更近/相近”
const int EDGE   = 5;    // TODO 实测
const int MARGIN = 4;    // TODO 实测

// ---- 测量 ----
int measure(int ledPin, int receiverPin, long freq) {
  int count = 0;
  for (int i = 0; i < sampleCount; i++) {
    tone(ledPin, freq);
    delay(2);
    if (digitalRead(receiverPin) == LOW) count++;
    noTone(ledPin);
    delay(2);
  }
  return count;
}

// ---- 相对算子（不用 cm）----
bool blocked(int v)          { return v > EDGE; }               // 有墙
bool muchCloser(int a, int b){ return a > b + MARGIN; }         // a 明显比 b 近
bool similar(int a, int b)   { return abs(a - b) <= MARGIN; }   // 差不多

// ---- LED ----
void clearLeds() {
  digitalWrite(rightRedLedPin, LOW);
  digitalWrite(frontRedLedPin, LOW);
  digitalWrite(leftRedLedPin, LOW);
}
void flashLed(int pin, unsigned long interval) {
  digitalWrite(pin, HIGH); delay(interval);
  digitalWrite(pin, LOW);  delay(interval);
}
void showScenario(int s) {
  clearLeds();
  switch (s) {
    case 0: break;                                  // 000
    case 1: digitalWrite(rightRedLedPin, HIGH); break;                    // 100
    case 2: digitalWrite(frontRedLedPin, HIGH); break;                    // 010
    case 3: digitalWrite(rightRedLedPin, HIGH);
            digitalWrite(frontRedLedPin, HIGH); break;                    // 110
    case 4: digitalWrite(leftRedLedPin, HIGH); break;                     // 001
    case 5: digitalWrite(rightRedLedPin, HIGH);
            digitalWrite(leftRedLedPin, HIGH); break;                     // 101
    case 6: digitalWrite(frontRedLedPin, HIGH);
            digitalWrite(leftRedLedPin, HIGH); break;                     // 011
    case 7: digitalWrite(rightRedLedPin, HIGH);
            digitalWrite(frontRedLedPin, HIGH);
            digitalWrite(leftRedLedPin, HIGH); break;                     // 111
    case 8: flashLed(rightRedLedPin, 1000); break;   // R 闪 1s
    case 9: flashLed(frontRedLedPin, 1000); break;   // M 闪 1s
    case 10: flashLed(rightRedLedPin, 1000);
             flashLed(frontRedLedPin, 1000); break;  // R+M 闪
  }
  // 显示后静止 5 秒（闪烁场景除外，闪烁本身已耗时）
  if (s <= 7) delay(5000);
}

// ---- 场景识别（骨架：请按实测继续完善）----
int detectScenario(int F, int L, int R) {
  bool fB = blocked(F), lB = blocked(L), rB = blocked(R);

  // 优先级：先排除 7/8（斜对墙），避免被误判成 1/2！
  // 7: 左近+前近，右远    8: 右近+前近，左远
  if (fB && lB && !rB && muchCloser(L, R)) return 7;
  if (fB && rB && !lB && muchCloser(R, L)) return 8;

  // 4 死路
  if (fB && lB && rB) return 4;

  // 2 右转位 / 3 左转位
  if (fB && lB && !rB) return 2;
  if (fB && !lB && rB) return 3;

  // 5 贴左墙平行 / 6 贴右墙平行
  // 注意：作业说“场景5=贴左墙时右传感器更近”，请按实测确认方向！
  if (!fB && lB && rB) {
    if (muchCloser(R, L)) return 5;
    if (muchCloser(L, R)) return 6;
    if (similar(L, R))    return 1;   // 左右等距 -> 走廊
  }

  // 1 走廊：左右都有墙且相近，前方远
  if (!fB && lB && rB && similar(L, R)) return 1;

  return 0;
}

// ---- 舵机动作：桩函数（到实验室填）----
void doScenario(int s) {
  // TODO: 用 Servo 实现每个场景的脱离动作
}

void setup() {
  Serial.begin(9600);
  pinMode(leftIrLedPin, OUTPUT);   pinMode(leftIrReceiverPin, INPUT);
  pinMode(rightIrLedPin, OUTPUT);  pinMode(rightIrReceiverPin, INPUT);
  pinMode(frontIrLedPin, OUTPUT);  pinMode(frontIrReceiverPin, INPUT);
  pinMode(leftRedLedPin, OUTPUT);
  pinMode(rightRedLedPin, OUTPUT);
  pinMode(frontRedLedPin, OUTPUT);
  clearLeds();
}

void loop() {
  int F = measure(frontIrLedPin, frontIrReceiverPin, FRONT_FREQ);
  int L = measure(leftIrLedPin,  leftIrReceiverPin,  LEFT_FREQ);
  int R = measure(rightIrLedPin, rightIrReceiverPin, RIGHT_FREQ);

  Serial.print("L="); Serial.print(L);
  Serial.print(" F="); Serial.print(F);
  Serial.print(" R="); Serial.print(R);

  int s = detectScenario(F, L, R);
  Serial.print("  -> scenario "); Serial.println(s);

  showScenario(s);
  // doScenario(s);   // 实验室再打开
  delay(300);
}
```

把**文字段 + 代码段**一起贴到笔记本那台 AI 上,它就拿到了和你现在完全一样的上下文,可以无缝接着帮你调。

建议明天第一件事还是:烧录这个骨架 → 开串口 → 用白纸找出 `EDGE`,再摆几个姿势确定 5/6/7/8 的方向,回来告诉我实测数,我们就能把阈值和判断彻底定死。
对,这个限制反而更好——**逐个扫,比三个一起扫更准**,因为不会互相串扰,而且每个传感器能有独立的 base/peak。把校准改成"按键驱动、一个一个来"就行。

## 核心思路

不要用"固定 3 秒同时扫",改成**每个传感器一个独立的采集窗口**:

1. 提示:"前传感器:把纸由远到近慢慢扫,扫完按回车"
2. 程序不断读这个传感器,实时更新它的 min/max,**一直等到你按回车**才结束
3. 存下 base=min、peak=max,切下一个传感器

好处:你有充足时间,单人也从容;每个传感器的窗口互不干扰。

## 替换掉原来的 calibrate()

```cpp
// 单个传感器的采集：实时更新 base/peak，直到串口收到一个字符
void calibrateOne(int i, const char* name) {
  Serial.print(name);
  Serial.println(": 把白纸由远到近慢慢扫, 扫完在串口输入框敲个回车...");

  baseV[i] = 1024;     // 先置成极端值，好让 min 能更新
  peakV[i] = 0;

  while (Serial.available()) Serial.read();   // 清掉残留输入

  unsigned long t0 = millis();
  while (millis() - t0 < 300) {               // 先空转 0.3s，避免手还没准备好
    oneRead(i);
  }

  while (true) {
    int v = oneRead(i);
    if (v < baseV[i]) baseV[i] = v;
    if (v > peakV[i]) peakV[i] = v;

    Serial.print("  当前="); Serial.print(v);
    Serial.print("  min=");  Serial.print(baseV[i]);
    Serial.print("  max=");  Serial.println(peakV[i]);

    if (Serial.available()) {                 // 收到回车/任意键 -> 结束这个传感器
      while (Serial.available()) Serial.read();
      break;
    }
  }
  Serial.print(name); Serial.print(" 校准完成: base=");
  Serial.print(baseV[i]); Serial.print(" peak=");
  Serial.println(peakV[i]);
}

void calibrate() {
  calibrateOne(1, "前");   // 按你说的顺序：先前
  calibrateOne(0, "左");   // 再左
  calibrateOne(2, "右");   // 最后右
}
```

索引沿用之前约定:**0=左, 1=前, 2=右**,所以 `calibrateOne(1,...)` 是前,`(0,...)` 是左,`(2,...)` 是右。

## 操作步骤(明天照做)

1. 烧录,开**串口监视器**,波特率 9600。
2. 看到 `前: 把白纸...` → 拿白纸,先放**很远**(传感器读 0 附近),再**慢慢移近到贴住**,来回扫几遍。
3. 盯串口看 `min/max` 有没有更新到位,然后在下方的输入框敲个**回车**发送。
4. 自动跳到 `左:` → 同样扫一遍,回车。
5. 再 `右:` → 扫一遍,回车。三个都完成就进主循环。

## 几个单人操作的小提醒

- **扫纸只动纸,别动板子**——板子一动,之前扫的基准就偏了。
- base 一定要在"完全没墙"的位置取到:第一次放纸前,把纸拿开,让读数先落到 0。
- peak 要真正贴到墙(约 1–2cm 内),否则归一化的上限偏低,后面"有墙"的判定会虚高。
- 如果你输入框回车它没反应,检查串口监视器右下角的**行结尾**设置(选 "Newline" 或 "回车")。
- 三个都扫完后,如果发现某个 `base` 和 `peak` 太接近(比如差不到 5),说明那一路没扫好,重开一次单独补扫即可。

## 和主程序怎么接

`setup()` 里保持调用 `calibrate();` 即可,其余(归一化、查表、N 次确认)都不用改。串口监视器在你扫完后还能继续用,`loop()` 里那些 `L=/F=/R=/idx=` 的打印正好拿来现场摆姿势、填 `table[8]`。

这样你一个人、一只纸、一台笔记本就能把三路校准走完。扫完后把三组 `base/peak` 发我,我帮你核一下数值合不合理,顺便把 5/6/7/8 那几条比值规则补上。


可以，而且这个功能很有用——校准完成后，你可以用同一个串口监视器来**实时验证每个姿势被识别成哪个场景**，相当于在家就把"演示给老师看"的流程跑一遍。

下面是完整的代码，把之前的骨架加上"场景对照表"的串口输出：

```cpp
// ============================================================
// ELEC1601 迷宫项目 - 传感器感知 / 场景识别
// 含：逐个自校准 + 归一化 + 查表 + 串口实时输出场景表格
// ============================================================

const int emitP[3] = {10, 6, 2};       // 0=左, 1=前, 2=右 发射
const int recvP[3] = {11, 7, 3};       // 0=左, 1=前, 2=右 接收
const long freqV[3] = {41300, 44300, 42300};

const int rLedR = A0, rLedM = A1, rLedL = A2;

const int N = 30;

int baseV[3] = {0, 0, 0};
int peakV[3] = {1, 1, 1};

// 迟滞阈值（百分比，归一化后 0~100）
const int NEAR_ON  = 60;
const int NEAR_OFF = 40;

// 场景查表：idx = (Lb<<2)|(Fb<<1)|Rb
// 0=左, 1=前, 2=右 对应 bit2, bit1, bit0
int table[8] = {
  0,  // 000 三面无墙 -> 未知
  1,  // 001 仅右有墙 -> TODO 摆姿势后填
  1,  // 010 仅前有墙 -> TODO
  3,  // 011 右+前    -> 疑左转位(场景3)/场景8，需实测
  1,  // 100 仅左有墙 -> TODO
  1,  // 101 左+右    -> 走廊(场景1)，细分5/6/7/8靠比值
  2,  // 110 左+前    -> 疑右转位(场景2)/场景7，需实测
  4   // 111 三面有墙 -> 死路(场景4)
};

const char* scenarioName[11] = {
  "0  未知(停止)",
  "1  走廊直行",
  "2  右转位",
  "3  左转位",
  "4  死路(180转)",
  "5  贴左墙平行",
  "6  贴右墙平行",
  "7  贴左墙~30度",
  "8  贴右墙~30度",
  "9  自定义A",
  "10 自定义B"
};

// ---- 测量 ----
int oneRead(int i) {
  int c = 0;
  for (int k = 0; k < N; k++) {
    tone(emitP[i], freqV[i]); delay(2);
    if (digitalRead(recvP[i]) == LOW) c++;
    noTone(emitP[i]); delay(2);
  }
  return c;
}

int median3(int i) {
  int a = oneRead(i), b = oneRead(i), c = oneRead(i);
  if (a > b) { int t=a; a=b; b=t; }
  if (b > c) { int t=b; b=c; c=t; }
  if (a > b) { int t=a; a=b; b=t; }
  return b;
}

int normPct(int i) {
  int v = median3(i);
  int lo = baseV[i], hi = peakV[i];
  if (hi <= lo) return 0;
  return constrain((long)(v - lo) * 100 / (hi - lo), 0, 100);
}

// ---- 逐个自校准 ----
void calibrateOne(int i, const char* name) {
  Serial.print("\n[校准] ");
  Serial.print(name);
  Serial.println(" 传感器：把白纸由远到近慢慢扫，扫完在串口输入框敲回车...");

  baseV[i] = 9999;
  peakV[i] = 0;

  while (Serial.available()) Serial.read();
  delay(500);

  while (true) {
    int v = oneRead(i);
    if (v < baseV[i]) baseV[i] = v;
    if (v > peakV[i]) peakV[i] = v;

    Serial.print("  raw="); Serial.print(v);
    Serial.print("  base="); Serial.print(baseV[i]);
    Serial.print("  peak="); Serial.println(peakV[i]);

    if (Serial.available()) {
      while (Serial.available()) Serial.read();
      break;
    }
  }

  Serial.print("[完成] "); Serial.print(name);
  Serial.print(" base="); Serial.print(baseV[i]);
  Serial.print("  peak="); Serial.println(peakV[i]);
}

void calibrate() {
  calibrateOne(1, "前");
  calibrateOne(0, "左");
  calibrateOne(2, "右");
}

// ---- 迟滞二值化 ----
bool lastB[3] = {false, false, false};
bool blocked(int i, int nv) {
  if (lastB[i]) lastB[i] = (nv > NEAR_OFF);
  else          lastB[i] = (nv > NEAR_ON);
  return lastB[i];
}

// ---- 细分场景 5/6/7/8（在查表结果为1/走廊时调用）----
int refineScenario(int nL, int nF, int nR,
                   bool Lb, bool Fb, bool Rb) {
  const int MARGIN = 20;   // 归一化后"明显更近"的差值，可调

  // 7: 左近+前近，右没墙（贴左墙成角度）
  if (Lb && Fb && !Rb && (nL > nR + MARGIN)) return 7;

  // 8: 右近+前近，左没墙（贴右墙成角度）
  if (Rb && Fb && !Lb && (nR > nL + MARGIN)) return 8;

  // 5: 左右都有墙，右明显更近（贴左墙平行）
  if (Lb && Rb && !Fb && (nR > nL + MARGIN)) return 5;

  // 6: 左右都有墙，左明显更近（贴右墙平行）
  if (Lb && Rb && !Fb && (nL > nR + MARGIN)) return 6;

  // 走廊（左右相近）
  if (Lb && Rb && !Fb) return 1;

  return 0;
}

int classify() {
  int nL = normPct(0), nF = normPct(1), nR = normPct(2);
  bool Lb = blocked(0, nL);
  bool Fb = blocked(1, nF);
  bool Rb = blocked(2, nR);

  int idx = (Lb << 2) | (Fb << 1) | Rb;
  int s = table[idx];

  // 查表得到1时，用比值细分
  if (s == 1) {
    s = refineScenario(nL, nF, nR, Lb, Fb, Rb);
  }

  return s;
}

// ---- LED 二进制编码 ----
void showLed(int s) {
  if (s >= 8) {
    // 8/9/10 闪烁
    digitalWrite(rLedR, LOW);
    digitalWrite(rLedM, LOW);
    digitalWrite(rLedL, LOW);
    bool flashR = (s == 8 || s == 10);
    bool flashM = (s == 9 || s == 10);
    for (int i = 0; i < 5; i++) {
      if (flashR) digitalWrite(rLedR, HIGH);
      if (flashM) digitalWrite(rLedM, HIGH);
      delay(1000);
      digitalWrite(rLedR, LOW);
      digitalWrite(rLedM, LOW);
      delay(1000);
    }
  } else {
    digitalWrite(rLedR, (s & 1)      ? HIGH : LOW);
    digitalWrite(rLedM, ((s >> 1)&1) ? HIGH : LOW);
    digitalWrite(rLedL, ((s >> 2)&1) ? HIGH : LOW);
    delay(5000);
  }
}

// ---- 串口场景表格输出 ----
void printScenarioTable(int nL, int nF, int nR,
                        bool Lb, bool Fb, bool Rb, int s) {
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.println(F("| 传感器  |  左   |  前   |  右   |"));
  Serial.println(F("+---------+-------+-------+-------+"));

  Serial.print(F("| 归一化% | "));
  Serial.print(nL); Serial.print(F("%\t| "));
  Serial.print(nF); Serial.print(F("%\t| "));
  Serial.print(nR); Serial.println(F("%\t|"));

  Serial.print(F("| 有墙?   |  "));
  Serial.print(Lb ? "是  " : "否  ");
  Serial.print(F(" |  "));
  Serial.print(Fb ? "是  " : "否  ");
  Serial.print(F(" |  "));
  Serial.print(Rb ? "是  " : "否  ");
  Serial.println(F(" |"));

  Serial.println(F("+---------+-------+-------+-------+"));

  Serial.print(F("-> 场景: "));
  if (s >= 0 && s <= 10) {
    Serial.println(scenarioName[s]);
  } else {
    Serial.println(s);
  }

  Serial.print(F("   LED: R(A0)="));
  Serial.print((s < 8) ? ((s & 1) ? "亮" : "灭") : "闪");
  Serial.print(F("  M(A1)="));
  Serial.print((s < 8) ? (((s>>1)&1) ? "亮" : "灭") : ((s==9||s==10)?"闪":"灭"));
  Serial.print(F("  L(A2)="));
  Serial.println((s < 8) ? (((s>>2)&1) ? "亮" : "灭") : "灭");

  Serial.println();
}

void setup() {
  Serial.begin(9600);
  for (int i = 0; i < 3; i++) {
    pinMode(emitP[i], OUTPUT);
    pinMode(recvP[i], INPUT);
  }
  pinMode(rLedR, OUTPUT);
  pinMode(rLedM, OUTPUT);
  pinMode(rLedL, OUTPUT);

  digitalWrite(rLedR, LOW);
  digitalWrite(rLedM, LOW);
  digitalWrite(rLedL, LOW);

  calibrate();

  Serial.println(F("\n=== 校准完成，进入识别循环 ==="));
  Serial.println(F("摆不同姿势，观察下方表格\n"));
}

void loop() {
  int nL = normPct(0), nF = normPct(1), nR = normPct(2);
  bool Lb = blocked(0, nL);
  bool Fb = blocked(1, nF);
  bool Rb = blocked(2, nR);

  // N 次确认：连续 3 次同号才认账
  int s1 = classify(), s2 = classify(), s3 = classify();
  int s = (s1 == s2 && s2 == s3) ? s1 : 0;

  printScenarioTable(nL, nF, nR, Lb, Fb, Rb, s);
  showLed(s);

  delay(300);
}
```

## 串口输出长这样

校准阶段：
```
[校准] 前 传感器：把白纸由远到近慢慢扫，扫完在串口输入框敲回车...
  raw=0  base=0  peak=0
  raw=2  base=0  peak=2
  raw=28 base=0  peak=28
  ...
[完成] 前 base=0  peak=28
```

识别阶段每次循环输出：
```
+---------+-------+-------+-------+
| 传感器  |  左   |  前   |  右   |
+---------+-------+-------+-------+
| 归一化% | 72%   | 15%   | 68%   |
| 有墙?   |  是   |  否   |  是   |
+---------+-------+-------+-------+
-> 场景: 1  走廊直行
   LED: R(A0)=亮  M(A1)=灭  L(A2)=灭
```

## 明天用的节奏

1. 烧录 → 开串口 → 按提示逐个扫三路传感器
2. 进入识别循环后，把板子摆成作业图里各个姿势
3. 对照表格里的"有墙/归一化%"确认识别对不对
4. 如果某个场景判断错了，看归一化%的数，调 `NEAR_ON/NEAR_OFF` 或 `MARGIN` 那两个常量
5. `table[8]` 里标了 TODO 的格子，摆姿势后按实测填进去

两个问题分开回答。

## 关于准确性

之前的代码**方向是对的，但有几个实际问题**：

1. `refineScenario` 里场景 5/6 的条件和场景 7/8 的条件**有逻辑重叠**——`Lb && Rb && !Fb` 和 `Lb && Fb && !Rb` 可能同时成立，顺序不对就会误判。
2. `table[8]` 里几个格子是 TODO，没填——查表会返回错误场景。
3. `loop()` 里调用了三次 `classify()`，每次 `classify()` 内部又调用 `normPct()` 三次，每次 `normPct()` 里有 `median3()`，每次 `median3()` 有三次 `oneRead()`，每次 `oneRead()` 跑 30 次采样……**三次 classify 合计约 810 次采样，耗时超过 3 秒**，机器人在这期间一直停着不动，走迷宫时会卡顿严重。
4. 走迷宫时不能每次识别一个场景就停 5 秒——5 秒是**验收时**的要求，跑迷宫时要去掉。

---

## 走迷宫的完整代码

两个模式用一个常量切换：`DEMO_MODE = true` 是验收模式（显示 LED + 停 5 秒），`false` 是跑迷宫模式（识别后直接执行动作）。

```cpp
// ============================================================
// ELEC1601 迷宫项目 - 完整版
// DEMO_MODE true  = 验收：显示LED停5秒再动
// DEMO_MODE false = 跑迷宫：识别后直接动
// ============================================================

#include <Servo.h>
// 到 take-home board 时改为：
// #include "ELEC1601_TakeHomeBoard.h"
// 并注释掉上面这行

// ---- 模式切换 ----
const bool DEMO_MODE = true;   // 验收时 true，跑迷宫时改 false

// ---- 引脚：0=左, 1=前, 2=右 ----
const int emitP[3] = {10, 6,  2};
const int recvP[3] = {11, 7,  3};
const long freqV[3] = {41300, 44300, 42300};

const int rLedR = A0, rLedM = A1, rLedL = A2;

const int leftServoPin  = 12;
const int rightServoPin = 13;

Servo servoLeft;
Servo servoRight;

// ---- 舵机参数（实验室实测后填）----
const int LEFT_STOP    = 1490, RIGHT_STOP    = 1490;
const int LEFT_FWD     = 1440, RIGHT_FWD     = 1545;
const int LEFT_BACK    = 1560, RIGHT_BACK    = 1440;
const int LEFT_CW      = 1430, RIGHT_CW      = 1430;   // 顺时针(右转)
const int LEFT_CCW     = 1550, RIGHT_CCW     = 1550;   // 逆时针(左转)

// 走廊宽20cm，小车居中时两侧各5cm
// 以下时长需实验室校准
const int TIME_FWD_5CM  = 400;    // 前进5cm的毫秒数
const int TIME_TURN_90  = 700;    // 转90度的毫秒数
const int TIME_TURN_180 = 1400;   // 转180度的毫秒数
const int TIME_TURN_SMALL = 200;  // 场景5/6/7/8微调角度
const int TIME_CORRECT  = 150;    // 走廊行进时每次修正量

// ---- 采样 ----
const int N = 20;    // 跑迷宫时减少采样提升速度

// ---- 自校准 ----
int baseV[3] = {0,    0,    0};
int peakV[3] = {1,    1,    1};

// ---- 阈值（归一化后百分比）----
const int NEAR_ON  = 60;   // 进入"有墙"
const int NEAR_OFF = 40;   // 退出"有墙"（迟滞）
const int MARGIN   = 20;   // "明显更近"的差值

// ============================================================
// 基础测量
// ============================================================

int oneRead(int i) {
  int c = 0;
  for (int k = 0; k < N; k++) {
    tone(emitP[i], freqV[i]); delay(2);
    if (digitalRead(recvP[i]) == LOW) c++;
    noTone(emitP[i]); delay(2);
  }
  return c;
}

int median3(int i) {
  int a = oneRead(i), b = oneRead(i), c = oneRead(i);
  if (a > b) { int t=a; a=b; b=t; }
  if (b > c) { int t=b; b=c; c=t; }
  if (a > b) { int t=a; a=b; b=t; }
  return b;
}

int normPct(int i) {
  int v = median3(i);
  int lo = baseV[i], hi = peakV[i];
  if (hi <= lo) return 0;
  return (int)constrain((long)(v - lo) * 100L / (hi - lo), 0, 100);
}

// 一次性读三路（避免重复采样）
void readAll(int &nL, int &nF, int &nR) {
  nL = normPct(0);
  nF = normPct(1);
  nR = normPct(2);
}

// ============================================================
// 自校准（逐个传感器，回车触发下一个）
// ============================================================

void calibrateOne(int i, const char* name) {
  Serial.print(F("\n[校准] "));
  Serial.print(name);
  Serial.println(F(" 传感器：白纸由远到近慢慢扫，扫完敲回车..."));

  baseV[i] = 9999;
  peakV[i] = 0;
  while (Serial.available()) Serial.read();
  delay(500);

  while (true) {
    int v = oneRead(i);
    if (v < baseV[i]) baseV[i] = v;
    if (v > peakV[i]) peakV[i] = v;
    Serial.print(F("  raw=")); Serial.print(v);
    Serial.print(F("  base=")); Serial.print(baseV[i]);
    Serial.print(F("  peak=")); Serial.println(peakV[i]);
    if (Serial.available()) {
      while (Serial.available()) Serial.read();
      break;
    }
  }
  Serial.print(F("[完成] ")); Serial.print(name);
  Serial.print(F("  base=")); Serial.print(baseV[i]);
  Serial.print(F("  peak=")); Serial.println(peakV[i]);
}

void calibrate() {
  Serial.println(F("\n=== 开始校准，串口监视器行结尾选 Newline ==="));
  calibrateOne(1, "前");
  calibrateOne(0, "左");
  calibrateOne(2, "右");
  Serial.println(F("\n=== 校准完成 ===\n"));
}

// ============================================================
// 迟滞二值化
// ============================================================

bool lastB[3] = {false, false, false};

bool blocked(int i, int nv) {
  if (lastB[i]) lastB[i] = (nv > NEAR_OFF);
  else          lastB[i] = (nv > NEAR_ON);
  return lastB[i];
}

// ============================================================
// 场景识别
// ============================================================

int detectScenario(int nL, int nF, int nR) {
  bool Lb = blocked(0, nL);
  bool Fb = blocked(1, nF);
  bool Rb = blocked(2, nR);

  // 7: 贴左墙~30°：左近+前近，右无墙，且左明显比右近
  // 必须在场景3之前判断，否则会误判为左转位
  if (Lb && Fb && !Rb && (nL > nR + MARGIN)) return 7;

  // 8: 贴右墙~30°：右近+前近，左无墙，且右明显比左近
  // 必须在场景2之前判断
  if (Rb && Fb && !Lb && (nR > nL + MARGIN)) return 8;

  // 4: 死路，三面有墙
  if (Lb && Fb && Rb) return 4;

  // 2: 右转位，前+左有墙，右无墙
  if (Fb && Lb && !Rb) return 2;

  // 3: 左转位，前+右有墙，左无墙
  if (Fb && !Lb && Rb) return 3;

  // 前方无墙，左右都有墙：细分1/5/6
  if (!Fb && Lb && Rb) {
    if (nR > nL + MARGIN) return 5;   // 右更近=靠左墙
    if (nL > nR + MARGIN) return 6;   // 左更近=靠右墙
    return 1;                          // 左右相近=走廊居中
  }

  // 前方无墙，只有一侧有墙（走廊入口/出口附近）
  // 暂时直行，让机器人继续推进
  if (!Fb && (Lb || Rb)) return 1;

  return 0;  // 未知
}

// ============================================================
// LED 显示
// ============================================================

void setLed(int s) {
  if (s >= 0 && s <= 7) {
    digitalWrite(rLedR, (s & 1)       ? HIGH : LOW);
    digitalWrite(rLedM, ((s >> 1) & 1)? HIGH : LOW);
    digitalWrite(rLedL, ((s >> 2) & 1)? HIGH : LOW);
  } else if (s == 8) {
    // R 闪，其余灭
    digitalWrite(rLedM, LOW); digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedR, HIGH); delay(1000);
      digitalWrite(rLedR, LOW);  delay(1000);
    }
  } else if (s == 9) {
    digitalWrite(rLedR, LOW); digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedM, HIGH); delay(1000);
      digitalWrite(rLedM, LOW);  delay(1000);
    }
  } else if (s == 10) {
    digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedR, HIGH); digitalWrite(rLedM, HIGH); delay(1000);
      digitalWrite(rLedR, LOW);  digitalWrite(rLedM, LOW);  delay(1000);
    }
  }
}

// ============================================================
// 舵机动作封装
// ============================================================

void stopRobot() {
  servoLeft.writeMicroseconds(LEFT_STOP);
  servoRight.writeMicroseconds(RIGHT_STOP);
}

void moveForward(int ms) {
  servoLeft.writeMicroseconds(LEFT_FWD);
  servoRight.writeMicroseconds(RIGHT_FWD);
  delay(ms);
  stopRobot();
}

void moveBackward(int ms) {
  servoLeft.writeMicroseconds(LEFT_BACK);
  servoRight.writeMicroseconds(RIGHT_BACK);
  delay(ms);
  stopRobot();
}

void turnCW(int ms) {    // 顺时针=右转
  servoLeft.writeMicroseconds(LEFT_CW);
  servoRight.writeMicroseconds(RIGHT_CW);
  delay(ms);
  stopRobot();
}

void turnCCW(int ms) {   // 逆时针=左转
  servoLeft.writeMicroseconds(LEFT_CCW);
  servoRight.writeMicroseconds(RIGHT_CCW);
  delay(ms);
  stopRobot();
}

// ---- 走廊修正：根据左右读数差微调方向 ----
// 两侧各5cm时认为居中；偏差超过MARGIN就微调
void correctCourse(int nL, int nR) {
  if (nR > nL + MARGIN) {
    // 右侧更近=偏左=微右转
    turnCW(TIME_CORRECT);
  } else if (nL > nR + MARGIN) {
    // 左侧更近=偏右=微左转
    turnCCW(TIME_CORRECT);
  }
}

// ============================================================
// 场景动作
// ============================================================

void executeScenario(int s, int nL, int nF, int nR) {
  switch (s) {
    case 0:
      stopRobot();
      break;

    case 1:
      // 走廊：前进5cm，修正居中
      correctCourse(nL, nR);
      moveForward(TIME_FWD_5CM);
      break;

    case 2:
      // 右转位：右转90°，前进回走廊
      turnCW(TIME_TURN_90);
      delay(100);
      moveForward(TIME_FWD_5CM);
      break;

    case 3:
      // 左转位：左转90°，前进回走廊
      turnCCW(TIME_TURN_90);
      delay(100);
      moveForward(TIME_FWD_5CM);
      break;

    case 4:
      // 死路：转180°，前进
      turnCW(TIME_TURN_180);
      delay(100);
      moveForward(TIME_FWD_5CM);
      break;

    case 5:
      // 贴左墙平行：微右转→前进→微左转回正
      turnCW(TIME_TURN_SMALL);
      moveForward(TIME_FWD_5CM);
      turnCCW(TIME_TURN_SMALL);
      break;

    case 6:
      // 贴右墙平行：微左转→前进→微右转回正
      turnCCW(TIME_TURN_SMALL);
      moveForward(TIME_FWD_5CM);
      turnCW(TIME_TURN_SMALL);
      break;

    case 7:
      // 贴左墙成角：微右转至平行
      turnCW(TIME_TURN_SMALL);
      break;

    case 8:
      // 贴右墙成角：微左转至平行
      turnCCW(TIME_TURN_SMALL);
      break;

    default:
      stopRobot();
      break;
  }
}

// ============================================================
// 串口表格输出
// ============================================================

const char* scenarioName[11] = {
  "0  未知(停止)",
  "1  走廊直行",
  "2  右转位",
  "3  左转位",
  "4  死路(180转)",
  "5  贴左墙平行",
  "6  贴右墙平行",
  "7  贴左墙~30度",
  "8  贴右墙~30度",
  "9  自定义A",
  "10 自定义B"
};

void printTable(int nL, int nF, int nR, int s) {
  bool Lb = lastB[0], Fb = lastB[1], Rb = lastB[2];

  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.println(F("| 传感器  |  左   |  前   |  右   |"));
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.print(F("| 归一化% |  "));
  Serial.print(nL); Serial.print(F("%\t|  "));
  Serial.print(nF); Serial.print(F("%\t|  "));
  Serial.print(nR); Serial.println(F("%\t|"));
  Serial.print(F("| 有墙?   |  "));
  Serial.print(Lb?"是  ":"否  ");
  Serial.print(F(" |  "));
  Serial.print(Fb?"是  ":"否  ");
  Serial.print(F(" |  "));
  Serial.print(Rb?"是  ":"否  ");
  Serial.println(F(" |"));
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.print(F("-> 场景: "));
  if (s >= 0 && s <= 10) Serial.println(scenarioName[s]);
  else Serial.println(s);
  Serial.print(F("   LED  : R="));
  Serial.print((s<8)?((s&1)?"亮":"灭"):((s==8||s==10)?"闪":"灭"));
  Serial.print(F("  M="));
  Serial.print((s<8)?(((s>>1)&1)?"亮":"灭"):((s==9||s==10)?"闪":"灭"));
  Serial.print(F("  L="));
  Serial.println((s<8)?(((s>>2)&1)?"亮":"灭"):"灭");
  Serial.println();
}

// ============================================================
// setup / loop
// ============================================================

void setup() {
  Serial.begin(9600);

  for (int i = 0; i < 3; i++) {
    pinMode(emitP[i], OUTPUT);
    pinMode(recvP[i], INPUT);
  }
  pinMode(rLedR, OUTPUT);
  pinMode(rLedM, OUTPUT);
  pinMode(rLedL, OUTPUT);
  digitalWrite(rLedR, LOW);
  digitalWrite(rLedM, LOW);
  digitalWrite(rLedL, LOW);

  servoLeft.attach(leftServoPin);
  servoRight.attach(rightServoPin);
  stopRobot();

  calibrate();
}

void loop() {
  int nL, nF, nR;
  readAll(nL, nF, nR);

  int s = detectScenario(nL, nF, nR);
  printTable(nL, nF, nR, s);

  if (DEMO_MODE) {
    // 验收模式：显示LED，停5秒，再动
    stopRobot();
    setLed(s);
    // setLed 里已经 delay(5000) 或闪烁10秒
    executeScenario(s, nL, nF, nR);
  } else {
    // 跑迷宫模式：识别后直接动，LED随时更新
    setLed(s);
    executeScenario(s, nL, nF, nR);
  }

  delay(50);
}
```

---

## 到实验室必须调的三个数

你已知走廊两侧各 5cm，到实验室后重点校准这三个时长常量：

| 常量 | 怎么校 |
|---|---|
| `TIME_FWD_5CM` | 放在走廊里，跑一段量实际走了多少cm，等比例调整 |
| `TIME_TURN_90` | 对着直角墙，转完看是否刚好90°（用走廊的垂直方向验证）|
| `TIME_TURN_SMALL` | 摆成场景5/6姿势，转完看是否回到平行，微调 |

`MARGIN = 20` 这个值也要实地看串口输出的归一化%，如果两侧差值在5cm时不到20，就调小一点。



马达转速不一致是连续底盘机器人的经典问题，解决方案有两个层次：**开环补偿（简单，够用）** 和 **闭环 PD 控制（精确，推荐）**。你已经有归一化的左右传感器读数，正好可以直接拿来做闭环，不需要额外硬件。

## 核心思路

走廊宽 20cm，居中时两侧各 10cm（你说的 5cm 是贴墙时），所以：

- 理想状态：左右归一化读数**相等**
- 偏左：右侧读数 > 左侧读数（右边墙更近）
- 偏右：左侧读数 > 右侧读数（左边墙更近）

用误差来实时调整两侧舵机转速，就是**墙跟随 PD 控制**。

## 误差定义（比值，与灵敏度无关）

```
error = (nR - nL) / (nR + nL + 1)   // -1.0 到 +1.0
```

- `error > 0`：右边更近，偏左，需要右转修正
- `error < 0`：左边更近，偏右，需要左转修正
- `error ≈ 0`：居中

用比值而不是差值，是因为比值**自动消除了传感器灵敏度差异**。

## 完整代码（替换你现有版本中的相关部分）

```cpp
// ============================================================
// ELEC1601 迷宫项目 - 完整版（含 PD 墙跟随修正）
// DEMO_MODE true  = 验收模式
// DEMO_MODE false = 跑迷宫模式
// ============================================================

#include <Servo.h>

const bool DEMO_MODE = false;

// ---- 引脚：0=左, 1=前, 2=右 ----
const int emitP[3] = {10, 6,  2};
const int recvP[3] = {11, 7,  3};
const long freqV[3] = {41300, 44300, 42300};

const int rLedR = A0, rLedM = A1, rLedL = A2;
const int leftServoPin  = 12;
const int rightServoPin = 13;

Servo servoLeft;
Servo servoRight;

// ---- 舵机基准（实验室实测后填）----
const int LEFT_STOP  = 1490, RIGHT_STOP  = 1490;
const int LEFT_FWD   = 1440, RIGHT_FWD   = 1545;
const int LEFT_BACK  = 1560, RIGHT_BACK  = 1440;
const int LEFT_CW    = 1430, RIGHT_CW    = 1430;
const int LEFT_CCW   = 1550, RIGHT_CCW   = 1550;

// ---- 时长（实验室实测后填）----
const int TIME_FWD_5CM    = 400;
const int TIME_TURN_90    = 700;
const int TIME_TURN_180   = 1400;
const int TIME_TURN_SMALL = 200;

// ---- PD 参数（关键，需实测调整）----
// Kp: 比例增益，越大修正越猛，太大会震荡
// Kd: 微分增益，抑制震荡，让修正更平滑
// MAX_CORRECTION: 单侧最大补偿 microseconds（避免过度修正）
float Kp = 80.0;
float Kd = 20.0;
const int MAX_CORRECTION = 60;

// ---- 采样 ----
const int N = 20;

// ---- 自校准 ----
int baseV[3] = {0, 0, 0};
int peakV[3] = {1, 1, 1};

// ---- 阈值 ----
const int NEAR_ON  = 60;
const int NEAR_OFF = 40;
const int MARGIN   = 20;

// ---- PD 状态 ----
float lastError = 0.0;

// ============================================================
// 测量
// ============================================================

int oneRead(int i) {
  int c = 0;
  for (int k = 0; k < N; k++) {
    tone(emitP[i], freqV[i]); delay(2);
    if (digitalRead(recvP[i]) == LOW) c++;
    noTone(emitP[i]); delay(2);
  }
  return c;
}

int median3(int i) {
  int a = oneRead(i), b = oneRead(i), c = oneRead(i);
  if (a > b) { int t=a; a=b; b=t; }
  if (b > c) { int t=b; b=c; c=t; }
  if (a > b) { int t=a; a=b; b=t; }
  return b;
}

int normPct(int i) {
  int v = median3(i);
  int lo = baseV[i], hi = peakV[i];
  if (hi <= lo) return 0;
  return (int)constrain((long)(v - lo) * 100L / (hi - lo), 0, 100);
}

void readAll(int &nL, int &nF, int &nR) {
  nL = normPct(0);
  nF = normPct(1);
  nR = normPct(2);
}

// ============================================================
// 自校准
// ============================================================

void calibrateOne(int i, const char* name) {
  Serial.print(F("\n[校准] "));
  Serial.print(name);
  Serial.println(F(" 传感器：白纸由远到近慢慢扫，扫完敲回车..."));
  baseV[i] = 9999; peakV[i] = 0;
  while (Serial.available()) Serial.read();
  delay(500);
  while (true) {
    int v = oneRead(i);
    if (v < baseV[i]) baseV[i] = v;
    if (v > peakV[i]) peakV[i] = v;
    Serial.print(F("  raw=")); Serial.print(v);
    Serial.print(F("  base=")); Serial.print(baseV[i]);
    Serial.print(F("  peak=")); Serial.println(peakV[i]);
    if (Serial.available()) { while (Serial.available()) Serial.read(); break; }
  }
  Serial.print(F("[完成] ")); Serial.print(name);
  Serial.print(F("  base=")); Serial.print(baseV[i]);
  Serial.print(F("  peak=")); Serial.println(peakV[i]);
}

void calibrate() {
  Serial.println(F("\n=== 开始校准 ==="));
  calibrateOne(1, "前");
  calibrateOne(0, "左");
  calibrateOne(2, "右");
  Serial.println(F("\n=== 校准完成 ===\n"));
}

// ============================================================
// 迟滞二值化
// ============================================================

bool lastB[3] = {false, false, false};

bool blocked(int i, int nv) {
  if (lastB[i]) lastB[i] = (nv > NEAR_OFF);
  else          lastB[i] = (nv > NEAR_ON);
  return lastB[i];
}

// ============================================================
// 场景识别
// ============================================================

int detectScenario(int nL, int nF, int nR) {
  bool Lb = blocked(0, nL);
  bool Fb = blocked(1, nF);
  bool Rb = blocked(2, nR);

  if (Lb && Fb && !Rb && (nL > nR + MARGIN)) return 7;
  if (Rb && Fb && !Lb && (nR > nL + MARGIN)) return 8;
  if (Lb && Fb && Rb)                         return 4;
  if (Fb && Lb && !Rb)                        return 2;
  if (Fb && !Lb && Rb)                        return 3;

  if (!Fb && Lb && Rb) {
    if (nR > nL + MARGIN) return 5;
    if (nL > nR + MARGIN) return 6;
    return 1;
  }

  if (!Fb && (Lb || Rb)) return 1;
  return 0;
}

// ============================================================
// PD 墙跟随：直行时实时修正两侧转速
// ============================================================
//
// 只在走廊直行（场景1/5/6）时调用。
// 当左右都有墙时，用误差比值驱动 PD；
// 只有单侧有墙时，退化成简单追墙。

void moveForwardPD(int durationMs, int nL, int nR, bool Lb, bool Rb) {
  unsigned long start = millis();
  lastError = 0.0;

  while (millis() - start < durationMs) {

    // 重新采样（循环内持续修正）
    int curL = normPct(0);
    int curR = normPct(2);
    bool curLb = blocked(0, curL);
    bool curRb = blocked(2, curR);

    float error = 0.0;

    if (curLb && curRb) {
      // 两侧都有墙：用比值误差
      // error > 0 = 偏左（右边更近），需右转
      // error < 0 = 偏右（左边更近），需左转
      error = (float)(curR - curL) / (float)(curR + curL + 1);
    } else if (curRb && !curLb) {
      // 只有右墙：靠右墙走，保持固定距离
      error = (float)(curR - 50) / 100.0;   // 目标50%（可调）
    } else if (curLb && !curRb) {
      // 只有左墙：靠左墙走
      error = -(float)(curL - 50) / 100.0;
    }
    // 两侧都没墙：不修正，保持直行

    // PD 计算
    float derivative = error - lastError;
    float correction = Kp * error + Kd * derivative;
    lastError = error;

    correction = constrain(correction, -MAX_CORRECTION, MAX_CORRECTION);

    // error > 0 偏左：左加速、右减速（右转）
    int leftSpeed  = LEFT_FWD  + (int)correction;
    int rightSpeed = RIGHT_FWD - (int)correction;

    // 防止超出合理范围
    leftSpeed  = constrain(leftSpeed,  LEFT_FWD  - MAX_CORRECTION, LEFT_FWD  + MAX_CORRECTION);
    rightSpeed = constrain(rightSpeed, RIGHT_FWD - MAX_CORRECTION, RIGHT_FWD + MAX_CORRECTION);

    servoLeft.writeMicroseconds(leftSpeed);
    servoRight.writeMicroseconds(rightSpeed);

    Serial.print(F("PD | L=")); Serial.print(curL);
    Serial.print(F(" R="));     Serial.print(curR);
    Serial.print(F(" err="));   Serial.print(error, 3);
    Serial.print(F(" corr="));  Serial.println((int)correction);

    delay(40);   // 控制循环约 25Hz（40ms + 采样时间）
  }

  servoLeft.writeMicroseconds(LEFT_STOP);
  servoRight.writeMicroseconds(RIGHT_STOP);
}

// ============================================================
// 其他基础动作
// ============================================================

void stopRobot() {
  servoLeft.writeMicroseconds(LEFT_STOP);
  servoRight.writeMicroseconds(RIGHT_STOP);
}

void moveForwardDumb(int ms) {
  servoLeft.writeMicroseconds(LEFT_FWD);
  servoRight.writeMicroseconds(RIGHT_FWD);
  delay(ms);
  stopRobot();
}

void moveBackward(int ms) {
  servoLeft.writeMicroseconds(LEFT_BACK);
  servoRight.writeMicroseconds(RIGHT_BACK);
  delay(ms);
  stopRobot();
}

void turnCW(int ms) {
  servoLeft.writeMicroseconds(LEFT_CW);
  servoRight.writeMicroseconds(RIGHT_CW);
  delay(ms);
  stopRobot();
}

void turnCCW(int ms) {
  servoLeft.writeMicroseconds(LEFT_CCW);
  servoRight.writeMicroseconds(RIGHT_CCW);
  delay(ms);
  stopRobot();
}

// ============================================================
// LED
// ============================================================

void setLed(int s) {
  if (s >= 0 && s <= 7) {
    digitalWrite(rLedR, (s & 1)        ? HIGH : LOW);
    digitalWrite(rLedM, ((s >> 1) & 1) ? HIGH : LOW);
    digitalWrite(rLedL, ((s >> 2) & 1) ? HIGH : LOW);
    if (DEMO_MODE) delay(5000);
  } else if (s == 8) {
    digitalWrite(rLedM, LOW); digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedR, HIGH); delay(1000);
      digitalWrite(rLedR, LOW);  delay(1000);
    }
  } else if (s == 9) {
    digitalWrite(rLedR, LOW); digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedM, HIGH); delay(1000);
      digitalWrite(rLedM, LOW);  delay(1000);
    }
  } else if (s == 10) {
    digitalWrite(rLedL, LOW);
    for (int i = 0; i < 5; i++) {
      digitalWrite(rLedR, HIGH); digitalWrite(rLedM, HIGH); delay(1000);
      digitalWrite(rLedR, LOW);  digitalWrite(rLedM, LOW);  delay(1000);
    }
  }
}

// ============================================================
// 场景动作（走廊直行用 PD，其他用定时）
// ============================================================

void executeScenario(int s, int nL, int nF, int nR) {
  bool Lb = lastB[0], Rb = lastB[2];

  switch (s) {
    case 0:
      stopRobot();
      break;

    case 1:
      // 走廊：PD 持续修正，前进约5cm
      moveForwardPD(TIME_FWD_5CM, nL, nR, Lb, Rb);
      break;

    case 2:
      turnCW(TIME_TURN_90);
      delay(100);
      moveForwardPD(TIME_FWD_5CM, nL, nR, false, true);
      break;

    case 3:
      turnCCW(TIME_TURN_90);
      delay(100);
      moveForwardPD(TIME_FWD_5CM, nL, nR, true, false);
      break;

    case 4:
      turnCW(TIME_TURN_180);
      delay(100);
      moveForwardPD(TIME_FWD_5CM, nL, nR, Lb, Rb);
      break;

    case 5:
      // 贴左墙平行：先微右转，再用 PD 直行回正
      turnCW(TIME_TURN_SMALL);
      moveForwardPD(TIME_FWD_5CM, nL, nR, Lb, Rb);
      break;

    case 6:
      turnCCW(TIME_TURN_SMALL);
      moveForwardPD(TIME_FWD_5CM, nL, nR, Lb, Rb);
      break;

    case 7:
      turnCW(TIME_TURN_SMALL);
      break;

    case 8:
      turnCCW(TIME_TURN_SMALL);
      break;

    default:
      stopRobot();
      break;
  }
}

// ============================================================
// 串口表格
// ============================================================

const char* scenarioName[11] = {
  "0  未知(停止)",    "1  走廊直行",     "2  右转位",
  "3  左转位",        "4  死路(180转)",  "5  贴左墙平行",
  "6  贴右墙平行",    "7  贴左墙~30度",  "8  贴右墙~30度",
  "9  自定义A",       "10 自定义B"
};

void printTable(int nL, int nF, int nR, int s) {
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.println(F("| 传感器  |  左   |  前   |  右   |"));
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.print(F("| 归一化% |  ")); Serial.print(nL);
  Serial.print(F("%\t|  "));        Serial.print(nF);
  Serial.print(F("%\t|  "));        Serial.print(nR);
  Serial.println(F("%\t|"));
  Serial.print(F("| 有墙?   |  "));
  Serial.print(lastB[0]?"是  ":"否  ");
  Serial.print(F(" |  "));
  Serial.print(lastB[1]?"是  ":"否  ");
  Serial.print(F(" |  "));
  Serial.print(lastB[2]?"是  ":"否  ");
  Serial.println(F(" |"));
  Serial.println(F("+---------+-------+-------+-------+"));
  Serial.print(F("-> 场景: "));
  if (s >= 0 && s <= 10) Serial.println(scenarioName[s]);
  else Serial.println(s);
  Serial.println();
}

// ============================================================
// setup / loop
// ============================================================

void setup() {
  Serial.begin(9600);
  for (int i = 0; i < 3; i++) {
    pinMode(emitP[i], OUTPUT);
    pinMode(recvP[i], INPUT);
  }
  pinMode(rLedR, OUTPUT); pinMode(rLedM, OUTPUT); pinMode(rLedL, OUTPUT);
  digitalWrite(rLedR, LOW); digitalWrite(rLedM, LOW); digitalWrite(rLedL, LOW);
  servoLeft.attach(leftServoPin);
  servoRight.attach(rightServoPin);
  stopRobot();
  calibrate();
}

void loop() {
  int nL, nF, nR;
  readAll(nL, nF, nR);

  int s = detectScenario(nL, nF, nR);
  printTable(nL, nF, nR, s);
  setLed(s);
  executeScenario(s, nL, nF, nR);

  delay(50);
}
```

---

## 到实验室怎么调 Kp 和 Kd

按这个顺序，不要同时改两个：

**第一步：把 Kd 设 0，只调 Kp**

| 现象 | 操作 |
|---|---|
| 走直线，完全不修正 | Kp 加倍 |
| 能修正，但慢慢漂移 | Kp 再加大 |
| 左右来回摇摆（震荡） | Kp 减小 10~20% |
| 摇摆幅度小但停不下来 | 进入第二步 |

**第二步：Kp 稳定后，逐步加 Kd**

从 `Kd = Kp * 0.1` 开始，每次加 5，看震荡是否收敛更快。Kd 过大会让修正变得迟钝。

典型起点：`Kp = 60~100`，`Kd = 15~25`，走廊里跑 3~4 次微调一次。






先把文档剩余部分读完，然后综合回答你所有问题。

继续读完文档剩余部分。

读完文档剩余内容。

文档读完了。现在给你完整回答四个问题。

---

## 一、到实验室的执行顺序

### 阶段 0：上机前（5分钟）
确认代码里 `DEMO_MODE = true`，`#include <Servo.h>` 已打开（不是 take-home board 那行）。

### 阶段 1：校准传感器（10分钟）

1. 把最新代码烧录到实验室机器人
2. 开串口监视器，行结尾选 **Newline**，波特率 9600
3. 按提示逐个扫三个传感器（前→左→右），用**迷宫的真实墙壁**当参照，不要用白纸——传感器垂直排列，读数和在家不同
4. 扫完后串口会打出 base/peak，检查每路 peak 明显大于 base（差值至少 10 以上），否则重扫
5. 进入识别循环后，**不要动机器人**，先用手挡住每个传感器，确认归一化% 能跑到 80+

### 阶段 2：验证场景识别（15分钟）

把机器人摆进迷宫，逐个场景摆姿势，看串口表格输出是否匹配：

| 要验证的 | 摆法 |
|---|---|
| 场景 1 走廊 | 放走廊中间，前方开阔 |
| 场景 2/3 转弯 | 推到 T 型路口 |
| 场景 4 死路 | 推进死角 |
| 场景 5/6 贴墙 | 靠左/右墙平行放 |
| **场景 7/8 成角** | 贴左/右墙斜 30°，**这个最容易误判，重点测** |

如果识别不对，**只调这两个数**，不要动其他：
- `NEAR_ON / NEAR_OFF`：调"有墙/没墙"的边界
- `MARGIN`：调"明显更近"的灵敏度，实验室两侧各 5cm 时左右差值能有多大，就把 MARGIN 设成那个值的一半

### 阶段 3：校准舵机时长（20分钟）

这是最花时间的，按顺序来，不要乱跳：

**第一步：找停止点**
把 `LEFT_STOP / RIGHT_STOP` 调到机器人**静止不动**。两个舵机停止点可能不一样（比如一个 1490 一个 1495），逐个微调。

**第二步：校准 TIME_TURN_90**
在走廊里让机器人原地转，转完用眼睛或对着墙验证是否 90°。误差 5° 以内可以接受。

**第三步：校准 TIME_FWD_5CM**
走廊里直行，用尺子量走了多少 cm，等比例调整。比如设 400ms 走了 8cm，那 5cm 就改成 250ms。

**第四步：调 Kp（PD 控制）**
先把 `Kd = 0`，让机器人走廊直行，看串口的 `PD | err=` 那行。如果 error 一直非零但不修正，加大 Kp；如果左右摇摆，减小 Kp。找到不摇摆又能修正的值，再从 `Kd = Kp × 0.1` 开始加 Kd。

### 阶段 4：逐场景验收（剩余时间）

`DEMO_MODE = true`，逐个摆姿势让老师看 LED 亮 5 秒 + 执行动作。顺序建议：

0 → 1 → 4 → 2 → 3 → 5 → 6 → 7 → 8

场景 0（未知/停止）是最容易丢分的——老师会故意摆一个你没处理的姿势，确认你的机器人真的不动。

---

## 二、给明天笔记本 AI 的交接文档

直接复制这整块：

```
【项目】ELEC1601 迷宫机器人 Essential 部分，现在在实验室调试阶段。

【代码状态】已有完整代码，含：
- 逐个传感器自校准（开机扫纸，回车确认，得到 base/peak）
- 归一化（0~100%）+ 迟滞二值化（NEAR_ON=60, NEAR_OFF=40）
- 场景识别 detectScenario()，优先级：7/8 > 4 > 2/3 > 1/5/6
- PD 墙跟随 moveForwardPD()，走廊直行时实时修正两侧转速
- DEMO_MODE 开关：true=验收(LED停5秒), false=跑迷宫

【引脚】0=左, 1=前, 2=右
emitP: {10, 6, 2}  recvP: {11, 7, 3}  freqV: {41300, 44300, 42300}
LED: A0=右(R), A1=中(M), A2=左(L)
舵机: 左12, 右13

【需要在实验室实测的常量】
- baseV[3] / peakV[3]：开机校准自动得到，不用手填
- NEAR_ON / NEAR_OFF / MARGIN：识别精度，摆姿势后微调
- LEFT_STOP / RIGHT_STOP：让机器人静止不动
- TIME_FWD_5CM：前进5cm的毫秒数
- TIME_TURN_90：转90°的毫秒数
- TIME_TURN_180：转180°的毫秒数
- TIME_TURN_SMALL：场景5/6/7/8微调角度
- Kp / Kd：PD控制增益，Kd先设0，只调Kp

【走廊已知参数】宽20cm，居中时两侧各约5cm。

【当前问题/需要帮助的事】
（在这里写你今天遇到的具体问题，比如：场景7和场景2识别混淆、
转弯角度偏差大、PD震荡等）

【最新完整代码】
（把最新的 .ino 文件内容粘贴在这里）
```

---

## 三、这些技术是否超出课程水平

**是的，部分技术明显超出了基础要求，但方式是对的。**

| 技术 | 课程要求 | 你用的 | 评价 |
|---|---|---|---|
| 传感器校准 | 固定阈值 | 开机自校准 + 归一化 | 超出，但让你到实验室不用重写代码 |
| 场景识别 | if/else | 优先级决策树 + 迟滞 | 略超出，但结构更清晰 |
| 直行控制 | 定时直行 | PD 闭环控制 | **明显超出**，这是控制工程的内容 |
| LED 编码 | switch/case | 位运算三行搞定 | 技巧性超出，但更简洁 |
| 中值滤波 | 无 | median3() | 略超出，但噪声处理必要 |

超出不是坏事——老师看到 PD 控制和自校准会加分，而且这些技术解决了真实问题（马达不一致、换环境要重校）。唯一要注意的是：**你得能向老师解释清楚你做了什么**，不能只是粘贴代码。下面的原理讲解就是为这个准备的。

---

## 四、技术原理讲解

### 1. IR 传感器检测原理

发射器发出特定频率的红外光（`tone()` 产生方波驱动 LED），接收器是一个调谐到同频率的光电晶体管。**只有频率匹配的光才会触发**，所以普通环境光不会干扰。墙壁把光反射回来，接收器触发，`digitalRead()` 读到 LOW。

"发射 N 次数 LOW 的次数"这个方式相当于**软件积分**——单次测量可能因为光斑角度、灰尘等原因不准，多次求和让噪声平均掉。三个传感器频率不同（41300/42300/44300 Hz），是为了**互不干扰**，避免左边的光被右边的接收器收到。

### 2. 归一化（0~100%）

原始读数（0~N）受传感器个体差异影响，三路不能直接比大小。归一化把每路映射到统一尺度：

```
归一值 = (读数 - 远处基线) / (贴墙峰值 - 远处基线) × 100
```

物理意义：0% = 完全没墙，100% = 贴墙。归一化之后，"左边比右边近"就变成了简单的数字比大小，而且**自动补偿了三个传感器灵敏度的差异**。

### 3. 迟滞（Hysteresis）

普通阈值判断有一个问题：传感器读数在边界附近抖动时，"有墙/没墙"会每几毫秒翻转一次，造成场景识别反复跳变。

迟滞的解决方案是**用两个不同的阈值**：进入"有墙"状态需要读数超过 60%，而退出"有墙"状态需要读数低于 40%。这中间 20% 的区间是一个"惰性带"——读数在这里波动不会改变状态。就像恒温器：设定 20°C，但只有温度跌到 18°C 才开暖气，暖到 22°C 才关，不会每秒开关。

### 4. PD 控制（比例-微分控制器）

这是控制论的基础工具，用于让系统追踪目标值。

**P（比例）**：误差越大，修正越猛。如果机器人偏左 5%，给一个小修正；偏左 50%，给一个大修正。问题是纯 P 控制会在目标附近持续小幅震荡（永远在补过头）。

**D（微分）**：看误差的**变化速度**，而不是误差本身。如果误差在快速缩小（已经在回正了），D 项会减小修正力度，防止冲过头。相当于"预判"——不只看现在偏多少，还看偏差是在变大还是变小。

在你的代码里：
```
error = (右读数 - 左读数) / (右 + 左)   ← 归一化误差，-1到+1
correction = Kp × error + Kd × (error - 上次error)
左马达速度 = 基准速度 + correction
右马达速度 = 基准速度 - correction
```

偏左时右边读数更大，error > 0，左马达加速、右马达减速，机器人右转回正。用比值而不是差值，是因为比值在两侧传感器灵敏度不同时仍然有效。

### 5. 中值滤波（Median Filter）

对同一传感器连续读三次，取**中间值**（不是平均值）。原因：单次脉冲噪声（比如路过一辆车的反光）会把平均值拉偏，但无法影响中值——你需要两次以上的噪声才能污染中值。这是嵌入式系统里最常用的去噪方法之一，计算量极小。