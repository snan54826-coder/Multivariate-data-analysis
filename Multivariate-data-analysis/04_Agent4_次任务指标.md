# Agent 4｜次任务指标提取

## 任务
量化实验过程中次任务表现，用于观察关键事件、HMI查看和注意切换是否伴随任务表现变化。

## 输入
- Agent 1：`Master_Event_Window.csv`
- 次任务题目日志
- 答题记录
- 正确/错误数据
- 反应时间戳（若有）

## 核心指标

### 1. 次任务正确率
字段：`secondary_accuracy`

定义：`正确回答数 / 有效作答数`

若事件窗口仅有 1 题，直接记录正确=1、错误=0。

### 2. 反应时间
字段：`secondary_rt_s`

定义：`提交答案时间 - 题目呈现时间`

一个窗口多题时优先使用中位数。仅在时间戳可靠时计算。

## 辅助字段
- `secondary_n_items`
- `secondary_n_answered`
- `secondary_n_correct`

## 不计算
- 自定义综合认知负荷分数
- 未经验证的加权总分
- 用正确率单独代表认知负荷强弱

## 输出
`SecondaryTask_Metrics.csv`

最少字段：
| participant_id | condition | run_id | event_id | secondary_n_items | secondary_accuracy | secondary_omission_rate | secondary_rt_s |
|---|---|---|---|---:|---:|---:|---:|

## 质量检查
- 区分错误回答与漏答。
- RT只使用有效提交。
- 异常RT先标记，不直接删除。
- 无题目落入事件窗口时相关指标记缺失。
