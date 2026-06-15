# xarticle & xbook — Quarto 学术 PDF 模板集

基于标准 LaTeX 文档类的 Quarto 学术 PDF 模板集合，包含三个模板：

| 模板 | LaTeX 基础类 | 适用场景 |
|------|-------------|---------|
| **xarticle** | `article` | 预印本、工作论文、通用学术短文 |
| **xbook-en** | `book` | 英文学术专著、博士论文、长篇技术报告 |
| **xbook-cn** | `ctexbook` | 中文学术专著、博士论文、长篇技术报告 |

均由 `dfolio/quarto-ieee` 修改而来。

---

## xarticle — Quarto PDF Template (Standard LaTeX Article Class)

基于标准 LaTeX `article` 文档类的 Quarto 学术 PDF 模板，适用于预印本、工作论文及通用学术写作。

### 快速开始

#### 1. 安装扩展

将 `_extensions/xarticle/` 目录复制到你的 Quarto 项目根目录：

```bash
cp -r _extensions/xarticle/ /path/to/your-project/_extensions/
```

#### 2. 项目配置

在项目 `_quarto.yml` 中注册格式（可选，也可仅在文档 YAML 头部声明）：

```yaml
project:
  output-dir: .

format:
  xarticle-pdf:
    pdf-engine: xelatex
    keep-tex: true
    mainfont: "TeX Gyre Pagella"
    CJKmainfont: "Kaiti SC"
    CJKsansfont: "Noto Sans SC"
    CJKmonofont: "Noto Sans SC"
```

字体在 `_quarto.yml` 中配置，无需修改 LaTeX 文件即可更换字体。

#### 3. 编写文档

```qmd
---
title: "你的论文标题"
author:
  - name: 张三
    affiliations:
      - name: 东南大学
        department: 数学学院
        city: 南京
        country: China
    corresponding: true
    orcid: 0000-0002-9079-593X
    email: zhangsan@seu.edu.cn
  - name: 李四
    affiliations:
      - name: 北京大学
abstract: |
  摘要内容...
keywords: [关键词1, 关键词2, 关键词3]
bibliography: references.bib
format:
  xarticle-pdf:
    keep-tex: true
---

# 引言

正文...
```

#### 4. 编译

```bash
quarto render document.qmd
```

### 环境要求

- Quarto >= 1.3.0
- XeLaTeX (通过 TeX Live 或 MacTeX 安装)
- 中文字体：Kaiti SC、Noto Sans SC

### 模板特性

| 特性 | 说明 |
|------|------|
| **LaTeX 基础类** | 标准 `article` 文档类 |
| **PDF 引擎** | XeLaTeX |
| **正文字体** | Palatino-like (TeX Gyre Pagella，通过 `_quarto.yml` 的 `mainfont` 配置) |
| **数学字体** | Latin Modern Math (unicode-math) |
| **中文支持** | 通过 `xeCJK`，字体在 `_quarto.yml` 中配置：CJK 正文 Kaiti SC，无衬线/等宽 Noto Sans SC |
| **参考文献** | natbib，数字序号，方括号，排序压缩。样式 `plainnat-doi`，含 DOI 链接 |
| **页面布局** | 11pt 字号，四边 1 英寸页边距 |
| **行距** | 1.2 倍行距 |
| **标题** | `\Large` 字号 |
| **定理环境** | 通过 `tcolorbox` 提供圆角边框的定理/引理/推论/命题/定义/例子/注记环境 |
| **代码输出** | 默认 `echo: false, warning: false, freeze: true`，表格使用 `kable` |
| **超链接** | 红色内部链接、蓝色引用链接，支持 PDF 书签 |
| **ORCID 图标** | 在 `author` 字段中提供 `orcid:` 即自动生成 ORCID 链接图标 |

### 定理环境

在 `.qmd` 中使用 Quarto 的 fenced div 语法：

```markdown
::: {#thm-example .theorem}
## 定理名称
定理内容...
:::

::: {#lem-example .lemma}
## 引理名称
引理内容...
:::

::: {#cor-example .corollary}
## 推论名称
推论内容...
:::

::: {#def-example .definition}
## 定义名称
定义内容...
:::
```

