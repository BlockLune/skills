# Markdown 工具参考

需要自动格式化、检查 Markdown、修复中英混排空格、检查中文字数等时使用本参考

## 安全规则

- 若工具缺失，则终止对应的自动化步骤并明确告知用户；可继续进行人工检查或撰写
- 不使用在同一条命令中同时读取和写入同一文件的重定向
- 用户未明确要求格式化时，优先使用只检查、不修改文件的命令
- 具体参数和能力以工具的 `--help` 输出为准

## rumdl

`rumdl` 是 Markdown 检查和格式化工具，可用于发现格式问题、自动格式化文件、修复部分可自动修复的问题。

```bash
rumdl --help
```

## pangu

`pangu` 是中英混排空格处理工具，可用于在中文与英文、数字、技术术语之间补充合适的空格。

```bash
npx -y pangu@latest --help
```

处理文件时必须使用临时文件或工具提供的安全写入方式，避免把输出直接重定向到原文件导致内容被清空。

## 中文字符统计

### python3

`python3` 跨平台性最好，优先使用：

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
