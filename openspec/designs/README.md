# Long-Lived Design Docs

这里存放长期有效的系统设计文档，不替代每次变更下的 `design.md`。

推荐按领域或系统级主题拆分，例如：

- `system-overview.md`
- `auth-domain.md`
- `order-domain.md`
- `integration-events.md`

使用原则：

1. 这里记录“系统现在是什么样”。
2. `changes/*/design.md` 记录“某次改动为什么这么改”。
3. 当某次变更中的设计结论已经稳定为系统事实，再提炼同步到这里。
