# 工作记忆与历史记忆管理

## Purpose

工作记忆与历史记忆管理能力用于记录 agent 在运行过程中的上下文轨迹，并以结构化方式保存会话、对话和动作过程，为后续追踪、学习、推荐和审计提供数据基础。

## Requirements

### Requirement: 系统必须按会话聚合用户多轮交互

系统 MUST 将同一连续交互过程中的多次问答组织为一个会话，并维护该会话的基本元数据、状态和时间范围。

#### Scenario: 新用户开始一次新的连续交互

- **GIVEN** 用户尚未处于一个有效会话中
- **WHEN** 用户发起新的提问
- **THEN** 系统创建一个新的 `conversation`
- **AND** 后续相关问答默认归属于该会话

#### Scenario: 已有会话中继续追加问答

- **GIVEN** 用户当前处于一个有效会话中
- **WHEN** 用户继续发起新的提问
- **THEN** 系统将新的问答追加到现有 `conversation`
- **AND** 保持会话级别的时间顺序和关联关系

### Requirement: 系统必须将单次提问及最终回答记录为对话

系统 MUST 将用户一次提问与模型最终返回结果记录为一个 `chat`，并将其挂接到所属 `conversation` 之下。

#### Scenario: 一次提问生成一个完整对话记录

- **GIVEN** 用户发起一次提问
- **WHEN** 模型完成最终回答
- **THEN** 系统生成一个 `chat`
- **AND** 该 `chat` 包含用户输入、模型最终输出和必要的上下文引用

#### Scenario: 对话与会话保持归属关系

- **GIVEN** 某次提问发生在一个已存在的会话中
- **WHEN** 系统完成该次问答记录
- **THEN** 新生成的 `chat` 归属于对应 `conversation`
- **AND** 系统能够按会话顺序查询该对话

### Requirement: 系统必须记录单次对话中的中间动作轨迹

系统 MUST 记录从用户一次提问到模型最终回答之间发生的关键中间动作，并将每个动作保存为 `action`。

#### Scenario: 模型在回答过程中调用工具

- **GIVEN** 模型在生成回答过程中需要调用工具
- **WHEN** 工具调用被执行
- **THEN** 系统记录一条 `action`
- **AND** 该 `action` 包含动作类型、输入、输出和执行顺序

#### Scenario: 模型在回答过程中查询知识或接口

- **GIVEN** 模型在生成回答过程中查询知识库或外部接口
- **WHEN** 查询动作被执行
- **THEN** 系统记录对应 `action`
- **AND** 该 `action` 与所属 `chat` 建立可追溯关系

### Requirement: 系统必须维护 conversation、chat、action 的层级关联

系统 MUST 维护 `conversation`、`chat`、`action` 之间稳定且可查询的层级关系，以支持按会话、按对话和按动作追踪 agent 行为。

#### Scenario: 按会话追踪完整执行链路

- **GIVEN** 一个会话下存在多条对话和多条动作记录
- **WHEN** 调用方按 `conversation` 查询执行历史
- **THEN** 系统返回该会话下的 `chat` 集合
- **AND** 每条 `chat` 下可继续追踪对应的 `action` 集合

#### Scenario: 按对话查看动作明细

- **GIVEN** 某个 `chat` 已记录多个中间动作
- **WHEN** 调用方查看该 `chat` 的执行过程
- **THEN** 系统返回完整的 `action` 序列
- **AND** 动作顺序与实际执行顺序一致
