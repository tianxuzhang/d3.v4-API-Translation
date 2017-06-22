# D3.js 4.x API中文手册

本文档会随官方文档同步更新。

# 说说4.x
今天（2016-05-14）打开D3的项目地址https://github.com/d3/d3 ，发现描述已经变成了：
>Bring data to life with SVG, Canvas and HTML

比以前多个了`Canvas`，也就是说D3.js的历史进入了新纪元。这是历经早期`Protovis`只支持`SVG`到后来d3.v3支持`HTML`操作，如今又进入了一个崭新的阶段将支持`Canvas`了。d3.v4的源码也有相当大的调整，最明显的是分成了很多小模块单独开发。D3留给我们的想象空间还很大。好吧，为了更好地拥抱新技术！本项目将通过对D3 V4官方文档的翻译对d3.v4做个全面深入的了解。本文为保持原汁原味，会采用直译，希望成为帮助大家入门d3.v4的第一手资料。

# 题外话

如果大家想在官方博客发文章可以参考：http://blockbuilder.org/

如果想检索4.x的案例可以参考：http://blockbuilder.org/search#d3version=v4

# 4.x的新功能

## 颜色，插值器，比例尺

+ 颜色支持透明度（rgba，hsla等）。
+ 新增Cubehelix颜色空间。
+ 新增连续型颜色比例尺：绿松石（Viridis）和周期性的彩虹（cyclical Rainbow）。
+ 新增点比例尺和段比例尺替代以前的ordinal.rangeBands和ordinal.rangePoints。
+ 新增基本样条曲线插值器（例如连续的ColorBrewer）。
+ 新增d3.interpolateDate
+ d3.interpolate支持特殊的日期
+ d3.interpolate支持类似数字的对象

## 形状和布局。

+ 形状支持渲染成Canvas。
+ 增加了参数化的 Catmull–Rom 和natural样条曲线。
+ 新的确定，可扩展的*速度Verlet*力布局。
+ 新的圆形填充布局。
+ 新的可扩展的矩形树布局；改良squarified treemaps；新增binary treemaps。
+ 新增d3.stratify用于处理行列式层次型数据（以前只支持JSON）。
+ 新增diagram.find支持Voronoi快速检索
+ 添加node.count
+ 包含d3-chord 
+ 默认的轴样式。

----------------
+ 更快，可变的，非递归的四叉树。
+ 泰森多边形暴露有用的拓扑信息。
+ 使圆形弧线更健壮

----------------
+ 修复了cardinal 和 monotone样条曲线。
+ 修复d3.curveCatmullRom中的bug
+ 修复当范围的最小值是非0值时voronoi.size的异常。
+ 修复在voronoi diagram.find时发生崩溃
+ 修复在voronoi diagram.triangles时发生崩溃
* 修复treemaps中有0值时挂起
* 修复d3.pack和d3.packSiblings的重叠点bug
* 修复force.initialize支持孤立点

## 选择器，过渡，缓动和定时器。

+ 新增selection.raise， selection.lower 和selection.dispatch 方法。
+ 时间在后台是冻结的，避免无意识的操作。
+ 定时器可以在外部停止。
+ 过渡现在支持 CSS 变换。
+ 可使用selection.interrupt取消过渡。

----------------
+ 更简单的过渡链（d3.active，transition.delay）。
+ 为同质转换提供更好的性能（例如元素间共享插值器）。
+ 更好地执行和持续过渡状态。

----------------
+ 修复松紧带缓冲函数和弹性缓冲函数。
+ 修复链式过渡不会打断它之前的过渡。
+ 修复最后一个节拍抛出错误时过渡不会卡住
+ 修复抛出错误时过渡不会内存泄漏
+ 修复当序数轴过渡被打断时的无效转换

## 地理

+ 添加projection.fitExtent和projection.fitSize
+ 添加d3.geoIdentity用于缩放，平移和剪切平面几何。
+ 添加d3.geoGraticule10用于生成默认为10°的经纬网
+ 添加d3.geoPath的优化参数用于支持投影和context。
+ 为d3.geoIdentity添加identity.reflectX和identity.reflectY函数
+ 添加path.measure
+ 添加d3.geoContains
+ d3.geoIdentity的clipExtent替代d3.geoClipExtent
+ 导出原始地理投影。

----------------
+ 优化地图投影的默认值
+ 优化d3.geoPath
+ 提高d3.path的性能
+ 优化d3.geoCentroid

----------------
+ 修复d3.geoBounds时发生崩溃
+ 修复d3.geoStereographic反转函数
+ 修复d3.geoAlbersUsa缓存失效
+ 修复调用collide.radius没有反应。
+ 修复d3.geoConicConformal反转函数
+ 修复d3.geoConicEqualArea
+ 修复d3.geoPath的默认投影和上下文为null而不是undefined
+ 修复d3.geoBounds计算线几何体的bug
+ 修复d3.geoCentroid计算细节地理特征的bug

## 数据

+ 添加d3.ticks。
+ 添加d3.cross
+ d3.pairs添加一个reducer入参
+ 本地数字格式现在可以定义数字系统（如阿拉伯）
+ 内置的用于并行加载数据的异步队列。

----------------
+ 修复颜色规范中对不寻常的数字格式的解析
+ 修复interval.every(…).range入参是无效日期时挂起。
+ 修复负无穷的数字格式化
+ 修复d3.interpolateRgb.gamma的透明度插值
+ time.ticks的step参数改为interval.every。
+ 如果d3.request回调是无效的时候抛出一个异常。
+ 修复d3.queue的await回调函数中吃掉异常

## 交互

+ 更好的刷子交互。
+ 添加zoom.interpolate来控制聚焦过渡行为
+ 可禁用双击聚焦过渡

