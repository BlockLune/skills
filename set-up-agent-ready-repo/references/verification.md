# 验证方法

## 检查命令

检查命令定义在构建配置（例如 `package.json` 的 `scripts`）里，入口文件只用一行命令指向该脚本。检查命令需要满足三个条件：一条命令运行完毕、退出码可靠、报错能够定位到文件名和行号。仓库只有分开的脚本（例如 `lint` 和 `test`）时，在入口文件里把现有命令用 `&&` 连接成一行，并在差距报告里建议合并成一个脚本；构建配置留给用户修改。

## 推荐 verify skill

verify skill（能够启动并驱动真实应用、带有功能清单的验证 skill）由专用工具生成。仓库还没有 verify skill 时，在差距报告里推荐使用 [@poteto](https://github.com/poteto) 的 `create-verification-skill`、`maintain-verification-skill`、`create-formal-verification-skill`、`maintain-formal-verification-skill`（<https://github.com/cursor/plugins/tree/main/pstack/skills>）。同时说明：这些 skill 默认把结果写到 `.cursor/skills/verify-*`，在其他 agent 产品下可能要改成对应的 skill 目录。
