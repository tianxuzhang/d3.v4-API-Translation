# d3.v4-API-Translation
D3.js最新版4.xのAPI中文翻译

# 好吧，说说我要做啥？
今天打开D3的项目地址https://github.com/d3/d3 ，发现描述已经变成了：
>Bring data to life with SVG, Canvas and HTML

比以前多个了`Canvas`，也就是说D3.js的历史进入了新纪元。这是历经早期`Protovis`只支持`SVG`到后来d3.v3支持`HTML`操作，如今又进入了一个崭新的阶段将支持`Canvas`了。d3.v4的源码也有相当大的调整，最明显的是分成了很多小模块单独开发。模块化开发果然和预想的一样是要为支持`Canvas`做准备，这确实是一件让人热血澎湃的好事。D3留给我们的想象空间还很大。好吧，为了更好地拥抱新技术！本项目将通过对D3 V4官方文档的翻译对d3.v4做个全面深入的了解。本文为保持原汁原味，会采用直译，希望成为帮助大家入门d3.v4的第一手资料。

# 翻译有感

* 2016-5-20日下午五点左右，D3的star数超过50000次，位列所有前端库第二（仅次于boostrap）。自从2013年关注D3以来，几乎都超过每个月1000的增幅上涨着。虽然距离排名第一的前端库boostrap有些差距，但D3的这种发展速度和受欢迎程度相信会继续给我带来更多的惊喜。

* 翻译D3 V4的API发现与D3 V3的差别很大，功能也更多更完善，就力导向图就从原来的12个功能函数增加到现在的42个（包含二级函数），这势必会给我们做数据可视化带来更多的便利。

-----------

下面是译文，欢迎一起翻译，探讨~

-----------

# D3: 数据驱动文档（Data-Driven Documents）

<a href="https://d3js.org"><img src="https://d3js.org/logo.svg" align="left" hspace="10" vspace="6"></a>

**D3** (或**D3.js**) 是一个用来使用Web标准做数据可视化的JavaScript库。D3帮助我们使用SVG, Canvas 和 HTML技术让数据生动有趣。D3将强大的**可视化**，**动态交互**和**数据驱动的DOM操作方法**完美结合，让我们可以充分发挥现代浏览器的功能，自由的设计正确的可视化界面。