支持的环境类型：`theorem`, `lemma`, `corollary`, `proposition`, `definition`, `example`, `remark`。

### 交叉引用

支持标准 Quarto 交叉引用语法：

```markdown
参见定理 @thm-example 和表 @tbl-sample。
```

### 参考文献

使用 `.bib` 文件管理引用，在文档 YAML 头部指定：

```yaml
bibliography: references.bib
```

正文中引用：

```markdown
关于随机微积分的基础知识参见 @karatzas1991brownian。
```

### 自定义微分算子

模板预定义 `\dd` 命令用于微分算子：

```latex
\int f(x) \dd x
```

### 附录

使用 Quarto 的附录语法：

```markdown
[]{.appendix options="An Appendix"}

附录内容...
```

### 致谢

使用无编号标题：

```markdown
# Acknowledgment {-}

致谢内容...
```

### 自定义

如需修改模板行为，编辑 `_extensions/xarticle/_extension.yml` 及 `_extensions/xarticle/partials/` 下的 `.tex` 文件：

| 文件 | 用途 |
|------|------|
| `doc-class.tex` | LaTeX 文档类声明 |
| `title.tex` | 标题排版 |
| `author.tex` | 作者信息排版 |
| `affiliation.tex` | 隶属单位排版 |
| `before-body.tex` | 正文前内容（摘要、关键词等） |
| `before-bib.tex` | 参考文献前插入内容 |
| `after-body.tex` | 参考文献后插入内容 |
| `preamble.tex` | 宏包加载与全局设置 |
| `theorem-boxes.tex` | 定理盒子样式定义 |

---

## xbook-en — Quarto PDF Template (Standard LaTeX Book Class, English)

基于标准 LaTeX `book` 文档类的 Quarto 英文学术书籍 PDF 模板，适用于学术专著、博士论文及长篇学术写作。

### 快速开始

#### 1. 安装扩展

将 `_extensions/xbook-en/` 目录复制到你的 Quarto 项目根目录：

```bash
cp -r _extensions/xbook-en/ /path/to/your-project/_extensions/
```

#### 2. 项目配置

在项目 `_quarto.yml` 中注册格式（可选，也可仅在文档 YAML 头部声明）：

```yaml
project:
  output-dir: .

format:
  xbook-en-pdf:
    pdf-engine: xelatex
    keep-tex: true
    mainfont: "TeX Gyre Pagella"
    CJKmainfont: "Kaiti SC"
    CJKsansfont: "Noto Sans SC"
    CJKmonofont: "Noto Sans SC"
```

字体在 `_quarto.yml` 中配置，无需修改 LaTeX 文件即可更换字体。

#### 3. 编写文档

```qmd
---
title: A Sample Book Using Quarto with Standard LaTeX Book Class
author:
  - id: xz
    name: Xin Zhang
    affiliations:
      - name: Southeast University
        department: School of Mathematics
        city: Nanjing
        country: China
        postal-code: 211189
    corresponding: true
    orcid: 0000-0001-6670-5351
    email: xzhangseu@seu.edu.cn
    url: https://math.seu.edu.cn/zx_en/list.htm
    attributes:
      corresponding: true
    bio: |
      Xin Zhang is a professor at the School of Mathematics, Southeast University.
      His research interests include stochastic control theory and its applications
      in finance and insurance.
  - name: John Doe
    affiliations:
      - name: Anonymous University
    bio: |
      John Doe is a researcher at Anonymous University.
abstract: |
  This document demonstrates how to use Quarto with the standard LaTeX book
  document class. It produces PDF output suitable for monographs,
  dissertations, and long-form academic writing.
keywords: [Quarto, LaTeX, book, Pandoc, template]
bibliography: bibliography.bib
date: 2023-06-23
format:
  xbook-en-pdf:
    keep-tex: true
---

# Introduction {#sec-intro}

正文...
```

#### 4. 编译

```bash
quarto render xbook-template-en.qmd
```

