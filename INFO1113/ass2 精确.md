这次对了，**你自己实现的八个类都齐了**。现在可以完全结合你的代码讲，不再用假设代替实际实现。

我会先解释基础和运行过程，再逐题讲 R1–R3、C1–C10，并给你能在 viva 中使用的英文表达。下面的结果是根据代码逐步推导的；我没有在这里实际运行 GUI，也没有看到场景文件，因此示例金额不会冒充场景中的真实票据。

你的代码有几个特别容易被问到的点，先记住：

- **day 0 就是节假日。**
- **节假日同一个乘客对象当天第一张成功订的票半价，之后免费。**
- **不符合资格的优惠乘客不会被拒绝创建，而是不享受乘客折扣。**
- **Train 奇数次调用移动 4 并变成 `AT_STOP`，偶数次不移动但变成 `IN_SERVICE`。**
- **收入是每次遍历票据计算出来的，没有单独保存的收入字段。**
- **乘客身份通过 `==` 判断，不是通过名字判断。**

这些都要按实际代码解释，不能靠日常直觉猜。

---

**一、先建立整体理解：谁负责什么**

你的程序可以分成四组：

| 类或接口 | 责任 |
|---|---|
| `TransitApp` | 管理时间、车辆和票据，协调订票流程 |
| `Bus`、`Train`、`Tram` | 决定每次 `advance()` 如何改变位置和状态 |
| `NormalFare`、`HolidayFare` | 计算日期政策后的价格 |
| `AdultPassenger`、`ConcessionPassenger` | 计算乘客折扣后的价格 |
| `Trip` | 保存起点、终点、距离 |
| `Ticket` | 保存订票结果和三个阶段的价格 |
| `Vehicle`、`Passenger` | 提供共享状态和抽象行为 |
| `TransitSystem`、`FarePolicy` | 定义行为契约 |

最重要的一条调用链是：

```text
TransitApp.book(passenger, trip)
    │
    ├─ TransitApp：距离 × 25，算基础票价
    │
    ├─ NormalFare / HolidayFare：算日期票价
    │
    ├─ AdultPassenger / ConcessionPassenger：算最终票价
    │
    └─ Ticket：验证并保存这些结果
```

另一条是：

```text
TransitApp.tick()
    │
    ├─ currentTick 加 1
    │
    └─ 对每辆 Vehicle 调用 advance()
           ├─ Bus.advance()
           ├─ Train.advance()
           └─ Tram.advance()
```

你在 viva 中最重要的能力，就是沿着这两条链解释。

---

**二、理解代码前必须掌握的 Java 基础**

**1. 类、对象、字段、方法**

例如：

```java
Train train = new Train("T1");
```

- `Train` 是类，也是在这里声明的变量类型。
- `new Train("T1")` 创建一个对象。
- `train` 保存对这个对象的引用。
- `step`、`position` 是字段，保存对象状态。
- `advance()` 是方法，改变对象状态。

两个对象：

```java
Train a = new Train("T1");
Train b = new Train("T2");
```

各自拥有自己的 `step` 和 `position`。

这正是为什么某一列火车的运行阶段不会自然影响另一列。

**2. `extends` 和 `implements`**

你的代码：

```java
public class Train extends Vehicle
```

表示 Train 继承 Vehicle，Train 是一种 Vehicle。

```java
public class HolidayFare implements FarePolicy
```

表示 HolidayFare 实现 FarePolicy 规定的计算方法。

可以这样记：

- `extends`：继承父类的结构和行为。
- `implements`：满足接口规定的行为契约。

Java 一个类只能直接继承一个类，但可以实现多个接口。

**3. `super(...)` 是什么？**

例如：

```java
public AdultPassenger(String name) {
    super(name);
}
```

它调用 `Passenger` 的构造器：

```java
protected Passenger(String name) {
    if (name == null || name.isBlank()) {
        throw new IllegalArgumentException("passenger name required");
    }
    this.name = name.trim();
}
```

因此 AdultPassenger 不必重复验证、保存名字的代码。

`ConcessionPassenger` 同样先调用父类构造器，再验证优惠类型和年龄。

**4. 抽象类和抽象方法**

```java
public abstract class Passenger
```

不能直接创建：

```java
new Passenger(...); // 不允许
```

但它可以保存共同数据：

```java
protected final String name;
```

并要求子类实现：

```java
public abstract long applyDiscount(long fareCents);
```

意思是：

> 所有具体乘客都必须能计算折扣后的票价，但不同乘客的算法不同。

`Vehicle` 同理：

```java
public abstract void advance();
```

所有具体车辆必须提供自己的推进方式。

**5. 多态：声明类型和实际对象类型可以不同**

例如：

```java
Passenger p = new ConcessionPassenger("Amy", "A", 70);
```

- 声明类型：`Passenger`。
- 实际对象类型：`ConcessionPassenger`。

调用：

```java
p.applyDiscount(100);
```

实际执行：

```java
ConcessionPassenger.applyDiscount(...)
```

结果是 50。

这就是你代码中的运行时多态。

同样：

```java
Vehicle vehicle = new Train("T1");
vehicle.advance();
```

实际执行的是 `Train.advance()`。

**6. `@Override` 的作用**

它告诉编译器：

> 我打算重写父类方法，或者实现接口方法。

如果方法名或参数写错，编译器可以帮助发现。

但**不是 `@Override` 这个标记产生多态**；多态来自继承关系和方法重写。

**7. `private`、`protected`、`final`、`static`**

结合你的代码理解：

```java
private int step = 0;
```

`step` 只能由声明它的类直接访问，隐藏内部实现。

```java
protected double position;
```

车辆子类可以访问继承的 `position`；`protected` 也允许同包访问。

```java
private final List<Ticket> tickets = new ArrayList<>();
```

`final` 表示不能重新给这个字段赋另一个列表：

```java
tickets = new ArrayList<>(); // 不允许
```

但仍然可以：

```java
tickets.add(ticket); // 允许
```

所以 **final 引用不等于列表内容不可变**。

```java
private static final int TICKS_PER_DAY = 24;
```

- `static`：类共享。
- `final`：初始化后不能重新赋值。

一天多少 tick 对所有 TransitApp 都一样，所以适合做共享常量。

车辆 `step` 则不能随便改成 `static`，否则同类车辆会共享运行进度。

---

**三、时间系统：这是解释票价和车辆的前提**

你的字段：

```java
private int currentTick;
private int nextTicketNumber = 1;
```

构造器：

```java
public TransitApp() {
    this(0);
}
```

`this(0)` 调用同一个类中的另一个构造器：

