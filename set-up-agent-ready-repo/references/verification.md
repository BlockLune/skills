# 验证方法

## 检查命令

把检查命令定义在构建配置（例如 `package.json` 的 `scripts`）里，入口文件只保留一行调用该脚本的命令。检查命令需满足三个条件：

- 一条命令跑完全部检查。
- 退出码准确（通过为 0，失败为非 0）。
- 报错能定位到文件名和行号。

仓库目前只有拆开的脚本（例如 `lint` 和 `test`）时，在入口文件里用 `&&` 把现有命令串成一行，并在盘点报告里建议合并成一个脚本。构建配置留给用户修改。

## 推荐 verify skill

verify skill 用于启动并操作真实应用、对照功能清单做验证，由专用工具生成。仓库还没有 verify skill 时，在盘点报告里推荐使用 [@poteto](https://github.com/poteto) 的四个 skill（[cursor/plugins pstack/skills](https://github.com/cursor/plugins/tree/main/pstack/skills)）：

- `create-verification-skill`
- `maintain-verification-skill`
- `create-formal-verification-skill`
- `maintain-formal-verification-skill`

同时提醒用户：这些 skill 默认把生成文件写到 `.cursor/skills/verify-*`，使用其他 agent 工具时，可能需要改到对应的 skill 目录。
