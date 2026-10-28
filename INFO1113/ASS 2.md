

---

# 第 0 步：这个程序到底在干嘛

一句话：**一个公交收费系统**。它能做的事：

1. 往系统里**加车**（Bus/Train/Tram）
2. 给**乘客**卖**票**（票上要算出价格）
3. **走时钟**（时间往前走，车也跟着动）
4. 统计**总营收**

项目分成两半：

| 位置 | 是什么 | 你能改吗 |
|---|---|---|
| `contracts/given/` | 题目**给好的** 7 个文件（注释写着 `SUPPLIED - do not modify or submit`） | **不能改，也不提交** |
| `src/` | 你要写的 8 个类 | 这是你的作业 |

`given` 里给的是「规则和骨架」，`src` 里是你的「实现」。这就像填空：题目给好句子结构，填内容是你的事。

---

# 第 1 步：题目给的 7 个文件（契约）

「契约」的意思：**它规定了必须长什么样，但不说怎么做**。先看两个 Java 概念，后面全靠它们：

- **接口 interface**：一份纯合同。只写「必须有哪些方法」，一句实现都没有。谁 `implements` 它，谁就必须把这些方法全写出来。
- **抽象类 abstract class**：一半合同一半实现。可以是「不能直接用 `new` 造、只能被继承」的类。它里面**既有写好的方法，也有留白的抽象方法**。

## 1.1 `VehicleStatus`（枚举 enum）

```java
public enum VehicleStatus { IN_SERVICE, APPROACHING, AT_STOP }
```

`enum` = 一组**固定的、只能从中选**的常量。车状态只能是这三种之一：行驶中 / 接近站 / 在站。好处：你要是手滑写成 `IN_SERIVCE`，编译器当场报错，不会悄悄错。

## 1.2 `Vehicle`（抽象类，所有车的父类）

```java
public abstract class Vehicle {
    protected final String id;        // 编号，如 "B1"
    protected double position;        // 位置
    protected VehicleStatus status = VehicleStatus.IN_SERVICE;

    protected Vehicle(String id) { ... }   // 校验 id 非空

    public final String id() { return id; }
    public final double position() { return position; }
    public final VehicleStatus status() { return status; }

    public abstract void advance();   // ★ 留白：怎么动，子类自己定
}
```

要点：

- `abstract class` → **不能 `new Vehicle(...)`**，只能被 Bus/Train/Tram 继承。
- `protected` 修饰的字段，**子类能直接访问**（Bus 里能直接写 `position = ...`）。
- `advance()` 是**抽象方法**：只声明「每辆车都得会动」，但**不写怎么动**。因为公交、火车、电车走法完全不同 → 丢给各自子类实现。这就是「多态」的入口。
- 三个 getter 是 `final`，意思是**子类不许改写这几个方法**（id/position/status 的读取方式定死）。

## 1.3 `Passenger`（抽象类，所有乘客的父类）

```java
public abstract class Passenger {
    protected final String name;
    protected Passenger(String name) { ... }
    public final String name() { return name; }
    public abstract long applyDiscount(long fareCents);   // 留白：怎么打折
}
```

同样套路：存名字，留一个抽象方法 `applyDiscount` 给子类（成人不打折、优惠票打半价……）。

## 1.4 `Trip`（普通类，一次出行）

```java
public final class Trip {
    private final String origin, destination;
    private final int distance;
    public Trip(String origin, String destination, int distance) { ...校验... }
    public String origin() {...}
    public String destination() {...}
    public int distance() {...}
    @Override public String toString() {
        return origin + " -> " + destination + " (" + distance + ")";
    }
}
```

- `final class` → 不能被继承。
- 构造器做三件校验：起点/终点不能空、**起点终点不能相同**、**距离至少 1**。不满足就抛 `IllegalArgumentException`。
- **关键认知**：`Trip` 只管「从哪到哪、多远」，**它完全不知道价钱**。价钱是系统算的。这样分工，改票价不用动 Trip。
- `toString()` 决定了打印格式 `Central -> Bondi Junction (12)`——Demo 输出里那一串就是这个来的。

## 1.5 `FarePolicy`（接口，计价政策）

```java
public interface FarePolicy {
    long dayFare(long baseCents, int earlierTripsToday);
}
```

只有**一个方法**。含义：任何「计价政策」都得回答同一个问题——**给定原价 `baseCents`，以及今天这是第几趟 `earlierTripsToday`，这一天该收多少**。假期政策和非假期政策各答各的。

## 1.6 `Ticket`（普通类，一张票）

