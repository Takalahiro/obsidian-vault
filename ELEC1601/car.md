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