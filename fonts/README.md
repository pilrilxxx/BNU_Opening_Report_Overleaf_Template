# 项目字体文件

模板默认编译器仍是 `pdfLaTeX`。`pdfLaTeX` 不能直接读取 `.ttf` 或 `.ttc`，因此默认编译时使用 Overleaf 自带的宋体类 CJK 字体和 Times 兼容字体。

本 ZIP 已包含下列字体，供 XeLaTeX 精确排版时使用：

- `simsun.ttc`：中文正文宋体，使用字体集合中的第 0 个字体 SimSun；
- `simhei.ttf`：中文标题黑体；
- `times.ttf`：Times New Roman 常规体；
- `timesbd.ttf`：Times New Roman 粗体；
- `timesi.ttf`：Times New Roman 斜体；
- `timesbi.ttf`：Times New Roman 粗斜体。

需要精确字体时，在 Overleaf 的 `Settings -> Compiler` 中选择 `XeLaTeX`，然后重新编译。`main.tex` 会自动调用这些文件，不需要再编辑字体命令。

无论采用默认 pdfLaTeX 还是可选 XeLaTeX，正文均固定为五号 `10.5 pt`，标题固定为三号 `16 pt`，不会因为内容增多而缩小。
