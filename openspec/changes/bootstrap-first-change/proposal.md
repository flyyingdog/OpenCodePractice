## Why

当前仓库已经完成 OpenSpec 初始化，但还缺少一条可直接参考的标准变更样例，导致团队在第一次使用 proposal、design、tasks 和 delta specs 时缺少统一起点。

本变更用于建立一个最小可用的示例骨架，帮助后续真实需求可以直接复制、修改并落到具体 capability 上。

## What Changes

- 增加一条用于演示 OpenSpec 工作流的首个变更骨架
- 提供 proposal、design、tasks 和 specs 的基础写法示例
- 约定该示例变更以“修改已有能力”方式演示，挂靠到 `user-auth`
- 为后续真实需求提供可直接替换内容的模板化结构

## Capabilities

### New Capabilities

- 无

### Modified Capabilities

- `working-memory-management`: 演示如何为已有能力补充或调整 requirement delta，并将变更挂靠到现有 capability

## Impact

- 影响 OpenSpec 文档目录下的 change 骨架内容
- 不影响任何运行时代码、接口、数据库或外部依赖
- 为后续 Java 项目真实需求提供统一写作起点
