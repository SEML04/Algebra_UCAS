# Repository Guidelines

## OCR 校正规则

- 查阅 `txt/Cartan-Eilenberg - Homological Algebra.txt` 时，注意其会将原书的希腊大写字母 `\Lambda` 误提取为 `A`。在模论语境中，`left A-module`、`left ideal I of A` 等表述应先按 `left \Lambda-module`、`left ideal I of \Lambda` 理解，并以对应 PDF 原页复核。

## 项目结构

这个仓库是一个代数学习与整理工作区，核心文件如下：

- `pdf/`：教材 PDF，如 `Algebra I.pdf`、`Algebra III.pdf`。
- `references/`：补充参考资料 PDF。
- `txt/`：统一存放所有由 PDF 提取出的可检索文本，文件名应尽量与原 PDF 同名。
- `collection/collection.tex`：正式主文档，统一收纳概念辨析、专题整理、题目整理与索引。
- `collection/collection.pdf`：由 `collection.tex` 编译生成的输出文件。
- `draft.md`：临时工作板，用于记录当前任务、证明草稿、待办与阶段性说明。
- `AGENTS.md`：仓库协作规则，不存放数学正文。

## 内容分工

- `collection/collection.tex` 只放长期保留的正式内容。
- `draft.md` 只放临时计划、重构说明、证明草稿和短期待办。
- 同一主题若既有正式结论又有当前安排：正式内容写入 `collection.tex`，临时说明写入 `draft.md`。
- 不再使用 `notes.md` 或旧的 `mistake collection.tex` 作为主文件；相关职责已经并入 `collection/collection.tex`。

## 文档结构约定

`collection/collection.tex` 当前按以下层次组织：

- `概念辨析`：记录定义差别、条件边界、常见误解。
- `专题整理`：放更完整的集中整理。
- `题目整理`：记录经典题目、题目来源、常用方法，以及必要时的错误点与修正思路。
- `索引`：只放一句话级别的定位条目，并尽量可点击跳转。

目录用于快速导航，不要把过细的子层级全部塞进目录。

## 常用命令

- `New-Item -ItemType Directory -Force .\txt; pdftotext -layout "pdf/Algebra III.pdf" "txt/Algebra III.txt"`：重新生成提取文本。
- `Select-String -Path ".\txt\Algebra III.txt" -Pattern "Proposition 5.3.12"`：定位原文。
- `Get-Content .\draft.md`：查看当前工作板。
- `Set-Location .\collection; xelatex collection.tex`：在 `collection/` 目录内编译正式文档。
- `Get-ChildItem .\collection,.\review -Recurse -File -Include *.aux,*.log,*.out,*.toc,*.synctex.gz,*.fls,*.fdb_latexmk,*.xdv | Remove-Item -Force`：清理 LaTeX 编译副产物，只保留 `tex/pdf` 与正文实际需要的资源文件。

修改 `collection.tex` 后，通常至少编译两次，以刷新目录和交叉引用。

## 写作与维护规则

- 新增内容前，先核对 PDF 或提取文本，不凭记忆补写结论。
- 所有 PDF 提取得到的 `txt` 文件统一放在 `txt/` 目录，不再分散存放在 `pdf/` 或 `references/` 下。
- 书中命题、定理、推论尽量保留编号，例如 `(III.Prop 5.3.12)`。
- 已在“专题整理”中完整展开的内容，在“概念辨析”里只保留短结论，避免重复堆叠。
- 每次向 `collection/collection.tex` 新增正式内容后，必须同步补入“索引”。
- 索引条目应尽量压缩成一句话，并显式带出所属 `subsection` 信息；若能点击跳转，则优先保留可点击定位。
- 索引中各条目的排列顺序必须与正文中对应内容的实际出现顺序一致；新增、拆分或移动小节后，要同步检查并重排索引，避免定位顺序错乱。
- 同一 `tex` 文件若需多次编译（例如为刷新目录、交叉引用），必须串行执行，不能并行运行多个 `xelatex` 进程；否则可能竞争写入 `aux`、`toc`、`out` 与 `pdf` 文件并导致输出损坏。
- 之后编译 `.tex` 文件时，无论处理的是哪个文件，都只能在 `.\collection` 文件夹内执行编译命令；不要在仓库根目录直接运行 `xelatex "collection/..."`，以免把 `pdf`、`aux`、`toc`、`log` 等产物写到错误位置。
- 编译结束后，若不再需要中间文件，应清理 `aux`、`log`、`out`、`toc`、`synctex.gz` 等副产物；默认只保留 `tex`、`pdf` 以及正文实际引用的图片等资源文件。
- 保留数学公式与交换图所需宏包，尤其是 `amsmath`、`amsthm`、`amssymb`、`tikz-cd`。
- 修改现有文档前，先阅读原内容，避免覆盖已完成整理。
- 题目整理部分的词条按主题顺序排列：`galois`（域论/Galois，含群论基础）→ `module`（模论）→ `ring`（环论，含 prime/radical/CSA）→ `representation`（表示论）→ `homology`（同调代数，暂未加入）。新增或移动题目时须归入对应主题区并保持该整体顺序，同时同步重排索引（索引顺序必须与正文对应内容的实际出现顺序一致）。
