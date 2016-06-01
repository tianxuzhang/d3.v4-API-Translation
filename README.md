# d3.v4-API-Translation
D3.js 4.0 API中文翻译

# 好吧，说说我要做啥？
今天打开D3的项目地址https://github.com/d3/d3 ，发现描述已经变成了：
>Bring data to life with SVG, Canvas and HTML

比以前多个了`Canvas`，也就是说D3.js的历史进入了新纪元。这是历经早期`Protovis`只支持`SVG`到后来d3.v3支持`HTML`操作，如今又进入了一个崭新的阶段将支持`Canvas`了。d3.v4的源码也有相当大的调整，最明显的是分成了很多小模块单独开发。模块化开发果然和预想的一样是要为支持`Canvas`做准备，这确实是一件让人热血澎湃的好事。D3留给我们的想象空间还很大。好吧，为了更好地拥抱新技术！本项目将通过对D3 V4官方文档的翻译对d3.v4做个全面深入的了解。本文为保持原汁原味，会采用直译，希望成为帮助大家入门d3.v4的第一手资料。

# 翻译有感

* 2016-5-20日下午五点左右，D3的star数超过50000次，位列所有前端库第二（仅次于boostrap）。自从2013年关注D3以来，几乎都超过每个月1000的增幅上涨着。虽然距离排名第一的前端库boostrap有些差距，但D3的这种发展速度和受欢迎程度相信会继续给我带来更多的惊喜。

* 翻译D3 V4的API发现与D3 V3的差别很大，功能也更多更完善，就力导向图就从原来的12个功能函数增加到现在的41个（包含二级函数），这势必会给我们做数据可视化带来更多的便利。

* 路径这部分的API主要用来将Canvas命令转换为SVG路径的d属性的值。本质上最后还是用SVG画图。这一点可能跟我们想要的直接用Canvas画大数据量数据的需求不一样，看来以后还是得手动来实现了，这一点略微还是有些失望的~

* D3 V4的大量API由原来的二级函数升级为一级函数（实际上就是把两级的单词合并，使用驼峰命名法重命名了），这样给使用者带来了一些记忆负担，其实以前的API设计得更好用点~

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

## [插值器](https://github.com/d3/d3-interpolate)

插补数字，字符串，颜色，数组，对象等。

