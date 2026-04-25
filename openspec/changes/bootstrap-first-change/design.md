## Context

当前仓库已经具备 OpenSpec 基础目录、Java 项目规则和长期设计文档，但还没有一条完整的变更样例来展示 proposal、design、tasks 和 delta specs 之间的衔接方式。

为了降低后续使用成本，需要建立一个最小可用骨架，让团队在接入真实需求时可以直接替换内容，而不是从空白文档开始编写。

### Background

- 当前仅有长期 `specs/` 和 `designs/` 骨架
- 首次接入 OpenSpec 的使用者，往往最缺的是“一个完整 change 到底应该长什么样”
- 该变更仅用于演示文档结构，不引入代码实现

### Scope

- 影响目录：`openspec/changes/bootstrap-first-change/`
- 影响 capability：`working-memory-management`
- 不涉及 Java 代码包、类、数据库表或 API 实现

## Goals / Non-Goals

**Goals:**

- 提供一条完整的 OpenSpec 变更骨架
- 演示如何在已有 capability 上编写 delta spec
- 演示 Java 项目下 proposal、design、tasks 的推荐结构
- 让后续真实需求可以基于本骨架快速复制和改写

**Non-Goals:**

- 不实现任何业务功能
- 不修改运行时代码
- 不引入新的 capability
- 不进行数据库或接口实际变更

## Decisions

### 决策 1：使用单一示例 change 作为团队参考模板

- 选择：创建 `bootstrap-first-change` 作为长期可参考的示例变更
- 原因：比仅提供零散模板说明更直观，团队可以直接对照目录和文件结构使用
- 备选方案：
  - 只保留 `README` 说明：信息不够具体，首次使用仍然容易无从下手
  - 直接等待真实需求再补：会把学习成本转移到第一条正式需求上

### 决策 2：示例变更挂靠到已有 `working-memory-management` capability

- 选择：通过修改已有 `working-memory-management` capability 来演示 delta spec 的写法
- 原因：更贴近旧仓接入 OpenSpec 的真实场景，多数需求并不是新增 capability，而是修改已有能力
- 备选方案：
  - 新建一个演示 capability：无法体现“如何挂靠旧能力”这一关键问题

### 决策 3：设计文档保留 Java 项目完整章节，即使本次没有真实实现

- 选择：在骨架中保留领域模型、数据模型、接口定义、应用层改动、持久化改动等章节
- 原因：便于后续真实需求直接替换内容，同时强化团队写作习惯
- 备选方案：
  - 仅保留极简 design 结构：首次使用时仍需反复思考该补哪些章节

## Domain Model

本示例不引入新的领域对象，仅用于说明当真实需求涉及以下内容时应如何编写：

- 聚合：如用户账户、会话、认证凭据
- 实体：如用户、登录会话、验证码记录
- 值对象：如手机号、邮箱、认证渠道
- 状态流转：如未登录、已登录、已过期、已注销
- 业务规则：如凭据校验、登录态有效期、失败次数限制

## Data Model

本示例不引入实际数据模型变更。

当真实需求涉及数据库时，应至少补充：

| 项目 | 说明 |
| --- | --- |
| 表 | 受影响的表名 |
| 字段 | 新增、修改、删除字段 |
| 约束 | 唯一约束、非空约束、外键等 |
| 索引 | 新增或调整索引 |
| 迁移 | DDL、回填、灰度与回滚方式 |

## API Contract

本示例不引入实际接口变更。

当真实需求涉及接口时，应至少补充：

| 项目 | 说明 |
| --- | --- |
| Endpoint / Interface | 接口路径或服务方法 |
| Method | HTTP 方法或调用类型 |
| Request | 请求参数、校验规则 |
| Response | 返回结构、关键字段 |
| Error Codes | 业务错误码与语义 |
| Compatibility | 是否兼容旧调用方 |

## Application Changes

本示例不修改实际应用层代码。

真实需求中建议说明：

- 影响的 controller / resource
- 影响的 service / application use case
- 是否新增 command / query
- 是否影响定时任务、事件处理器或消息消费者

## Persistence Changes

本示例不修改实际持久化层代码。

真实需求中建议说明：

- 影响的 entity / DO / PO
- 影响的 repository / mapper / DAO
- 事务边界
- 一致性与并发风险

## Compatibility Impact

本变更仅新增示例文档，不影响已有调用方、存量数据或部署流程，因此不存在实际兼容性风险。

## Risks / Trade-offs

- [风险] 示例内容过于抽象，后续团队可能仍不确定如何落到真实业务
  → 缓解：后续选择一条真实需求，再基于本骨架补一个业务化示例

- [风险] 示例长期不更新，可能与团队实际写法逐渐偏离
  → 缓解：当团队沉淀出更成熟写法后，定期同步更新本骨架

## Rollout and Rollback

### Rollout

1. 保留当前示例变更作为团队参考
2. 后续创建真实 change 时，以该骨架为参考直接替换内容
3. 当团队形成稳定习惯后，可根据需要保留、归档或删除该示例

### Rollback

1. 若团队不再需要该示例，可直接删除该 change
2. 本变更不影响代码与运行环境，无额外回滚成本

## Testing Strategy

- 校验 `proposal.md`、`design.md`、`tasks.md`、`specs/` 目录结构完整
- 使用 `openspec validate bootstrap-first-change` 验证 OpenSpec 结构是否通过
- 人工检查内容是否符合 Java 项目的设计章节要求

## Open Questions

- 后续是否需要再补一条基于真实业务需求的示例 change
- 是否要将该示例 change 长期保留在仓库中作为团队 onboarding 材料
