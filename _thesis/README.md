# `_thesis/`（版式与参考文献样式）

一般只需通过根目录 `_quarto.yml` 与正文 `.qmd` 写作；本目录为 **PDF/LaTeX 基础设施**。

| 路径 | 说明 |
|------|------|
| `latex/preamble.tex` | 导言：版式、页眉页脚、`titlesec`/`titletoc`、`natbib` 等 |
| `latex/before-body.tex` | Pandoc partial：封面 + 双摘要 |
| `latex/toc.tex` | 目录 partial |
| `latex/fonts.tex` | 按 OS 设置宋体 + BoldFont 黑体（`\textbf` / `\bfseries`） |
| `bst/gbt7714-numerical.bst` | GB/T 7714 数字顺序制 BibTeX 样式 |
| `reference/` | 西北工大 LaTeX 模板参考（`main.tex`、`nwputhesis.cls`），**不参与 Quarto 编译** |

编译 PDF 前请设置 `BSTINPUTS` 以找到 `bst/`（见根目录 `README.md`）。