* [d3.interpolate](https://github.com/d3/d3-interpolate#interpolate) - 插补任意值。
* [d3.interpolateArray](https://github.com/d3/d3-interpolate#interpolateArray) - 插补任意值的数组。
* [d3.interpolateNumber](https://github.com/d3/d3-interpolate#interpolateNumber) - 插补数组。
* [d3.interpolateObject](https://github.com/d3/d3-interpolate#interpolateObject) - 插补充任意对象
* [d3.interpolateRound](https://github.com/d3/d3-interpolate#interpolateRound) - 插补整数。
* [d3.interpolateString](https://github.com/d3/d3-interpolate#interpolateString) - 插补嵌入数字的字符串。
* [d3.interpolateTransformCss](https://github.com/d3/d3-interpolate#interpolateTransformCss) - 插补2D CSS变换。
* [d3.interpolateTransformSvg](https://github.com/d3/d3-interpolate#interpolateTransformSvg) - 插补2D SVG变换。
* [d3.interpolateZoom](https://github.com/d3/d3-interpolate#interpolateZoom) - 两个视图之间平移和缩放。
* [d3.interpolateRgb](https://github.com/d3/d3-interpolate#interpolateRgb) - 插补RGB颜色。
* [d3.interpolateHsl](https://github.com/d3/d3-interpolate#interpolateHsl) - 插补HSL颜色。
* [d3.interpolateHslLong](https://github.com/d3/d3-interpolate#interpolateHslLong) - 插补HSL颜色（长整型）。
* [d3.interpolateLab](https://github.com/d3/d3-interpolate#interpolateLab) - 插补Lab颜色。
* [d3.interpolateHcl](https://github.com/d3/d3-interpolate#interpolateHcl) - 插补HCL颜色。
* [d3.interpolateHclLong](https://github.com/d3/d3-interpolate#interpolateHclLong) - 插补HCL颜色（长整型）。
* [d3.interpolateCubehelix](https://github.com/d3/d3-interpolate#interpolateCubehelix) - 插补Cubehelix颜色。
* [d3.interpolateCubehelixLong](https://github.com/d3/d3-interpolate#interpolateCubehelixLong) - 插补Cubehelix颜色（长整型）。
* [*interpolate*.gamma](https://github.com/d3/d3-interpolate#interpolate_gamma) - 在插值过程中使用`γ`矫正。

## [数字格式化](https://github.com/d3/d3-format)

将数字格式化为人类可读的形式。

* [d3.format](https://github.com/d3/d3-format#format) - enUs.format的别名。
* [d3.formatPrefix](https://github.com/d3/d3-format#formatPrefix) - enUs.formatPrefix的别名。
* [d3.formatSpecifier](https://github.com/d3/d3-format#formatSpecifier) - 解析数字格式说明符。
* [d3.formatLocale](https://github.com/d3/d3-format#formatLocale) - 定义一个自定义的本地化。
* [*locale*.format](https://github.com/d3/d3-format#locale_format) - 创建一个数字格式。
* [*locale*.formatPrefix](https://github.com/d3/d3-format#locale_formatPrefix) - 创建一个SI-前缀数字格式化。
* [d3.formatCaEs](https://github.com/d3/d3-format#formatCaEs) - Catalan (西班牙) 本地化。
* [d3.formatCsCz](https://github.com/d3/d3-format#formatCsCz) - Czech (捷克) 本地化。
* [d3.formatDeCh](https://github.com/d3/d3-format#formatDeCh) - German (瑞士) 本地化。
* [d3.formatDeDe](https://github.com/d3/d3-format#formatDeDe) - German (德国) 本地化。
* [d3.formatEnCa](https://github.com/d3/d3-format#formatEnCa) - English (加拿大) 本地化。
* [d3.formatEnGb](https://github.com/d3/d3-format#formatEnGb) - English (英国) 本地化。
* [d3.formatEnUs](https://github.com/d3/d3-format#formatEnUs) - English (美国 ) 本地化。
* [d3.formatEsEs](https://github.com/d3/d3-format#formatEsEs) - Spanish (西班牙) 本地化。
* [d3.formatFiFi](https://github.com/d3/d3-format#formatFiFi) - Finnish (芬兰) 本地化。
* [d3.formatFrCa](https://github.com/d3/d3-format#formatFrCa) - French (加拿大) 本地化。
* [d3.formatFrFr](https://github.com/d3/d3-format#formatFrFr) - French (法国) 本地化。
* [d3.formatHeIl](https://github.com/d3/d3-format#formatHeIl) - Hebrew (以色列) 本地化。
* [d3.formatHuHu](https://github.com/d3/d3-format#formatHuHu) - Hungarian (匈牙利) 本地化。
* [d3.formatItIt](https://github.com/d3/d3-format#formatItIt) - Italian (意大利) 本地化。
* [d3.formatJaJp](https://github.com/d3/d3-format#formatJaJp) - Japanese (日本) 本地化。
* [d3.formatKoKr](https://github.com/d3/d3-format#formatKoKr) - Korean (韩国) 本地化。
* [d3.formatMkMk](https://github.com/d3/d3-format#formatMkMk) - Macedonian (马其顿) 本地化。
* [d3.formatNlNl](https://github.com/d3/d3-format#formatNlNl) - Dutch (荷兰) 本地化。
* [d3.formatPlPl](https://github.com/d3/d3-format#formatPlPl) - Polish (波兰) 本地化。
* [d3.formatPtBr](https://github.com/d3/d3-format#formatPtBr) - Portuguese (巴西) 本地化。
* [d3.formatRuRu](https://github.com/d3/d3-format#formatRuRu) - Russian (俄罗斯) 本地化。
* [d3.formatSvSe](https://github.com/d3/d3-format#formatSvSe) - Swedish (瑞典) 本地化。
* [d3.formatZhCn](https://github.com/d3/d3-format#formatZhCn) - Chinese (中国) 本地化。
* [d3.precisionFixed](https://github.com/d3/d3-format#precisionFixed) - 计算定点表示法的小数精度。
* [d3.precisionPrefix](https://github.com/d3/d3-format#precisionPrefix) - 计算SI-前缀记号法的小数精度。
* [d3.precisionRound](https://github.com/d3/d3-format#precisionRound) - 计算有效数字。

## [路径](https://github.com/d3/d3-path)

序列化Canvas路径命令为SVG。

* [d3.path](https://github.com/d3/d3-path#path) - 创建一个新的路径序列化。
* [*path*.moveTo](https://github.com/d3/d3-path#path_moveTo) - 移动到给定的点。
* [*path*.closePath](https://github.com/d3/d3-path#path_closePath) - 关闭当前的子路径。
* [*path*.lineTo](https://github.com/d3/d3-path#path_lineTo) - 画一条直线段。
* [*path*.quadraticCurveTo](https://github.com/d3/d3-path#path_quadraticCurveTo) - 画一条二次贝塞尔曲线段。
* [*path*.bezierCurveTo](https://github.com/d3/d3-path#path_bezierCurveTo) - 画一条三次贝塞尔曲线段。
* [*path*.arcTo](https://github.com/d3/d3-path#path_arcTo) - 画一条三次贝塞尔曲线弧。
* [*path*.arc](https://github.com/d3/d3-path#path_arc) - 画一条三次贝塞尔曲线弧。
* [*path*.rect](https://github.com/d3/d3-path#path_rect) - 画一个矩形。
* [*path*.toString](https://github.com/d3/d3-path#path_toString) - 序列化为SVG路径的data属性字符串。

## [多边形](https://github.com/d3/d3-polygon)

二维多边形的几何操作。

* [d3.polygonArea](https://github.com/d3/d3-polygon#polygonArea) - 计算给定多边形的面积。
* [d3.polygonCentroid](https://github.com/d3/d3-polygon#polygonCentroid) - 计算给定多边形的中心。
* [d3.polygonHull](https://github.com/d3/d3-polygon#polygonHull) - 计算给定点集的凸包。
* [d3.polygonContains](https://github.com/d3/d3-polygon#polygonContains) - 测试点是否在多边形内。
* [d3.polygonLength](https://github.com/d3/d3-polygon#polygonLength) - 计算给定多边形的周长的长度。

## [四叉树](https://github.com/d3/d3-quadtree)

二维递归空间细分。

* [d3.quadtree](https://github.com/d3/d3-quadtree#quadtree) - 创建一个新的空的四叉树。
* [*quadtree*.x](https://github.com/d3/d3-quadtree#quadtree_x) - 设置*x*访问器。
* [*quadtree*.y](https://github.com/d3/d3-quadtree#quadtree_y) - 设置*y*访问器。
* [*quadtree*.add](https://github.com/d3/d3-quadtree#quadtree_add) - 添加数据到四叉树中。
* [*quadtree*.remove](https://github.com/d3/d3-quadtree#quadtree_remove) - 删除四叉树中的数据。
* [*quadtree*.copy](https://github.com/d3/d3-quadtree#quadtree_copy) - 创建一个四叉树的副本。
* [*quadtree*.root](https://github.com/d3/d3-quadtree#quadtree_root) - 获取四叉树的根节点。
* [*quadtree*.data](https://github.com/d3/d3-quadtree#quadtree_data) - 从四叉树检索所有数据。
* [*quadtree*.size](https://github.com/d3/d3-quadtree#quadtree_size) - 计算在四叉树中数据的数量。
* [*quadtree*.find](https://github.com/d3/d3-quadtree#quadtree_find) - 在四叉树快速找到最接近的数据。
* [*quadtree*.visit](https://github.com/d3/d3-quadtree#quadtree_visit) - 选择性地访问四叉树中的节点。
* [*quadtree*.visitAfter](https://github.com/d3/d3-quadtree#quadtree_visitAfter) - 访问四叉树中的所有节点。
* [*quadtree*.cover](https://github.com/d3/d3-quadtree#quadtree_cover) - 扩充四叉树覆盖一个点。
* [*quadtree*.extent](https://github.com/d3/d3-quadtree#quadtree_extent) - 扩充四叉树覆盖一个范围。

## [队列](https://github.com/d3/d3-queue)

使用可配置的并发性评估异步任务。

* [d3.queue](https://github.com/d3/d3-queue#queue) - 管理异步任务的并发评估。
* [*queue*.defer](https://github.com/d3/d3-queue#queue_defer) - 注册一个用来评估的任务。
* [*queue*.abort](https://github.com/d3/d3-queue#queue_abort) - 中止任何活动任务,取消任何挂起任务。
* [*queue*.await](https://github.com/d3/d3-queue#queue_await) - 注册一个任务结束后的回调函数。
* [*queue*.awaitAll](https://github.com/d3/d3-queue#queue_awaitAll) - 注册一个所有任务结束后的回调函数。

## [随机数](https://github.com/d3/d3-random)

生成不同分布的随机数。

* [d3.randomUniform](https://github.com/d3/d3-random#randomUniform) - 均匀分布。
* [d3.randomNormal](https://github.com/d3/d3-random#randomNormal) - 正态分布。
* [d3.randomLogNormal](https://github.com/d3/d3-random#randomLogNormal) - 对数正态分布。
* [d3.randomBates](https://github.com/d3/d3-random#randomBates) - 贝茨分布。
* [d3.randomIrwinHall](https://github.com/d3/d3-random#randomIrwinHall) - Irwin-Hall分布。
* [d3.randomExponential](https://github.com/d3/d3-random#randomExponential) - 指数分布

## [请求](https://github.com/d3/d3-request)

XMLHttpRequest的简便封装。

* [d3.request](https://github.com/d3/d3-request#request) - 创建一个异步请求。
* [*request*.header](https://github.com/d3/d3-request#request_header) - 设置请求头。
* [*request*.user](https://github.com/d3/d3-request#request_user) - 设置用来认证身份的用户名。
* [*request*.password](https://github.com/d3/d3-request#request_password) - 设置用来认证身份的密码。
* [*request*.mimeType](https://github.com/d3/d3-request#request_mimeType) - 设置MIME类型。
* [*request*.timeout](https://github.com/d3/d3-request#request_timeout) - 设置超时时长（以秒为单位）。
* [*request*.responseType](https://github.com/d3/d3-request#request_responseType) - 设置响应类型。
* [*request*.response](https://github.com/d3/d3-request#request_response) - 设置响应函数。
* [*request*.get](https://github.com/d3/d3-request#request_get) - 发送GET请求。
* [*request*.post](https://github.com/d3/d3-request#request_post) - 发送POST请求。
* [*request*.send](https://github.com/d3/d3-request#request_send) - 设置请求。
* [*request*.abort](https://github.com/d3/d3-request#request_abort) - 中断请求。
* [*request*.on](https://github.com/d3/d3-request#request_on) - 监听请求事件。
* [d3.csv](https://github.com/d3/d3-request#csv) - 获取CSV文件。
* [d3.html](https://github.com/d3/d3-request#html) - 获取HTML文件。
* [d3.json](https://github.com/d3/d3-request#json) - 获取JSON文件。
* [d3.text](https://github.com/d3/d3-request#text) - 获取文本文件。
* [d3.tsv](https://github.com/d3/d3-request#tsv) - 获取TSV文件。
* [d3.xml](https://github.com/d3/d3-request#xml) - 获取XML文件。

## [比例尺](https://github.com/d3/d3-scale)

映射抽象数据为可视化表示所需要的形式。

### [连续型比例尺](https://github.com/d3/d3-scale#continuous-scales)

将连续的，数量的定义域映射为连续的值域上。

* [*continuous*](https://github.com/d3/d3-scale#_continuous) - 计算对应于给定的定义域的值域。
* [*continuous*.invert](https://github.com/d3/d3-scale#continuous_invert) - 计算对应于给定的值域的定义域。
* [*continuous*.domain](https://github.com/d3/d3-scale#continuous_domain) - 设置输入的定义域。
* [*continuous*.range](https://github.com/d3/d3-scale#continuous_range) - 设置输出的值域。
* [*continuous*.rangeRound](https://github.com/d3/d3-scale#continuous_rangeRound) - 设置取整后的值域
* [*continuous*.clamp](https://github.com/d3/d3-scale#continuous_clamp) - 启用闭合。
* [*continuous*.interpolate](https://github.com/d3/d3-scale#continuous_interpolate) - 设置输出插值器。
* [*continuous*.ticks](https://github.com/d3/d3-scale#continuous_ticks) - 计算定义域中有代表性的刻度值。
* [*continuous*.tickFormat](https://github.com/d3/d3-scale#continuous_tickFormat) - 格式化刻度值。
* [*continuous*.nice](https://github.com/d3/d3-scale#continuous_nice) - 优化定义域。
* [*continuous*.copy](https://github.com/d3/d3-scale#continuous_copy) - 创建比例尺的副本。
* [d3.scaleLinear](https://github.com/d3/d3-scale#scaleLinear) - 创建定量线性比例尺。
* [d3.scalePow](https://github.com/d3/d3-scale#scalePow) - 创建定量幂比例尺。
* [*pow*](https://github.com/d3/d3-scale#_pow) - 计算对应于给定的定义域的值域。
* [*pow*.invert](https://github.com/d3/d3-scale#pow_invert) - 计算对应于给定的值域的定义域。
* [*pow*.exponent](https://github.com/d3/d3-scale#pow_exponent) - 设置幂指数。
* [*pow*.domain](https://github.com/d3/d3-scale#pow_domain) - 设置输入的定义域。
* [*pow*.range](https://github.com/d3/d3-scale#pow_range) - 设置输出的值域。
* [*pow*.rangeRound](https://github.com/d3/d3-scale#pow_rangeRound) - 设置取整后的值域
* [*pow*.clamp](https://github.com/d3/d3-scale#pow_clamp) - 启用闭合。
* [*pow*.interpolate](https://github.com/d3/d3-scale#pow_interpolate) - 设置输出插值器。
* [*pow*.ticks](https://github.com/d3/d3-scale#pow_ticks) - 计算定义域中有代表性的刻度值。
* [*pow*.tickFormat](https://github.com/d3/d3-scale#pow_tickFormat) - 格式化刻度值。
* [*pow*.nice](https://github.com/d3/d3-scale#pow_nice) - 优化定义域。
* [*pow*.copy](https://github.com/d3/d3-scale#pow_copy) - 创建比例尺的副本。
* [d3.scaleSqrt](https://github.com/d3/d3-scale#scaleSqrt) - 创建一个幂比例尺，指数是0.5。
* [d3.scaleLog](https://github.com/d3/d3-scale#scaleLog) - 创建定量对数比例尺。
* [*log*](https://github.com/d3/d3-scale#_log) - 计算对应于给定的定义域的值域。
* [*log*.invert](https://github.com/d3/d3-scale#log_invert) - 计算对应于给定的值域的定义域。
* [*log*.base](https://github.com/d3/d3-scale#log_base) - 设置对数基底。
* [*log*.domain](https://github.com/d3/d3-scale#log_domain) - 设置输入的定义域。
* [*log*.range](https://github.com/d3/d3-scale#log_range) - 设置输出的值域。
* [*log*.rangeRound](https://github.com/d3/d3-scale#log_rangeRound) - 设置取整后的值域
* [*log*.clamp](https://github.com/d3/d3-scale#log_clamp) - 启用闭合。
* [*log*.interpolate](https://github.com/d3/d3-scale#log_interpolate) - 设置输出插值器。
* [*log*.ticks](https://github.com/d3/d3-scale#log_ticks) - 计算定义域中有代表性的刻度值。
* [*log*.tickFormat](https://github.com/d3/d3-scale#log_tickFormat) - 格式化刻度值。
* [*log*.nice](https://github.com/d3/d3-scale#log_nice) - 优化定义域。
* [*log*.copy](https://github.com/d3/d3-scale#log_copy) - 创建比例尺的副本。
* [d3.scaleIdentity](https://github.com/d3/d3-scale#identity) - 创建定量恒等比例尺。
* [d3.scaleTime](https://github.com/d3/d3-scale#scaleTime) - 创建时间线性比例尺。
* [*time*](https://github.com/d3/d3-scale#_time) - 计算对应于给定的定义域的值域。
* [*time*.invert](https://github.com/d3/d3-scale#time_invert) - 计算对应于给定的值域的定义域。
* [*time*.domain](https://github.com/d3/d3-scale#time_domain) - 设置输入的定义域。
* [*time*.range](https://github.com/d3/d3-scale#time_range) - 设置输出的值域。
* [*time*.rangeRound](https://github.com/d3/d3-scale#time_rangeRound) - 设置取整后的值域
* [*time*.clamp](https://github.com/d3/d3-scale#time_clamp) - 启用闭合。
* [*time*.interpolate](https://github.com/d3/d3-scale#time_interpolate) - 设置输出插值器。
* [*time*.ticks](https://github.com/d3/d3-scale#time_ticks) - 计算定义域中有代表性的刻度值。
* [*time*.tickFormat](https://github.com/d3/d3-scale#time_tickFormat) - 格式化刻度值。
* [*time*.nice](https://github.com/d3/d3-scale#time_nice) - 优化定义域。
* [*time*.copy](https://github.com/d3/d3-scale#time_copy) - 创建比例尺的副本。
* [d3.scaleUtc](https://github.com/d3/d3-scale#scaleUtc) - 创建UTC时间的线性比例尺。

### [连续颜色比例尺](https://github.com/d3/d3-scale#sequential-color-scales)

将连续的，数量的定义域映射为连续的，固定的颜色渐变。

* [d3.scaleViridis](https://github.com/d3/d3-scale#scaleViridis) - 暗到明的颜色组合。
* [d3.scaleInferno](https://github.com/d3/d3-scale#scaleInferno) - 暗到明的颜色组合。
* [d3.scaleMagma](https://github.com/d3/d3-scale#scaleMagma) - 暗到明的颜色组合。
* [d3.scalePlasma](https://github.com/d3/d3-scale#scalePlasma) - 暗到明的颜色组合。
* [d3.scaleWarm](https://github.com/d3/d3-scale#scaleWarm) - 色相环颜色组合。
* [d3.scaleCool](https://github.com/d3/d3-scale#scaleCool) - 色相环颜色组合。
* [d3.scaleRainbow](https://github.com/d3/d3-scale#scaleRainbow) - 循环的色相环颜色组合。
* [d3.scaleCubehelix](https://github.com/d3/d3-scale#scaleCubehelix) - 暗到明的色相环颜色组合。

-----------
上面这段翻译了但是比较模糊，以后提供点小例子解释下~
-----------

### [量化比例尺](https://github.com/d3/d3-scale#quantize-scales)

将连续的数量的定义域映射为离散的值域。

* [d3.scaleQuantize](https://github.com/d3/d3-scale#scaleQuantize) - 创建一个均匀的量化的线性比例尺。
* [*quantize*](https://github.com/d3/d3-scale#_quantize) - 计算对应于给定的定义域的值域。
* [*quantize*.invertExtent](https://github.com/d3/d3-scale#quantize_invertExtent) - 计算对应于给定的值域的定义域。
* [*quantize*.domain](https://github.com/d3/d3-scale#quantize_domain) - 设置输入的定义域。
* [*quantize*.range](https://github.com/d3/d3-scale#quantize_range) - 设置输出的值域。
* [*quantize*.nice](https://github.com/d3/d3-scale#quantize_nice) - 优化定义域。
* [*quantize*.ticks](https://github.com/d3/d3-scale#quantize_ticks) - 计算定义域中有代表性的刻度值。
* [*quantize*.tickFormat](https://github.com/d3/d3-scale#quantize_tickFormat) - 格式化刻度值。
* [*quantize*.copy](https://github.com/d3/d3-scale#quantize_copy) - 创建比例尺的副本。
* [d3.scaleQuantile](https://github.com/d3/d3-scale#scaleQuantile) - 创建一个分位数的量化的线性比例尺。
* [*quantile*](https://github.com/d3/d3-scale#_quantile) - 计算对应于给定的定义域的值域。
* [*quantile*.invertExtent](https://github.com/d3/d3-scale#quantile_invertExtent) - 计算对应于给定的值域的定义域。
* [*quantile*.domain](https://github.com/d3/d3-scale#quantile_domain) - 设置输入的定义域。
* [*quantile*.range](https://github.com/d3/d3-scale#quantile_range) - 设置输出的值域。
* [*quantile*.quantiles](https://github.com/d3/d3-scale#quantile_quantiles) - 设置分位数的阈值。
* [*quantile*.copy](https://github.com/d3/d3-scale#quantile_copy) - 创建比例尺的副本。
* [d3.scaleThreshold](https://github.com/d3/d3-scale#scaleThreshold) - 创建一个任意的量化的线性比例尺。
* [*threshold*](https://github.com/d3/d3-scale#_threshold) - 计算对应于给定的定义域的值域。
* [*threshold*.invertExtent](https://github.com/d3/d3-scale#threshold_invertExtent) - 计算对应于给定的值域的定义域。
* [*threshold*.domain](https://github.com/d3/d3-scale#threshold_domain) - 设置输入的定义域。
* [*threshold*.range](https://github.com/d3/d3-scale#threshold_range) - 设置输出的值域。
* [*threshold*.copy](https://github.com/d3/d3-scale#threshold_copy) - 创建比例尺的副本。

### [序数比例尺](https://github.com/d3/d3-scale#ordinal-scales)

定义域和值域都是离散的。

* [d3.scaleOrdinal](https://github.com/d3/d3-scale#scaleOrdinal) - 创建一个序数比例尺。
* [*ordinal*](https://github.com/d3/d3-scale#_ordinal) - 计算对应于给定的定义域的值域。
* [*ordinal*.domain](https://github.com/d3/d3-scale#ordinal_domain) - 设置输入的定义域。
* [*ordinal*.range](https://github.com/d3/d3-scale#ordinal_range) - 设置输出的值域。
* [*ordinal*.unknown](https://github.com/d3/d3-scale#ordinal_unknown) - 设置未知输入域的输出值。
* [*ordinal*.copy](https://github.com/d3/d3-scale#ordinal_copy) - 创建比例尺的副本。
* [d3.scaleImplicit](https://github.com/d3/d3-scale#scaleImplicit) - 隐域的一个特殊的未知值。
* [d3.scaleBand](https://github.com/d3/d3-scale#scaleBand) - 创建序数段比例尺。
* [*band*](https://github.com/d3/d3-scale#_band) - 计算对应于给定的定义域的值域。
* [*band*.domain](https://github.com/d3/d3-scale#band_domain) - 设置输入的定义域。
* [*band*.range](https://github.com/d3/d3-scale#band_range) - 设置输出的值域。
* [*band*.rangeRound](https://github.com/d3/d3-scale#band_rangeRound) - 设置输出的值域并取整。
* [*band*.round](https://github.com/d3/d3-scale#band_round) - 取整。
* [*band*.paddingInner](https://github.com/d3/d3-scale#band_paddingInner) - 段间距。
* [*band*.paddingOuter](https://github.com/d3/d3-scale#band_paddingOuter) - 外边距。
* [*band*.padding](https://github.com/d3/d3-scale#band_padding) - 设置间距（段间距和外边距）。
* [*band*.align](https://github.com/d3/d3-scale#band_align) - 设置段对齐。
* [*band*.bandwidth](https://github.com/d3/d3-scale#band_bandwidth) - 获取每段宽度。
* [*band*.step](https://github.com/d3/d3-scale#band_step) - 开始相邻段之间的距离。
* [*band*.copy](https://github.com/d3/d3-scale#band_copy) - 创建比例尺的副本。
* [d3.scalePoint](https://github.com/d3/d3-scale#scalePoint) - 创建序数点比例尺。
* [*point*](https://github.com/d3/d3-scale#_point) - 计算对应于给定的定义域的值域。
* [*point*.domain](https://github.com/d3/d3-scale#point_domain) - 设置输入的定义域。
* [*point*.range](https://github.com/d3/d3-scale#point_range) - 设置输出的值域。
* [*point*.rangeRound](https://github.com/d3/d3-scale#point_rangeRound) - 设置输出的值域并取整。
* [*point*.round](https://github.com/d3/d3-scale#point_round) - 取整。
* [*point*.padding](https://github.com/d3/d3-scale#point_padding) - 外边距。
* [*point*.align](https://github.com/d3/d3-scale#point_align) - 设置点对齐。
* [*point*.bandwidth](https://github.com/d3/d3-scale#point_bandwidth) - 返回0。
* [*point*.step](https://github.com/d3/d3-scale#point_step) - 开始相邻点之间的距离。
* [*point*.copy](https://github.com/d3/d3-scale#point_copy) - 创建比例尺的副本。
* [d3.scaleCategory10](https://github.com/d3/d3-scale#scaleCategory10) - 10种分类颜色。
* [d3.scaleCategory20](https://github.com/d3/d3-scale#scaleCategory20) - 20种分类颜色。
* [d3.scaleCategory20b](https://github.com/d3/d3-scale#scaleCategory20b) - 20种分类颜色。
* [d3.scaleCategory20c](https://github.com/d3/d3-scale#scaleCategory20c) - 20种分类颜色。

## [选择器](https://github.com/d3/d3-selection)

通过选择元素和加入数据来转换DOM。

### [选择元素](https://github.com/d3/d3-selection#selecting-elements)

* [d3.selection](https://github.com/d3/d3-selection#selection) - 选择根文档元素。
* [d3.select](https://github.com/d3/d3-selection#select) - 从文档中选择一个元素。
* [d3.selectAll](https://github.com/d3/d3-selection#selectAll) - 从文档中选择多个元素。
* [*selection*.select](https://github.com/d3/d3-selection#selection_select) - 选择每个选中元素的一个后代元素。
* [*selection*.selectAll](https://github.com/d3/d3-selection#selection_selectAll) - 选择每个选中元素的多个后代元素。
* [*selection*.filter](https://github.com/d3/d3-selection#selection_filter) - 基于数据过滤元素。
* [*selection*.merge](https://github.com/d3/d3-selection#selection_merge) - 合并两个选择。
* [d3.matcher](https://github.com/d3/d3-selection#matcher) - 测试一个元素是否匹配选择器。
* [d3.selector](https://github.com/d3/d3-selection#selector) - 选择一个元素。
* [d3.selectorAll](https://github.com/d3/d3-selection#selectorAll) - 选择多个元素。
* [d3.window](https://github.com/d3/d3-selection#window) - 得到节点的所有者窗口。

### [修改元素](https://github.com/d3/d3-selection#modifying-elements)

* [*selection*.attr](https://github.com/d3/d3-selection#selection_attr) - 设置或获取特性。
* [*selection*.classed](https://github.com/d3/d3-selection#selection_classed) - 获取，添加或移除CSS类。
* [*selection*.style](https://github.com/d3/d3-selection#selection_style) - 设置或获取样式。
* [*selection*.property](https://github.com/d3/d3-selection#selection_property) - 设置或获取行内属性。
* [*selection*.text](https://github.com/d3/d3-selection#selection_text) - 设置或获取文本内容。
* [*selection*.html](https://github.com/d3/d3-selection#selection_html) - 设置或获取inner HTML。
* [*selection*.append](https://github.com/d3/d3-selection#selection_append) - 创建，添加或选择新的元素。
* [*selection*.remove](https://github.com/d3/d3-selection#selection_remove) - 移除文档中的元素。
* [*selection*.sort](https://github.com/d3/d3-selection#selection_sort) - 基于数据给文档中的元素排序。
* [*selection*.order](https://github.com/d3/d3-selection#selection_order) - 重排列文档中的元素以匹配选择中的顺序。
* [*selection*.raise](https://github.com/d3/d3-selection#selection_raise) - 重新排列每个元素为父元素的最后一个子节点。
* [*selection*.lower](https://github.com/d3/d3-selection#selection_lower) - 重新排列每个元素为父元素的第一个子节点。
* [d3.creator](https://github.com/d3/d3-selection#creator) - 通过名称创建元素。

### [数据绑定](https://github.com/d3/d3-selection#joining-data)

* [*selection*.data](https://github.com/d3/d3-selection#selection_data) - 元素和数据绑定。
* [*selection*.enter](https://github.com/d3/d3-selection#selection_enter) - 获得进入（enter）选择器（数据无元素）。
* [*selection*.exit](https://github.com/d3/d3-selection#selection_exit) - 获得退出（exit）选择器（元素无数据）。 
* [*selection*.datum](https://github.com/d3/d3-selection#selection_datum) - 获取或设置元素的数据（不绑定）。

### [事件处理](https://github.com/d3/d3-selection#handling-events)

* [*selection*.on](https://github.com/d3/d3-selection#selection_on) - 添加或移除事件监听器。
* [*selection*.dispatch](https://github.com/d3/d3-selection#selection_dispatch) - 分发自定义事件。
* [d3.event](https://github.com/d3/d3-selection#event) - 交互中的当前用户事件。
* [d3.customEvent](https://github.com/d3/d3-selection#customEvent) - 暂时定义一个自定义事件。
* [d3.mouse](https://github.com/d3/d3-selection#mouse) - 获取相对给定容器的鼠标位置。
* [d3.touch](https://github.com/d3/d3-selection#touch) - 获取相对给定容器的单点触控位置。
* [d3.touches](https://github.com/d3/d3-selection#touches) - 获取相对给定容器的多点触控位置。

### [控制语句](https://github.com/d3/d3-selection#control-flow)

* [*selection*.each](https://github.com/d3/d3-selection#selection_each) - 为每个元素调用一次指定的方法。
* [*selection*.call](https://github.com/d3/d3-selection#selection_call) - 选择器调用指定的方法。
* [*selection*.empty](https://github.com/d3/d3-selection#selection_empty) - 返回是否是空选择。
* [*selection*.nodes](https://github.com/d3/d3-selection#selection_nodes) - 返回所有选中元素的数组。
* [*selection*.node](https://github.com/d3/d3-selection#selection_node) - 返回第一个非空元素。
* [*selection*.size](https://github.com/d3/d3-selection#selection_size) - 返回元素数量。

### [命名空间](https://github.com/d3/d3-selection#namespaces)

* [d3.namespace](https://github.com/d3/d3-selection#namespace) - 限定XML命名空间，如“xlink:href "。
* [d3.namespaces](https://github.com/d3/d3-selection#namespaces) - 内置的XML命名空间。

## [形状](https://github.com/d3/d3-shape)

可视化的图形原语。

### [弧](https://github.com/d3/d3-shape#arcs)

圆形或环形扇区，如饼图或甜甜圈图。

* [d3.arc](https://github.com/d3/d3-shape#arc) - 创建一个新的弧生成器。
* [*arc*](https://github.com/d3/d3-shape#_arc) - 创建给定数据的弧。
* [*arc*.centroid](https://github.com/d3/d3-shape#arc_centroid) - 弧中心。
* [*arc*.innerRadius](https://github.com/d3/d3-shape#arc_innerRadius) - 设置内径。
* [*arc*.outerRadius](https://github.com/d3/d3-shape#arc_outerRadius) - 设置外径。
* [*arc*.cornerRadius](https://github.com/d3/d3-shape#arc_cornerRadius) - 设置圆角半径。
* [*arc*.startAngle](https://github.com/d3/d3-shape#arc_startAngle) - 设置起始角度。
* [*arc*.endAngle](https://github.com/d3/d3-shape#arc_endAngle) - 设置结束角度。
* [*arc*.padAngle](https://github.com/d3/d3-shape#arc_padAngle) - 设置相邻弧之间的夹角。
* [*arc*.padRadius](https://github.com/d3/d3-shape#arc_padRadius) - 设置线性填充半径。
* [*arc*.context](https://github.com/d3/d3-shape#arc_context) - 设置渲染上下文。

### [饼](https://github.com/d3/d3-shape#pies)

计算用于展示饼图或甜环形图的必要的角度值。

* [d3.pie](https://github.com/d3/d3-shape#pie) - 创建一个饼生成器。
* [*pie*](https://github.com/d3/d3-shape#_pie) - 计算给定数据集的角度值。
* [*pie*.value](https://github.com/d3/d3-shape#pie_value) - 设置值访问器。
* [*pie*.sort](https://github.com/d3/d3-shape#pie_sort) - 设置排序比较器。
* [*pie*.sortValues](https://github.com/d3/d3-shape#pie_sortValues) - 设置排序比较器。
* [*pie*.startAngle](https://github.com/d3/d3-shape#pie_startAngle) - 设置整体的起始角度。
* [*pie*.endAngle](https://github.com/d3/d3-shape#pie_endAngle) - 设置整体的结束角度。
* [*pie*.padAngle](https://github.com/d3/d3-shape#pie_padAngle) - 设置相邻弧间隔角度。

### [线](https://github.com/d3/d3-shape#lines)

用于绘制线图的样条曲线或者折线。

* [d3.line](https://github.com/d3/d3-shape#line) - 创建一个新的线生成器。
* [*line*](https://github.com/d3/d3-shape#_line) - 生成给定数据的线。
* [*line*.x](https://github.com/d3/d3-shape#line_x) - 设置*x*访问器。
* [*line*.y](https://github.com/d3/d3-shape#line_y) - 设置*y*访问器。
* [*line*.defined](https://github.com/d3/d3-shape#line_defined) - 设置定义访问器。
* [*line*.curve](https://github.com/d3/d3-shape#line_curve) - 设置曲线插值器。
* [*line*.context](https://github.com/d3/d3-shape#line_context) - 设置渲染上下文。
* [d3.radialLine](https://github.com/d3/d3-shape#radialLine) - 创建一个新的径向线生成器。
* [*radialLine*](https://github.com/d3/d3-shape#_radialLine) - 生成给定数据的线。
* [*radialLine*.angle](https://github.com/d3/d3-shape#radialLine_angle) - 设置角度访问器。
* [*radialLine*.radius](https://github.com/d3/d3-shape#radialLine_radius) - 设置半径访问器。
* [*radialLine*.defined](https://github.com/d3/d3-shape#radialLine_defined) - 设置定义访问器。
* [*radialLine*.curve](https://github.com/d3/d3-shape#radialLine_curve) - 设置曲线插值器。
* [*radialLine*.context](https://github.com/d3/d3-shape#radialLine_context) - 设置渲染上下文。

### [面积](https://github.com/d3/d3-shape#areas)

由顶线基线构成，用于面积图。

* [d3.area](https://github.com/d3/d3-shape#area) - 创建一个新的面积生成器。
* [*area*](https://github.com/d3/d3-shape#_area) - 为给定数据集生成面积。
* [*area*.x](https://github.com/d3/d3-shape#area_x) - 设置 *x0* 和 *x1* 访问器。
* [*area*.x0](https://github.com/d3/d3-shape#area_x0) - 设置 基线的 *x* 访问器。
* [*area*.x1](https://github.com/d3/d3-shape#area_x1) - 设置顶线的 *x* 访问器。
* [*area*.y](https://github.com/d3/d3-shape#area_y) - 设置 *y0* 和 *y1* 访问器。
* [*area*.y0](https://github.com/d3/d3-shape#area_y0) - 设置基线的 *y* 访问器。
* [*area*.y1](https://github.com/d3/d3-shape#area_y1) - 设置顶线的 *y* 访问器。
* [*area*.defined](https://github.com/d3/d3-shape#area_defined) - 设置定义点访问器。
* [*area*.curve](https://github.com/d3/d3-shape#area_curve) - 设置曲线插值器。
* [*area*.context](https://github.com/d3/d3-shape#area_context) - 设置渲染上下文。
* [d3.radialArea](https://github.com/d3/d3-shape#radialArea) - 创建一个新的径向面积生成器。
* [*radialArea*](https://github.com/d3/d3-shape#_radialArea) - 为给定数据集生成面积。
* [*radialArea*.angle](https://github.com/d3/d3-shape#radialArea_angle) - 设置起始角度/结束角度访问器。
* [*radialArea*.startAngle](https://github.com/d3/d3-shape#radialArea_startAngle) - 设置起始角度访问器。
* [*radialArea*.endAngle](https://github.com/d3/d3-shape#radialArea_endAngle) - 设置结束角度访问器。
* [*radialArea*.radius](https://github.com/d3/d3-shape#radialArea_radius) - 设置内半径/外半径访问器。
* [*radialArea*.innerRadius](https://github.com/d3/d3-shape#radialArea_innerRadius) - 设置内半径访问器。
* [*radialArea*.outerRadius](https://github.com/d3/d3-shape#radialArea_outerRadius) - 设置外半径访问器。
* [*radialArea*.defined](https://github.com/d3/d3-shape#radialArea_defined) - 设置定义点访问器。
* [*radialArea*.curve](https://github.com/d3/d3-shape#radialArea_curve) - 设置曲线插值器。
* [*radialArea*.context](https://github.com/d3/d3-shape#radialArea_context) - 设置渲染上下文。

### [曲线](https://github.com/d3/d3-shape#curves)

通过在点间插值生成一条曲线。

* [d3.curveBasis](https://github.com/d3/d3-shape#curveBasis) - 立方基本样条，终点循环。
* [d3.curveBasisClosed](https://github.com/d3/d3-shape#curveBasisClosed) - 闭合立方基本样条。
* [d3.curveBasisOpen](https://github.com/d3/d3-shape#curveBasisOpen) - 开放立方基本样条。
* [d3.curveBundle](https://github.com/d3/d3-shape#curveBundle) - 直立方基本样条。
* [d3.curveCardinal](https://github.com/d3/d3-shape#curveCardinal) - 三次C样条。
* [d3.curveCardinalClosed](https://github.com/d3/d3-shape#curveCardinalClosed) - 闭合三次C样条。
* [d3.curveCardinalOpen](https://github.com/d3/d3-shape#curveCardinalOpen) - 开放三次C样条。
* [d3.curveCatmullRom](https://github.com/d3/d3-shape#curveCatmullRom) - 立方Catmull-Rom样条。
* [d3.curveCatmullRomClosed](https://github.com/d3/d3-shape#curveCatmullRomClosed) - 闭合立方Catmull-Rom样条。
* [d3.curveCatmullRomOpen](https://github.com/d3/d3-shape#curveCatmullRomOpen) - 开放立方Catmull-Rom样条。
* [d3.curveLinear](https://github.com/d3/d3-shape#curveLinear) - 折线。
* [d3.curveLinearClosed](https://github.com/d3/d3-shape#curveLinearClosed) - 闭合折线。
* [d3.curveMonotoneX](https://github.com/d3/d3-shape#curveMonotoneX) - 立方样条。鉴于y单调性，保持x。
* [d3.curveMonotoneY](https://github.com/d3/d3-shape#curveMonotoneY) - 立方样条。鉴于y单调性，保持x。
* [d3.curveNatural](https://github.com/d3/d3-shape#curveNatural) - 自然三次样条。
* [d3.curveStep](https://github.com/d3/d3-shape#curveStep) - 分段常值函数。
* [d3.curveStepAfter](https://github.com/d3/d3-shape#curveStepAfter) - 分段常值函数。
* [d3.curveStepBefore](https://github.com/d3/d3-shape#curveStepBefore) - 分段常值函数。
* [*curve*.areaStart](https://github.com/d3/d3-shape#curve_areaStart) - 开始一个面积片段。
* [*curve*.areaEnd](https://github.com/d3/d3-shape#curve_areaEnd) - 结束一个面积片段。
* [*curve*.lineStart](https://github.com/d3/d3-shape#curve_lineStart) - 开始一条新的线段。
* [*curve*.lineEnd](https://github.com/d3/d3-shape#curve_lineEnd) - 结束一条新的线段。
* [*curve*.point](https://github.com/d3/d3-shape#curve_point) - 给当前线段加一个点。
