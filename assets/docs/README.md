# Quarto 本科毕业论文（PDF）

## 根目录你要管的内容

| 文件 / 目录 | 用途 |
|-------------|------|
| `_quarto.yml` | 书名、作者、章节列表、摘要、封面字段、PDF 选项 |
| `*.qmd` | 各章正文 |
| `references.bib` | 参考文献库 |
| `assets/pic/` | 封面 logo、页眉条图（见该目录 `README.md`） |
| `assets/docs/` | 学校 Word/PDF 模版等参考资料（不参与编译） |
| `README.md` | 本说明 |

版式与 LaTeX partial、`.bst`、NWPU 参考稿在 **`_thesis/`**（说明见 [`_thesis/README.md`](_thesis/README.md)）。

## 编译 PDF

```bash
export BSTINPUTS="$(pwd)/_thesis/bst:$BSTINPUTS"   # 使用 _thesis/bst 中的 gbt7714-numerical.bst
export TEXLIVE_AUTOINSTALL=0                        # 可选
quarto render --to pdf
```

输出：`_book/thesis.pdf`。

## 路径约定

- 摘要与封面字段：`_quarto.yml` → `metadata`
- 中文字体：按操作系统自动选用系统宋体/黑体（见 `_thesis/latex/fonts.tex`）
