# ggplot2

绘图过程：
- 数据 data
- 转换 transformation
- 度量 scale
- 坐标系 coordinate
- 主题 theme
- 元素 element
- 指引 guide
- 显示 display

`ggplot()`
- `data=usedata`
	- 指定绘图所使用的数据集
- `mapping=aes()`
	- 指定绘图所使用的一些图形要素：x轴和y轴所使用的变量

`theme_***()`
- `theme_bw`
- `theme_gray`
- `theme_minimal`
- `theme_classic`
- 控制主题显示细节的参数：
	- `base_size`
	- `base_family`
	- `base_line_size`
	- `base_rect_size`

`geom_***()`：绘制图形元素
- `geom_abline()`
- `geom_area()`
- `geom_bar()`
- `geom_bar2()`
- `geom_bin2d()`
- `geom_boxplot()`
- `geom_contour()`
- `geom_density()`
- `geom_density_2d()`
- `geom_errorbar()`
- `geom_errorbarh()`
- `geom_hex()`
- `geom_histogram()`
- `geom_jitter()`
- `geom_point()`
- `geom_polygon()`
- `geom_qq()`
- `geom_rect()`
- `geom_smooth()`
- `geom_step()`
- `geom_text()`
- `geom_tile()`
- `geom_violin()`

`labs()`：设置图形的标签
- `x`
- `y`
- `title`

`theme()`
- `axis.title.x`
- `axis.title.y`
- `axis.text.x`
- `axis.text.y`
- `axis.ticks.x`
- `axis.ticks.y`
- `legend.background`
- `legend.key.size`
- `legend.position`
	- `none, left, right, bottom, top`
- `legend.text`
- `legend.title`
- `line`
- `panel.border`
- `panel.grid`
- `plot.background`
- `plot.subtitle`
- `plot.title`
- `rect`
- `text`
- `title`

`element_text()`：调整文本
- `angle`
- `colour, color`
- `family`
- `size`
- `hjust`
- `vjust`