```java
public TransitApp(int startTick)
```

所以默认系统从 tick 0 开始。

日期：

```java
public int day() {
    return currentTick / TICKS_PER_DAY;
}
```

其中一天是 24 ticks。整数除法舍弃小数部分：

| currentTick | day |
|---:|---:|
| 0 | 0 |
| 23 | 0 |
| 24 | 1 |
| 47 | 1 |
| 48 | 2 |

注意：这里没有真实日期时间库，day 是从零开始的模拟日编号。

节假日：

```java
int dayOfYear = day() % 365;
return dayOfYear == 0 || dayOfYear == 25 || dayOfYear == 114
    || dayOfYear == 358 || dayOfYear == 359;
```

`%` 是求余数。

因此节假日每 365 天重复：

```text
day 0   → holiday
day 1   → normal
day 25  → holiday
day 365 → holiday，因为 365 % 365 = 0
```

**但每年重复的是节假日规则，不是票据记录中的 day。**

统计当日票数时比较的是完整日编号：

```java
t.day() == today
```

所以 day 0 的票不会算进 day 365。

还有一个容易漏掉的事实：

> `new TransitApp(24)` 只是把系统时间设为 24，不会自动把之后加入的车辆推进 24 次。

车辆进度取决于自己的 `advance()` 被调用了多少次。

---

**四、逐步讲透 `book()`**

这是你最值得练熟的方法。

**第 1 步：验证输入引用**

```java
if (passenger == null || trip == null) {
    throw new IllegalArgumentException("passenger and trip required");
}
```

防止后面调用：

```java
trip.distance()
passenger.applyDiscount(...)
```

时发生空引用问题。

这里没有修改系统状态。

**第 2 步：记录当前日期，算基础票价**

```java
int today = day();
long base = (long) trip.distance() * CENTS_PER_DISTANCE_UNIT;
```

其中：

```java
CENTS_PER_DISTANCE_UNIT = 25;
```

所以：

\[
base = distance \times 25\text{ cents}
\]

距离 5：

```text
5 × 25 = 125 cents = $1.25
```

这里基础票价只看距离，不看：

- 乘客类型；
- 车辆类型；
- 起终点名字；
- CO₂；
- 当天第几次订票。

`long` 用来保存整数金额。显式转换让表达式明确使用长整数；实际上常量本身就是 `long`，即使没有这个转换，此处乘法也会提升为 `long`。

**第 3 步：统计同一乘客今天此前成功订了多少张票**

```java
int earlierToday = 0;
for (Ticket t : tickets) {
    if (t.passenger() == passenger && t.day() == today) earlierToday++;
}
```

两个条件同时满足才计数：

1. 是同一个乘客对象；
2. 是同一天的票。

非常重要：

```java
t.passenger() == passenger
```

比较对象身份，不比较名字。

例如：

```java
Passenger a = new AdultPassenger("Alex");
Passenger b = new AdultPassenger("Alex");
```

虽然名字一样：

```java
a == b // false
```

在你的系统中，他们的当日次数分开计算。

相反：

```java
Passenger b = a;
```

两个引用指向同一个对象，次数共享。

这也意味着：系统需要复用代表同一乘客的对象，才能按当前实现累计该乘客历史。

**第 4 步：选择日期政策**

```java
boolean holiday = isHoliday();
FarePolicy policy = holiday ? new HolidayFare() : new NormalFare();
```

三元运算符：

```java
condition ? valueIfTrue : valueIfFalse
```

即：

```text
holiday 为 true  → HolidayFare
holiday 为 false → NormalFare
```

变量使用接口类型 `FarePolicy`，后面可以统一调用：

```java
policy.dayFare(...)
```

**第 5 步：计算日期票价**

```java
long dayFare = policy.dayFare(base, earlierToday);
```

普通日：

```java
return baseCents;
```

不打日期折扣。

节假日：

```java
if (earlierTripsToday == 0) {
    return baseCents / 2;
}
return 0;
```

因此：

- 当天第一张成功订票：基础票价的一半；
- 当天第二张及以后：免费。

严格说，代码统计的是**成功订票记录**。它没有追踪乘客是否真正上车完成旅程。

**第 6 步：验证日期票价**

```java
if (dayFare < 0 || dayFare > base) {
    throw new IllegalArgumentException("day fare out of range");
}
```

保证：

```text
0 ≤ dayFare ≤ base
```

**第 7 步：计算乘客最终票价**

```java
long finalFare = passenger.applyDiscount(dayFare);
```

成人：

```java
return fareCent;
```

保持不变。

优惠乘客：

```java
return eligible ? fareCents / 2 : fareCents;
```

- 有资格：日期票价再减半；
- 无资格：保持日期票价。

这里输入的是 `dayFare`，**不是 `base`**。

**第 8 步：验证最终票价**

```java
if (finalFare < 0 || finalFare > dayFare) {
    throw new IllegalArgumentException("final fare out of range");
}
```

保证：

```text
0 ≤ finalFare ≤ dayFare
```

**第 9 步：构造票据**

```java
Ticket ticket = new Ticket("T" + nextTicketNumber, passenger, trip,
        today, holiday, base, dayFare, finalFare);
```

票号依次：

```text
T1、T2、T3……
```

`Ticket` 再验证自己的数据约束。

这里说明了两层验证的不同责任：

- `TransitApp` 验证计价流程的结果；
- `Ticket` 确保任何通过其构造器创建的票据都合法。

**第 10 步：提交订票状态**

```java
nextTicketNumber++;
tickets.add(ticket);
return ticket;
```

这之前，正常业务验证已经完成。

另外，`book()` **不会推进时钟，也不会推进车辆**。

---

**五、三阶段票价：一定要会手算**

用距离 5，也就是基础票价 125 分，做代码推导：

| 日期和乘客 | Base | Day fare | Final fare |
|---|---:|---:|---:|
| 普通日，成人 | 125 | 125 | 125 |
| 普通日，有资格优惠乘客 | 125 | 125 | 62 |
| 节假日，当天第一张，成人 | 125 | 62 | 62 |
| 节假日，当天第一张，有资格优惠乘客 | 125 | 62 | 31 |
| 节假日，当天后续票 | 125 | 0 | 0 |
| 节假日，当天第一张，无资格优惠乘客 | 125 | 62 | 62 |

为什么 125 除以 2 是 62？

因为 `long / int` 在这里进行整数除法：

```text
125 / 2 = 62
```

对非负金额，相当于向下取整，不是四舍五入。

例如票价链：

```text
125 → 62 → 31
```

则：

