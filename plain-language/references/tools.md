# Markdown 工具与字数统计

未经用户同意不安装工具；用户未明确要求修改文件时，只运行只读检查命令。

## 格式检查

- `rumdl`：`rumdl check 文件名.md`
- `autocorrect` / `pangu`：`autocorrect --lint 文件名.md`

## 中文字符统计

按用户要求确定是否计入英文、标点和代码。仅统计汉字时：

```bash
# python3（基本汉字区间 \u4e00-\u9fff）
python3 -c "import sys, pathlib; s = pathlib.Path(sys.argv[1]).read_text(encoding='utf-8'); print(sum('\u4e00' <= c <= '\u9fff' for c in s))" 文件名.md

# ripgrep（Unicode Han 字符类）
rg -o '\p{Han}' 文件名.md | wc -l
```
