好的！那我重新为你设计一个**完美的R语言3图方案**，使用R生态系统中的多样化可视化库。

## 完美3图方案：NYPD犯罪数据分析（R版本）

---

### **Figure 1: 交互式地理热力图 - 犯罪空间分布**
**库：leaflet + sf + viridis**

**分析目的**：回答"哪里最危险？"

**具体实现**：
```r
library(leaflet)
library(sf)
library(dplyr)
library(viridis)

# 主图：Leaflet交互式地图
# - 使用addCircleMarkers()标注犯罪点位
# - 使用addHeatmap()（leaflet.extras包）创建热力层
# - 按Borough分层，可切换显示
# - 添加Popup显示犯罪详情（类型、日期、地点）

# 辅助图：sf + ggplot2 choropleth地图
# - 使用NYC shapefile（可从NYC Open Data获取）
# - 按Precinct着色，显示犯罪密度
# - 使用scale_fill_viridis()配色
# - 叠加主要街道和地标

# 代码框架：
crime_sf <- st_as_sf(crime_data, 
                     coords = c("Longitude", "Latitude"),
                     crs = 4326)

leaflet(crime_sf) %>%
  addTiles() %>%
  addHeatmap(lng = ~Longitude, lat = ~Latitude,
             intensity = ~1, blur = 20, max = 0.05) %>%
  addCircleMarkers(radius = 2, 
                   popup = ~paste("Type:", OFNS_DESC, "<br>",
                                  "Date:", CMPLNT_FR_DT))
```

**支持的假设检验**：
```r
# H0: 犯罪在NYC各区均匀分布
# H1: 某些区域犯罪率显著高于其他区域

# 卡方检验
chisq.test(table(crime_data$BORO_NM))

# 空间自相关检验（Moran's I）
library(spdep)
# 检验犯罪是否存在空间聚集
```

**外部证据整合**：
- NYC人口普查数据（tidycensus包）
- 计算标准化犯罪率（每10万人）

**为什么完美**：
- Leaflet是R中最强大的交互式地图库
- 直接回答"安全区域"问题
- 整合空间统计分析

---

### **Figure 2: 多维度统计分析 - 犯罪类型与受害者特征**
**库：ggplot2 + patchwork + ggridges**

**分析目的**：回答"谁最容易受害？什么犯罪最常见？"

**具体实现**：
```r
library(ggplot2)
library(patchwork)
library(ggridges)
library(scales)

# 创建4个子图，使用patchwork组合：

# 子图1：Heatmap - 犯罪类型 vs 时段
p1 <- crime_data %>%
  mutate(hour = hour(CMPLNT_FR_TM)) %>%
  count(OFNS_DESC_top10, hour) %>%
  ggplot(aes(x = hour, y = OFNS_DESC_top10, fill = n)) +
  geom_tile() +
  scale_fill_viridis_c(option = "plasma") +
  labs(title = "Crime Type by Hour of Day",
       x = "Hour", y = "Crime Type") +
  theme_minimal()

# 子图2：Ridgeline Plot - 犯罪时间分布
p2 <- crime_data %>%
  ggplot(aes(x = hour(CMPLNT_FR_TM), y = BORO_NM, fill = BORO_NM)) +
  geom_density_ridges(alpha = 0.7) +
  scale_fill_brewer(palette = "Set2") +
  labs(title = "Crime Time Distribution by Borough",
       x = "Hour of Day", y = "Borough") +
  theme_ridges()

# 子图3：Stacked Bar - 受害者人口统计
p3 <- crime_data %>%
  filter(!is.na(VIC_AGE_GROUP), VIC_AGE_GROUP != "UNKNOWN") %>%
  count(VIC_AGE_GROUP, VIC_SEX) %>%
  ggplot(aes(x = VIC_AGE_GROUP, y = n, fill = VIC_SEX)) +
  geom_col(position = "fill") +
  scale_y_continuous(labels = percent) +
  scale_fill_manual(values = c("#E69F00", "#56B4E9", "#999999")) +
  labs(title = "Victim Demographics",
       x = "Age Group", y = "Proportion") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# 子图4：Violin Plot with Points - 犯罪严重程度
p4 <- crime_data %>%
  mutate(severity = case_when(
    LAW_CAT_CD == "FELONY" ~ 3,
    LAW_CAT_CD == "MISDEMEANOR" ~ 2,
    LAW_CAT_CD == "VIOLATION" ~ 1
  )) %>%
  ggplot(aes(x = BORO_NM, y = severity, fill = BORO_NM)) +
  geom_violin(alpha = 0.6) +
  geom_boxplot(width = 0.2, alpha = 0.8) +
  scale_fill_brewer(palette = "Dark2") +
  labs(title = "Crime Severity by Borough",
       x = "Borough", y = "Severity Score") +
  theme_minimal()

# 使用patchwork组合
(p1 | p2) / (p3 | p4) +
  plot_annotation(
    title = "Multi-dimensional Crime Analysis",
    theme = theme(plot.title = element_text(size = 16, face = "bold"))
  )
```