### 环境要求

- Quarto >= 1.3.0
- XeLaTeX (通过 TeX Live 或 MacTeX 安装)
- 中文字体：Kaiti SC、Noto Sans SC（用于 CJK fallback）

### 模板特性

| 特性 | 说明 |
|------|------|
| **LaTeX 基础类** | 标准 `book` 文档类 |
| **PDF 引擎** | XeLaTeX |
| **正文字体** | Palatino-like (TeX Gyre Pagella，通过 `_quarto.yml` 的 `mainfont` 配置) |
| **数学字体** | Latin Modern Math (unicode-math) |
| **中文支持** | 通过 `xeCJK`（fallback 模式），字体在 `_quarto.yml` 中配置：CJK 正文 Kaiti SC，无衬线/等宽 Noto Sans SC |
| **参考文献** | natbib，数字序号，方括号，排序压缩。样式 `plainnat-doi`，含 DOI 链接 |
| **页面布局** | 11pt 字号，twoside 双面排版，内外边距各 1 英寸 |
| **行距** | 1.2 倍行距 |
| **标题** | `\Large` 字号 |
| **章节编号** | `top-level-division: chapter`，支持章/节/小节层级 |
| **目录** | 自动生成，toc-depth=2，标题 "Contents" |
| **定理环境** | 通过 `tcolorbox` 提供圆角边框的定理/引理/推论/命题/定义/例子/注记环境 |
| **页眉页脚** | fancyhdr：页眉居中显示当前节标题，页脚居中显示页码，无横线 |
| **代码输出** | 默认 `echo: false, warning: false, freeze: true`，表格使用 `kable` |
| **超链接** | 红色内部链接、蓝色引用链接，PDF 书签编号且展开 |
| **ORCID 图标** | 在 `author` 字段中提供 `orcid:` 即自动生成 ORCID 链接图标 |
| **作者简介** | 在 `author` 中提供 `bio:` 字段，自动在文末生成作者简介 |
| **通讯作者** | 在 `author.attributes.corresponding: true` 标注通讯作者 |

### 定理环境

在 `.qmd` 中使用 Quarto 的 fenced div 语法：

```markdown
::: {#thm-residue .theorem}
## Residue Theorem
Let $f$ be analytic in a simply connected domain $D$. Then for any closed contour $\gamma \subset D$,
$$
\oint_\gamma f(z)\,dz = 2\pi i \sum_{k} \mathrm{Res}(f, z_k)
$$
:::

::: {#lem-key .lemma}
## Key Lemma
If $f$ is continuous on $[a,b]$, then $f$ is integrable on $[a,b]$.
:::

::: {#cor-easy .corollary}
## Easy Corollary
Every continuous function on a closed interval is bounded.
:::

::: {#def-model .definition}
## Model Definition
A stochastic process $\{X_t\}_{t \ge 0}$ is a collection of random variables indexed by time.
:::
```

支持的环境类型：`theorem`, `lemma`, `corollary`, `proposition`, `definition`, `example`, `remark`。

### 交叉引用

支持标准 Quarto 交叉引用语法：

```markdown
You can refer to Theorem @thm-residue and Table @tbl-sample in the text.
```

### 参考文献

使用 `.bib` 文件管理引用，在文档 YAML 头部指定：

```yaml
bibliography: bibliography.bib
```

正文中引用：

```markdown
It is assumed that the reader has a basic working knowledge of stochastic calculus @karatzas1991brownian.
```

### 自定义微分算子

模板预定义 `\dd` 命令用于微分算子：

```latex
\int f(x) \dd x
```

### 附录

使用 Quarto 的附录语法：

```markdown
[]{.appendix options="An Appendix"}

Appendix content...
```

> **注意**：不要在 `\appendix` 之后使用 `\section{}`。

### 致谢

使用无编号标题：

```markdown
# Acknowledgment {-}

Acknowledgment content...
```

### 页面结构

xbook-en 的正文前页面结构如下：

