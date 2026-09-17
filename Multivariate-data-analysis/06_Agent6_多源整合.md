# Agent 6｜多源整合与证据链

## 任务
把眼动、行为日志、次任务和访谈整合到同一事件层级，建立客观过程证据链，并识别一致、部分一致、冲突和边界条件。

## 输入
- `Master_Event_Window.csv`
- `Eye_Metrics.csv`
- `Behavior_Metrics.csv`
- `SecondaryTask_Metrics.csv`
- `Interview_Mechanism.csv`
- 必要时读取原始 AOI 区间和行为日志事件

## 第一步：建立事件级总表
按以下键合并：

`participant_id + condition + run_id + event_id`

输出：`Multisource_Master.csv`

## 第二步：计算三个关键跨源指标

### 1. 解释卡实际观看
字段：
- `card_hmi_overlap_s`
- `card_hmi_viewed`

定义：`GAZE_HMI` 区间与 `reason_card_open` 区间求交。

`card_hmi_viewed = 1`：交集时长 > 0。

### 2. 事件后HMI响应
字段：`post_event_hmi_response`

结合：
- `hmi_seen`
- `hmi_first_latency_s`
- `reason_card_opened`

只描述事件后的 HMI 信息获取路径。

### 3. 注意切换—次任务联动
字段：`attention_task_pattern`

依据：
- `aoi_transition_count`
- `secondary_accuracy`
- `secondary_omission_rate`
- `secondary_rt_s`

只描述共同出现的模式，不做因果判断。

## 第三步：验证四类访谈机制

### A. 持续监测
主要证据：
- `scene_time_ratio`
- AOI序列中反复返回 `SCENE`

### B. 注意切换
主要证据：
- `aoi_transition_count`
- AOI时间序列
- 次任务表现变化

### C. HMI依赖
需多源共同支持：
- 访谈明确 `HMI_RELIANCE`
- 事件后稳定出现 HMI 查看
- 较短首次HMI延迟、重复HMI glance或主动开卡中的至少一种
- 跨多个事件具有重复性

单次长时间看 HMI 不足以判定依赖。

### D. 认知负荷/注意冲突
主要证据：
- 访谈 `COGNITIVE_CONFLICT`
- AOI切换增加
- 次任务正确率下降、漏答增加或RT变长中的至少一种

## 第四步：建立证据矩阵
输出：`Evidence_Matrix.csv`

每个机制 × 每名被试/事件分为：
- `consistent_support`
- `partial_support`
- `conflict`
- `insufficient`

## 第五步：制作典型事件时间轴
每个典型案例至少包含四层：
1. 系统事件
2. 解释卡/交互日志
3. AOI视觉朝向
4. 次任务题目与作答

统一以 `event_onset = 0 s`。

## 第六步：选择典型案例
至少包含：
- 多源一致支持案例
- 部分支持案例
- 明确冲突案例
- 边界条件案例

## 输出
1. `Multisource_Master.csv`
2. `Evidence_Matrix.csv`
3. `Timeline_Figures/`
4. `Integration_Findings.md`

## 严格限制
- 不将相关关系写成因果关系。
- 不用单一数据源直接确认心理机制。
- 不忽略冲突或否定案例。
- 所有跨源指标保留计算依据。