**支持的假设检验**：
```r
# H0: 不同年龄组的犯罪受害率无显著差异
# H1: 25-44岁群体受害率显著高于其他年龄组

# ANOVA检验
crime_age <- crime_data %>%
  filter(!is.na(VIC_AGE_GROUP), VIC_AGE_GROUP != "UNKNOWN") %>%
  count(VIC_AGE_GROUP)

anova_result <- aov(n ~ VIC_AGE_GROUP, data = crime_age)
summary(anova_result)

# Tukey HSD事后检验
TukeyHSD(anova_result)

# 卡方检验（受害者特征 vs 犯罪类型）
chisq.test(table(crime_data$VIC_RACE, crime_data$LAW_CAT_CD))
```

**数值证据**：
```r
# Table 1: 描述性统计
library(gtsummary)
crime_data %>%
  select(OFNS_DESC, LAW_CAT_CD, VIC_AGE_GROUP, VIC_SEX, BORO_NM) %>%
  tbl_summary(by = BORO_NM) %>%
  add_p() %>%
  bold_labels()
```

**为什么完美**：
- ggplot2是R可视化的黄金标准
- patchwork让多图组合优雅
- ggridges提供独特的密度分布视角
- 直接支持假设检验

---

### **Figure 3: 交互式时间序列 - 犯罪动态演变**
**库：plotly + forecast + gganimate**

**分析目的**：回答"犯罪趋势如何变化？未来会怎样？"

**具体实现**：
```r
library(plotly)
library(forecast)
library(gganimate)
library(lubridate)
library(tsibble)

# 准备时间序列数据
crime_ts <- crime_data %>%
  mutate(year_month = floor_date(CMPLNT_FR_DT, "month")) %>%
  count(year_month, OFNS_DESC_top5) %>%
  as_tsibble(key = OFNS_DESC_top5, index = year_month)

# 主图：Plotly交互式时间序列
p_interactive <- crime_ts %>%
  plot_ly(x = ~year_month, y = ~n, color = ~OFNS_DESC_top5,
          type = 'scatter', mode = 'lines',
          hovertemplate = paste(
            '<b>%{fullData.name}</b><br>',
            'Date: %{x}<br>',
            'Count: %{y}<br>',
            '<extra></extra>'
          )) %>%
  layout(
    title = "Crime Trends Over Time (2006-2023)",
    xaxis = list(title = "Date",
                 rangeslider = list(visible = TRUE)),
    yaxis = list(title = "Number of Crimes"),
    hovermode = "x unified"
  )

# 辅助图1：季节性分解
crime_total_ts <- crime_data %>%
  mutate(year_month = floor_date(CMPLNT_FR_DT, "month")) %>%
  count(year_month) %>%
  pull(n) %>%
  ts(frequency = 12, start = c(2006, 1))

decomp <- stl(crime_total_ts, s.window = "periodic")
autoplot(decomp) +
  labs(title = "Seasonal Decomposition of Crime Data") +
  theme_minimal()

# 辅助图2：ARIMA预测
fit <- auto.arima(crime_total_ts)
forecast_result <- forecast(fit, h = 12)

autoplot(forecast_result) +
  labs(title = "12-Month Crime Forecast",
       x = "Time", y = "Number of Crimes") +
  theme_minimal()

# 动画图：gganimate展示年度变化
p_animate <- crime_data %>%
  mutate(year = year(CMPLNT_FR_DT)) %>%
  count(year, BORO_NM) %>%
  ggplot(aes(x = BORO_NM, y = n, fill = BORO_NM)) +
  geom_col() +
  scale_fill_brewer(palette = "Set1") +
  labs(title = "Crime Count by Borough: {frame_time}",
       x = "Borough", y = "Number of Crimes") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  transition_time(year) +
  ease_aes('linear')

animate(p_animate, nframes = 100, fps = 10)
```

