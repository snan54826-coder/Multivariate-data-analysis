# 多源数据对齐分析｜总控说明

## 目标
把 **眼动/AOI、行为日志、次任务、访谈** 对齐到同一事件时间轴，形成可追溯的客观证据链，并用于验证或修正访谈中的加工机制判断。

## 最终分析链路
**事件触发 → 注意分配/切换 → HMI使用与环境监测 → 次任务表现变化 → 访谈机制解释**

## 统一分析单位
固定为：`participant_id × condition × run_id × event_id`

## 统一时间原则
1. 保留每个数据源的原始时间戳。
2. 新建 `aligned_time_s`，统一换算为相对事件时间。
3. 每个事件的 `event_onset` 以实验行为日志中的正式事件触发时刻为准。
4. 事件窗口的起止规则必须在批量分析前固定。
5. 各 Agent 不得自行修改事件窗口、被试编号或条件名称。

## 核心文件
- `Master_Event_Window.csv`
- `Eye_Metrics.csv`
- `Behavior_Metrics.csv`
- `SecondaryTask_Metrics.csv`
- `Interview_Mechanism.csv`
- `Multisource_Master.csv`
- `Evidence_Matrix.csv`
- `Timeline_Figures/`

## 执行顺序
1. Agent 1先固定 ID、时间口径、事件窗口。
2. Agent 2–5并行提取各自数据。
3. Agent 6统一合并并完成证据链分析。
4. 总控 Agent 做最终质量审查和统计准备。

## 严格规则
- 不自行新增指标。
- 不把单一指标直接解释成心理机制。
- `HMI高频查看`只能表述为“HMI使用强度高”；“HMI依赖”需结合多源证据。
- 数据源出现冲突时必须保留冲突。
- 所有结论必须能追溯到原始数据或编码记录。