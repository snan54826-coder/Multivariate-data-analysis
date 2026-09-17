# Agent 2｜眼动 / AOI 指标提取

## 任务
从 BORIS `aggregated.tsv` 中提取事件级视觉朝向指标，用于描述 HMI 信息获取、环境监测和注意切换。

## 输入
- Agent 1：`Master_Event_Window.csv`
- BORIS：`*_aggregated.tsv`

AOI固定为：
- `GAZE_PHONE`
- `GAZE_SCENE`
- `GAZE_HMI`
- `GAZE_OTHER`
- `GAZE_UNCODABLE`

## 核心指标

### 1. HMI是否被查看
字段：`hmi_seen`

定义：事件窗口内出现 ≥1 段 `GAZE_HMI` 记为 1，否则 0。

### 2. 首次HMI查看延迟
字段：`hmi_first_latency_s`

定义：`首次 GAZE_HMI onset - event_onset`

窗口内未出现 HMI 时记缺失。

### 3. HMI glance次数
字段：`hmi_glance_count`

定义：事件窗口内独立 `GAZE_HMI` 段数。

### 4. HMI累计时长
字段：`hmi_total_duration_s`

定义：事件窗口内所有 `GAZE_HMI` 与窗口交集时长之和。

### 5. SCENE累计占比
字段：`scene_time_ratio`

定义：`GAZE_SCENE累计时长 / 有效可编码窗口时长`

有效可编码窗口时长扣除 `GAZE_UNCODABLE`。

### 6. AOI切换次数
字段：`aoi_transition_count`

定义：按时间排序后，相邻有效 AOI 发生变化的次数。`UNCODABLE` 前后的转移不强行跨越合并。

## 辅助保留字段
- `phone_total_duration_s`
- `uncodable_duration_s`
- `valid_window_duration_s`
- `aoi_sequence`

## 不计算
- fixation
- saccade
- 眼球精确落点
- 自定义“认知负荷指数”
- 仅凭 HMI 时长直接判定“HMI依赖”

## 输出
`Eye_Metrics.csv`

最少字段：
| participant_id | condition | run_id | event_id | hmi_seen | hmi_first_latency_s | hmi_glance_count | hmi_total_duration_s | scene_time_ratio | aoi_transition_count | uncodable_duration_s |
|---|---|---|---|---:|---:|---:|---:|---:|---:|---:|

## 质量检查
- 每个 AOI 区间满足 `stop > start`。
- 检查重叠和明显空档。
- 事件窗口边界处按时间交集截断。
- `UNCODABLE` 必须保留。
- 所有指标可回溯到具体 AOI 区间。