```text
日期优惠 = 125 - 62 = 63
乘客优惠 = 62 - 31 = 31
总支付   = 31
```

这里“半价”在奇数分金额上必须按整数实现解释。

再提醒一个容易口误的地方：

> 不符合优惠资格，只是没有额外的乘客折扣；仍然可以享受节假日政策。

---

**六、ConcessionPassenger：你的资格规则到底是什么**

允许的类型：

```java
"A", "D", "V", "AD", "AV", "DV", "ADV"
```

不接受：

```text
null
"S"
"a"
"DA"
"A "
```

因为代码使用精确字符串匹配，没有转大写、排序或者 `trim()`。

年龄要求：

```java
if (age < 0) {
    throw new IllegalArgumentException(...);
}
```

负年龄被拒绝。代码没有设置年龄上限。

资格判断：

```java
if (concessionType.equals("A") && age < 65) {
    this.eligible = false;
} else {
    this.eligible = true;
}
```

严格解释如下：

| 类型 | 年龄 | eligible |
|---|---:|---|
| A | 64 | false |
| A | 65 | true |
| D | 任意非负年龄 | true |
| V | 任意非负年龄 | true |
| AD、AV、DV、ADV | 任意非负年龄 | true |

最容易说错的是：

> 你的代码不是“只要包含 A 且不到 65 岁，就没有资格”。

它只检查：

```java
concessionType.equals("A")
```

所以 `"AD"`、年龄 20，仍然有资格。

组合类型也不会叠加多次折扣：

```text
ADV → 仍然只减半一次
```

最后区分三种情况：

- 类型非法：构造器抛异常，没有成功创建对象。
- 年龄为负：构造器抛异常。
- 类型 A 且不足 65：对象创建成功，但 `eligible = false`，付未经乘客折扣的日期票价。

---

**七、车辆：一步一步推导，别被状态名误导**

父类默认：

```java
position = 0.0
status = IN_SERVICE
```

其中 `position` 没有显式赋值，实例 `double` 字段默认是 `0.0`。

**Bus**

```java
position = position + 1;
status = VehicleStatus.IN_SERVICE;
```

每调用一次：

- 位置加 1；
- 状态设置为 `IN_SERVICE`。

**Train**

```java
step++;
if (step % 2 == 1) {
    position += 4;
    status = VehicleStatus.AT_STOP;
} else {
    status = VehicleStatus.IN_SERVICE;
}
```

`step` 从 0 开始，先加 1，再判断奇偶。

因此：

- 第 1、3、5……次：位置加 4，状态 `AT_STOP`；
- 第 2、4、6……次：位置不变，状态 `IN_SERVICE`。

**Tram**

```java
step++;
if (step % 2 == 1) {
    position += 1;
    status = VehicleStatus.APPROACHING;
} else {
    position += 2;
    status = VehicleStatus.IN_SERVICE;
}
```

因此：

- 奇数次：位置加 1，状态 `APPROACHING`；
- 偶数次：位置加 2，状态 `IN_SERVICE`。

假设三辆新车都加入一个从 tick 0 开始的系统，且每辆只添加一次：

| 调用 tick 次数 | Bus 位置 / 状态    | Train 位置 / 状态   | Tram 位置 / 状态    |
| ---------: | -------------- | --------------- | --------------- |
|          0 | 0 / IN_SERVICE | 0 / IN_SERVICE  | 0 / IN_SERVICE  |
|          1 | 1 / IN_SERVICE | 4 / AT_STOP     | 1 / APPROACHING |
|          2 | 2 / IN_SERVICE | 4 / IN_SERVICE  | 3 / IN_SERVICE  |
|          3 | 3 / IN_SERVICE | 8 / AT_STOP     | 4 / APPROACHING |
|          4 | 4 / IN_SERVICE | 8 / IN_SERVICE  | 6 / IN_SERVICE  |
|          5 | 5 / IN_SERVICE | 12 / AT_STOP    | 7 / APPROACHING |
|          6 | 6 / IN_SERVICE | 12 / IN_SERVICE | 9 / IN_SERVICE  |

**Train 的关键答法：**

> 奇数次调用会移动到新位置，然后把结果状态设为 AT_STOP。偶数次调用不改变位置，但把结果状态设为 IN_SERVICE。

不要说“`AT_STOP` 所以这次没有移动”，这与你的代码相反。

你的实现中，status 是这次调用结束时保存的状态；下一步行为通过 `step` 判断，并不是通过读取 status 判断。

---

**八、R1：选一张票，解释三个阶段**

你现场要点开真实票据，然后依次指出：

1. 距离；
2. 基础票价；
3. 订票日期是否节假日；
4. 该乘客当天此前票数；
5. 具体乘客类型和资格；
6. 最终金额。

可以用下面这段练习。数字是距离 5、有资格优惠乘客在节假日第一张票的示例：

> “The base fare is 125 cents. `TransitApp` calculates it as five distance units times 25 cents. This is the passenger’s first booking on a holiday, so `HolidayFare` returns 62 cents using integer division. `ConcessionPassenger` then halves that amount to 31 cents because the passenger is eligible. `Ticket` stores the three amounts.”

中文理解：

> TransitApp 算基础价，HolidayFare 算日期价，ConcessionPassenger 算最终价，Ticket 保存。

老师问：

> Why is it 62 rather than 62.5?

答：

> “The fares use integer cents, so division by two truncates the fractional cent.”

老师问：

> What happens on the next booking today?

答：

> “For the same passenger object, `earlierToday` is now one, so `HolidayFare` returns zero.”

---

**九、R2：按一下 Step，解释每辆车做了什么**

你可以先定位系统：

```java
public void tick() {
    currentTick++;
    for (Vehicle vehicle : vehicles) vehicle.advance();
}
```

说明：

1. 系统时间先加一；
2. 遍历车辆列表；
3. 每个列表项调用一次 `advance()`；
4. 每种车辆根据自己的实现更新。

以新系统第二个 tick 为例：

> “The clock increases to two. The bus moves from one to two and remains in service. The train’s step becomes two, so it takes the even branch: its position stays at four and its status becomes `IN_SERVICE`. The tram also takes its even branch, moving from one to three and becoming `IN_SERVICE`.”

老师追问：

> Is the train using the system tick to choose the branch?

答：

> “No. It uses its own instance field, `step`, which counts calls to that train’s `advance()`.”

这很重要：车辆中途加入时，其 `step` 不会自动等于全局 tick。

---

**十、R3：解释两个乘客为什么支付总额不同**

不要只看乘客名称或类型就下结论。

需要检查：

- 订了多少张票；
- 每次距离；
- 哪一天订的；
- 当天第一张还是后续；
- 是否有优惠资格；
- 整数舍入影响。

