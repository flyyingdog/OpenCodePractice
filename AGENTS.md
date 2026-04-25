# AGENTS.md

## OpenSpec 工作约定

本仓库使用 OpenSpec 驱动需求、设计、任务拆解与实施过程。

在处理需求、变更设计、任务分解、归档整理时，请优先遵循 `openspec/` 目录下的规则和文档。

## 优先读取

以下文档在参与 OpenSpec 工作流时应优先读取：

- `openspec/config.yaml`
- `openspec/README.md`

## 按需读取

根据任务类型选择性读取以下文档：

- `openspec/designs/system-overview.md`
  - 用于理解系统长期架构、模块边界、运行时关系和横切关注点
- `openspec/designs/*.md`
  - 用于查阅已经沉淀下来的领域设计和系统设计
- `openspec/specs/*/spec.md`
  - 用于理解已有业务能力的当前行为、约束和场景
- `openspec/playbooks/backfill-existing-java-specs.md`
  - 用于在旧 Java 代码区域中补齐或挂靠 spec

## 处理原则

- spec 按业务能力组织，不按 controller、service、repository 等技术层组织
- 对已有 Java 代码仓，不要求先补齐全部历史 spec，再开始新需求
- 只对当前变更涉及的能力补充最小可用 spec，并在后续逐步完善
- 如果暂时无法判断需求归属到哪个已有 capability，应选择最可能的能力先挂靠，并在 proposal、design 或 tasks 中标注后续整理工作
- 单次变更下的 `openspec/changes/<change-id>/design.md` 用于记录该次变更的技术决策
- 已经稳定、可长期复用的设计结论，应同步沉淀到 `openspec/designs/` 下的长期设计文档

## Java 项目设计要求

在编写或补充 `design.md` 时，应尽量覆盖以下内容：

- 背景与目标
- 影响范围
- 领域模型
- 数据模型
- 接口定义
- 应用层改动
- 持久化改动
- 兼容性影响
- 发布、迁移与回滚
- 测试策略

当变更涉及数据库、接口或外部集成时，应明确写出：

- 数据表、字段、约束、索引或迁移说明
- 接口请求、响应、校验规则、错误码和兼容性影响
- 对调用方、消费者、历史数据和运行配置的影响

## 执行建议

- 在开始新需求前，先判断它是修改已有能力，还是引入新能力
- 在开始设计前，先查看相关长期设计文档和已有 spec
- 在归档变更时，保留 change 下的 proposal、design、tasks 和 specs 历史
- 不要把所有 change 的 design 简单拼接成一个总文档，应将稳定结论提炼后再更新到长期设计文档