**支持的假设检验**：
```r
# H0: 犯罪数量无季节性模式
# H1: 夏季（6-8月）犯罪率显著高于冬季

# 季节性检验
crime_seasonal <- crime_data %>%
  mutate(season = case_when(
    month(CMPLNT_FR_DT) %in% c(6, 7, 8) ~ "Summer",
    month(CMPLNT_FR_DT) %in% c(12, 1, 2) ~ "Winter",
    TRUE ~ "Other"
  )) %>%
  filter(season %in% c("Summer", "Winter"))

t.test(n ~ season, 
       data = crime_seasonal %>% 
         count(CMPLNT_FR_DT, season))

# 时间序列平稳性检验
library(tseries)
adf.test(crime_total_ts)  # Augmented Dickey-Fuller检验
```

**外部证据整合**：
```r
# 整合COVID-19数据
covid_timeline <- data.frame(
  date = as.Date(c("2020-03-01", "2020-06-01", "2021-01-01")),
  event = c("NYC Lockdown", "Phase 1 Reopening", "Vaccine Rollout")
)

# 在图中添加垂直线标注
p_interactive %>%
  add_segments(
    x = covid_timeline$date, xend = covid_timeline$date,
    y = 0, yend = max(crime_ts$n),
    line = list(color = "red", dash = "dash"),
    showlegend = FALSE
  ) %>%
  add_annotations(
    x = covid_timeline$date,
    y = max(crime_ts$n),
    text = covid_timeline$event,
    showarrow = TRUE
  )
```

**为什么完美**：
- Plotly提供R中最强的交互性
- forecast包是时间序列分析的标准
- gganimate创造动态视觉效果
- 整合重大社会事件（COVID-19）

---

## 三图协同逻辑：

```
Figure 1 (leaflet) → 空间分析：WHERE
        ↓
Figure 2 (ggplot2) → 人群分析：WHO & WHAT
        ↓
Figure 3 (plotly) → 时间分析：WHEN & WHY
```

---

## R技术栈总结：

| 图表 | 主库 | 辅助库 | 统计方法 | 外部数据 |
|------|------|--------|----------|----------|
| Figure 1 | leaflet | sf, viridis | 卡方检验, Moran's I | tidycensus |
| Figure 2 | ggplot2 | patchwork, ggridges | ANOVA, Tukey HSD | 无 |
| Figure 3 | plotly | forecast, gganimate | ARIMA, ADF检验 | COVID数据 |

**使用的R包（满足多样性要求）**：
1. **leaflet** - 交互式地图
2. **sf** - 空间数据处理
3. **ggplot2** - 统计图形语法
4. **patchwork** - 多图组合
5. **ggridges** - 密度脊线图
6. **plotly** - 交互式图表
7. **forecast** - 时间序列预测
8. **gganimate** - 动画可视化
9. **viridis** - 色盲友好配色
10. **gtsummary** - 统计表格

---

## 评分标准对应：

✅ **Evidence (3分)**：每个图都有统计表格和数值解释  
✅ **Hypothesis testing (2分)**：卡方、ANOVA、时间序列检验  
✅ **External Evidence (2分)**：整合人口普查、COVID数据  
✅ **ggplot (2分)**：三个图都是R可视化最佳实践  
✅ **Limitations (2分)**：讨论数据缺失、报案延迟、空间精度  

---

## 数据准备代码：

```r
library(tidyverse)
library(lubridate)

# 读取NYPD数据（假设已下载CSV）
crime_data <- read_csv("NYPD_Complaint_Data_Historic.csv") %>%
  # 清洗日期
  mutate(
    CMPLNT_FR_DT = mdy(CMPLNT_FR_DT),
    CMPLNT_FR_TM = hms(CMPLNT_FR_TM)
  ) %>%
  # 过滤无效坐标
  filter(
    !is.na(Latitude), !is.na(Longitude),
    Latitude != 0, Longitude != 0,
    between(Latitude, 40.4, 41.0),
    between(Longitude, -74.3, -73.7)
  ) %>%
  # 提取前10大犯罪类型
  mutate(
    OFNS_DESC_top10 = fct_lump_n(OFNS_DESC, 10)
  )

# 保存清洗后的数据
saveRDS(crime_data, "crime_data_clean.rds")
```

---

你想让我开始编写完整的R Markdown报告模板吗？还是需要我先帮你探索数据，确认哪些字段可用？