```java
public final class Ticket {
    private final String id;
    private final Passenger passenger;
    private final Trip trip;
    private final int day;
    private final boolean holiday;
    private final long baseFareCents;    // 原价
    private final long dayFareCents;     // 一天的票价
    private final long finalFareCents;   // 最后实付

    public Ticket(..., long baseFareCents, long dayFareCents, long finalFareCents) {
        ...校验...
        if (baseFareCents < 0 || dayFareCents < 0 || dayFareCents > baseFareCents
                || finalFareCents < 0 || finalFareCents > dayFareCents) {
            throw new IllegalArgumentException(
                "fares must satisfy 0 <= final <= day fare <= base fare");
        }
        ...
    }
    // 一堆 getter
    public long dayDiscountCents() { return baseFareCents - dayFareCents; }
    public long passengerDiscountCents() { return dayFareCents - finalFareCents; }
}
```

三个票价概念要记牢（这是全题的**价格链**）：

```
base（原价） ≥ day fare（当天价） ≥ final（实付）
```

- **base**：原始价 = 距离 × 25 分
- **day fare**：经过「当天政策」后的价（假期会砍）
- **final**：再经过「乘客折扣」后的价（优惠票会砍）

构造器里那个 `if` **强制** `final ≤ day fare ≤ base`。这条约束是护栏：**你算价的顺序不能乱**，一旦写反（比如先打折再应用假期），这里立刻抛异常，等于自带检查。

`final` 字段全用 `final`：票一旦开出就固定，票号、金额都不能事后改。

## 1.7 `TransitSystem`（接口，系统总合同）

```java
public interface TransitSystem {
    void addVehicle(Vehicle vehicle);
    Ticket book(Passenger passenger, Trip trip);
    void tick();
    int currentTick();
    int day();
    boolean isHoliday();
    List<Ticket> tickets();
    long revenueCents();
}
```

这 8 个方法就是**整个作业要实现的总账**。你的 `TransitApp` 必须一字不差地全实现。

---

# 第 2 步：你 `src/` 里的 8 个类

一批一批看。

## 2.1 乘客三兄弟

### `AdultPassenger`（成人）

```java
public class AdultPassenger extends Passenger {
    public AdultPassenger(String name) { super(name); }   // 校验交给父类
    @Override
    public long applyDiscount(long fareCent) { return fareCent; }  // 不打折
}
```

`super(name)` = 把名字交给父类 `Passenger` 去存、去校验。`applyDiscount` 原样返回 → 成人不打折。✅

### `ConcessionPassenger`（优惠票乘客）

```java
public class ConcessionPassenger extends Passenger {
    private final boolean eligible;   // 是否够格享受半价

    public ConcessionPassenger(String name, String type, int age) {
        super(name);
        if (type == null) throw new IllegalArgumentException("type must not be null");
        switch (type) {
            case "A": case "D": case "V":
            case "AD": case "AV": case "DV":
            case "ADV":
                break;   // 合法
            default:
                throw new IllegalArgumentException("invalid concession type: " + type);
        }
        if (type.contains("A") && age < 65) {
            this.eligible = false;   // 含 A（老年）但不到 65 → 不够格
        } else {
            this.eligible = true;
        }
    }

    @Override
    public long applyDiscount(long fareCents) {
        return eligible ? fareCents / 2 : fareCents;   // 够格打半价
    }
}
```

- `type` 是优惠类别（A=老年、D=残障、V=退伍 等的组合）。`switch` 校验只允许那 7 种合法写法，其它（如 `"S"`）直接抛异常——正是 Demo 里 "concession type S rejected" 那句的来源。
- **核心规则**：含 `"A"`（老年）的就要求 `age >= 65`，否则不够格；其它类别直接够格。
- `eligible` 用 `private final` 存下来，因为构造器算一次，之后只读。

✅ 对上 expected-output：Ben(`DV`) → 够格 → 打半价；Cal(`A`, 60 岁) → 含 A 但没到 65 → 不够格 → 不打折（这就是 T6 是 300 的原因）。

### 2.2 车三兄弟

### `Bus`（公交）

```java
public class Bus extends Vehicle {
    public Bus(String id) { super(id); }
    @Override
    public void advance() {
        position = position + 1;   // 走 1 格
        status = VehicleStatus.IN_SERVICE;
    }
}
```

每 tick 前进 1，状态查不到变化就 IN_SERVICE。✅ 对上 `B1`：1,2,3,4。

### `Train`（火车）

```java
public class Train extends Vehicle {
    private int step = 0;
    public Train(String id) { super(id); }
    @Override
    public void advance() {
        step++;
        if (step % 2 == 1) {        // 奇数次调用
            position += 4;          // 前进 4
            status = VehicleStatus.AT_STOP;
        } else {                    // 偶数次：不动
            status = VehicleStatus.IN_SERVICE;
        }
    }
}
```