----------------
+ 修复变焦同时应用到一个元素和其祖先时发生崩溃。
+ 修复在brush.move中清除brush时发生崩溃
+ 修复zoom.translateExtent小于zoom.extent时挂起
+ 修复多点触摸触发的聚焦行为挂起

# 我的感受

* 2016-5-20日下午五点左右，D3的star数超过50000次，位列所有前端库第二（仅次于boostrap）。自从2013年关注D3以来，几乎都超过每个月1000的增幅上涨着。严谨的可视化理论、便捷的数据驱动方法和丰富友好的文档案例让社区日渐繁荣。

* 翻译D3 V4的API发现与D3 V3的差别很大。暴露了更丰富的功能细节，就力导向图就从原来的12个功能函数增加到现在的41个（包含二级函数）。V4的大量API由原来的二级函数升级为一级函数（实际上就是把两级的单词合并，使用驼峰命名法重命名了），这样给使用者带来了一些记忆负担，其实以前的API设计得更好用点~

# 加群讨论

||新手群|专业群|研究群|
|---|---|---|---|
|说明|免费（暂时）|付费|免费（新手别加）|
|群名|D3.js|D3数据可视化|大数据可视化|
|群号|437278817|205076374|436442115|
|二维码| <img src="http://img.blog.csdn.net/20161105095608477" width = "300" height = "300" alt="D3.js" align=center />|<img src="http://img.blog.csdn.net/20161105095649087" width = "300" height = "300" alt="D3数据可视化" align=center />|<img src="http://img.blog.csdn.net/20161105095514714" width = "300" height = "300" alt="大数据可视化" align=center />|

-----------

下面是译文，欢迎一起翻译，探讨~

-----------

# D3: 数据驱动文档（Data-Driven Documents）

<a href="https://d3js.org"><img src="https://d3js.org/logo.svg" align="left" hspace="10" vspace="6"></a>

**D3** (或**D3.js**) 是一个用来使用Web标准做数据可视化的JavaScript函数库。

D3帮助我们可以融合SVG, Canvas 和 HTML操作技术让数据变得生动有趣。

D3将强大的**可视化**，**动态交互**和**数据驱动的DOM操作方法**完美结合，让我们可以充分发挥现代浏览器的功能，自由地设计正确的可视化界面。



## 资料