你可以这样做一个练习案例：

```text
day 0，节假日
成人 A：distance 5，然后 distance 8
有资格优惠乘客 B：distance 5，然后 distance 8
```

推导：

| 乘客 | 第一张票 | 第二张票 | 支付合计 |
|---|---:|---:|---:|
| 成人 A | 125 → 62 → 62 | 200 → 0 → 0 | 62 |
| 优惠 B | 125 → 62 → 31 | 200 → 0 → 0 | 31 |

口述：

> “Both passengers receive the same holiday discount: their first booking is half price, and later bookings that day are free. The eligible concession passenger also receives a passenger discount on the first ticket, reducing 62 cents to 31 cents. The adult pays 62 cents.”

界面的具体汇总范围需要看你运行时显示的列；解释时用该行对应票据核对，别把全系统收入和单个乘客支出混为一谈。

---

**十一、C1：为什么 rejected booking 不留下东西？**

你这里可以有根据地回答：

> 在正常业务验证和票据构造成功前，`book()` 没有修改内部票据列表，也没有递增票号。

执行顺序：

```text
检查 null
→ 计算基础价
→ 统计历史
→ 计算并验证日期价
→ 计算并验证最终价
→ 构造 Ticket
→ 增加票号
→ 加入列表
```

关键代码：

```java
Ticket ticket = new Ticket(...);
nextTicketNumber++;
tickets.add(ticket);
```

构造器如果拒绝，后面两行不会执行。

还有一个你的实现特别好的解释点：

```java
public long revenueCents() {
    long total = 0;
    for (Ticket ticket : tickets) total += ticket.finalFareCents();
    return total;
}
```

收入没有独立字段。

所以：

> 失败订票没有进入列表，就不会被收入计算包含，也不会被后续 `earlierToday` 统计包含。

英文：

> “All business validation happens before the ticket number and ticket list are updated. If validation or ticket construction rejects the booking, neither changes. Revenue is derived from the stored tickets, so a rejected booking cannot increase revenue or the earlier-trip count.”

重要边界和严谨限定：

- 这个解释针对正常业务拒绝路径。
- 代码不是对任何运行时故障都提供事务保证，例如极端情况下 `tickets.add()` 因内存不足失败，票号此前已递增。
- `Passenger` 是可扩展类型，理论上某个其他实现的 `applyDiscount()` 可以有自身副作用；你现在两个乘客类没有这种副作用。

口试一般不用主动展开内存不足，但不要说“绝对任何异常都能自动回滚”。

老师问：

> Why validate the final fare?

答：

> “The application accepts the `Passenger` abstraction, so it should not assume every implementation returns a valid amount. It rejects negative fares or fares above the day fare.”

---

**十二、C2：一个循环为什么能移动三种车辆？**

展示：

```java
private final List<Vehicle> vehicles = new ArrayList<>();
```

和：

```java
for (Vehicle vehicle : vehicles) vehicle.advance();
```

完整逻辑：

- 列表保存的是 Vehicle 引用；
- Bus、Train、Tram 都是 Vehicle 的子类；
- Vehicle 声明了 `advance()`；
- 三个子类都重写了它；
- Java 根据实际对象类型执行对应版本。

英文：

> “The list stores `Vehicle` references. Each concrete vehicle overrides `advance()`, so Java dispatches the call to the actual object’s implementation. The loop does not need `instanceof` or a branch for each vehicle type.”

设计理由：

> 新类型只要遵守 Vehicle 契约，通常不用修改这个循环。

一个真实边界：

```java
addVehicle(vehicle)
```

只检查 null，没有检查重复。

因此如果同一个对象被加入两次，一个 tick 会对它调用两次 `advance()`。

所以严格说，循环是“每个列表项一次”，不保证“每个独立对象一次”。

---

**十三、C3：phase 存哪里？为什么在那里？**

你可以选 Train：

```java
private int step = 0;
```

`step` 保存调用次数，奇偶性代表两个阶段：

```java
step % 2 == 1
```

即：

```text
奇数阶段：移动 4，AT_STOP
偶数阶段：不移动，IN_SERVICE
```

为什么是实例字段？

- 需要跨多次调用保存。
- 每辆车需要独立进度。

为什么不是局部变量？

```java
public void advance() {
    int step = 0;
    step++;
}
```

每次都变成 1，永远进入奇数分支。

为什么不是 static？

同一个类的所有车辆会共享计数，互相干扰。

为什么不放在 TransitApp？

系统只负责通知车辆推进，不应该管理每种车辆的内部阶段。

英文：

> “The train remembers its phase in the private instance field `step`. Its parity selects the branch. An instance field preserves the phase between calls and keeps each train independent. A local variable would reset, and a static field would share the phase across trains.”

可讲的取舍：

> 实际只需要两个阶段，布尔值或只取 0、1 的状态字段也可以表达。当前计数器直接易懂，但不需要无限增长。

严谨地说，`int` 长期溢出后负奇数 `% 2` 是 `-1`，不满足 `== 1`，因此无限长模拟下当前判断会出问题。正常 viva 场景无需运行到这种规模；设计追问时可以把它作为改用交替状态的理由。

---

**十四、C4：HolidayFare 的次数从哪里来，为什么不拿整张票据表？**

展示 TransitApp：

```java
for (Ticket t : tickets) {
    if (t.passenger() == passenger && t.day() == today) earlierToday++;
}
```

再展示：

```java
policy.dayFare(base, earlierToday);
```

最后展示 HolidayFare：

```java
if (earlierTripsToday == 0) {
    return baseCents / 2;
}
return 0;
```

责任分工：

- TransitApp 拥有历史，负责查询。
- HolidayFare 只负责把输入转换为价格。

英文：

> “`TransitApp` counts stored tickets for the same passenger object and the current day. It passes that count into `HolidayFare`. The policy only needs the count, so it does not need access to the whole ticket list or knowledge of how tickets are stored.”

为什么好？

- 政策不依赖 Ticket 的存储细节；
- 不必重复乘客和日期筛选；
- 不会拿到内部列表去修改；
- 测试时直接传 0、1、2 即可。

取舍：

> 当前每次订票扫描所有票据，复杂度是 O(n)。小系统简单清晰；规模大时可以维护“乘客＋日期”的计数，但那会增加必须保持一致的状态。

边界：

> 失败订票不会加入列表，免费但成功的票会加入列表，后者也算一次此前订票。

---

**十五、C5：Passenger 为什么是抽象类，FarePolicy 为什么是接口？**

针对你的代码回答：

