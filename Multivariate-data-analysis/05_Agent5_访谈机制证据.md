# Agent 5｜访谈机制证据整理

## 任务
从已完成的访谈编码/NVivo结果中提取与客观数据交叉验证直接相关的机制证据。

## 输入
- 稳定版访谈代码本
- NVivo编码结果
- 个案摘要
- Agent 1：事件/条件映射表

## 核心机制

### 1. 持续监测
代码：`CONTINUOUS_MONITORING`

定义：参与者明确描述持续关注外部环境、反复回看场景、持续确认系统/环境状态。

### 2. 注意切换
代码：`ATTENTION_SWITCHING`

定义：参与者明确描述在手机/次任务、HMI、外部场景之间来回切换注意。

### 3. HMI依赖
代码：`HMI_RELIANCE`

定义：参与者明确表达需要借助 HMI 才能确认、理解、安心或决定如何应对。

仅表达“看过HMI”不计为依赖。

### 4. 认知负荷/注意冲突
代码：`COGNITIVE_CONFLICT`

定义：参与者明确描述次任务、HMI信息和外部环境之间存在注意资源竞争、来不及处理、被打断或感觉负担增加。

## 每条机制证据记录格式
| participant_id | condition | run_id | event_id | mechanism_code | evidence_status | evidence_summary | source_ref |
|---|---|---|---|---|---|---|---|

`evidence_status`：
- `support`
- `contradiction`
- `unclear`

没有相关内容时不强行生成记录。

## 不做
- 不用出现次数直接代表机制强度。
- 不把含糊表述强行归类。
- 不根据客观数据倒推访谈编码。
- 不删除否定案例。

## 输出
`Interview_Mechanism.csv`