更多参考? [见wiki。](https://github.com/d3/d3/wiki)


案例[见gallery](https://github.com/d3/d3/wiki/Gallery) 和 [作者mbostock的博客bl.ocks](http://bl.ocks.org/mbostock).


## 安装

现在主分支已经包含了D3 4.0预览版。4.0的API不是固定的并且发布前可能会改变。最近的稳定版 (3.5.17), 可以按照wiki里的 [安装介绍 ](https://github.com/d3/d3/wiki#installing) 安装使用。如果你使用NPM, 可执行`npm install d3@next`命令。不然的话可以下载[最新版](https://npmcdn.com/d3@next/build/)。 发布包支持AMD, CommonJS, 和 vanilla 环境。自定义编译可以使用 [Rollup](https://github.com/rollup/rollup) 或者其他打包工具。也可以直接从[d3js.org](https://d3js.org)引用:

```html
<script src="https://d3js.org/d3.v4.0.0-alpha.40.min.js"></script>
```

非压缩版移除上面的`.min`即可。

## API 总览

选择元素
* [选择](#selections) ([选择](#selecting-elements), [修改](#modifying-elements), [数据](#joining-data), [事件](#handling-events), [控制](#control-flow), [命名空间](#namespaces))

数据类型
* [数组](#arrays) ([统计](#statistics), [直方图](#histograms), [查找](#search), [转换](#transformations))
* [集合](#collections) ([对象](#objects), [映射（map）](#maps), [集合（set）](#sets), [嵌套](#nests))
* [颜色](#colors)
* [DSV（分隔符分割的值）](#delimiter-separated-values)
* [随机值](#random-numbers)
* [时间序列](#time-intervals)

格式化
* [数字格式化](#number-formats)
* [时间格式化](#time-formats)

加载数据
* [队列](#queues)
* [请求](#requests)

数据映射
* [比例尺](#scales) ([连续型](#continuous-scales), [颜色序数型](#sequential-color-scales), [数值型](#quantize-scales), [序数型](#ordinal-scales), [分类颜色型](#categorical-color-scales))

图形几何
* [形状](#shapes) ([弧](#arcs), [饼](#pies), [线](#lines), [面积](#areas), [曲线](#curves), [符号](#symbols), [堆叠](#stacks))
* [轴](#axes)
* [泰森多边形](#voronoi-diagrams)
* [路径](#paths)
* [多边形](#polygons)
* [四叉树](#quadtrees)

布局
* [力布局](#forces)
* [层次布局](#hierarchies)

动态交互
* [定时器](#timers)
* [过渡](#transitions)
* [插值器](#interpolators)
* [缓动](#easings)
* [事件分派](#dispatches)
* [拖动](#dragging)

D3 使用 [语义命名](http://semver.org/)。可使用d3.version获取当前版本号。

## [数组](https://github.com/d3/d3-array)

数组操作，排序，查找，汇总等。

#### [统计](https://github.com/d3/d3-array#statistics)

计算基本汇总统计的一些方法。

* [d3.min](https://github.com/d3/d3-array#min) - 计算数组中的最小值。
* [d3.max](https://github.com/d3/d3-array#max) - 计算数组中的最大值。
* [d3.extent](https://github.com/d3/d3-array#extent) - 计算数组的范围。
* [d3.sum](https://github.com/d3/d3-array#sum) - 数组中所有元素求和。
* [d3.mean](https://github.com/d3/d3-array#mean) - 计算数组的算术平均值。
* [d3.median](https://github.com/d3/d3-array#median) - 计算数组的中位数。
* [d3.quantile](https://github.com/d3/d3-array#quantile) - 计算一个数字数组排序后的分位数。
* [d3.variance](https://github.com/d3/d3-array#variance) - 数组中数字的方差。
* [d3.deviation](https://github.com/d3/d3-array#deviation) - 数组中数字的标准差。

#### [直方图](https://github.com/d3/d3-array#histograms)

将离散样本分成连续的无重叠的间隔。

* [d3.histogram](https://github.com/d3/d3-array#histogram) - 创建一个新的直方图生成器。
* [*histogram*](https://github.com/d3/d3-array#_histogram) - 对给定的样本数组计算直方图。
* [*histogram*.value](https://github.com/d3/d3-array#histogram_value) - 为每个样本指定一个值访问器。
* [*histogram*.domain](https://github.com/d3/d3-array#histogram_domain) - 指定可观测值的间隔。
* [*histogram*.thresholds](https://github.com/d3/d3-array#histogram_thresholds) - 指定值划分成不同箱的方法。
* [d3.thresholdFreedmanDiaconis](https://github.com/d3/d3-array#thresholdFreedmanDiaconis) - Freedman–Diaconis装箱规则。
* [d3.thresholdScott](https://github.com/d3/d3-array#thresholdScott) - Scott’s normal reference装箱规则。
* [d3.thresholdSturges](https://github.com/d3/d3-array#thresholdSturges) - Sturges’装箱准则。

#### [查找](https://github.com/d3/d3-array#search)

检索数组中特定的值。

* [d3.scan](https://github.com/d3/d3-array#scan) - 使用比较器线查找。
* [d3.bisect](https://github.com/d3/d3-array#bisect) - 二分查找排序数组中的值。
* [d3.bisectRight](https://github.com/d3/d3-array#bisectRight) - 二分查找排序数组中的值。
* [d3.bisectLeft](https://github.com/d3/d3-array#bisectLeft) - 二分查找排序数组中的值。
* [d3.bisector](https://github.com/d3/d3-array#bisector) - 使用访问器和比较器二分查找。
* [*bisector*.left](https://github.com/d3/d3-array#bisector_left) - 使用给定的比较器的bisectLeft。
* [*bisector*.right](https://github.com/d3/d3-array#bisector_right) - 使用给定的比较器的bisectRight。
* [d3.ascending](https://github.com/d3/d3-array#ascending) - 升序排序。
* [d3.descending](https://github.com/d3/d3-array#descending) - 降序排序。

#### [转换](https://github.com/d3/d3-array#transformations)

转换数组并返回一个新的数组。

* [d3.merge](https://github.com/d3/d3-array#merge) - 将多个数组合并成一个。
* [d3.pairs](https://github.com/d3/d3-array#pairs) - 创建一个相邻对数组。
* [d3.permute](https://github.com/d3/d3-array#permute) - 安装指定的索引数组重排数组。
* [d3.shuffle](https://github.com/d3/d3-array#shuffle) - 数组随机排序。
* [d3.ticks](https://github.com/d3/d3-array#ticks) - 从一个数组间隔生成有代表的值。
* [d3.tickStep](https://github.com/d3/d3-array#tickStep) - 从一个数组间隔生成有代表的值。
* [d3.range](https://github.com/d3/d3-array#range) - 生成一组数值。
* [d3.transpose](https://github.com/d3/d3-array#transpose) - 数组转置。
* [d3.zip](https://github.com/d3/d3-array#zip) - 转置多个数组。

## [轴](https://github.com/d3/d3-axis)

人类可读的刻度轴。

* [d3.axisTop](https://github.com/d3/d3-axis#axisTop) - 创建一个上部轴生成器。
* [d3.axisRight](https://github.com/d3/d3-axis#axisTight) - 创建一个右部轴生成器。
* [d3.axisBottom](https://github.com/d3/d3-axis#axisTottom) - 创建一个底部轴生成器。
* [d3.axisLeft](https://github.com/d3/d3-axis#axisTeft) - 创建一个左部轴生成器。
* [*axis*](https://github.com/d3/d3-axis#_axis) - 为给定的选择生成轴。
* [*axis*.scale](https://github.com/d3/d3-axis#axis_scale) - 设置比例尺。
* [*axis*.ticks](https://github.com/d3/d3-axis#axis_ticks) - 自定义刻度的生成和格式化方式。
* [*axis*.tickArguments](https://github.com/d3/d3-axis#axis_tickArguments) - 自定义刻度的生成和格式化方式。
* [*axis*.tickValues](https://github.com/d3/d3-axis#axis_tickValues) - 明确地指定刻度值。
* [*axis*.tickFormat](https://github.com/d3/d3-axis#axis_tickFormat) - 明确地指定刻度格式。
* [*axis*.tickSize](https://github.com/d3/d3-axis#axis_tickSize) - 设置刻度的大小。
* [*axis*.tickSizeInner](https://github.com/d3/d3-axis#axis_tickSizeInner) - 设置内刻度的大小。
* [*axis*.tickSizeOuter](https://github.com/d3/d3-axis#axis_tickSizeOuter) - 设置外刻度的大小。
* [*axis*.tickPadding](https://github.com/d3/d3-axis#axis_tickPadding) - 设置刻度和标签之间的间距。

## [集合](https://github.com/d3/d3-collection)

便捷的数据结构，元素的键是字符串类型。

#### [对象](https://github.com/d3/d3-collection#objects)

将对象转为数组的方法。

* [d3.keys](https://github.com/d3/d3-collection#keys) - 列举关联数组的键。
* [d3.values](https://github.com/d3/d3-collection#values) - 列举关联数组的值。
* [d3.entries](https://github.com/d3/d3-collection#entries) - 列举关联数组的键值对实体。

#### [映射](https://github.com/d3/d3-collection#maps)

类似ES6 Map，但是键时字符类型的，并且有点其他区别。

* [d3.map](https://github.com/d3/d3-collection#map) - 创建一个空的map。
* [*map*.has](https://github.com/d3/d3-collection#map_has) - 返回map中是否包含某个值。
* [*map*.get](https://github.com/d3/d3-collection#map_get) - 获取值。
* [*map*.set](https://github.com/d3/d3-collection#map_set) - 设置值。
* [*map*.remove](https://github.com/d3/d3-collection#map_remove) - 移除值。
* [*map*.clear](https://github.com/d3/d3-collection#map_clear) - 移除所有值。
* [*map*.keys](https://github.com/d3/d3-collection#map_keys) - 获取键数组。
* [*map*.values](https://github.com/d3/d3-collection#map_values) - 获取值数组。
* [*map*.entries](https://github.com/d3/d3-collection#map_entries) - 获取键值对数组。
* [*map*.each](https://github.com/d3/d3-collection#map_each) - 为每个元素调用一次指定的方法。
* [*map*.empty](https://github.com/d3/d3-collection#map_empty) - 返回map是否为空。
* [*map*.size](https://github.com/d3/d3-collection#map_size) - 计算值的数量。

#### [集合](https://github.com/d3/d3-collection#sets)

类似ES6 Set，但是键时字符类型的，并且有点其他区别。

* [d3.set](https://github.com/d3/d3-collection#set) - 创建一个空的set。
* [*set*.has](https://github.com/d3/d3-collection#set_has) - 返回set中是否包含某个值。
* [*set*.add](https://github.com/d3/d3-collection#set_add) - 添加指定值。
* [*set*.remove](https://github.com/d3/d3-collection#set_remove) - 删除指定值。
* [*set*.clear](https://github.com/d3/d3-collection#set_clear) - 移除所有值。
* [*set*.values](https://github.com/d3/d3-collection#set_values) - 获取值数组。
* [*set*.each](https://github.com/d3/d3-collection#set_each) - 为每个元素调用一次指定的方法。
* [*set*.empty](https://github.com/d3/d3-collection#set_empty) - 返回set是否为空。
* [*set*.size](https://github.com/d3/d3-collection#set_size) - 计算值的数量。

#### [嵌套](https://github.com/d3/d3-collection#nests)

将数据组织成任意层次。

* [d3.nest](https://github.com/d3/d3-collection#nest) - 创建一个嵌套生成器。
* [*nest*.key](https://github.com/d3/d3-collection#nest_key) - 在嵌套层级中加一级。
* [*nest*.sortKeys](https://github.com/d3/d3-collection#nest_sortKeys) - 当前层级按键排序。
* [*nest*.sortValues](https://github.com/d3/d3-collection#nest_sortValues) - 叶子层级按值排序。
* [*nest*.rollup](https://github.com/d3/d3-collection#nest_rollup) -为叶子层指定汇总函数。
* [*nest*.map](https://github.com/d3/d3-collection#nest_map) - 生成一个嵌套，返回一个map。
* [*nest*.object](https://github.com/d3/d3-collection#nest_object) - 生成一个嵌套，返回一个关联数组。
* [*nest*.entries](https://github.com/d3/d3-collection#nest_entries) - 生成一个嵌套，返回一个键值对数组。

## [颜色](https://github.com/d3/d3-color)

颜色操作和颜空间转换。

* [d3.color](https://github.com/d3/d3-color#color) - 解析给定的CSS颜色名。
* [*color*.rgb](https://github.com/d3/d3-color#color_rgb) - 计算该颜色的RGB值。
* [*color*.brighter](https://github.com/d3/d3-color#color_brighter) - 该颜色的高亮副本。
* [*color*.darker](https://github.com/d3/d3-color#color_darker) - 该颜色的较亮副本。
* [*color*.displayable](https://github.com/d3/d3-color#color_displayable) - 如果该颜色在标准硬件上可以显示则返回true。
* [*color*.toString](https://github.com/d3/d3-color#color_toString) - 将该颜色格式化为一个十六进制
RGB值字符串。
* [d3.rgb](https://github.com/d3/d3-color#rgb) - 创建一个RGB颜色。
* [d3.hsl](https://github.com/d3/d3-color#hsl) - 创建一个HSL颜色。
* [d3.lab](https://github.com/d3/d3-color#lab) - 创建一个Lab颜色。
* [d3.hcl](https://github.com/d3/d3-color#hcl) - 创建一个HCL颜色。
* [d3.cubehelix](https://github.com/d3/d3-color#cubehelix) - 创建一个Cubehelix颜色。

## [分隔符分隔的值](https://github.com/d3/d3-dsv)

解析和格式分隔符分隔的值（特别是TSV和CSV）

* [d3.dsvFormat](https://github.com/d3/d3-dsv#dsvFormat) - 为指定的分隔符指定一个解析器和格式化器。
* [*dsv*.parse](https://github.com/d3/d3-dsv#dsv_parse) - 解析给定的字符串返回一组对象。
* [*dsv*.parseRows](https://github.com/d3/d3-dsv#dsv_parseRows) - 解析给定的字符串返回行数组。
* [*dsv*.format](https://github.com/d3/d3-dsv#dsv_format) - 格式化一组对象。
* [*dsv*.formatRows](https://github.com/d3/d3-dsv#dsv_formatRows) - 格式化行数组。
* [d3.csvParse](https://github.com/d3/d3-dsv#csvParse) - 解析给定的CSV字符串，返回一组对象。
* [d3.csvParseRows](https://github.com/d3/d3-dsv#csvParseRows) - 解析给定的CSV字符串，返回行数组。
* [d3.csvFormat](https://github.com/d3/d3-dsv#csvFormat) - 格式化给定的CSV对象。
* [d3.csvFormatRows](https://github.com/d3/d3-dsv#csvFormatRows) - 格式化给定的CSV行数组。
* [d3.tsvParse](https://github.com/d3/d3-dsv#tsvParse) -解析给定的TSV字符串，返回一组对象。
* [d3.tsvParseRows](https://github.com/d3/d3-dsv#tsvParseRows) - 解析给定的TSV字符串，返回行数组。
* [d3.tsvFormat](https://github.com/d3/d3-dsv#tsvFormat) - 格式化给定的TSV对象。
* [d3.tsvFormatRows](https://github.com/d3/d3-dsv#tsvFormatRows) - 格式化给定的TSV行数组。

## [事件分发](https://github.com/d3/d3-dispatch)

命名回调函数。

* [d3.dispatch](https://github.com/d3/d3-dispatch#dispatch) - 创建一个定制的事件分发器。
* [*dispatch*.on](https://github.com/d3/d3-dispatch#dispatch_on) - 注册或者解除注册事件监听器。
* [*dispatch*.copy](https://github.com/d3/d3-dispatch#dispatch_copy) - 创建分发器副本。
* [*dispatch*.*call*](https://github.com/d3/d3-dispatch#dispatch_call) - 给注册的监听器分发事件。
* [*dispatch*.*apply*](https://github.com/d3/d3-dispatch#dispatch_apply) - 给注册的监听器分发事件。

## [拖曳](https://github.com/d3/d3-drag)

使用鼠标或触屏拖曳SVG，HTML 或 Canvas。

* [d3.drag](https://github.com/d3/d3-drag#drag) - 创建一个拖曳行为。
* [*drag*](https://github.com/d3/d3-drag#_drag) - 对一个选择应用拖曳行为。
* [*drag*.container](https://github.com/d3/d3-drag#drag_container) - 设置坐标系统。
* [*drag*.filter](https://github.com/d3/d3-drag#drag_filter) - 忽略一些初始的事件。
* [*drag*.subject](https://github.com/d3/d3-drag#drag_subject) - 设置被拖曳对象。
* [*drag*.x](https://github.com/d3/d3-drag#drag_x) - 设置被拖曳对象的*x*-坐标。
* [*drag*.y](https://github.com/d3/d3-drag#drag_y) - 设置被拖曳对象的*y*-坐标。
* [*drag*.on](https://github.com/d3/d3-drag#drag_on) - 监听拖曳事件。
* [*event*.on](https://github.com/d3/d3-drag#event_on) - 监听当前动作的拖曳事件。

## [缓动](https://github.com/d3/d3-ease)

用来平滑过渡的缓动函数。

* [*ease*](https://github.com/d3/d3-ease#_ease) - 缓动给定的标准化时间。
* [d3.easeLinear](https://github.com/d3/d3-ease#easeLinear) - 线性缓动，就是个恒等函数。
* [d3.easePolyIn](https://github.com/d3/d3-ease#easePolyIn) - 多项式缓动，加速到指定的速率。
* [d3.easePolyOut](https://github.com/d3/d3-ease#easePolyOut) - 逆多项式缓动。
* [d3.easePolyInOut](https://github.com/d3/d3-ease#easePolyInOut) - 均匀多项式缓动。
* [*poly*.exponent](https://github.com/d3/d3-ease#poly_exponent) - 指定多项式的指数。
* [d3.easeQuad](https://github.com/d3/d3-ease#easeQuad) - easeQuadInOut的别名。
* [d3.easeQuadIn](https://github.com/d3/d3-ease#easeQuadIn) - 平方缓动。
* [d3.easeQuadOut](https://github.com/d3/d3-ease#easeQuadOut) - 逆平方缓动。
* [d3.easeQuadInOut](https://github.com/d3/d3-ease#easeQuadInOut) - 均匀平方缓动。
* [d3.easeCubic](https://github.com/d3/d3-ease#easeCubic) - easeCubicInOut的别名。
* [d3.easeCubicIn](https://github.com/d3/d3-ease#easeCubicIn) - 立方缓动。
* [d3.easeCubicOut](https://github.com/d3/d3-ease#easeCubicOut) - 逆立方缓动。
* [d3.easeCubicInOut](https://github.com/d3/d3-ease#easeCubicInOut) - 均匀立方缓动。
* [d3.easeSin](https://github.com/d3/d3-ease#easeSin) - easeSinInOut的别名。
* [d3.easeSinIn](https://github.com/d3/d3-ease#easeSinIn) - 正弦缓动。
* [d3.easeSinOut](https://github.com/d3/d3-ease#easeSinOut) - 逆正弦缓动。
* [d3.easeSinInOut](https://github.com/d3/d3-ease#easeSinInOut) - 均匀正弦缓动。
* [d3.easeExp](https://github.com/d3/d3-ease#easeExp) - easeExpInOut的别名。
* [d3.easeExpIn](https://github.com/d3/d3-ease#easeExpIn) - 指数缓动。
* [d3.easeExpOut](https://github.com/d3/d3-ease#easeExpOut) - 逆指数缓动。
* [d3.easeExpInOut](https://github.com/d3/d3-ease#easeExpInOut) - 均匀指数缓动。
* [d3.easeCircle](https://github.com/d3/d3-ease#easeCircle) - easeCircleInOut的别名。
* [d3.easeCircleIn](https://github.com/d3/d3-ease#easeCircleIn) - 圆形缓动。
* [d3.easeCircleOut](https://github.com/d3/d3-ease#easeCircleOut) - 逆圆形缓动。
* [d3.easeCircleInOut](https://github.com/d3/d3-ease#easeCircleInOut) - 均匀圆形缓动。
* [d3.easeElastic](https://github.com/d3/d3-ease#easeElastic) - easeElasticOut的别名。
* [d3.easeElasticIn](https://github.com/d3/d3-ease#easeElasticIn) - 弹性缓动，类似松紧带。
* [d3.easeElasticOut](https://github.com/d3/d3-ease#easeElasticOut) - 逆弹性缓动。
* [d3.easeElasticInOut](https://github.com/d3/d3-ease#easeElasticInOut) - 均匀弹性缓动。
* [*elastic*.amplitude](https://github.com/d3/d3-ease#elastic_amplitude) - 指定弹性振幅。
* [*elastic*.period](https://github.com/d3/d3-ease#elastic_period) - 指定弹性周期。
* [d3.easeBack](https://github.com/d3/d3-ease#easeBack) - easeBackInOut的别名。
* [d3.easeBackIn](https://github.com/d3/d3-ease#easeBackIn) - 提早缓动。
* [d3.easeBackOut](https://github.com/d3/d3-ease#easeBackOut) - 逆提早缓动。
* [d3.easeBackInOut](https://github.com/d3/d3-ease#easeBackInOut) - 均匀提早缓动。
* [*back*.overshoot](https://github.com/d3/d3-ease#back_overshoot) - 指定超调量。
* [d3.easeBounce](https://github.com/d3/d3-ease#easeBounce) - easeBounceOut的别名。
* [d3.easeBounceIn](https://github.com/d3/d3-ease#easeBounceIn) - 弹跳缓动，类似弹跳的小球。
* [d3.easeBounceOut](https://github.com/d3/d3-ease#easeBounceOut) - 逆弹跳缓动。
* [d3.easeBounceInOut](https://github.com/d3/d3-ease#easeBounceInOut) - 均匀弹跳缓动。

## [力导向图](https://github.com/d3/d3-force)

力导向图使用velocity Verlet整合算法实现。

* [d3.forceSimulation](https://github.com/d3/d3-force#forceSimulation) - 创建一个力模拟。
* [*simulation*.restart](https://github.com/d3/d3-force#simulation_restart) - 重启力模拟。
* [*simulation*.stop](https://github.com/d3/d3-force#simulation_stop) - 停止力模拟。
* [*simulation*.tick](https://github.com/d3/d3-force#simulation_tick) - 将力模拟向前推进一步。
* [*simulation*.nodes](https://github.com/d3/d3-force#simulation_nodes) - 设置力模拟的节点。
* [*simulation*.alpha](https://github.com/d3/d3-force#simulation_alpha) - 设置当前的`α`值。
* [*simulation*.alphaMin](https://github.com/d3/d3-force#simulation_alphaMin) -设置`α`最小阈值。
* [*simulation*.alphaDecay](https://github.com/d3/d3-force#simulation_alphaDecay) - 设置`α`指数衰减率。
* [*simulation*.alphaTarget](https://github.com/d3/d3-force#simulation_alphaTarget) - 设置目标`α`。
* [*simulation*.drag](https://github.com/d3/d3-force#simulation_drag) - 设置曳引系数。
* [*simulation*.force](https://github.com/d3/d3-force#simulation_force) - 添加或移除力。
* [*simulation*.fix](https://github.com/d3/d3-force#simulation_fix) - 固定节点位置。
* [*simulation*.unfix](https://github.com/d3/d3-force#simulation_unfix) - 释放固定的节点。
* [*simulation*.find](https://github.com/d3/d3-force#simulation_find) - 查找给定位置最近的节点。
* [*simulation*.on](https://github.com/d3/d3-force#simulation_on) - 添加或移除事件监听器。
* [*force*](https://github.com/d3/d3-force#_force) - 应用力模拟。
* [*force*.initialize](https://github.com/d3/d3-force#force_initialize) - 使用给定的节点初始化力布局。
* [d3.forceCenter](https://github.com/d3/d3-force#forceCenter) - 创建一个力中心。
* [*center*.x](https://github.com/d3/d3-force#center_x) - 设置中心的*x*-坐标。
* [*center*.y](https://github.com/d3/d3-force#center_y) - 设置中心的*y*-坐标。
* [d3.forceCollide](https://github.com/d3/d3-force#forceCollide) - 创建一个圆碰撞力。
* [*collide*.radius](https://github.com/d3/d3-force#collide_radius) - 设置圆的半径。
* [*collide*.strength](https://github.com/d3/d3-force#collide_strength) - 设置碰撞检测强度。
* [*collide*.iterations](https://github.com/d3/d3-force#collide_iterations) - 设置迭代次数。
* [d3.forceLink](https://github.com/d3/d3-force#forceLink) - 创建连接力。
* [*link*.links](https://github.com/d3/d3-force#link_links) - 设置连接数组。
* [*link*.id](https://github.com/d3/d3-force#link_id) - 连接数组。
* [*link*.distance](https://github.com/d3/d3-force#link_distance) - 设置连接距离。
* [*link*.strength](https://github.com/d3/d3-force#link_strength) - 设置连接强度。
* [*link*.iterations](https://github.com/d3/d3-force#link_iterations) - 设置迭代次数。
* [d3.forceManyBody](https://github.com/d3/d3-force#forceManyBody) - 创建多体力。
* [*manyBody*.strength](https://github.com/d3/d3-force#manyBody_strength) - 设置力强度。
* [*manyBody*.theta](https://github.com/d3/d3-force#manyBody_theta) - 设置Barnes-Hut近似精度。
* [*manyBody*.distanceMin](https://github.com/d3/d3-force#manyBody_distanceMin) - 当节点关闭限制力。
* [*manyBody*.distanceMax](https://github.com/d3/d3-force#manyBody_distanceMax) - 当节点太远限制力。
* [d3.forceX](https://github.com/d3/d3-force#forceX) - 创建*x*-定位力。
* [*x*.strength](https://github.com/d3/d3-force#x_strength) - 设置力强度。
* [*x*.x](https://github.com/d3/d3-force#x_x) - 设置目标*x*-坐标。
* [d3.forceY](https://github.com/d3/d3-force#forceY) - 创建*y*-定位力。
* [*y*.strength](https://github.com/d3/d3-force#y_strength) - 设置力强度。
* [*y*.y](https://github.com/d3/d3-force#y_y) - 设置目标*y*-坐标。

## [层次布局](https://github.com/d3/d3-hierarchy)

用来可视化层次型数据的布局算法。

* [d3.hierarchy](#hierarchy) - 从层次型的数据构造一个根节点。
* [*node*.ancestors](#node_ancestors) - 生成祖先数组。
* [*node*.descendants](#node_descendants) - 生成后代数组。
* [*node*.leaves](#node_leaves) - 生成层级数组。
* [*node*.path](#node_path) - 生成到达另一个节点的最短路径。
* [*node*.sum](#node_sum) - 求和。
* [*node*.sort](#node_sort) - 排序所有后代的兄弟节点。
* [*node*.each](#node_each) - 广度优先遍历。
* [*node*.eachAfter](#node_eachAfter) - 后序遍历。
* [*node*.eachBefore](#node_eachBefore) - 先序遍历。
* [*node*.copy](#node_copy) - 拷贝层次布局。
* [d3.stratify](#stratify) - 创建一个层操作符。
* [*stratify*](#_stratify) - 从表格式的数据构造一个根节点。
* [*stratify*.id](#stratify_id) - 设置节点ID访问器。
* [*stratify*.parentId](#stratify_parentId) - 设置父节点ID访问器。
* [d3.cluster](#cluster) - 创建一个新的簇（系统树图）布局。
* [*cluster*](#_cluster) - 将给定的层次数据排列到簇中。
* [*cluster*.size](#cluster_size) - 设置布局大小。
* [*cluster*.nodeSize](#cluster_nodeSize) - 设置节点大小。
* [*cluster*.separation](#cluster_separation) - 设置层间距。
* [d3.tree](#tree) - 创建新的整齐的树布局。
* [*tree*](#_tree) - 将给定的层次数据排列到树中。
* [*tree*.size](#tree_size) - 设置布局大小。
* [*tree*.nodeSize](#tree_nodeSize) - 设置节点大小。
* [*tree*.separation](#tree_separation) - 设置层间距。
* [d3.treemap](#treemap) - 创建一个新的矩形填充树布局（简称矩形树布局）。
* [*treemap*](#_treemap) - 使用矩形填充树布局排列给定的层次数据。
* [*treemap*.tile](#treemap_tile) - 设置铺砌方法。
* [*treemap*.size](#treemap_size) - 设置布局大小。
* [*treemap*.round](#treemap_round) - 设置输出坐标是否是取整的。
* [*treemap*.padding](#treemap_padding) - 设置间距。
* [*treemap*.paddingInner](#treemap_paddingInner) - 设置兄弟节点之间的间距。
* [*treemap*.paddingOuter](#treemap_paddingOuter) - 设置父子节点之间的间距。
* [*treemap*.paddingTop](#treemap_paddingTop) - 设置父节点顶边缘和子节点的间距。
* [*treemap*.paddingRight](#treemap_paddingRight) - 设置父节点右边缘和子节点的间距。
* [*treemap*.paddingBottom](#treemap_paddingBottom) - 设置父节点底边缘和子节点的间距。
* [*treemap*.paddingLeft](#treemap_paddingLeft) - 设置父节点左边缘和子节点的间距。
* [d3.treemapBinary](#treemapBinary) - 使用平衡二叉树铺砌。
* [d3.treemapDice](#treemapDice) - 水平行铺砌。
* [d3.treemapSlice](#treemapSlice) - 垂直列铺砌。
* [d3.treemapSliceDice](#treemapSliceDice) - 水平和垂直交替铺砌。
* [d3.treemapSquarify](#treemapSquarify) - 正方形铺砌。
* [*squarify*.ratio](#squarify_ratio) - 设置期望的矩形长宽比。
* [d3.partition](#partition) - 创建新的分区布局（旭日图和冰柱图）。
* [*partition*](#_partition) - 使用分区布局排列给定的层次数据。
* [*partition*.size](#partition_size) - 设置布局大小。
* [*partition*.round](#partition_round) - 设置输出坐标是否是取整的。
* [*partition*.padding](#partition_padding) - 设置间距。
* [d3.pack](#pack) - 创建一个新的圆形填充布局（简称包布局）。
* [*pack*](#_pack) - 使用包布局排列给定的层次数据。
* [*pack*.radius](#pack_radius) - 设置半径访问器。
* [*pack*.size](#pack_size) - 设置布局大小。
* [*pack*.padding](#pack_padding) - 设置间距。
* [d3.packSiblings](#packSiblings) - 包装指定的圆数组。
* [d3.packEnclose](#packEnclose) - 围住指定的圆数组。
