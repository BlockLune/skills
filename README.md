# skills

A collection of skills for AI agents.

## Installation

```shell
npx skills add BlockLune/skills
```

## Agent 输出质量体系

约束 Agent 文字产出（对话回复、文档类产出、代码注释）的规则按触发时机分为常驻规则与按需 skill（领域术语见 [GLOSSARY.md](GLOSSARY.md)）：

| 载体 | 触发方式 | 适用范围 |
| --- | --- | --- |
| `AGENTS.md` | 每轮常驻 | 清理过程旁白与文档自指、开头答题（BLUF）、断言附依据与未完成项单列、简明语言与限定词保留、日常代码注释、按需 skill 分流 |
| [plain-language](plain-language/SKILL.md) | 半自动（常驻规则点名、按 `description` 触发或手动调用） | 正式文档写作（报告、设计方案、README、PR 描述）、中英文改写润色、清理套话、Markdown 版式与工具检查 |
| [communication-helper](communication-helper/SKILL.md) | 手动（`disable-model-invocation: true`） | 面向领导、客户、同事的邮件、即时消息与工作汇报语气适配 |
| [git-commit](git-commit/SKILL.md) | 手动（`disable-model-invocation: true`） | Commit 描述结构（先写问题背景与影响，再写修改原因）与提交纪律 |
| [no-comments](no-comments/SKILL.md) | 手动（`disable-model-invocation: true`） | 清理冗余与历史注释，将内部约束编码为类型、断言、测试或 lint |

### `AGENTS.md` 常驻规则示例

```markdown
# 输出质量

- 直接给出内容，写完即停。不写寒暄、动作预告、修改复述、结尾客套，以及指向文本自身的话（“本文将/下表/综上所述/值得注意的是”）。
- 第一句直接给结论或结果（前提不成立时先指出）；回答每个子问题，同一事实只说一次。
- 结果断言附上文件路径或命令输出，推断标明推断；任务汇报单列未完成、未验证和待决事项。
- 按 80% 的 `ASD-STE100` + `ISO 24495-1:2023 Plain language` 写作；保留全部事实、数字、前置条件和“可能/通常/至少/尽快”等限定词，不改变断言强度。
- 代码注释只写代码看不出来的意图、外部约束和陷阱，不复述代码动作，不写修改历史。
- 写正式文档（报告、设计方案、README、PR 描述）或改写润色时调用 `plain-language`。
```

## References

- [mattpocock/skills: Agent Skills for real engineers. Straight from my .claude directory.](https://github.com/mattpocock/skills)
- [Waza/rules/english.md at 526f5600d9256068e9aad74cd8d2a887be7cb48f · tw93/Waza](https://github.com/tw93/Waza/blob/526f5600d9256068e9aad74cd8d2a887be7cb48f/rules/english.md)
- [Waza/rules/chinese.md at cdc91822e2ea5fefc1b96cda4dfc1379a7a1f123 · tw93/Waza](https://github.com/tw93/Waza/blob/cdc91822e2ea5fefc1b96cda4dfc1379a7a1f123/rules/chinese.md)
- [Andrej Karpathy on 80% ASD-STE100 and the Understanding Ladder](https://x.com/karpathy/status/2105819303471976479)
- [ChangWenC/understanding-ladder: plain-chinese & understanding-ladder skills](https://github.com/ChangWenC/understanding-ladder)
- [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/about_STE.html) & [ISO 24495-1:2023 Plain language](https://www.iso.org/standard/78907.html)
- [blader/humanizer](https://github.com/blader/humanizer), [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop), & [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [Diátaxis Technical Documentation Framework](https://diataxis.fr/)
- [Quantifying Overclaiming Propensity in Frontier LLM Agents (arXiv:2609.20812)](https://arxiv.org/abs/2609.20812) & [Plans They Abandon, Reports They Author (arXiv:2609.12205)](https://arxiv.org/abs/2609.12205)
- [I hated making this video... - Theo - YouTube](https://www.youtube.com/watch?v=FDxW2bfBOWE)
- [The One Weird Git Trick That Makes Coding Agents More Effect-ive | Effect Documentation](https://effect.website/blog/the-one-weird-git-trick-that-makes-coding-agents-more-effect-ive/)
- <https://x.com/jakevin7/status/2112244985156481059>
- <https://x.com/vista8/status/2107887033947660597>