1. **标题页** — `\maketitle` 自动生成
2. **空白页** — 标题页后插入一页空白（双面排版需要）
3. **前置页面** — 使用罗马数字编页（`pagenumbering{Roman}`）
4. **正文** — 阿拉伯数字编页

### 自定义

如需修改模板行为，编辑 `_extensions/xbook-en/_extension.yml` 及 `_extensions/xbook-en/partials/` 下的 `.tex` 文件：

| 文件 | 用途 |
|------|------|
| `doc-class.tex` | LaTeX 文档类声明（`book`） |
| `title.tex` | 标题排版 |
| `author.tex` | 作者信息排版（含通讯作者标注） |
| `affiliation.tex` | 隶属单位排版 |
| `before-body.tex` | 正文前内容（标题页、空白页、罗马数字页码） |
| `before-bib.tex` | 参考文献前插入内容（清空页眉标记） |
| `after-body.tex` | 参考文献后插入内容（作者简介） |
| `preamble.tex` | 宏包加载与全局设置 |
| `theorem-boxes.tex` | 定理盒子样式定义 |

### 与 xarticle 的主要差异

| 差异点 | xarticle | xbook-en |
|--------|----------|----------|
| 文档类 | `article` | `book` |
| 排版方式 | 单面 | 双面 (twoside) |
| 章节结构 | `#` → section | `#` → chapter |
| 目录 | 无 | 自动生成 (toc-depth=2) |
| 前置页面 | 无 | 罗马数字编页 |
| 作者简介 | 无 | 支持 `bio` 字段 |
| 通讯作者标注 | "Corresponding author" | "Corresponding author" |

---

## xbook-cn — Quarto PDF Template (ctexbook 中文书籍类)

基于 `ctexbook` 文档类的 Quarto 中文学术书籍 PDF 模板，适用于中文专著、博士论文及长篇学术写作。

### 快速开始

#### 1. 安装扩展

将 `_extensions/xbook-cn/` 目录复制到你的 Quarto 项目根目录：

```bash
cp -r _extensions/xbook-cn/ /path/to/your-project/_extensions/
```

#### 2. 项目配置

在项目 `_quarto.yml` 中注册格式（可选，也可仅在文档 YAML 头部声明）：

```yaml
project:
  output-dir: .

format:
  xbook-cn-pdf:
    pdf-engine: xelatex
    keep-tex: true
    mainfont: "TeX Gyre Pagella"
    CJKmainfont: "Kaiti SC"
    CJKsansfont: "Noto Sans SC"
    CJKmonofont: "Noto Sans SC"
```

字体在 `_quarto.yml` 中配置，无需修改 LaTeX 文件即可更换字体。

#### 3. 编写文档

```qmd
---
title: 基于 Quarto 与标准 LaTeX Book 文档类的中文书籍模板
lang: zh-CN
author:
  - id: xz
    name: 张鑫
    affiliations:
      - name: 东南大学
        department: 数学学院
        city: 南京
        country: 中国
        postal-code: 211189
    corresponding: true
    orcid: 0000-0001-6670-5351
    email: xzhangseu@seu.edu.cn
    url: https://math.seu.edu.cn/zx_en/list.htm
    attributes:
      corresponding: true
    bio: |
      张鑫，东南大学数学学院教授。
      研究方向为随机控制理论及其在金融保险中的应用。
  - name: John Doe
    affiliations:
      - name: Anonymous University
    bio: |
      John Doe is a researcher at Anonymous University.
abstract: |
  本文档演示如何使用 Quarto 配合 ctexbook 文档类生成中文书籍 PDF。
  适用于中文学术专著、博士论文及长篇学术写作。
keywords: [Quarto, LaTeX, ctexbook, 中文, 模板]
bibliography: bibliography.bib
date: 2023-06-23
format:
  xbook-cn-pdf:
    keep-tex: true
---

# 引言 {#sec-intro}

正文...
```

#### 4. 编译

```bash
quarto render xbook-template-cn.qmd
```

### 环境要求

- Quarto >= 1.3.0
- XeLaTeX (通过 TeX Live 或 MacTeX 安装)
- 中文字体：Kaiti SC、Noto Sans SC
- 需安装 `thmtools` 宏包（用于重定义定理环境的中文名称）

