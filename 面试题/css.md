## link和@import的区别

### 父亲不同

- link属于html
- @import属于css

### 加载方式不同

- link会和页面一起加载完
- @import需要等页面加载完后，才加载

### 权重不同

- link引入的样式权重要高于@import

### 兼容性不同

- link无兼容性
- @import只支持iE5以上的才能识别

## transition和animation的区别

### 相同点

- 功能是都可以控制元素的状态实现动画效果
- 很多属性都相同
- 都是随时间改变元素的属性值

### 不同点

- 触发条件不同

	- transition需要触发一个事件才能改变属性值
	- animation不需要任何触发条件

- 运动的方式不同

	- transition为2帧  from ..to...
	- animation可以是一帧一帧的

## flex

### flex容器

- flex-direction设置子元素的排列方式，默认是横向排列

	- column
	- row

- flex-wrap设置是否换行

	- nowrap
	- wrap
	- wrap-reverse

- flex-flow

	- 前俩个属性的简写

- justify-content

	- 定义主轴的对齐方式

		- flex-start
		- flex-end
		- center
		- space-around
		- space-between

- align-items

	- 定义交叉轴的对齐方式

		- flex-start
		- flex-end
		- center
		- stretch
		- baseline

- align-content

	- 定义了多根轴线的排列方式  如果第单根轴线则不起作用

### flex项目（子元素）

- order
- flex-grow
- flex-shink
- flex-bases
- align-self

## 清除浮动

### 创建块格式化上下文BFC(block formation context)

- 父级元素 overflow:hidden

### 使用带clear：both

### 在直接子元素下加上clear:both

### 使用伪元素加clear

## BFC块格式化上下文

### 定义

- 是块盒子布局过程产生的区域
- 也是浮动元素与其它元素交互的区域

### 创建块级格式化上下文

- 定位position

	- absolute
	- fixed

- display属性

	- inline-block
	- flex
	- grid
	- flow-root
	- table-cell
	- table-caption

- contain

	- layout
	- content
	- paint

- overflow

	- hidden
	- auto

- 根元素<html>

### 功能

- 消除浮动
- 外边距塌陷（避免两个相邻的div外边距合并的问题）

## 外边距塌陷问题

### 定义

- 标准流 块的上边距和下边距有时合并为单个边距，其大小为单个边距的最大值

### 不产生外边距塌陷问题

- float
- position:absolution

### 产生条件

- 同级相邻的两个元素

	- 解决：后一个元素加上 清除浮动

- 空的块级元素
- 没有内容将父元素和后代元素分开

### 解决方式

- 创建BFC块格式化上下文
- 清除浮动

## 垂直居中的方式

### 图片垂直居中

- 父元素 display:table-cell; verticle-align:middle;text-align:center;
- 子元素 verticle-align:middle;

### 脱离标准流

- 父元素 display:flex
- 父元素 position:absolute;top:50%;left:50%;transform:translateX(-50%);

	- 

### 不脱离标准流

- 元素本身 margin:auto

## js动画和css动画的区别

### 代码复杂度

- css

	- 简单动画  代码相对简单，性能调优方向固定
	- 复杂动画  代码会变得很冗长

- js动画

	- 简单动画 代码复杂度较高些
	- 复杂动画  js实现起来更优

### 兼容性

- css有浏览器兼容性问题
- js动画大多是没有的

### 性能

- css动画相对更优些

	- css动画通过GUI解析
	- js动画通过js引擎解析后再进行GUI解析渲染

### 对动画的控制程度

- js动画比较灵活，可以控制动画暂停 取消 终止 返回 回放等交互性更强的操作
- css动画不能添加事件，只能在固定的节点进行什么样的过渡动画

### css动画

- 优点

	- 浏览器可以对动画进行优化
	- 使用GPU运算，不会 发生阻塞
	- 对于帧速表现不好的低版本浏览器可以做到自然降级 而js需要撰写额外的代码

- 缺点

	- 不能添加事件，动画交互性没有js好
	- 要实现复杂一点的动画，会很冗余

### js动画

- 优点

	- 动画的 控制能力很强
	- 动画效果比css3丰富
	- 大多没有兼容性问题

- 缺点

	- 在浏览器主线程中运行，可能出现阻塞，造成帧丢失
	- 代码复杂度高于css3
	- 占用CPU

### 总结

- 要实现简单的动画，优先css3,复杂一点优先js动画

## 块元素，行内元素

### 块元素

- 可以设置宽度和高度margin和padding值
- 独占一行
- 自动填满父元素
- 常见的块元素

	- <div>/<h1>~<h6>/<p>/<ul>/<table>

### 行内元素

- 不能设置宽高和垂直方向的margin和padding值
- 排列在一行
- span/a

### 行内块元素

- 可以设置宽高和margin和padding值
- 默认宽度是本身的内容的宽度
- 不能独占一行
- <img>/<input>

## 文本溢出

### 多行

- display:-webkit-box
- -webkit-box-orient:vertical
- -webkit-line-clamp:3
- overflow:hidden

### 单行

- overflow:hidden
- text-overflow:ellipsis

## 页面元素隐藏

### visibility:hidden

- 不改变布局
- 元素绑定的事件不会执行

### display:none

- 布局改变
- 相当于删除元素

### opacity:0

- 布局不改变
- 元素绑定的样式会执行

### z-index 让其他元素覆盖

### position定位到窗口之外

## position定位

### 默认static

- 设置top right left等属性无用

### relative

- 占据原来的位置
- 相对于原来位置进行移动
- 移动元素会覆盖其它元素

### absolute

- 脱离标准流 不占据空间
- 相对于最近一个有relative的父元素移动
- 如果父元素都没有相对定位，则相对于html

