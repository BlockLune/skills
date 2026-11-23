---
name: set-up-agent-ready-repo
description: 盘点并补齐仓库的 agent 基础配置：入口文件、文档分工与 ADR 规则、文档更新清单、计划文件和检查命令。
disable-model-invocation: true
---

# 整理 agent-ready 仓库

把新建仓库或已有仓库整理为 agent-ready 状态。能用代码和自动检查说清的，就不另写文档；每类文档只放在一个固定位置；硬性规则尽量靠权限规则、hook 或 lint 兜底；改动有一条统一的检查命令；目录结构是次要的。

先盘点仓库现状，只补缺少的部分，沿用已有的文件名和路径（例如已有 `CONTEXT.md` 就继续用 `CONTEXT.md`）。

## 流程

1. 盘点仓库现状

   读取仓库根目录的 `AGENTS.md` 或 `CLAUDE.md`、`docs/`、`README`、构建配置（例如 `package.json`）、已有 skill，以及 hook 和权限配置。按需读取以下参考文件对照检查：

   - 入口文件、硬性规则的强制手段、重复出错时的修正位置：读 [entry-file.md](references/entry-file.md)。
   - 内容分工、ADR 规则、文档更新清单、计划文件：读 [fact-ownership.md](references/fact-ownership.md)。
   - 检查命令与 verify skill 推荐：读 [verification.md](references/verification.md)。
   - 仓库会写入真实外部系统时：再读 [external-systems.md](references/external-systems.md)。

   完成标准：已读参考文件覆盖的每一项，都已标明现状（已有、缺失或重复）并附上对应文件路径。

2. 输出盘点报告并等待确认

   把盘点结果整理成一份盘点报告发给用户，等用户确认后再改文件。

   代码和配置看不出仓库是否会写入真实外部系统时，只问用户一个问题：这个仓库会不会写入真实外部系统（用于决定是否配置 [external-systems.md](references/external-systems.md) 的安全边界）。能从代码和配置看出来时直接判定。

   以下问题在盘点报告中只列位置和现状，留给用户处理：

   - 多处重复维护（同一内容写在多处）：列出各文件路径，由用户决定保留哪份并合并。
   - 仅靠文字提醒的硬性规则：列出缺少权限规则、hook 或 lint 兜底的条目（见 [entry-file.md](references/entry-file.md) 的“硬性规则的强制手段”）。
   - 疑似过期或模型默认就会遵守的规则：列出 `AGENTS.md` 或 `CLAUDE.md` 中的对应行，由用户决定是否删除。
   - 缺失的自动检查：指出缺少的类型检查、测试或 lint，由用户补充。
   - 缺失的 verify skill：附上推荐链接（见 [verification.md](references/verification.md) 的“推荐 verify skill”）。
   - 代码与 ADR 或规格文档不一致：列出冲突位置，由用户判断是实现出错还是决策已变。

   完成标准：已向用户发送完整盘点报告并收到确认；如提出了外部系统问题，已收到答复。

3. 写入缺失内容

   按 [entry-file.md](references/entry-file.md) 的“选择入口文件”确定入口文件。只补充用户确认的缺失项；已有章节原地更新，保留用户在周围写的内容，同一章节不重复出现。

   完成标准：用户确认的缺失项均已写入对应文件，每个章节在文件内只出现一次。

4. 核对并汇报

   逐项检查写入结果，向用户汇报修改了哪些文件与章节，并列出留给用户决定的事项。

   完成标准：入口文件里能找到每类文档的唯一存放位置；文档更新清单指向的文件全部存在；入口文件里的检查命令在终端可正常运行。