`Passenger` 共享：

```java
name
名字验证
name()
```

差异：

```java
applyDiscount()
```

所以抽象类可以复用共同状态和实现，同时要求子类提供差异行为。

`FarePolicy`：

```java
long dayFare(long baseCents, int earlierTripsToday);
```

只需要定义计算能力。

你的 NormalFare 和 HolidayFare 都没有实例字段，是不保存历史的策略对象。

英文：

> “`Passenger` shares a name field, constructor validation and the `name()` method, but leaves discount behaviour abstract. `FarePolicy` only defines a calculation contract. The current fare policies do not need shared instance state, so an interface is appropriate.”

别说：

> “接口不能有方法实现。”

现代 Java 接口可以有某些带实现的方法。你的这个接口只声明抽象方法而已。

---

**十六、C6：tickets() 为什么不能直接返回自己的列表？**

你的实现：

```java
return new ArrayList<>(tickets);
```

它创建一个新的列表，复制元素引用。

外部：

```java
List<Ticket> result = app.tickets();
result.clear();
```

清空的是副本，不影响系统内部记录。

如果直接：

```java
return tickets;
```

外部就可以：

```java
app.tickets().clear();
```

导致：

- 全部售票历史消失；
- `revenueCents()` 重新计算后降低；
- 当天次数被重置；
- 节假日政策被错误地重新当作第一张票；
- 票号计数仍然继续，历史和编号之间出现异常。

或者外部直接加入 Ticket，绕过 `book()`。

这里要结合你的实现讲：**你的收入会随内部列表被篡改而改变**，不是“收入字段没有同步”，因为你没有收入字段。

英文：

> “I return a defensive copy of the list. Callers can modify that copy without changing the system’s ticket history. If I returned the internal list, callers could bypass `book()`, altering revenue and the earlier-trip count.”

老师问：

> Is the returned list immutable?

答：

> “No. The copy is mutable, but modifying its structure does not affect the internal list.”

老师问：

> Is it a deep copy?

答：

> “No. It copies the list structure, while both lists reference the same ticket objects.”

你的 Ticket 金额字段不能修改，但 Ticket 引用 Passenger，所以不能仅凭列表复制就宣称整个对象图都深度不可变。

取舍：每次复制需要 O(n) 时间和额外空间。

---

**十七、C7：ConcessionPassenger 为什么是子类，资格哪里检查，TransitApp 知道什么？**

三部分分开答。

**为什么是子类？**

它是 Passenger 的一种：

- 复用姓名及验证；
- 增加优惠类型、年龄、资格；
- 重写折扣行为。

这样 TransitApp 统一调用：

```java
passenger.applyDiscount(dayFare)
```

不需要判断成人还是优惠乘客。

**资格哪里检查？**

构造器：

```java
if (concessionType.equals("A") && age < 65)
```

结果保存在：

```java
private final boolean eligible;
```

强调：

> 不符合 A 年龄条件不会抛异常，只会把资格设为 false。

**TransitApp 知道什么？**

它知道对象满足 Passenger 契约。

它不知道也不查询：

```text
age
concessionType
isEligible()
```

这些方法即使公开存在，`book()` 也没用它们。

英文：

> “`ConcessionPassenger` extends `Passenger` to reuse name handling and encapsulate concession-specific data and behaviour. Eligibility is calculated in its constructor and stored in `eligible`. `TransitApp` only calls `applyDiscount()` and validates the returned fare; it does not inspect the concession type or age.”

设计取舍：

> 用字段表达类型也可以设计，但如果把各类折扣分支放进 TransitApp，就会让协调类承担乘客业务规则。当前设计通过子类保持职责集中。

---

**十八、C8：新增 HoverBus、EcoBus、SnakeBus 怎么改？**

你的 Bus 没有标成 `final`，所以技术上可以继承。

但要看新车的行为：

- 如果完全沿用 Bus 的移动，只增加其他属性，可以考虑继承 Bus。
- 如果有独立移动阶段，可以直接继承 Vehicle。
- 如果已有 Bus 行为仍可复用，也可以继承 Bus 并重写相关行为。

例如概念结构：

```java
class HoverBus extends Vehicle {
    @Override
    public void advance() {
        // 新车辆自己的移动规则
    }
}
```

需要变化：

- 增加新类；
- 创建车辆的地方要能创建它；
- 如果输入文件使用类型名称，相关创建入口也要识别新类型。

通常不变：

```java
TransitApp.addVehicle(Vehicle vehicle)
TransitApp.tick()
List<Vehicle>
```

现有车辆的实现通常也不必改。

英文：

> “I would add a concrete vehicle class. If it genuinely shares bus behaviour, it could extend `Bus`; otherwise it can extend `Vehicle` directly. The creation code must construct the new type, but `addVehicle()` and the tick loop can remain unchanged because they use `Vehicle`.”

重要边界：

> 你的 `book()` 没有接收车辆，也没有把票据与某辆车关联。因此仅仅新增 EcoBus，不会自动改变票价。

这正好能衔接 C9。

---

**十九、C9：按路线 CO₂ 打折，哪些类会受影响？**

这题最重要的不是说“新增一个 EcoFare”，而是发现：

> **当前程序不知道选了哪条路线，也没有 CO₂ 数据。**

现有：

```java
Trip(origin, destination, distance)
```

没有路线身份或排放。

现有：

```java
book(Passenger passenger, Trip trip)
```

没有车辆或路线参数。

现有：

```java
dayFare(long baseCents, int earlierTripsToday)
```

也没有排放输入。

因此必须先解决信息来源。

一个合理的设计回答：

1. 引入路线身份和 CO₂ 数据，并让订票知道选择的路线。
2. 在计价过程中加入环保规则。
3. 明确环保优惠与节假日、乘客优惠的先后顺序。
4. 决定票据是否需要单独记录环保优惠。

你当前基础票价在：

```java
long base = (long) trip.distance() * CENTS_PER_DISTANCE_UNIT;
```

如果环保规则放在日期政策之前，TransitApp 这一段或被它调用的新计价组件会变化。

NormalFare、HolidayFare 可以继续接收调整后的基础价，但这意味着“base fare”的业务含义需要明确。

如果要求单独展示：

```text
原始基础价 → 环保价 → 日期价 → 最终价
```

当前 Ticket 只有三个阶段，就需要新的记录设计。

你的 supplied 文件不允许直接修改，所以答题要区分：

> 这是未来需求下的设计变更建议；如果原有给定契约必须保持不变，就需要额外上下文、包装对象或扩展入口来表达路线选择。不能假装当前参数已经足够。

英文：

