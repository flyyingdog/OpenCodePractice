## ADDED Requirements

### Requirement: 变更必须能够挂靠到已有能力并保留变更上下文

系统在为已有 Java 代码仓引入 OpenSpec 时，MUST 允许新的变更先挂靠到最可能相关的已有 capability，并通过 change 下的 proposal、design、tasks 和 delta specs 记录本次变更上下文。

#### Scenario: 旧功能归属尚不完全清晰时先完成临时挂靠
- **WHEN** 团队无法立即确定一个需求准确对应哪个既有 capability
- **THEN** 团队仍然可以选择最可能相关的 capability 先创建 change
- **AND** 在 proposal 或 design 中明确记录后续对长期 spec 进行整理的计划

### Requirement: 团队必须拥有可直接复用的 change 编写参考

系统 MUST 提供一条可直接复用的示例 change，用于指导团队编写 proposal、design、tasks 和 specs。

#### Scenario: 首次使用 OpenSpec 的成员需要参考完整样例
- **WHEN** 新成员首次在仓库中创建 OpenSpec change
- **THEN** 仓库中存在一条结构完整的示例 change 可供参考
- **AND** 该示例 change 展示 proposal、design、tasks 和 delta spec 的基本组织方式
