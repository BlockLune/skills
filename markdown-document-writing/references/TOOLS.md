# Markdown 工具参考

## 安全规则

- 未经用户同意不安装工具，也不执行有破坏风险的重写命令。
- 工具缺失时停止对应的自动化步骤并告知用户，可继续人工检查或撰写。
- 重写文件时使用临时文件或工具提供的安全写入方式，不将读取结果直接重定向回原文件。
- 用户未明确要求格式化时，优先使用只检查、不修改文件的命令
- 具体参数和能力以工具的 `--help` 输出为准

## 工具选择

- `rumdl`：检查或格式化 Markdown。
- `pangu`：修复中英混排空格。调用方式以本地安装为准；`npx -y pangu@latest` 可能下载并安装包，受上述安装权限约束。

## 中文字符统计

按用户要求确定统计口径，包括是否计入英文、标点和代码。以下命令只统计汉字，不能直接代表所有字数要求：Python 和 GNU grep 示例仅覆盖基本汉字区间，`rg` 的 `Han` 范围更广。

### python3

统计基本汉字时优先使用 `python3`：

```bash
python3 -c "import sys, pathlib; s = pathlib.Path(sys.argv[1]).read_text(encoding='utf-8'); print(sum('\u4e00' <= c <= '\u9fff' for c in s))" 文件名.md
```

### ripgrep

如果环境中有 `rg`，可以使用 Unicode 字符类：

```bash
rg -o '\p{Han}' 文件名.md | wc -l
```

### grep

如果环境中有支持 `-P` 的 GNU grep，可以使用 Perl 兼容正则：

```bash
grep -oP '[\x{4e00}-\x{9fff}]' 文件名.md | wc -l
```