> “The current trip has no route identity or CO₂ value, so the booking calculation first needs access to the selected route. I would add the eco rule to the pricing flow and define its order relative to the existing discounts. Passenger eligibility and vehicle movement can stay unchanged. The ticket model would need extending if the eco discount must be shown separately.”

特别好的边界情况：

> 节假日同一乘客的后续票已经免费。如果仍然保留免费规则，低排放路线不可能比零元还便宜。因此“更便宜”应明确为收费情况下的优惠，或者重新定义与免费政策的优先级。

这是直接来自你代码的真实设计冲突，讲出来很有说服力。

---

**二十、C10：新增 S，学生年龄小于 26**

你的现有类已经按代码保存类型，所以**不一定要新增子类**。

至少修改两个地方。

第一处：允许 `"S"`：

```java
switch (concessionType) {
    ...
    case "S":
        break;
}
```

第二处：资格规则。

如果 S 同样享受半价，可以表达为：

```java
if (concessionType.equals("A")) {
    this.eligible = age >= 65;
} else if (concessionType.equals("S")) {
    this.eligible = age < 26;
} else {
    this.eligible = true;
}
```

此前的 `age < 0` 检查继续保留。

**不能只增加 `case "S"`。**

因为你当前代码的 else 会让所有非纯 A 类型都符合资格，那么 S、年龄 40 也会得到半价。

不需要变化：

```java
applyDiscount()
```

前提是学生也是同样半价。

也不需要变化：

- AdultPassenger；
- NormalFare、HolidayFare；
- TransitApp 的折扣调用；
- Ticket；
- 车辆。

输入端如果有独立的类型白名单，也要更新，但不能在没看到它的情况下断言具体位置。

英文：

> “I would add S to the accepted codes and explicitly calculate its eligibility as age below 26. Adding the code alone would be wrong because the current default eligibility branch returns true. If students receive the same half-price discount, `applyDiscount()` and `TransitApp` can remain unchanged.”

边界：

```text
25 → eligible
26 → not eligible
```

另一个要明确的需求：

> 是否允许 AS、DS 等组合？当前代码明确枚举允许的组合，并不支持任意字符组合。新增 S 不自动代表所有包含 S 的组合都合法。

---

**二十一、你最应该背熟的是这几段逻辑，不是整篇文章**

**订票逻辑：**

> 距离乘 25 得基础价；系统按同一个乘客对象和同一天统计历史票；日期政策算 day fare；乘客对象算 final fare；验证后构造 Ticket，最后更新票号和列表。

**车辆逻辑：**

> tick 先增加系统时间，再统一调用 advance；实际车辆类决定行为；Train 和 Tram 用自己的 step 奇偶保存阶段。

**封装逻辑：**

> TransitApp 管历史，FarePolicy 管日期规则，Passenger 管乘客折扣，Vehicle 管移动，Ticket 保存结果。

**失败逻辑：**

> 正常业务验证失败发生在提交之前；没有票进入列表，就不影响历史次数或计算出的收入，票号也不增加。

**扩展逻辑：**

> 新类型优先把变化放在对应职责的类中；但如果新需求需要现有接口没有提供的信息，就必须说明数据和契约如何扩展。

练习时先打开 `TransitApp.book()`，用 **“distance 5、day 0、有资格优惠乘客、当天第一张票”** 口头追踪出 `125 → 62 → 31`；再打开三种车辆，解释前两个 tick。把这两条运行路径讲熟后，绝大多数 viva 题都能落到具体代码上。





下面按 viva 的真实问法，给你“**老师问什么，你应该怎么回答**”。你要记住回答结构：

> **先指出代码，再说明执行顺序，最后解释设计理由和边界情况。**

---

## R1：选一张票，解释三个票价阶段

你可以这样回答：

> 这张票有三个价格阶段。  
> 第一阶段是基础票价，由 `TransitApp.book()` 根据行程距离计算：
>
> ```java
> base = trip.distance() * 25;
> ```
>
> 第二阶段是日期政策后的票价。如果当天不是节假日，使用 `NormalFare`，价格不变。如果是节假日，使用 `HolidayFare`：当天同一个乘客的第一张票是基础价的一半，之后的票是免费。
>
> 第三阶段是乘客折扣后的最终票价。`AdultPassenger` 不打折；符合资格的 `ConcessionPassenger` 把日期票价再除以二。
>
> 最后，`Ticket` 保存这三个金额。

例如距离是 5：

```text
基础票价 = 5 × 25 = 125 cents
节假日第一张 = 125 / 2 = 62 cents
优惠乘客最后再减半 = 62 / 2 = 31 cents
```

你还要指出：

> 这里使用整数 cents，所以 `125 / 2` 的结果是 62，而不是 62.5。

如果老师问“哪个类产生每个数字”：

```text
基础票价：TransitApp
日期票价：NormalFare 或 HolidayFare
最终票价：AdultPassenger 或 ConcessionPassenger
保存结果：Ticket
```

---

## R2：按一次 Step，解释每辆车做了什么

先解释系统：

> `TransitApp.tick()` 先把 `currentTick` 加一，然后遍历所有车辆，对每辆车调用 `advance()`。虽然循环中的变量类型是 `Vehicle`，但 Java 会根据实际对象调用 `Bus`、`Train` 或 `Tram` 的具体方法。

然后分别解释。

### Bus

> `Bus.advance()` 每次把位置加 1，并把状态设置为 `IN_SERVICE`。

### Train

> `Train` 有一个自己的 `step` 字段。每次调用 `advance()`，先把 `step` 加一。奇数次调用时，位置加 4，状态变成 `AT_STOP`；偶数次调用时，位置不变，状态变成 `IN_SERVICE`。

例如：

```text
第 1 次：位置 0 → 4，状态 AT_STOP
第 2 次：位置保持 4，状态 IN_SERVICE
第 3 次：位置 4 → 8，状态 AT_STOP
```

### Tram

> `Tram` 也使用自己的 `step`。奇数次调用时位置加 1，状态是 `APPROACHING`；偶数次调用时位置加 2，状态是 `IN_SERVICE`。

例如：

```text
第 1 次：位置 0 → 1，APPROACHING
第 2 次：位置 1 → 3，IN_SERVICE
```

最后补一句：

> 每种车的行为不同，是因为每个子类都重写了 `advance()`。

---

## R3：解释 Passengers 面板的两行，为什么总价不同？

你不要只说“一个人有折扣”。你要先比较票据。

可以这样回答：

> 我会比较这两位乘客的票据数量、行程距离、订票日期、当天此前已经订过几张票，以及乘客是否符合优惠资格。最终总额是这些票的 `finalFareCents()` 之和。