### fixed

- 脱离标准流 不占空间
- 相对于浏览器窗口

### sticky

- 先相对定位，然后固定定位
- 必须有个top值
- 到了那个top值，就变固定定位

### inherit

- 从父元素继承position属性的值

## css3新特性

### 边框

- border-radius
- box-shadow
- border-image

### 背景

- background-size
- background-image

	- linear-gradient
	- radial-gradient

- background-origin

	- 指定background-position属性的相对位置
	- content-box
	- border-box
	- padding-box

- background-clip

	- 指定图片绘制区域
	- contnet-box
	- padding-box
	- border-box

### 文字

- text-shadow
- box-shadow
- text-overflow
- word-wrap
- word-break

### 字体

- @font-face字体规则

	- font-family 引入字体的名字
	- src:url(字体地址)

### 2D

- transform

	- translate
	- rotate
	- scale
	- skew
	- matrix(上面几种方法混合写法)

### 3D

- rotateX
- rotateY

### 过渡

- transition

### 动画

- animation

### 多列

- column-count
- column-gap
- column-rule

### 用户界面

- resize
- box-sizing
- outline-offset

### 多媒体查询

### 选择器

- 属性选择器
- 伪元素选择器
- 伪类选择器

## 选择器

### 类型

- id选择器
- 类选择器
- 标签选择器
- 属性选择器
- 伪类选择器
- 伪元素选择器

### 权重

- 老大

	- !important

- 老二

	- 行内样式

- 100

	- id选择器

- 10

	- 类选择器
	- 伪类选择器
	- 属性选择器

- 1

	- 伪元素选择器
	- 标签选择器

### 样式表优先级

- 内联样式
- 内部样式
- 外部样式
- 浏览器用户自定义样式
- 浏览器默认样式

## 盒子模型

### 标准盒子模型 content-box

- width=content

### IE盒子模型 border-box

- width=content+padding+border

### padding-box

- width=content+padding

## css动画如何实现

### @keyframes 和animation

- animation-name 动画名称
- animation-duratio 动画执行时间
- animation-timing-function 动画曲线 ease|linear
- annimation-delay 延迟时间
- animation-iteration-count ：n|infinite  动画播放次数
- animation-direction：normal|alternate 动画播放方向
- animation-fill-mode：none|both|backwards|forwards 动画结束后的状态

### transition

- propetry
- duration
- timing-function
- delay

### 区别

- 触发条件不同

	- transition需要触发条件才能执行animation不需要

- 运动轨迹不同

	- animation可以是一帧一帧的运行
	- transition只有from..to...

## css3对溢出文本的处理

### text-overflow

- clip 截断超出文本
- ellipsis 用省略号代替文本
- string 用字符串替代超出文本

### overflow:hidden

### white-space:nowrap

## 三栏布局实现方式

### float+margin

### display:flex

### position

### display:grid; grid-template-columns:100px auto 100px

### 圣杯布局 float:left;position:relative

### 双飞翼布局

## display:table和table有什么区别

### display:table

- 这个声明能让一个html元素和它的子节点像table元素一样，使用基于表格的css布局
- 能够轻松的定义一个单元格的边界，背景样式
- 不会产生因为使用了table那样的制表符导致的语义化问题
- div+css布局写出来的文件要比table的要小
- table要等页面渲染完才能显示出来

## z-index

设置元素的堆叠顺序

只能在定位元素上才能生效

该属性设置一个定位元素沿z轴的位置，数值越大，离用户越近，数值越小，离用户越远

属性auto:默认堆叠顺序与父元素相等

inherit 从父元素继承z-index属性的值

## display

### 设置外部显示类型

- block
- inline-block
- inline

### 设置内部显示类型(可以控制其子元素的布局)

- flex
- grid
- table

## [脱离文档流](https://www.zhihu.com/question/24529373)

### 定义

- 将元素从普通的布局排版中拿走
- 其它盒子定位时，会当脱离文档流的元素不存在
- 脱离文档流并不等于从dom树中脱离，依然会在dom树下
- 脱离文档流不占空间

### float

- 其它盒子直接无视
- 盒子里面的文本依然会为其让出位置

### position

- 其它盒子以及盒子内的文本都会无视

## [relayout重排和重绘replaint](https://segmentfault.com/a/1190000016990089)

### 浏览器输入url发生了什么

- html->解析html->生成dom树

	- dom树和style树结合生成渲染树render tree

		- paint绘制页面元素

- style sheets->css解析->生成style tree

### 重排

- 当元素几何属性变化

	- 改变元素的宽高 元素的位置
	- 浏览器不得不重新计算元素的几何属性
	- 重新构建渲染树

### 重绘

- 完成重排后
- 将重新构建的渲染树重新渲染到屏幕上

### 关系

- 重排一定会引起重绘
- 重绘不一定会引起重排

### 重排触发机制

- 添加或删除可见的DOM元素
- 元素位置改变
- 元素本身的尺寸改变
- 内容改变
- 页面染初始化
- 浏览器窗口大小发生改变

### 性能优化

- 最小化重绘和重排

	- 改变样式 el.style.cssText
	- 切换类名 el.className=

- 批量修改DOM

	- 让元素脱离标准流

		- 隐藏元素，进行修改后，再显示该元素

			- 控制元素显示和隐藏发生两次重排

		- 使用文档片段创建一个子树，然后再拷贝到文档中

			- 添加文档片段时一次重排

		- 将原始元素拷贝到一个独立的节点中，操作这个节点，然后覆盖原始元素

			- 一次重排

		- 缓存布局信息

			- 要获取到页面上多个元素最好的办法就是第一次获取后就保存起来
			- 减少DOM的访问以提升性能