### 模板特性

| 特性 | 说明 |
|------|------|
| **LaTeX 基础类** | `ctexbook`（`fontset=none`，手动配置字体） |
| **PDF 引擎** | XeLaTeX |
| **正文字体** | Palatino-like (TeX Gyre Pagella，通过 `_quarto.yml` 的 `mainfont` 配置) |
| **数学字体** | Latin Modern Math (unicode-math) |
| **中文支持** | `ctexbook` + 字体在 `_quarto.yml` 中配置：CJK 正文 Kaiti SC，无衬线/等宽 Noto Sans SC |
| **中文标点** | 半角标点风格 (`\punctstyle{banjiao}`) |
| **参考文献** | natbib，数字序号，方括号，排序压缩。样式 `plainnat-doi`，含 DOI 链接 |
| **参考文献标题** | 自动显示为"参考文献"（通过 `xpatch` 修补 `\bibliography` 命令） |
| **页面布局** | 11pt 字号，oneside 单面排版，四边各 1 英寸页边距 |
| **行距** | 1.2 倍行距 |
| **标题** | `\Large` 字号 |
| **章节编号** | `top-level-division: chapter`，支持章/节/小节层级 |
| **目录** | 自动生成，toc-depth=2，标题"目录" |
| **定理环境** | 通过 `tcolorbox` 提供圆角边框环境，**中文名称**：定理/引理/推论/定义/命题/例/注 |
| **证明环境** | 证明名称自动改为"证明" |
| **页眉页脚** | fancyhdr：页眉居中显示当前节标题，页脚居中显示页码，无横线 |
| **代码输出** | 默认 `echo: false, warning: false, freeze: true`，表格使用 `kable` |
| **超链接** | 红色内部链接、蓝色引用链接，PDF 书签编号且展开 |
| **ORCID 图标** | 在 `author` 字段中提供 `orcid:` 即自动生成 ORCID 链接图标 |
| **作者简介** | 在 `author` 中提供 `bio:` 字段，自动在文末生成作者简介 |
| **通讯作者** | 在 `author.attributes.corresponding: true` 标注"通讯作者" |

### 定理环境

在 `.qmd` 中使用 Quarto 的 fenced div 语法，**定理名称在 PDF 中自动显示中文**：

```markdown
::: {#thm-residue .theorem}
## 留数定理
设 $f$ 在单连通区域 $D$ 内解析，则对任意闭曲线 $\gamma \subset D$，
$$
\oint_\gamma f(z)\,dz = 2\pi i \sum_{k} \mathrm{Res}(f, z_k)
$$
:::

::: {#lem-key .lemma}
## 关键引理
若 $f$ 在 $[a,b]$ 上连续，则 $f$ 在 $[a,b]$ 上可积。
:::

::: {#def-model .definition}
## 模型定义
随机过程 $\{X_t\}_{t \ge 0}$ 是一族以时间为指标的随机变量。
:::
```

支持的环境类型及中文名称：

| 环境类型 | 中文名称 | 编号方式 |
|---------|---------|---------|
| `theorem` | 定理 | section 级编号 |
| `lemma` | 引理 | section 级编号 |
| `corollary` | 推论 | section 级编号 |
| `proposition` | 命题 | section 级编号 |
| `definition` | 定义 | section 级编号 |
| `example` | 例 | section 级编号 |
| `remark` | 注 | section 级编号 |

### 交叉引用

支持标准 Quarto 交叉引用语法：

```markdown
参见定理 @thm-residue 和表 @tbl-sample。
```

### 参考文献

使用 `.bib` 文件管理引用，在文档 YAML 头部指定：

```yaml
bibliography: bibliography.bib
```

正文中引用：

```markdown
关于随机微积分的基础知识参见 @karatzas1991brownian。
```

### 自定义微分算子

模板预定义 `\dd` 命令用于微分算子：

```latex
\int f(x) \dd x
```

### 附录

使用 Quarto 的附录语法：

