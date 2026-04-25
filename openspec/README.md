# OpenSpec Working Notes

这个目录是一套适用于现有 Java 代码仓的 OpenSpec 骨架，目标是让团队先把流程跑起来，再逐步补齐历史能力说明。

## 目录约定

- `config.yaml`：全局规则与写作约束
- `specs/`：当前系统行为的长期真相源，按业务能力组织
- `designs/`：长期稳定的系统设计文档
- `changes/`：每次变更的提案、设计、任务与变更中的 spec
- `playbooks/`：团队操作说明，例如如何为旧系统补 spec

## 对已有 Java 仓的建议

1. 不要先补全全部历史 spec，再开始新需求。
2. 每次只为当前改动涉及的能力补最小可用 spec。
3. `changes/<change-id>/design.md` 用于记录本次技术决策。
4. 稳定下来的系统性结论，再同步到 `designs/` 下的长期设计文档。

## 当前项目建议能力划分

结合当前记忆系统，建议优先维护以下业务能力：

- `working-memory-management`
- `long-term-memory-management`
- `question-recommendation`

避免直接按 `controller/service/repository` 或单纯按技术实现拆分 spec。
