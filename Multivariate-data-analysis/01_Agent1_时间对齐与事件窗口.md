# Agent 1｜时间对齐与事件窗口

## 任务
建立全项目唯一的时间基准和事件分析单位，为其他 Agent 提供统一入口。

## 输入
- 实验行为日志
- BORIS `aggregated.tsv`
- 次任务日志
- 被试/条件/轮次对应表
- 实验事件定义

## 必须完成

### 1. 统一主键
固定字段：
- `participant_id`
- `condition`
- `run_id`
- `event_id`

### 2. 固定事件触发时刻
每个 `event_id` 明确：
- `event_onset_s`
- `event_onset_source`
- `window_start_s`
- `window_end_s`

`event_onset` 优先采用实验系统/行为日志中的正式触发时刻。

### 3. 建立统一相对时间
`aligned_time_s = raw_time_s - event_onset_s`

事件触发时刻固定为 `0 s`。

### 4. 输出事件窗口表
输出：`Master_Event_Window.csv`

最少字段：
| participant_id | condition | run_id | event_id | event_onset_s | window_start_s | window_end_s | window_duration_s | alignment_note |
|---|---|---|---|---:|---:|---:|---:|---|

## 质量检查
- 各数据源同一事件映射到同一 `event_id`。
- 时间单位统一为秒。
- 原始时间必须保留。
- 无法可靠对齐的数据单独标记。
- 检查窗口重叠、缺失、越界。
- 不自行推断缺失的事件触发时间。

## 交付
1. `Master_Event_Window.csv`
2. `ID_Mapping.csv`
3. `Alignment_QC.md`