`step` 是这辆车「被 advance 了几次」的计数器（`%2` 取奇偶）。结果：奇数步 +4 在站、偶数步原地不动。✅ 对上 `T1`：4, 4, 8, 8。

### `Tram`（电车）

```java
public class Tram extends Vehicle {
    private int step = 0;
    public Tram(String id) { super(id); }
    @Override
    public void advance() {
        step++;
        if (step % 2 == 1) {
            position += 1;          // 奇数步 +1
            status = VehicleStatus.APPROACHING;
        } else {                    // 偶数步：不动
            status = VehicleStatus.IN_SERVICE;
        }
    }
}
```

⚠️ **这里对不上预期，先记一笔**：expected-output 里 `L1` 是 `1, 3, 4, 6`（奇数步 +1，偶数步 **+2**），但你这段偶数步**没有加 position**，算出来会是 `1, 1, 2, 2`。你说了现在不改代码，那就先记住：**Tram 的偶数分支缺一个位移**，交之前得对一下 expected-output。（Train 的偶数步不动是对的，Tram 不一样。）

## 2.3 计价政策两兄弟

### `HolidayFare`（假期政策）

```java
public class HolidayFare implements FarePolicy {
    @Override
    public long dayFare(long baseCents, int earlierTripsToday) {
        if (earlierTripsToday == 0) return baseCents / 2;   // 今天第一趟：半价
        return 0;                                            // 之后：免费
    }
}
```

假期规则：**当天第一趟半价，之后再坐免费**。`earlierTripsToday` 就是「今天已经买过几趟」——传 0 时是今天头一趟。

✅ 对上 Ava：T1（第一趟）150、T2（第二趟）0。

### `NormalFare`（普通政策）

```java
public class NormalFare implements FarePolicy {
    @Override
    public long dayFare(long baseCents, int earlierTripsToday) {
        return baseCents;   // 原价
    }
}
```

非假期不打折。（`earlierTripsToday` 没用上，无所谓，接口要求有这参数。）

## 2.4 `TransitApp`（系统大脑）

最后看这个，它把上面全部串起来。逐块拆：

```java
public class TransitApp implements TransitSystem {
    private static final int TICKS_PER_DAY = 24;              // 一天 24 tick
    private static final long CENTS_PER_DISTANCE_UNIT = 25;   // 每单位距离 25 分

    private final List<Vehicle> vehicles = new ArrayList<>();
    private final List<Ticket> tickets  = new ArrayList<>();
    private int currentTick;
    private int nextTicketNumber = 1;    // 下一张票号，T1 起
```

- 两个 `List`：一个存所有车，一个存所有卖出的票。
- `nextTicketNumber` 从 1 起 → 票号 `T1, T2, ...`

**两个构造器**：

```java
public TransitApp() { this(0); }          // 默认 tick 0
public TransitApp(int startTick) {
    if (startTick < 0) throw new IllegalArgumentException("start tick must be >= 0");
    this.currentTick = startTick;
}
```

`this(0)` = 「先去调另一个构造器」,不重复写赋值。测试里 `new TransitApp(24)` 直接给起始 tick。

**`addVehicle`**：把车塞进列表。

**`book`（核心，四步链）**：

```java
public Ticket book(Passenger passenger, Trip trip) {
    if (passenger == null || trip == null) throw new IllegalArgumentException(...);
    int today = day();
    long base = (long) trip.distance() * CENTS_PER_DISTANCE_UNIT;   // ① 原价

    int earlierToday = 0;                                            // ② 今天第几趟
    for (Ticket t : tickets)
        if (t.passenger() == passenger && t.day() == today) earlierToday++;

    FarePolicy policy = isHoliday() ? new HolidayFare() : new NormalFare();
    long dayFare = policy.dayFare(base, earlierToday);              // ③ 当天价
    long finalFare = passenger.applyDiscount(dayFare);             // ④ 乘客折扣

    Ticket ticket = new Ticket("T" + nextTicketNumber, passenger, trip,
            today, isHoliday(), base, dayFare, finalFare);
    nextTicketNumber++;
    tickets.add(ticket);
    return ticket;
}
```

① **base** = 距离 × 25。② **earlierToday** = 遍历已有票，数「同一个人、同一天」的。注意用 `==`：比的是「**同一个乘客对象**」。`t.passenger() == passenger` 为真才算同一人。③ 选政策（假期/普通）多态调用 `dayFare`。④ 调乘客的 `applyDiscount`。最后组装票据、票号 +1、入列表。

**`tick`（时钟 + 车动）**：

```java
public void tick() {
    currentTick++;
    for (Vehicle vehicle : vehicles) vehicle.advance();   // 每辆车动一下
}
```

这个循环**就是多态的高光时刻**：系统只管喊一句 `advance()`，Bus 走 +1、Train 走奇偶、Tram 走奇偶……系统完全不用知道谁是谁。

