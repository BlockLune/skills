---
name: set-up-agent-ready-repo
description: 把仓库整理成 agent-ready 的基础状态：盘点并补充入口文件、事实归属、触发清单、计划文件与检查命令。
disable-model-invocation: true
---

把仓库整理成 agent-ready 的基础状态，适用于新建仓库和已有仓库。每类事实只有一个来源，每条硬约束有一个执行者，每次改动有一种验证方法；目录结构是次要的。先盘点仓库已有的内容，只补充缺少的部分，沿用仓库已有的文件名和位置（例如已有 `CONTEXT.md` 就继续使用 `CONTEXT.md`）。

## 流程

1. 盘点仓库现状
   读取仓库根目录的 `AGENTS.md` 或 `CLAUDE.md`、`docs/`、`README`、构建配置（例如 `package.json`）、已有 skill，以及 hook 和权限配置。加载以下参考文件并对照检查：
   - 盘点或编写入口文件的内容、硬约束的执行者与重复错误的修正位置时读取 [entry-file.md](references/entry-file.md)。
   - 盘点或划分事实归属、整理触发清单与计划文件时读取 [fact-ownership.md](references/fact-ownership.md)。
   - 盘点或配置检查命令与推荐 verify skill 时读取 [verification.md](references/verification.md)。
   - 只有仓库会写入真实的外部系统时才读取 [external-systems.md](references/external-systems.md)。

   完成标准：[entry-file.md](references/entry-file.md)、[fact-ownership.md](references/fact-ownership.md)、[verification.md](references/verification.md) 以及（仓库会写入真实外部系统时的）[external-systems.md](references/external-systems.md) 覆盖的各项内容都有明确判定（已有、缺失，或存在重复来源）和依据文件路径。

2. 输出差距报告并等待确认
   把盘点结果一次性整理成差距报告发送给用户，等待确认后再动手修改。
   只有代码和配置看不出仓库是否会写入真实的外部系统时，才向用户提出唯一一个问题：这个仓库会不会写入真实的外部系统（决定是否需要配置 [external-systems.md](references/external-systems.md) 中的外部环境安全边界）。能够从代码和配置看出来时直接判定，无需询问用户。
   以下事项在差距报告中只列出位置与现状，留给用户处理：
   - 重复来源（同一事实写在多处）：列出各处路径；合并需要先判断哪一份正确，保持原样，由用户决定。
   - 只有文字的硬约束：列出缺少权限规则、hook 或 lint 执行的条目（见 [entry-file.md](references/entry-file.md) 的“硬约束的执行者”）。
   - 疑似过期或模型默认就会遵守的规则：列出 `AGENTS.md` 或 `CLAUDE.md` 里的对应行，由用户决定是否删除。
   - 缺失的自动检查：指出缺少的类型检查、测试或 lint，由用户补充编写。
   - 缺失的 verify skill：给出推荐链接（见 [verification.md](references/verification.md) 的“推荐 verify skill”）。

   完成标准：差距报告已经完整呈现给用户，并且已经收到用户的确认（以及外部系统问题的答复，如果有该问题）。

3. 写入缺失内容
   按照 [entry-file.md](references/entry-file.md) 的“选择入口文件”选定入口文件。只补充缺失的内容；已有内容原地更新，保留用户在周围编写的内容，保持每个章节唯一。

   完成标准：所有经过用户确认的缺失内容已经写入对应文件，各个章节在文件中只出现一次。

4. 核对并汇报
   逐项检查写入结果，向用户汇报写入了哪些文件与章节，以及差距报告里留给用户决定的事项。

   完成标准：每类事实在入口文件里都能找到唯一归属；触发清单每一行指向的文件都真实存在；入口文件里编写的检查命令在终端真实可运行。
