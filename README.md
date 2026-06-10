# NPU 本科毕业论文 Quarto 模板

基于 [Quarto](https://quarto.org/) 的西北工业大学本科毕业设计（论文）写作模板。用 Markdown（`.qmd`）撰写正文，导出符合学校版式要求的 PDF；也可输出 HTML 在浏览器中预览。

## 为什么选择 Quarto

- **语法更简洁**：正文用 Markdown 写作，比直接写 LaTeX 更省时
- **代码与图表一体**：可在 `.qmd` 中嵌入 Jupyter 代码块，渲染时自动执行并插入结果
- **多格式输出**：同一份源文件可导出 PDF 或 HTML，便于预览与分享
- **引用体系统一**：支持文献、公式、表格、图片的交叉引用（见 `index.qmd` 示例）

## 环境要求

| 依赖 | 说明 |
|------|------|
| [Quarto](https://quarto.org/docs/get-started/) | ≥ 1.4，用于渲染项目 |
| LaTeX 发行版 | 需支持 **XeLaTeX**（推荐 [TeX Live](https://www.tug.org/texlive/) 或 [MacTeX](https://www.tug.org/mactex/)） |
| Python 或 R | 可选；仅在 `.qmd` 中使用可执行代码块时需要 |

macOS / Windows / Linux 上中文字体分别使用系统自带的 **Songti SC / SimSun / Noto Serif CJK SC**（宋体）与 **Heiti SC Medium / SimHei / Noto Sans CJK SC Medium**（黑体），详见 [`_thesis/latex/fonts.tex`](_thesis/latex/fonts.tex)。

## 快速开始

1. **克隆或下载本仓库**，在项目根目录打开终端。

2. **填写基本信息**：
   - `_quarto.yml`：论文题目、作者、章节列表
   - `_thesis/frontmatter.yml`：专业、指导教师、毕业时间、中英文摘要与关键词

3. **撰写正文**：编辑各章 `.qmd` 文件；参考文献条目写入 `references.bib`。

4. **（可选）准备图片资源**：将校徽与页眉图放入 `assets/pic/`（见 [`assets/pic/README.md`](assets/pic/README.md)）。

5. **编译 PDF**：

   ```bash
   export BSTINPUTS="$(pwd)/_thesis/bst:$BSTINPUTS"
   quarto render --to pdf
   ```

   输出文件：`_book/thesis.pdf`。

6. **浏览器预览（HTML）**：

   ```bash
   quarto preview
   ```

   默认在 <http://localhost:7440> 打开（端口见 `_quarto.yml`）。

## 项目结构

```
.
├── _quarto.yml              # 书籍配置：标题、作者、章节、PDF/HTML 选项
├── _thesis/
│   ├── frontmatter.yml      # 封面字段与中英文摘要
│   ├── latex/               # LaTeX 导言、封面、目录 partial
│   ├── bst/                 # GB/T 7714 数字顺序制参考文献样式
│   └── reference/           # NWPU 官方 LaTeX 模板参考（不参与编译）
├── index.qmd                # 第一章（绪论）；Quarto 项目必须有此文件
├── virtual-auditory.qmd     # 示例章节
├── references.qmd           # 参考文献列表页
├── acknowledgements.qmd     # 致谢
├── closing.qmd              # 毕业设计小结
├── references.bib           # BibTeX 文献库
└── assets/
    ├── pic/                 # 封面 logo、页眉条图、正文插图
    └── docs/                # 学校 Word/PDF 模版等参考资料
```

版式与 LaTeX 基础设施说明见 [`_thesis/README.md`](_thesis/README.md)。

## 常用配置

### 修改论文元数据

在 `_quarto.yml` 中更新 `book.title`、`book.author`，并按需增删 `book.chapters` 中的章节文件。

封面与摘要相关字段在 `_thesis/frontmatter.yml`：

| 字段 | 含义 |
|------|------|
| `thesis_major` | 专业名称 |
| `thesis_advisor` | 指导教师 |
| `thesis_grad_year` / `thesis_grad_month` | 毕业年月 |
| `abstract_zh` / `keywords_zh` | 中文摘要与关键词 |
| `abstract_en` / `keywords_en` | 英文摘要与关键词 |

### 引用文献

使用 Pandoc 引用语法，例如 `[@knuth84]` 或 `@knuth84`。参考文献样式为 GB/T 7714 数字顺序制（`gbt7714-numerical`），编译 PDF 前须设置 `BSTINPUTS` 指向 `_thesis/bst/`。

### 交叉引用

`index.qmd` 中演示了公式（`@eq-...`）、表格（`@tbl-...`）、图片（`@fig-...`）的写法；为元素添加 `{#eq-id}`、`{#tbl-id}`、`{#fig-id}` 标签后即可引用。

### 新增章节

1. 在项目根目录新建 `chapter-name.qmd`
2. 在 `_quarto.yml` 的 `book.chapters` 列表中加入该文件

## 输出说明

| 命令 | 输出 |
|------|------|
| `quarto render --to pdf` | `_book/thesis.pdf`（正式提交用） |
| `quarto render --to html` | `_book/` 下 HTML 电子书 |
| `quarto preview` | 本地热重载预览 |

PDF 使用 `ctexbook` 文档类与 XeLaTeX；页眉页脚、行距、标题样式等由 `_thesis/latex/preamble.tex` 等文件控制，思路摘录自西北工大 `nwputhesis.cls`。

## 常见问题

**编译找不到 `gbt7714-numerical.bst`**  
确认已执行 `export BSTINPUTS="$(pwd)/_thesis/bst:$BSTINPUTS"`，且命令在项目根目录运行。

**封面无校徽、页眉为纯文字**  
将 `nwpulogo.png` 与 `nwpuheader.png` 放入 `assets/pic/`（规格见该目录 README）。

**黑体显示异常**  
确认系统已安装对应中文字体：macOS 需 **Heiti SC**、Windows 需 **SimHei**、Linux 建议安装 **Noto Sans CJK SC**（或 **Source Han Sans SC**）。配置见 `_thesis/latex/fonts.tex`。

## 致谢

本模板基于 [Quarto](https://quarto.org/) 实现西北工业大学本科毕业设计（论文）的 PDF 版式。LaTeX 层（`_thesis/latex/`）参照 `_thesis/reference/nwputhesis.cls` 思路改写，并适配 `ctexbook`、Pandoc partial 与跨平台系统字体（`_thesis/latex/fonts.tex`）。

版式实现参考以下开源项目：

- [NWPU-Thesis-Template](https://github.com/lihanshu/NWPU-Thesis-Template)（MIT License）——西北工大本科毕业论文 LaTeX 模板；本仓库 `_thesis/reference/` 留存其参考副本，不参与 Quarto 编译。

本仓库还包含以下第三方组件：

- [gbt7714-bibtex-style](https://github.com/zepinglee/gbt7714-bibtex-style)（LPPL-1.3c）——GB/T 7714 参考文献样式；文件位于 `_thesis/bst/gbt7714-numerical.bst`。

Quarto、CTeX、fontspec 等工具与宏包的使用请遵循各自许可协议。