**三个时钟查询**：

```java
public int currentTick() { return currentTick; }
public int day()  { return currentTick / TICKS_PER_DAY; }   // 整除 24
public boolean isHoliday() { return day() == 0; }           // 只有 day 0 是假日
```

**`tickets`（返回副本）**：

```java
public List<Ticket> tickets() { return new ArrayList<>(tickets); }
```

为什么不直接 `return tickets`？因为测试 TIX03 会 `copy.clear()`。返回**新列表**，外面清空碰不到系统内部。

**`revenueCents`（营收）**：

```java
public long revenueCents() {
    long total = 0;
    for (Ticket t : tickets) total += t.finalFareCents();   // 累加实付
    return total;
}
```

---

# 第 3 步：Demo 怎么把它们串起来 + 对照 expected-output

`Demo.main()` 讲了个固定故事。跟着跑一遍你就全通了：

**① 建系统、加车、建乘客**

```java
TransitSystem system = new TransitApp();   // tick 0 → day 0 → 假期
system.addVehicle(new Bus("B1"));
system.addVehicle(new Train("T1"));
system.addVehicle(new Tram("L1"));
Passenger ava = new AdultPassenger("Ava");
Passenger ben = new ConcessionPassenger("Ben", "DV", 40);
Passenger cal = new ConcessionPassenger("Cal", "A", 60);
```

**② day 0 出三张票**

- `ava` 订 12 公里：base=300，假期且今天头一趟 → dayFare=150，成人 → final=**150** → `T1`
- `ava` 再订：今天第二趟 → dayFare=0 → final=**0** → `T2`
- `ben` 订：Ben 今天头一趟 → dayFare=150，DV 够格 → /2 = **75** → `T3`

对齐输出前三行 ✅

**③ 四个 tick**（时钟 +1，每辆车 advance）

输出：
```
tick 1: B1=1 IN_SERVICE, T1=4 AT_STOP, L1=1 APPROACHING
tick 2: B1=2 IN_SERVICE, T1=4 IN_SERVICE, L1=3 IN_SERVICE
tick 3: B1=3 IN_SERVICE, T1=8 AT_STOP, L1=4 APPROACHING
tick 4: B1=4 IN_SERVICE, T1=8 IN_SERVICE, L1=6 IN_SERVICE
```
Bus 每步 +1；Train 奇 +4 偶 0；Tram 应该奇 +1 偶 +2（**这就是上面 Tram 对不上的地方**）。

**④ 再 tick 到 24 → day 1（非假期）**，出三张：

- `ava` 订：非假期 → dayFare=300，成人 → **300** → `T4`
- `ben` 订：dayFare=300，DV → 150 → `T5`
- `cal` 订：dayFare=300，Cal 含 A 但 60 岁 → 不够格 → **300** → `T6`

**⑤ 拒绝测试**

- `book(null, ...)` → 抛异常 → 打印 "null passenger rejected; tickets=6"
- `new ConcessionPassenger("Dee","S",20)` → 非法类别 → 抛异常

**⑥ 汇总**

6 张票，营收 `150+0+75+300+150+300 = 975` ✅。最后清空 tickets 的副本，系统里还是 6 张（证明返回的是副本）。

---

# 第 4 步：`tests/PublicTest.java` 在测什么

5 个测试，每个钉一条行为，正好覆盖上面：

| 测试 | 测什么 | 靠哪个方法 |
|---|---|---|
| `CLK03` | `tick()` 让时钟正好 +1 | `tick()` / `currentTick()` |
| `HOL01` | day 0 是假期 | `isHoliday()` |
| `FARE01` | 正常日成人 = 距离 ×25（4→100） | `book` + base 公式 |
| `HFARE03` | 假期同一人第二趟免费（50→0） | `HolidayFare` + `earlierTripsToday` |
| `TIX03` | 清空 `tickets()` 的返回值不影响系统 | `tickets()` 返回副本 |

---

# 一句话总纲

`given` 给「车会动、票要有 base≥dayFare≥final、系统有 8 个方法」这些**规则和骨架**；你在 `src` 里填：**车怎么动**（Bus/Train/Tram 的 advance）、**怎么打折**（两种 Passenger）、**怎么计价**（两种 FarePolicy）、**怎么把前四者拼成一张票并记账**（TransitApp）。考试输出之所以对得上，是因为每一个 `src` 类都恰好接住了 `given` 留的那个洞。

唯一要复查的是 **Tram 偶数步的位移**（现在对不上 expected-output 的 1,3,4,6）。

要不要我接着把某一块再展开？比如「多态/继承到底怎么在内存里跑起来」，或者把 Tram 那段和 expected-output 逐格对一遍？