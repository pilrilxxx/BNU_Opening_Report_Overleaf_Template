# 图片放置说明

把正文图片上传到本目录。支持 PDF、PNG 和 JPG，建议文件名只使用英文字母、数字和短横线，不要包含空格。

在 `fields.tex` 的正文栏目中使用：

```tex
\ReportFigure{图片键}{文件名}{图题}
```

例如：

```tex
研究区如\FigureRef{study-area}所示。\par
\ReportFigure[0.70\linewidth]{study-area}{study-area.png}{研究区位置}
```

图片键只用于交叉引用，每张图必须唯一。可选参数 `0.70\linewidth` 用于调整宽度；不要超过 `\linewidth`。
