# 北京师范大学本科生毕业论文（设计）开题报告 LaTeX 模板

## 最快使用方法

1. 在 Overleaf 中选择 `New Project -> Upload Project`，上传整个 ZIP。
2. 主文件为 `main.tex`。模板默认编译器仍为 `pdfLaTeX`。
3. 打开 `fields.tex`，只修改每个命令最后一对大括号中的内容。
4. 点击 `Recompile`。内容增多时表格会自动延长并增加页数。

`fields.tex` 中的命令已经存在，请直接填写空括号，不要在文件末尾重复添加同名的 `\newcommand`。

```tex
\newcommand{\StudentName}{张三}
\newcommand{\StudentID}{202311010001}
\newcommand{\BasisAndContent}{第一段内容。\par 第二段内容。}
```

## 动态表格和跨页规则

- 每个栏目保留原 Word 的最小行高，因此内容较少时仍接近原空白模板。
- 内容超过最小行高后，当前单元格会自动增高，后面的栏目依次向后移动。
- 一个栏目可以从当前页延续到下一页，文字不会被裁切，也不会压住表格线。
- 跨页处会在前一页底部和后一页顶部同时绘制横线，并继续绘制左右边框和中间竖线。
- 每个续页片段都会重复完整栏目名，不再使用缩写或“（续）”。
- 从“选题依据及研究内容”到“部院系意见”，左栏约为两到三个五号汉字宽，右侧正文栏相应加宽。
- 最终页数不固定为两页，会随填写内容自动增加。
- 通常不要在正文命令里手工加入 `\newpage`、`\pagebreak` 或固定高度盒子。

## 字号和字体

所有用户填写内容，包括表头中的姓名、学号、专业、教师信息、论文题目以及各正文栏目，均固定为五号字，即 `10.5 pt`，行距约为 `15.6 pt`。内容增多时只增加正文单元格的行高和页数，不会自动缩小正文字号。报告标题使用三号字，即 `16 pt`。

表头中的短字段受原 Word 列宽和行高限制，也不会缩小字号。姓名、职称和单位名称过长时，请使用学校认可的规范简称，避免文字越过单元格边界。

模板默认保持 `pdfLaTeX`，这是最稳妥的直接编译方式：

- 中文使用 Overleaf 自带的宋体类字体；
- 英文和数字使用 Times 兼容字体；
- 不会调用 `fontspec`、`\setmainfont` 或 CTeX 的 Fandol fontset，因此不会再出现此前的编译错误。

ZIP 的 `fonts/` 中已经放入宋体、黑体和 Times New Roman 字体文件。如果需要字体文件意义上的精确字体，请在 Overleaf 的 `Settings -> Compiler` 中把编译器改为 `XeLaTeX`：正文中文会调用 `simsun.ttc`，标题会调用 `simhei.ttf`，英文和数字会调用 Times New Roman。`pdfLaTeX` 本身不能直接读取 `.ttf/.ttc`，所以保持默认编译器时使用的是外观接近的兼容字体。具体文件说明见 `fonts/README.md`。

## 添加图片

1. 把 PNG、JPG 或 PDF 图片上传到项目的 `images/` 文件夹。
2. 在 `fields.tex` 的正文栏目内写 `\ReportFigure{图片键}{文件名}{图题}`。
3. 在前文写 `\FigureRef{图片键}` 自动引用图号。

```tex
\renewcommand{\BasisAndContent}{
研究区如\FigureRef{study-area}所示。\par
\ReportFigure{study-area}{study-area.png}{研究区位置}
}
```

默认宽度为正文栏的 82%。需要调小时写：

```tex
\ReportFigure[0.65\linewidth]{workflow}{workflow.pdf}{研究流程}
```

建议文件名只使用英文字母、数字和短横线。图片太高时应先裁剪或调小宽度；图片本身不会从中间拆到两页。

## 正文、分段和网址

- `\par` 表示另起一段，长正文优先使用它。
- `\\` 表示强制换行，只在确实需要固定换行时使用。
- 长网址应写成 `\url{...}`，这样网址可以在 `/`、`-` 等位置自动换行。
- `\url{...}` 内的下划线通常不需要转义；普通正文中的特殊字符仍需转义。

```tex
\newcommand{\BasisAndContent}{
第一段研究内容。\par
数据来源为 \url{https://example.com/a/very/long/path}。
}
```

普通正文中常见的转义写法：

```tex
百分号：\%    下划线：\_    与号：\&    井号：\#
美元符号：\$  左花括号：\{  右花括号：\}
```

页码范围中的连接号建议写成 `1--10`。

## 参考文献交叉引用

模板内置轻量交叉引用，不需要 BibTeX 或 Biber。

### 第一步：在前文插入引用

在任意正文栏目中写 `\CiteRef{文献键}`：

```tex
\renewcommand{\BasisAndContent}{
已有研究讨论了这一问题\CiteRef{zhang2025}，
另一项研究采用了不同方法\CiteRef{smith2024}。
}
```

### 第二步：在参考文献栏定义条目

在 `\References` 中使用完全相同的键：

```tex
\renewcommand{\References}{
  \ReferenceItem{zhang2025}{张三, 李四. 文献题名[J]. 期刊名称, 2025, 10(2): 1--10.}
  \ReferenceItem{smith2024}{Smith J. Book Title[M]. Beijing: Publisher, 2024.}
}
```

### 第三步：编译并检查编号

前文和文末会自动对应为 `[1]`、`[2]`。编号顺序由 `\References` 中条目的排列顺序决定；同一篇文献可以重复引用。若首次显示 `[??]`，再次点击 `Recompile`。

文献键必须唯一，正文和文末拼写必须完全一致。建议只使用英文字母、数字、短横线和冒号。

## 常见问题

### 出现字体或 `\setmainfont` 错误

请先确认编译器选择是否与需求一致。默认 `pdfLaTeX` 不调用 `\setmainfont`；要使用 ZIP 内的真实宋体、黑体和 Times New Roman 时才切换 XeLaTeX。模板不会调用 `ctexart`，因此不会依赖 CTeX 的 Fandol fontset 模式。

### 长内容仍然跑出右边界

最常见原因是直接输入了很长的网址。请把网址改写成 `\url{完整网址}`。普通英文单词和中文正文会自动换行。

## 文件说明

- `main.tex`：动态表格、分页、字体和参考文献编号逻辑。
- `fields.tex`：日常填写内容，通常只编辑此文件。
- `fonts/`：宋体、黑体、Times New Roman 字体及 XeLaTeX 使用说明。
- `images/README.md`：插图文件夹和插图命令说明。
- `latexmkrc`：Overleaf 默认 pdfLaTeX 编译设置。

原始 Word 附件未被修改。由于模板现在需要动态增长，固定两页的 PDF 底图不再参与排版；标题、表格、签字区和栏目文字已经按原测量尺寸在 LaTeX 中重新绘制。