```markdown
[]{.appendix options="附录标题"}

附录内容...
```

> **注意**：不要在 `\appendix` 之后使用 `\section{}`。

### 致谢

使用无编号标题：

```markdown
# 致谢 {-}

致谢内容...
```

### 页面结构

xbook-cn 的正文前页面结构如下：

1. **标题页** — `\maketitle` 自动生成
2. **空白页** — 标题页后插入一页空白
3. **前置页面** — 使用罗马数字编页（`pagenumbering{Roman}`）
4. **正文** — 阿拉伯数字编页

### 自定义

如需修改模板行为，编辑 `_extensions/xbook-cn/_extension.yml` 及 `_extensions/xbook-cn/partials/` 下的 `.tex` 文件：

| 文件 | 用途 |
|------|------|
| `doc-class.tex` | LaTeX 文档类声明（`ctexbook`，`fontset=none`） |
| `title.tex` | 标题排版 |
| `author.tex` | 作者信息排版（含"通讯作者"标注） |
| `affiliation.tex` | 隶属单位排版 |
| `before-body.tex` | 正文前内容（标题页、空白页、罗马数字页码、中文定理环境重定义） |
| `before-bib.tex` | 参考文献前插入内容（修补 `\bibliography` 为中文标题，清空页眉标记） |
| `after-body.tex` | 参考文献后插入内容（作者简介） |
| `preamble.tex` | 宏包加载与全局设置 |
| `theorem-boxes.tex` | 定理盒子样式定义 |

### 与 xbook-en 的主要差异

| 差异点 | xbook-en | xbook-cn |
|--------|----------|----------|
| 文档类 | `book` | `ctexbook` (`fontset=none`) |
| 排版方式 | 双面 (twoside) | 单面 (oneside) |
| 页边距 | 内外边距各 1 英寸 (双面) | 左右边距各 1 英寸 (单面) |
| 目录标题 | "Contents" | "目录" |
| 参考文献标题 | "References" | "参考文献" |
| 定理环境中文名 | 无（英文默认） | 定理/引理/推论/定义/命题/例/注 |
| 证明环境 | Proof | 证明 |
| 通讯作者标注 | "Corresponding author" | "通讯作者" |
| 语言包 | `babel` (english) | ctexbook 内置中文支持 |

---

## 通用说明

### 编译命令

```bash
# 渲染为 PDF
quarto render document.qmd

# 保留中间 .tex 文件
quarto render document.qmd --to xarticle-pdf   # 或 xbook-en-pdf / xbook-cn-pdf
```

### 常见问题

**Q: 编译报错找不到字体？**

确保系统安装了 Kaiti SC 和 Noto Sans SC 字体。macOS 自带 Kaiti SC；Linux 可安装 `fonts-noto-cjk`，并将 `_quarto.yml` 中的 `CJKmainfont` 改为 `KaiTi`。

**Q: 如何更换字体？**

字体在 `_quarto.yml` 中集中配置，修改对应的键值即可，无需编辑 LaTeX 文件：

```yaml
format:
  xarticle-pdf:        # 或 xbook-en-pdf / xbook-cn-pdf
    mainfont: "Times New Roman"           # 西文正文
    CJKmainfont: "SimSun"                  # 中文正文
    CJKsansfont: "SimHei"                  # 中文无衬线
    CJKmonofont: "FangSong"                # 中文等宽
```

**Q: 如何切换为单面/双面排版？**

在 `_quarto.yml` 中修改 `classoption`：

```yaml
format:
  xbook-en-pdf:
    classoption: oneside   # 单面排版
    # classoption: twoside # 双面排版（默认）
```

**Q: 如何修改页边距？**

在 `_quarto.yml` 中覆盖 `geometry` 选项：

```yaml
format:
  xarticle-pdf:
    geometry: "left=1.5in,right=1.5in,top=1in,bottom=1in"
```

**Q: 如何使用作者简介功能？**

在 `author` 字段中添加 `bio:` 即可，模板会在文末自动生成作者简介段落。可选添加 `photo:` 字段显示作者照片。

### License

MIT