* [API参考](https://github.com/d3/d3/blob/master/API.md)
* [发行版](https://github.com/d3/d3/releases)
* [展廊](https://github.com/d3/d3/wiki/Gallery)
* [案例](http://bl.ocks.org/mbostock)
* [Wiki](https://github.com/d3/d3/wiki)

## 安装

最近的稳定版是 (4.7.1), 可以按照wiki里的 [安装介绍 ](https://github.com/d3/d3/wiki#installing) 安装使用。如果你使用NPM, 可执行`npm install d3`命令。不然的话可以下载[最新版](https://github.com/d3/d3/releases/latest)。 发布包支持AMD, CommonJS, 和 vanilla 环境。自定义编译可以使用 [Rollup](https://github.com/rollup/rollup) 或者其他打包工具。也可以直接从[d3js.org](https://d3js.org)引用:

```html
<script src="https://d3js.org/d3.v4.min.js"></script>
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
* [缩放](#zooming)

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
* [d3.quantile](https://github.com/d3/d3-array#quantile) - 计算一个数字数组排序后的分位数。[R和Excel使用的R-7分位数计算法](https://en.wikipedia.org/wiki/Quantile#Quantiles_of_a_population)
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
* [d3.pairs](https://github.com/d3/d3-array#pairs) - 数组邻接对。
* [d3.permute](https://github.com/d3/d3-array#permute) - 安装指定的索引数组重排数组。
* [d3.shuffle](https://github.com/d3/d3-array#shuffle) - 数组随机排序。[洗牌算法的讨论](https://bost.ocks.org/mike/shuffle/)
* [d3.ticks](https://github.com/d3/d3-array#ticks) - 从一个数组间隔生成有代表的值，刻度值。
* [d3.tickStep](https://github.com/d3/d3-array#tickStep) - 从一个数组间隔生成有代表的步长。
* [d3.tickIncrement](https://github.com/d3/d3-array#tickIncrement) - 增量（ticks中用到）。
* [d3.range](https://github.com/d3/d3-array#range) - 生成一组数值。
* [d3.transpose](https://github.com/d3/d3-array#transpose) - 数组转置。
* [d3.zip](https://github.com/d3/d3-array#zip) - 转置多个数组。
* [d3.cross](https://github.com/d3/d3-array#cross) - 两个数组的笛卡尔积。

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
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/linear.png" alt="linear" width="100%" height="240" style="max-width:100%;">
* [d3.easePolyIn](https://github.com/d3/d3-ease#easePolyIn) - 多项式缓动，加速到指定的速率。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/polyIn.png" alt="polyIn" width="100%" height="240" style="max-width:100%;">
* [d3.easePolyOut](https://github.com/d3/d3-ease#easePolyOut) - 逆多项式缓动，等价于1 - polyIn(1 - t)。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/polyOut.png" alt="polyOut" width="100%" height="240" style="max-width:100%;">
* [d3.easePolyInOut](https://github.com/d3/d3-ease#easePolyInOut) - 对称多项式缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/polyInOut.png" alt="polyInOut" width="100%" height="240" style="max-width:100%;">
* [*poly*.exponent](https://github.com/d3/d3-ease#poly_exponent) - 指定缓动多项式的指数。
```js
var linear = d3.easePoly.exponent(1),
    quad = d3.easePoly.exponent(2),
    cubic = d3.easePoly.exponent(3);
```
* [d3.easeQuad](https://github.com/d3/d3-ease#easeQuad) - easeQuadInOut的别名。
* [d3.easeQuadInOut](https://github.com/d3/d3-ease#easeQuadInOut) - 对称平方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/quadInOut.png" alt="quadInOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeQuadIn](https://github.com/d3/d3-ease#easeQuadIn) - 平方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/quadIn.png" alt="quadIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeQuadOut](https://github.com/d3/d3-ease#easeQuadOut) - 逆平方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/quadOut.png" alt="quadOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeCubic](https://github.com/d3/d3-ease#easeCubic) - easeCubicInOut的别名。
* [d3.easeCubicInOut](https://github.com/d3/d3-ease#easeCubicInOut) - 对称立方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/cubicInOut.png" alt="cubicInOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeCubicIn](https://github.com/d3/d3-ease#easeCubicIn) - 立方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/cubicIn.png" alt="cubicIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeCubicOut](https://github.com/d3/d3-ease#easeCubicOut) - 逆立方缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/cubicOut.png" alt="cubicOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeSinIn](https://github.com/d3/d3-ease#easeSinIn) - 正弦缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/sinIn.png" alt="sinIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeSinOut](https://github.com/d3/d3-ease#easeSinOut) - 逆正弦缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/sinOut.png" alt="sinOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeSin](https://github.com/d3/d3-ease#easeSin) - easeSinInOut的别名。
* [d3.easeSinInOut](https://github.com/d3/d3-ease#easeSinInOut) - 对称正弦缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/sinInOut.png" alt="sinInOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeExpIn](https://github.com/d3/d3-ease#easeExpIn) - 指数缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/expIn.png" alt="expIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeExpOut](https://github.com/d3/d3-ease#easeExpOut) - 逆指数缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/expOut.png" alt="expOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeExp](https://github.com/d3/d3-ease#easeExp) - easeExpInOut的别名。
* [d3.easeExpInOut](https://github.com/d3/d3-ease#easeExpInOut) - 对称指数缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/expInOut.png" alt="expInOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeCircleIn](https://github.com/d3/d3-ease#easeCircleIn) - 圆形缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/circleIn.png" alt="circleIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeCircleOut](https://github.com/d3/d3-ease#easeCircleOut) - 逆圆形缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/circleOut.png" alt="circleOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeCircle](https://github.com/d3/d3-ease#easeCircle) - easeCircleInOut的别名。
* [d3.easeCircleInOut](https://github.com/d3/d3-ease#easeCircleInOut) - 对称圆形缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/circleInOut.png" alt="circleInOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeElasticIn](https://github.com/d3/d3-ease#easeElasticIn) - 弹性缓动，类似松紧带。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/elasticIn.png" alt="elasticIn" width="100%" height="360" style="max-width:100%;">
* [d3.easeElastic](https://github.com/d3/d3-ease#easeElastic) - easeElasticOut的别名。
* [d3.easeElasticOut](https://github.com/d3/d3-ease#easeElasticOut) - 逆弹性缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/elasticOut.png" alt="elasticOut" width="100%" height="360" style="max-width:100%;">
* [d3.easeElasticInOut](https://github.com/d3/d3-ease#easeElasticInOut) - 对称弹性缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/elasticInOut.png" alt="elasticInOut" width="100%" height="360" style="max-width:100%;">
* [*elastic*.amplitude](https://github.com/d3/d3-ease#elastic_amplitude) - 指定弹性振幅。
* [*elastic*.period](https://github.com/d3/d3-ease#elastic_period) - 指定弹性周期。
* [d3.easeBackIn](https://github.com/d3/d3-ease#easeBackIn) - [预期缓动](https://en.wikipedia.org/wiki/12_basic_principles_of_animation#Anticipation)。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/backIn.png" alt="backIn" width="100%" height="300" style="max-width:100%;">
* [d3.easeBackOut](https://github.com/d3/d3-ease#easeBackOut) - 逆预期缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/backOut.png" alt="backOut" width="100%" height="300" style="max-width:100%;">
* [d3.easeBack](https://github.com/d3/d3-ease#easeBack) - easeBackInOut的别名。
* [d3.easeBackInOut](https://github.com/d3/d3-ease#easeBackInOut) - 对称预期缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/backInOut.png" alt="backInOut" width="100%" height="300" style="max-width:100%;">
* [*back*.overshoot](https://github.com/d3/d3-ease#back_overshoot) - 指定超调量。
* [d3.easeBounceIn](https://github.com/d3/d3-ease#easeBounceIn) - 弹跳缓动，类似弹跳的小球。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/bounceIn.png" alt="bounceIn" width="100%" height="240" style="max-width:100%;">
* [d3.easeBounce](https://github.com/d3/d3-ease#easeBounce) - easeBounceOut的别名。
* [d3.easeBounceOut](https://github.com/d3/d3-ease#easeBounceOut) - 逆弹跳缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/bounceOut.png" alt="bounceOut" width="100%" height="240" style="max-width:100%;">
* [d3.easeBounceInOut](https://github.com/d3/d3-ease#easeBounceInOut) - 均匀弹跳缓动。
<img src="https://raw.githubusercontent.com/d3/d3-ease/master/img/bounceInOut.png" alt="bounceInOut" width="100%" height="240" style="max-width:100%;">

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

### [连续颜色比例尺](https://github.com/d3/d3-scale#scaleSequential)

将连续的，数量的定义域映射为连续的，固定的颜色插值器。

* [d3.scaleSequential](https://github.com/d3/d3-scale#scaleSequential) - 创建一个顺序比例尺。create a sequential scale.
* [*sequential*.interpolator](https://github.com/d3/d3-scale#sequential_interpolator) - 设置比例尺的输出插值器。
* [d3.interpolateViridis](https://github.com/d3/d3-scale#interpolateViridis) - 暗到明的颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/viridis.png" width="100%" height="40" alt="viridis">

* [d3.interpolateInferno](https://github.com/d3/d3-scale#interpolateInferno) - 暗到明的颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/inferno.png" width="100%" height="40" alt="inferno">

* [d3.interpolateMagma](https://github.com/d3/d3-scale#interpolateMagma) - 暗到明的颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/magma.png" width="100%" height="40" alt="magma">

* [d3.interpolatePlasma](https://github.com/d3/d3-scale#interpolatePlasma) - 暗到明的颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/plasma.png" width="100%" height="40" alt="plasma">

* [d3.interpolateWarm](https://github.com/d3/d3-scale#interpolateWarm) - 色相环颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/warm.png" width="100%" height="40" alt="warm">

* [d3.interpolateCool](https://github.com/d3/d3-scale#interpolateCool) - 色相环颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/cool.png" width="100%" height="40" alt="cool">

* [d3.interpolateRainbow](https://github.com/d3/d3-scale#interpolateRainbow) - 循环的色相环颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/rainbow.png" width="100%" height="40" alt="rainbow">

* [d3.interpolateCubehelixDefault](https://github.com/d3/d3-scale#interpolateCubehelixDefault) - 暗到明的色相环颜色组合。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/cubehelix.png" width="100%" height="40" alt="cubehelix">

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
* [d3.schemeCategory10](https://github.com/d3/d3-scale#scaleCategory10) - 10种分类颜色。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/category10.png" width="100%" height="40" alt="category10">

* [d3.schemeCategory20](https://github.com/d3/d3-scale#scaleCategory20) - 20种分类颜色。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/category20.png" width="100%" height="40" alt="category20">

* [d3.schemeCategory20b](https://github.com/d3/d3-scale#scaleCategory20b) - 20种分类颜色。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/category20b.png" width="100%" height="40" alt="category20b">

* [d3.schemeCategory20c](https://github.com/d3/d3-scale#scaleCategory20c) - 20种分类颜色。
<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/category20c.png" width="100%" height="40" alt="category20c">

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
* [*area*.lineX0](https://github.com/d3/d3-shape#area_lineX0) - 为区域左边缘得到一条线。
* [*area*.lineX1](https://github.com/d3/d3-shape#area_lineX1) - 为区域右边缘得到一条线。
* [*area*.lineY0](https://github.com/d3/d3-shape#area_lineY0) - 为区域上边缘得到一条线。
* [*area*.lineY1](https://github.com/d3/d3-shape#area_lineY1) - 为区域下边缘得到一条线。
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
* [*radialArea*.lineStartAngle](https://github.com/d3/d3-shape#area_lineStartAngle) - 为区域起始边缘得到一条线。
* [*radialArea*.lineEndAngle](https://github.com/d3/d3-shape#area_lineEndAngle) - 为区域结束边缘得到一条线。
* [*radialArea*.lineInnerRadius](https://github.com/d3/d3-shape#area_lineInnerRadius) - 为区域内边缘得到一条线。
* [*radialArea*.lineOuterRadius](https://github.com/d3/d3-shape#area_lineOuterRadius) - 为区域外边缘得到一条线。

### [曲线](https://github.com/d3/d3-shape#curves)

通过在点间插值生成一条曲线。

* [d3.curveBasis](https://github.com/d3/d3-shape#curveBasis) - 立方基本样条，终点循环。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/basis.png" width="888" height="240" alt="basis" style="max-width:100%;" class="">

* [d3.curveBasisClosed](https://github.com/d3/d3-shape#curveBasisClosed) - 闭合立方基本样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/basisClosed.png" width="888" height="240" alt="basisClosed" style="max-width:100%;">

* [d3.curveBasisOpen](https://github.com/d3/d3-shape#curveBasisOpen) - 开放立方基本样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/basisOpen.png" width="888" height="240" alt="basisOpen" style="max-width:100%;">

* [d3.curveBundle](https://github.com/d3/d3-shape#curveBundle) - 直立方基本样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/bundle.png" width="888" height="240" alt="bundle" style="max-width:100%;">

* [d3.curveCardinal](https://github.com/d3/d3-shape#curveCardinal) - 三次C样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/cardinal.png" width="888" height="240" alt="cardinal" style="max-width:100%;">

* [d3.curveCardinalClosed](https://github.com/d3/d3-shape#curveCardinalClosed) - 闭合三次C样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/cardinalClosed.png" width="888" height="240" alt="cardinalClosed" style="max-width:100%;">

* [d3.curveCardinalOpen](https://github.com/d3/d3-shape#curveCardinalOpen) - 开放三次C样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/cardinalOpen.png" width="888" height="240" alt="cardinalOpen" style="max-width:100%;">

* [*cardinal*.tension](https://github.com/d3/d3-shape#cardinal_tension) - 设置基数样条曲线的张力。
* [d3.curveCatmullRom](https://github.com/d3/d3-shape#curveCatmullRom) - 立方Catmull-Rom样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/catmullRom.png" width="888" height="240" alt="catmullRom" style="max-width:100%;">

* [d3.curveCatmullRomClosed](https://github.com/d3/d3-shape#curveCatmullRomClosed) - 闭合立方Catmull-Rom样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/catmullRomClosed.png" width="888" height="330" alt="catmullRomClosed" style="max-width:100%;">

* [d3.curveCatmullRomOpen](https://github.com/d3/d3-shape#curveCatmullRomOpen) - 开放立方Catmull-Rom样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/catmullRomOpen.png" width="888" height="240" alt="catmullRomOpen" style="max-width:100%;">

* [*catmullRom*.alpha](https://github.com/d3/d3-shape#catmullRom_alpha) - 设置Catmull–Rom的*alpha*参数。
* [d3.curveLinear](https://github.com/d3/d3-shape#curveLinear) - 折线。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/linear.png" width="888" height="240" alt="linear" style="max-width:100%;">

* [d3.curveLinearClosed](https://github.com/d3/d3-shape#curveLinearClosed) - 闭合折线。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/linearClosed.png" width="888" height="240" alt="linearClosed" style="max-width:100%;">

* [d3.curveMonotoneX](https://github.com/d3/d3-shape#curveMonotoneX) - 立方样条。假设y是单调的，保持x的单调性。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/monotoneX.png" width="888" height="240" alt="monotoneX" style="max-width:100%;">

* [d3.curveMonotoneY](https://github.com/d3/d3-shape#curveMonotoneY) - 立方样条。假设x是单调的，保持y的单调性。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/monotoneY.png" width="888" height="240" alt="monotoneY" style="max-width:100%;">

* [d3.curveNatural](https://github.com/d3/d3-shape#curveNatural) - 自然三次样条。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/natural.png" width="888" height="240" alt="natural" style="max-width:100%;">

* [d3.curveStep](https://github.com/d3/d3-shape#curveStep) - 分段常值函数。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/step.png" width="888" height="240" alt="step" style="max-width:100%;">

* [d3.curveStepAfter](https://github.com/d3/d3-shape#curveStepAfter) - 分段常值函数。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/stepAfter.png" width="888" height="240" alt="stepAfter" style="max-width:100%;">

* [d3.curveStepBefore](https://github.com/d3/d3-shape#curveStepBefore) - 分段常值函数。
<img src="https://raw.githubusercontent.com/d3/d3-shape/master/img/stepBefore.png" width="888" height="240" alt="stepBefore" style="max-width:100%;">

* [*curve*.areaStart](https://github.com/d3/d3-shape#curve_areaStart) - 开始一个面积片段。
* [*curve*.areaEnd](https://github.com/d3/d3-shape#curve_areaEnd) - 结束一个面积片段。
* [*curve*.lineStart](https://github.com/d3/d3-shape#curve_lineStart) - 开始一条新的线段。
* [*curve*.lineEnd](https://github.com/d3/d3-shape#curve_lineEnd) - 结束一条新的线段。
* [*curve*.point](https://github.com/d3/d3-shape#curve_point) - 给当前线段加一个点。

### [符号](https://github.com/d3/d3-shape#symbols)

一些内置形状，用于散点图。

* [d3.symbol](https://github.com/d3/d3-shape#symbol) - 创建一个新的形状生成器。
* [*symbol*](https://github.com/d3/d3-shape#_symbol) - 为给定数据生成符号。
* [*symbol*.type](https://github.com/d3/d3-shape#symbol_type) - 设置符号类型。
* [*symbol*.size](https://github.com/d3/d3-shape#symbol_size) - 设置符号尺寸。
* [*symbol*.context](https://github.com/d3/d3-shape#symbol_context) - 设置渲染上下文。
* [d3.symbols](https://github.com/d3/d3-shape#symbols) - 符号类型数组。
* [d3.symbolCircle](https://github.com/d3/d3-shape#symbolCircle) - 圆形。
* [d3.symbolCross](https://github.com/d3/d3-shape#symbolCross) - 十字。
* [d3.symbolDiamond](https://github.com/d3/d3-shape#symbolDiamond) - 菱形。
* [d3.symbolSquare](https://github.com/d3/d3-shape#symbolSquare) - 方形。
* [d3.symbolStar](https://github.com/d3/d3-shape#symbolStar) - 五角星。
* [d3.symbolTriangle](https://github.com/d3/d3-shape#symbolTriangle) - 上三角。
* [d3.symbolWye](https://github.com/d3/d3-shape#symbolWye) - Y形。
* [*symbolType*.draw](https://github.com/d3/d3-shape#symbolType_draw) - 在给定的容器中绘制符号。

### [堆叠](https://github.com/d3/d3-shape#stacks)

将形状堆叠起来，就像分段条形图那样。

* [d3.stack](https://github.com/d3/d3-shape#stack) - 创建一个新的堆叠生成器。
* [*stack*](https://github.com/d3/d3-shape#_stack) - 为给定数据生成堆叠数据。
* [*stack*.keys](https://github.com/d3/d3-shape#stack_keys) - 设置键访问器。
* [*stack*.value](https://github.com/d3/d3-shape#stack_value) - 设置值访问器。
* [*stack*.order](https://github.com/d3/d3-shape#stack_order) - 设置排序访问器。
* [*stack*.offset](https://github.com/d3/d3-shape#stack_offset) - 设置偏移访问器。
* [d3.stackOrderAscending](https://github.com/d3/d3-shape#stackOrderAscending) - 将最小值放在底部。
* [d3.stackOrderDescending](https://github.com/d3/d3-shape#stackOrderDescending) - 将最大值放在底部。
* [d3.stackOrderInsideOut](https://github.com/d3/d3-shape#stackOrderInsideOut) - 将最大值放在中部。
* [d3.stackOrderNone](https://github.com/d3/d3-shape#stackOrderNone) - 使用给定的系列顺序。
* [d3.stackOrderReverse](https://github.com/d3/d3-shape#stackOrderReverse) - 系列给定的系列相反的顺序。
* [d3.stackOffsetExpand](https://github.com/d3/d3-shape#stackOffsetExpand) - 标准化为0=1之间。
* [d3.stackOffsetNone](https://github.com/d3/d3-shape#stackOffsetNone) - 应用零基准。
* [d3.stackOffsetSilhouette](https://github.com/d3/d3-shape#stackOffsetSilhouette) - 将流图居中在0附近。
* [d3.stackOffsetWiggle](https://github.com/d3/d3-shape#stackOffsetWiggle) - 流图最小摆动。

## [时间格式化](https://github.com/d3/d3-time-format)

解析和格式化时间。

* [d3.timeFormat](https://github.com/d3/d3-time-format#timeFormat) - enUs.format别名。
* [d3.timeParse](https://github.com/d3/d3-time-format#timeParse) - enUs.parse别名。
* [d3.utcFormat](https://github.com/d3/d3-time-format#utcFormat) -  enUs.utcFormat别名。
* [d3.utcFormat](https://github.com/d3/d3-time-format#utcParse) -  enUs.utcParse别名。
* [d3.isoFormat](https://github.com/d3/d3-time-format#isoFormat) - ISO 8601 UTC格式化。
* [d3.isoParse](https://github.com/d3/d3-time-format#isoParse) - ISO 8601 UTC解析器。
* [d3.timeFormatLocale](https://github.com/d3/d3-time-format#locale) - 自定义本地化。
* [*locale*.format](https://github.com/d3/d3-time-format#locale_format) - 创建一个时间格式化器。
* [*locale*.parse](https://github.com/d3/d3-time-format#locale_parse) - 创建一个时间解析器。
* [*locale*.utcFormat](https://github.com/d3/d3-time-format#locale_utcFormat) - 创建一个UTC格式化器。
* [*locale*.utcParse](https://github.com/d3/d3-time-format#locale_utcParse) - 创建一个UTC解析器。

## [时间间隔](https://github.com/d3/d3-time)

时间计算。

* [d3.timeInterval](https://github.com/d3/d3-time#timeInterval) - 实现一个新的自定义时间间隔。
* [*interval*](https://github.com/d3/d3-time#_interval) - *interval*.floor的别名。
* [*interval*.floor](https://github.com/d3/d3-time#interval_floor) - 下取整到最近的边界。
* [*interval*.round](https://github.com/d3/d3-time#interval_round) - 四舍五入到最近的边界。
* [*interval*.ceil](https://github.com/d3/d3-time#interval_ceil) - 上取整到最近的边界。
* [*interval*.offset](https://github.com/d3/d3-time#interval_offset) - 抵消一些日期的间隔。
* [*interval*.range](https://github.com/d3/d3-time#interval_range) - 生成的日期范围区间边界。
* [*interval*.filter](https://github.com/d3/d3-time#interval_filter) - 创建一个这个区间的过滤子集。
* [*interval*.every](https://github.com/d3/d3-time#interval_every) - 创建一个这个区间的过滤子集。
* [*interval*.count](https://github.com/d3/d3-time#interval_count) - 计算两个时间之间的间隔。
* [d3.timeMillisecond](https://github.com/d3/d3-time#timeMillisecond), [d3.utcMillisecond](https://github.com/d3/d3-time#timeMillisecond) - 毫秒间隔。
* [d3.timeMilliseconds](https://github.com/d3/d3-time#timeMillisecond), [d3.utcMilliseconds](https://github.com/d3/d3-time#timeMillisecond) - millisecond.range的别名。
* [d3.timeSecond](https://github.com/d3/d3-time#timeSecond), [d3.utcSecond](https://github.com/d3/d3-time#timeSecond) - 秒间隔。
* [d3.timeSeconds](https://github.com/d3/d3-time#timeSecond), [d3.utcSeconds](https://github.com/d3/d3-time#timeSecond) - second.range的别名。
* [d3.timeMinute](https://github.com/d3/d3-time#timeMinute), [d3.utcMinute](https://github.com/d3/d3-time#timeMinute) - 分钟间隔。
* [d3.timeMinutes](https://github.com/d3/d3-time#timeMinute), [d3.utcMinutes](https://github.com/d3/d3-time#timeMinute) - minute.range的别名。
* [d3.timeHour](https://github.com/d3/d3-time#timeHour), [d3.utcHour](https://github.com/d3/d3-time#timeHour) - 小时间隔。
* [d3.timeHours](https://github.com/d3/d3-time#timeHour), [d3.utcHours](https://github.com/d3/d3-time#timeHour) - hour.range的别名。
* [d3.timeDay](https://github.com/d3/d3-time#timeDay), [d3.utcDay](https://github.com/d3/d3-time#timeDay) - 天间隔。
* [d3.timeDays](https://github.com/d3/d3-time#timeDay), [d3.utcDays](https://github.com/d3/d3-time#timeDay) - day.range的别名。
* [d3.timeWeek](https://github.com/d3/d3-time#timeWeek), [d3.utcWeek](https://github.com/d3/d3-time#timeWeek) - 星期天的别名。
* [d3.timeWeeks](https://github.com/d3/d3-time#timeWeek), [d3.utcWeeks](https://github.com/d3/d3-time#timeWeek) - week.range的别名。
* [d3.timeSunday](https://github.com/d3/d3-time#timeSunday), [d3.utcSunday](https://github.com/d3/d3-time#timeSunday) - 星期间隔（周日开始）。
* [d3.timeSundays](https://github.com/d3/d3-time#timeSunday), [d3.utcSundays](https://github.com/d3/d3-time#timeSunday) - sunday.range的别名。
* [d3.timeMonday](https://github.com/d3/d3-time#timeMonday), [d3.utcMonday](https://github.com/d3/d3-time#timeMonday) - 星期间隔（周一开始）。
* [d3.timeMondays](https://github.com/d3/d3-time#timeMonday), [d3.utcMondays](https://github.com/d3/d3-time#timeMonday) - monday.range的别名。
* [d3.timeTuesday](https://github.com/d3/d3-time#timeTuesday), [d3.utcTuesday](https://github.com/d3/d3-time#timeTuesday) - 星期间隔（周二开始）。
* [d3.timeTuesdays](https://github.com/d3/d3-time#timeTuesday), [d3.utcTuesdays](https://github.com/d3/d3-time#timeTuesday) - tuesday.range的别名。
* [d3.timeWednesday](https://github.com/d3/d3-time#timeWednesday), [d3.utcWednesday](https://github.com/d3/d3-time#timeWednesday) - 星期间隔（周三开始）。
* [d3.timeWednesdays](https://github.com/d3/d3-time#timeWednesday), [d3.utcWednesdays](https://github.com/d3/d3-time#timeWednesday) - wednesday.range的别名。
* [d3.timeThursday](https://github.com/d3/d3-time#timeThursday), [d3.utcThursday](https://github.com/d3/d3-time#timeThursday) - 星期间隔（周四开始）。
* [d3.timeThursdays](https://github.com/d3/d3-time#timeThursday), [d3.utcThursdays](https://github.com/d3/d3-time#timeThursday) - thursday.range的别名。
* [d3.timeFriday](https://github.com/d3/d3-time#timeFriday), [d3.utcFriday](https://github.com/d3/d3-time#timeFriday) - 星期间隔（周五开始）。
* [d3.timeFridays](https://github.com/d3/d3-time#timeFriday), [d3.utcFridays](https://github.com/d3/d3-time#timeFriday) - friday.range的别名。
* [d3.timeSaturday](https://github.com/d3/d3-time#timeSaturday), [d3.utcSaturday](https://github.com/d3/d3-time#timeSaturday) - 星期间隔（周六开始）。
* [d3.timeSaturdays](https://github.com/d3/d3-time#timeSaturday), [d3.utcSaturdays](https://github.com/d3/d3-time#timeSaturday) - saturday.range的别名。
* [d3.timeMonth](https://github.com/d3/d3-time#timeMonth), [d3.utcMonth](https://github.com/d3/d3-time#timeMonth) - 月间隔。
* [d3.timeMonths](https://github.com/d3/d3-time#timeMonth), [d3.utcMonths](https://github.com/d3/d3-time#timeMonth) - month.range的别名。
* [d3.timeYear](https://github.com/d3/d3-time#timeYear), [d3.utcYear](https://github.com/d3/d3-time#timeYear) - 年间隔。
* [d3.timeYears](https://github.com/d3/d3-time#timeYear), [d3.utcYears](https://github.com/d3/d3-time#timeYear) - year.range的别名。

## [定时器](https://github.com/d3/d3-timer)

管理成千上万的并发动画的队列。

* [d3.now](https://github.com/d3/d3-timer#now) - 获取当前高分辨率时间。
* [d3.timer](https://github.com/d3/d3-timer#timer) - 安排一个新的定时器。
* [*timer*.restart](https://github.com/d3/d3-timer#timer_restart) - 重置定时器的开始时间和回调。
* [*timer*.stop](https://github.com/d3/d3-timer#timer_stop) - 停止定时器。
* [d3.timerFlush](https://github.com/d3/d3-timer#timerFlush) - 立即执行任何合格的定时器。
* [d3.timeout](https://github.com/d3/d3-timer#timeout) - 安排一个定时器在首次回调时停止。
* [d3.interval](https://github.com/d3/d3-timer#interval) - 安排一个可配置时期的定时器。

## [过渡](https://github.com/d3/d3-transition)

[selections](#selections)的动画过渡。

* [*selection*.transition](https://github.com/d3/d3-transition#selection_transition) - 为选定的元素安排一个过渡。
* [*selection*.interrupt](https://github.com/d3/d3-transition#selection_interrupt) - 中断和取消选定元素的过渡。
* [d3.transition](https://github.com/d3/d3-transition#transition) - 为文档根元素安排一个过渡。
* [*transition*.select](https://github.com/d3/d3-transition#transition_select) - 为选定的元素安排一个过渡。
* [*transition*.selectAll](https://github.com/d3/d3-transition#transition_selectAll) - 为选定的所有元素安排一个过渡。
* [*transition*.filter](https://github.com/d3/d3-transition#transition_filter) - 基于数据过滤元素。
* [*transition*.merge](https://github.com/d3/d3-transition#transition_merge) - 两个过渡合并。
* [*transition*.selection](https://github.com/d3/d3-transition#transition_selection) - 返回一个过渡选择。
* [*transition*.transition](https://github.com/d3/d3-transition#transition_transition) - 链式过渡。
* [*transition*.call](https://github.com/d3/d3-transition#transition_call) - 过渡调用一个函数。
* [*transition*.nodes](https://github.com/d3/d3-transition#transition_nodes) - 返回选定元素数组。
* [*transition*.node](https://github.com/d3/d3-transition#transition_node) - 返回第一个非空元素。
* [*transition*.size](https://github.com/d3/d3-transition#transition_size) - 返回元素数。
* [*transition*.empty](https://github.com/d3/d3-transition#transition_empty) - 如果过渡为空返回true。
* [*transition*.each](https://github.com/d3/d3-transition#transition_each) - 为每个元素调用一个函数。
* [*transition*.on](https://github.com/d3/d3-transition#transition_on) - 添加或删除过渡的事件侦听器。
* [*transition*.attr](https://github.com/d3/d3-transition#transition_attr) - 使用默认插值器过渡属性。
* [*transition*.attrTween](https://github.com/d3/d3-transition#transition_attrTween) - 使用自定义插值器过渡属性。
* [*transition*.style](https://github.com/d3/d3-transition#transition_style) - 使用默认插值器过渡样式。
* [*transition*.styleTween](https://github.com/d3/d3-transition#transition_styleTween) - 使用自定义插值器过渡样式。
* [*transition*.text](https://github.com/d3/d3-transition#transition_text) - 在过渡开始时设置文本内容。
* [*transition*.remove](https://github.com/d3/d3-transition#transition_remove) - 过渡结束后移除元素。
* [*transition*.tween](https://github.com/d3/d3-transition#transition_tween) - 在过渡期间运行自定义代码。
* [*transition*.delay](https://github.com/d3/d3-transition#transition_delay) - 指定每个元素的延迟时间（以毫米为单位）。
* [*transition*.duration](https://github.com/d3/d3-transition#transition_duration) - 指定每个元素的持续时间（以毫米为单位）。
* [*transition*.ease](https://github.com/d3/d3-transition#transition_ease) -指定缓动函数。
* [d3.active](https://github.com/d3/d3-transition#active) - 对于一个给定的节点选择活跃中的过渡。
* [d3.interrupt](https://github.com/d3/d3-transition#interrupt) - 中断过渡？。

## [冯罗诺](https://github.com/d3/d3-voronoi)

为给定的点集计算冯罗诺图。

* [d3.voronoi](https://github.com/d3/d3-voronoi#voronoi) - 创建一个新的冯罗诺生成器。
* [*voronoi*](https://github.com/d3/d3-voronoi#_voronoi) - 为给定的点集计算泰森多边形。
* [*voronoi*.polygons](https://github.com/d3/d3-voronoi#voronoi_polygons) - 为给定的点集计算冯罗诺多边形
* [*voronoi*.triangles](https://github.com/d3/d3-voronoi#voronoi_triangles) - 为给定的点集计算Delaunay三角形。
* [*voronoi*.links](https://github.com/d3/d3-voronoi#voronoi_links) - 为给定的点集计算Delaunay连接。
* [*voronoi*.x](https://github.com/d3/d3-voronoi#voronoi_x) - 设置*x*访问器。
* [*voronoi*.y](https://github.com/d3/d3-voronoi#voronoi_y) - 设置*y*访问器。
* [*voronoi*.extent](https://github.com/d3/d3-voronoi#voronoi_extent) - 设置点的观察范围。
* [*voronoi*.size](https://github.com/d3/d3-voronoi#voronoi_size) - 设置点的观察范围。

## [缩放](https://github.com/d3/d3-zoom)

使用鼠标或触摸平移和缩放SVG, HTML 或 Canvas。

* [d3.zoom](https://github.com/d3/d3-zoom#zoom) - 创建缩放行为。
* [*zoom*](https://github.com/d3/d3-zoom#_zoom) - 将缩放行为应用到选中的元素上。
* [*zoom*.transform](https://github.com/d3/d3-zoom#zoom_transform) - 改变选中元素的仿射变换。
* [*zoom*.translateBy](https://github.com/d3/d3-zoom#zoom_translateBy) - 平移。
* [*zoom*.scaleBy](https://github.com/d3/d3-zoom#zoom_scaleBy) - 缩放。
* [*zoom*.scaleTo](https://github.com/d3/d3-zoom#zoom_scaleTo) - 缩放到。
* [*zoom*.filter](https://github.com/d3/d3-zoom#zoom_filter) - 控制那个输入事件初始化缩放。
* [*zoom*.extent](https://github.com/d3/d3-zoom#zoom_extent) - 设置viewport的尺寸。
* [*zoom*.scaleExtent](https://github.com/d3/d3-zoom#zoom_scaleExtent) - 设置缩放范围。
* [*zoom*.translateExtent](https://github.com/d3/d3-zoom#zoom_translateExtent) - 设置平移范围。
* [*zoom*.duration](https://github.com/d3/d3-zoom#zoom_duration) - 设置缩放过渡的延时时间。
* [*zoom*.on](https://github.com/d3/d3-zoom#zoom_on) - 监听缩放事件。
* [d3.zoomTransform](https://github.com/d3/d3-zoom#zoomTransform) - 获取给定元素的仿射变换。
* [*transform*.scale](https://github.com/d3/d3-zoom#transform_scale) - 缩放指定大小。
* [*transform*.translate](https://github.com/d3/d3-zoom#transform_translate) - 平移指定大小。
* [*transform*.apply](https://github.com/d3/d3-zoom#transform_apply) - 将变换应用到给定的点。
* [*transform*.applyX](https://github.com/d3/d3-zoom#transform_applyX) - 将变换应用到给定的**x**坐标。
* [*transform*.applyY](https://github.com/d3/d3-zoom#transform_applyY) - 将变换应用到给定的**y**坐标。
* [*transform*.invert](https://github.com/d3/d3-zoom#transform_invert) - 解除给定点的变化。
* [*transform*.invertX](https://github.com/d3/d3-zoom#transform_invertX) - 解除给定**x**坐标的变化。
* [*transform*.invertY](https://github.com/d3/d3-zoom#transform_invertY) - 解除给定**y**坐标的变化。
* [*transform*.rescaleX](https://github.com/d3/d3-zoom#transform_rescaleX) - 应用平移到指定的**x**比例尺的定义域。
* [*transform*.rescaleY](https://github.com/d3/d3-zoom#transform_rescaleY) - 应用平移到指定的**y**比例尺的定义域。
* [*transform*.toString](https://github.com/d3/d3-zoom#transform_toString) - 将变换转换成SVG变换字符串。
* [d3.zoomIdentity](https://github.com/d3/d3-zoom#zoomIdentity) - 恒等变换。