如果其中一个是成人，另一个是有资格的优惠乘客：

> 两个人可能得到相同的基础票价和节假日票价，但是符合资格的 `ConcessionPassenger` 会在日期票价的基础上再减半，而 `AdultPassenger` 不会打折，所以他们的最终总额不同。

如果差异来自节假日次数：

> 在节假日，同一个乘客当天第一张票半价，之后的票免费。因此即使两个人类型一样，如果他们当天此前的订票数量不同，最终总额也可能不同。

你最好补一句：

> 我可以打开两张具体票，分别比较 `baseFareCents()`、`dayFareCents()` 和 `finalFareCents()`，确认差异发生在哪一个阶段。

---

## C1：展示 `book()`，说明票价流程，以及拒绝后为什么什么都不留下

你可以按顺序回答：

> `book()` 的流程是：
>
> 1. 检查 `passenger` 和 `trip` 不能是 `null`；
> 2. 根据距离计算基础票价；
> 3. 遍历已有票据，计算同一个乘客当天此前的票数；
> 4. 根据是否节假日选择 `NormalFare` 或 `HolidayFare`；
> 5. 计算并验证 `dayFare`；
> 6. 调用乘客的 `applyDiscount()`，计算并验证 `finalFare`；
> 7. 创建 `Ticket`；
> 8. 只有创建成功后，才增加票号并把票加入列表。

关键代码是：

```java
Ticket ticket = new Ticket(...);
nextTicketNumber++;
tickets.add(ticket);
```

所以：

> 如果前面的输入检查、票价检查或 `Ticket` 构造失败，程序会抛出异常，后面的 `nextTicketNumber++` 和 `tickets.add(ticket)` 不会执行。因此这张被拒绝的票不会进入票据列表，也不会影响之后的历史次数和收入。

还要说明：

> `revenueCents()` 每次都是遍历票据列表，把每张票的最终价格加起来。因此没有进入列表的失败订票不会被算进收入。

如果老师问“为什么异常本身不能保证没有副作用”：

> 因为异常不会自动撤销已经执行的修改，所以必须把修改列表和票号的操作放在所有验证之后。

---

## C2：展示 `tick()`，为什么一个循环能处理三种车辆，而且没有 `instanceof`？

直接这样说：

> `vehicles` 的类型是 `List<Vehicle>`，里面可以保存 `Bus`、`Train` 和 `Tram`，因为它们都是 `Vehicle` 的子类。
>
> `Vehicle` 声明了抽象方法 `advance()`，每种具体车辆都重写了这个方法。循环只需要写：
>
> ```java
> for (Vehicle vehicle : vehicles) {
>     vehicle.advance();
> }
> ```
>
> Java 会根据实际对象类型执行对应的 `advance()`。如果对象是 Bus，就执行 `Bus.advance()`；如果是 Train，就执行 `Train.advance()`。

最后说设计理由：

> 因为使用了多态，所以不需要写很多 `instanceof` 和类型判断。以后加入新的车辆类型，只要继承 `Vehicle` 并实现 `advance()`，这个循环通常不用修改。

如果老师问“多态是什么”：

> 变量可以声明为父类类型，但实际引用子类对象。调用重写方法时，运行时会执行实际子类的方法。

---

## C3：展示 Train 或 Tram，phase 记在哪里，为什么放在那里？

你的代码没有叫 `phase` 的字段，而是用：

```java
private int step = 0;
```

所以要诚实地说：

> 我的代码没有直接叫 `phase` 的字段，而是用私有实例字段 `step` 记住车辆当前处于哪一次阶段。`step` 的奇偶性决定下一次行为。

以 Train 为例：

```java
step++;
if (step % 2 == 1) {
    position += 4;
    status = VehicleStatus.AT_STOP;
} else {
    status = VehicleStatus.IN_SERVICE;
}
```

然后解释为什么：

> `step` 必须是实例字段，因为它需要在多次 `advance()` 调用之间保存，而且每辆车都需要自己的进度。不能用局部变量，因为方法结束后状态就丢失；也不能用 `static`，否则所有 Train 会共享同一个计数器。

如果老师问为什么不放在 `TransitApp`：

> 因为运行阶段属于具体车辆的内部行为。`TransitApp` 只负责通知车辆推进，不应该了解 Train 或 Tram 的内部规则。

---

## C4：展示 `HolidayFare`，earlier trips 从哪里来？为什么不传完整票据列表？

展示 `TransitApp` 里的代码：

```java
for (Ticket t : tickets) {
    if (t.passenger() == passenger && t.day() == today) {
        earlierToday++;
    }
}
```

然后说：

> `TransitApp` 拥有票据列表，所以由它负责统计历史。它只统计同一个乘客对象、同一天、当前订票之前已经成功保存的票。

接着：

```java
policy.dayFare(base, earlierToday);
```

然后说：

> `HolidayFare` 只接收基础票价和此前的票数。如果 `earlierToday == 0`，返回基础票价的一半；否则返回 0。

为什么不把整个列表传进去：

> 因为 `HolidayFare` 只需要一个数字，不需要知道票据如何保存，也不应该拥有或修改整个票据列表。这样可以降低耦合，也让 `HolidayFare` 更容易单独测试。

非常重要的细节：

> 代码使用 `t.passenger() == passenger`，比较的是同一个对象，而不是名字。如果两个 Passenger 对象名字相同但不是同一个对象，代码会把他们当成不同的乘客。

---

## C5：为什么 `Passenger` 是抽象类，而 `FarePolicy` 是接口？

你可以这样回答：

> `Passenger` 是抽象类，因为不同乘客共享一些数据和代码。父类保存 `name`，负责验证名字，并提供 `name()` 方法；但是具体的折扣算法由子类实现，所以 `applyDiscount()` 是抽象方法。

然后解释接口：

> `FarePolicy` 只定义一个行为：根据基础票价和当天此前的出行次数计算日期票价。它没有需要所有策略共享的字段或构造逻辑，所以用接口表示这个计算契约比较合适。

结合你的类：

```text
AdultPassenger → 不打乘客折扣
ConcessionPassenger → 根据资格决定是否减半
NormalFare → 不改变基础价
HolidayFare → 根据 earlierTripsToday 计算节假日价格
```

如果老师问“FarePolicy 能不能写成抽象类”：

> 理论上可以，但当前策略只需要一个行为契约，不需要共享实例状态，所以接口更合适。

---

## C6：展示 `tickets()`，如果返回自己的列表会怎样？

你的实现是：

```java
return new ArrayList<>(tickets);
```

