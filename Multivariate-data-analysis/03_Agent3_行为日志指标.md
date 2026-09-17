# Agent 3｜行为日志指标提取

## 任务
从系统/交互日志中提取被试主动调用 HMI/解释信息的行为，用于区分“信息可用、主动调用、实际查看”。

## 输入
- Agent 1：`Master_Event_Window.csv`
- 系统行为日志
- HMI/解释卡操作日志

## 核心指标

### 1. 是否打开解释卡
字段：`reason_card_opened`

定义：事件窗口内出现 ≥1 次有效打开操作记为 1，否则 0。

### 2. 首次打开延迟
字段：`reason_card_first_latency_s`

定义：`首次打开时间 - event_onset`

窗口内未打开时记缺失。

### 3. 打开次数
字段：`reason_card_open_count`

定义：事件窗口内独立打开事件数量。

### 4. 累计打开时长
字段：`reason_card_total_open_s`

定义：事件窗口内所有“打开—关闭”区间与窗口交集时长之和。

## 必须保留的原始事件
- `event_onset`
- `reason_card_open`
- `reason_card_close`
- 关键系统动作开始/结束时间

## 不在本 Agent 内计算
由 Agent 6 完成：
- 打开解释卡后是否真的看 HMI
- HMI 与解释卡的时间交集
- HMI依赖
- 注意切换机制

## 输出
`Behavior_Metrics.csv`

最少字段：
| participant_id | condition | run_id | event_id | reason_card_opened | reason_card_first_latency_s | reason_card_open_count | reason_card_total_open_s |
|---|---|---|---|---:|---:|---:|---:|

## 质量检查
- 打开与关闭必须成对。
- 跨事件窗口区间按窗口截断。
- 系统自动刷新不可误计为主动打开。
- 无法确认是否为主动操作的事件必须标记。