你可以说：

> 这里返回的是一个新的列表副本，而不是内部列表本身。调用者可以修改这个副本，但不会修改 `TransitApp` 内部的票据列表。

如果直接返回：

```java
return tickets;
```

外部就能这样做：

```java
app.tickets().clear();
```

后果是：

- 所有历史票据被删除；
- `revenueCents()` 计算出的收入会改变；
- `earlierToday` 的统计会改变；
- 外部可以加入没有经过 `book()` 验证的票。

所以：

> 返回副本保护了系统内部的集合，避免外部绕过 `book()` 修改系统状态。

但要准确说明：

> 这是浅复制。列表结构是新的，但是里面的 `Ticket` 引用仍然指向原来的票据对象。

如果老师问“返回的列表是不是不可修改”：

> 不是。返回的列表本身可以修改，但修改它不会影响内部列表。

---

## C7：展示 `ConcessionPassenger`，为什么是子类而不是 Passenger 的字段？

你可以这样回答：

> `ConcessionPassenger` 是一种特殊的 `Passenger`。它有自己的优惠类型、年龄和资格判断，并且有不同的 `applyDiscount()` 行为，所以把这些规则放在子类中，可以让乘客类型自己负责自己的折扣逻辑。

资格检查的位置：

```java
if (concessionType.equals("A") && age < 65) {
    this.eligible = false;
} else {
    this.eligible = true;
}
```

你要说得非常准确：

> 资格是在 `ConcessionPassenger` 构造器中检查的。类型和年龄通过验证后，资格保存到 `eligible` 字段中。对于类型 `"A"` 且年龄小于 65 的乘客，对象仍然可以创建，但 `eligible` 是 `false`，所以不会享受乘客折扣。

其他类型：

> `"D"`、`"V"`、`"AD"`、`"AV"`、`"DV"`、`"ADV"` 在当前代码中都会被视为 eligible，只要年龄不是负数。

`TransitApp` 知道什么：

> `TransitApp` 只把它当作 `Passenger` 使用，并调用 `applyDiscount()`。它不需要知道具体的优惠类型、年龄或者资格规则。

设计优点：

> 如果以后加入新的乘客类型，主要修改乘客类，而不是在 `TransitApp` 中不断增加类型判断。

---

## C8：增加 HoverBus、EcoBus 或 SnakeBus，哪些类修改？

回答步骤：

> 首先增加一个新的具体车辆类，让它继承 `Vehicle`，并实现 `advance()`。

例如：

```java
public class HoverBus extends Vehicle {
    @Override
    public void advance() {
        // HoverBus 自己的移动规则
    }
}
```

如果它确实完全共享 Bus 的行为，也可以考虑：

```java
class HoverBus extends Bus
```

但要说明：

> 不能只因为名字里有 Bus 就一定继承 Bus。要看它是否真正符合 Bus 的行为和设计。

需要修改：

- 新增车辆类；
- 创建车辆的代码，如果系统需要识别新的车辆名称；
- 如果场景文件或加载代码支持车辆类型字符串，也要更新相应的创建逻辑。

通常不需要修改：

```java
TransitApp.tick()
TransitApp.addVehicle()
List<Vehicle>
```

因为这些代码已经依赖父类 `Vehicle` 和多态。

你可以这样总结：

> 新增车辆主要扩展具体车辆类和创建入口；通用的 tick 循环可以保持不变。

---

## C9：新增环保折扣，哪些类会变化？

先指出当前代码的限制，这是高分关键：

> 目前 `Trip` 只有起点、终点和距离，没有路线身份或 CO₂ 成本。`book()` 也没有接收路线选择，`FarePolicy` 只收到基础票价和此前票数。因此当前数据不足以计算两条路线的 CO₂ 差异。

然后说设计步骤：

> 首先需要让系统知道乘客选择了哪条路线，以及该路线的 CO₂ 成本。可以增加路线对象，或者扩展订票时传入的路线信息。

之后：

> 然后把环保规则放进计价流程。需要决定它是在基础票价之前、日期政策之前，还是作为独立的折扣阶段执行。

可能涉及：

```text
TransitApp：协调新的路线和环保计算
Trip 或新的 Route 类：保存路线和 CO₂ 信息
FarePolicy 或新的 EcoFarePolicy：计算环保价格
Ticket：如果要单独显示环保折扣，也需要保存额外阶段
```

通常不变：

```text
Passenger 的年龄和优惠资格规则
AdultPassenger
ConcessionPassenger
Vehicle 的移动逻辑
tick()
```

一个非常好的边界情况：

> 如果节假日当天后续票已经是 0 cents，那么环保路线不可能比它更便宜。所以环保折扣和节假日免费政策的先后顺序必须明确。

---

## C10：增加学生优惠 S，年龄小于 26，哪些变化？

首先修改允许的类型：

```java
case "S":
    break;
```

然后增加学生资格规则。

例如：

```java
if (concessionType.equals("A")) {
    eligible = age >= 65;
} else if (concessionType.equals("S")) {
    eligible = age < 26;
} else {
    eligible = true;
}
```

你要特别指出：

> 只把 `"S"` 加入合法类型还不够。因为当前代码的默认分支会让所有非 `"A"` 类型都 eligible，这会导致 40 岁的学生类型也获得折扣。

年龄边界：

```text
25 岁：符合
26 岁：不符合
```

如果学生和其他优惠一样都是半价，那么以下代码不需要改变：

```java
public long applyDiscount(long fareCents) {
    return eligible ? fareCents / 2 : fareCents;
}
```

`TransitApp` 也不需要知道学生的存在，因为它仍然只调用：

```java
passenger.applyDiscount(dayFare);
```

不变的部分：

- `AdultPassenger`
- `NormalFare`
- `HolidayFare`
- `Ticket`
- 车辆逻辑
- `TransitApp` 的整体票价流程

如果题目要求学生必须有学生身份，而不只是年龄小于 26，还需要额外保存或验证学生身份。仅凭年龄不能证明一个人是学生。

---

## 最后给你一段总的开场回答

如果老师让你先概括设计，可以说：

> 我的系统把不同职责分开。`TransitApp` 负责协调订票、时间、车辆和票据；`NormalFare` 和 `HolidayFare` 负责日期相关票价；不同的 `Passenger` 子类负责乘客折扣；不同的 `Vehicle` 子类负责自己的移动方式。系统通过抽象类、接口和多态避免在 `TransitApp` 中写大量类型判断。票据在所有价格验证成功后才加入列表，而 `tickets()` 返回列表副本，保护系统内部状态。

这段话能很好地覆盖整个设计。