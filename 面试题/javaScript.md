# javaScript

## [闭包](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)

### 一个函数和对其词法环境的引用捆绑在一起，这样的组合就是闭包

### 闭包能让一个内层函数访问到其外层函数的作用域

### 每个闭包都有它自己的词法环境

- 在一个闭包内对变量的修改，不会影响到另外一个闭包中的变量

### 词法

- 词法作用域根据源代码中声明变量的位置来确定该变量在何处可用
- 嵌套函数可访问声明于他们外部的作用域（）这就是一个闭包

### 在循环中创建闭包：一个常见的错误

- 解决

	- 使用更多的闭包（匿名闭包）
	- var（变量提升，具有函数作用域）声明的变量改成let（具有块作用域）

### 功能

- 在函数外访问函数内的值
- 保持引用，不被垃圾回收（不会释放外部引用，函数内部的值可以保留）

### 为什么用闭包

- 封装

	- 实现类和继承

- 结果缓存
- 匿名自执行函数

## [用闭包实现一个单例模式](https://blog.csdn.net/xuyangxinlei/article/details/81282170)

### 单例模式

- 意图：保证一个类仅有一个实例，并提供一个访问它的全局访问点
- 主要解决：一个全局使用的类频繁的创建与销毁
- 何时使用：当您想要控制实例数目，节省系统资源的时候
- 如何实现：判断系统是否已经有这个单例，如果有则放回，如果没有则创建
- 代码

	- 

## JS作用域

### 全局作用域

- 在页面打开时创建，页面关闭时被销毁
- 编写在script标签中的变量和函数，作用域为全局作用域，在页面任意位置都可以访问到
- 在全局作用域中有全局对象window,代表一个浏览器窗口，由浏览器创建，可以直接调用
- 全局作用域中声明的变量和函数会作为window对象的属性和方法保存

### 函数作用域（局部作用域）

- 子主题调用函数时。函数的作用域被创建，函数执行完毕，作用域被销毁
- 每调用一次会创建一个新的函数作用域，他们之间是相互独立的
- 在函数作用域中可以访问到全局作用域的变量，在函数外无法访问到函数作用域的变量
- 在函数作用域中访问变量、函数时，会先在自身作用域中寻找，若没找到，则会在函数上一级作用域中寻找，，一直到全局作用域

### 作用域的深层次理解

- 当函数代码执行前期，会创建一个执行期上下文内部对象 AO(作用域)
- 这个内部对象时预编译的时候创建出来的，因为函数在被调用时，会先进行预编译
- 在全局代码执行的前期会创建一个执行期的上下文的对象GO

### 函数作用域预编译

- 创建Ao对象
- 找形参和声明变量  将变量和形参名 当做AO对象的属性名  值为undefined
- 实参形参相统一
- 在函数体里面找函数声明 值赋予函数体

### 全局作用域预编译

- 创建GO对象
- 找变量声明，将变量和形参名当做GO对象的属性名，值为undefined
- 找函数声明  值赋予函数体

## 类的创建和继承

### 定义

- 是用于创建对象的模板，用代码封装数据 以处理该数据

### 传统方式

- 创建

	- function 类名(agrs){}

		- 定义属性

			- this.变量名=""

		- 定义方法

			- this.方法名=function(){}

		- 原型方法

			- 类名.prototype.属性名=“”
			- 类名.prototype.方法名=function(){}

- 使用

	- let 变量名=new 类名

- 继承

	- 原型链继承

		- 基于原型链，既是父类的实例，也是子类的实例，无法实现多继承

	- [call方法构造函数继承](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call#%E4%BD%BF%E7%94%A8_call_%E6%96%B9%E6%B3%95%E8%B0%83%E7%94%A8%E7%88%B6%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)

		- 使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类，不继承原型上的实例
		- 可实现多继承
		- 只能继承父类实例的属性和方法，不能继承原型上的属性和方法

	- 组合继承（原型链继承和call方法构造函数组合）

		- 通过调用父类构造，继承父类的属性并保留传参的优点
		- 然后通过将父类实例作为子类原型，实现函数复用
		- 优点

			- 可继承父类的实例属性和方法，也可以继承原型属性方法

		- 缺点

			- 调用了两次父类构造函数，生成了两份实例

	- 寄生继承（推荐）

		- 通过寄生的方式，砍掉父类的实例属性
		- 这样在调用两次父类的构造时，就不会初始化两次实例方法/属性

### [ES6](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)

- 创建

	- 先声明

		- [函数声明会提升，类不会](https://developer.mozilla.org/zh-CN/docs/Glossary/Hoisting)

		- 匿名
		- 命名

	- 再使用

		- new l类名

- 继承

	- 使用extends扩展子类
	- 如果子类中定义了构造函数，那么它必须先调用 super() 才能使用 this 。

## 如何解决异步回调问题

### promise

### ES7 的async await

### generator

## 说说前端中的事件流

### 什么是事件流

- 描述的是从页面中接受事件的顺序

### DOM 2级事件流包括三个阶段

- 事件捕获阶段
- 事件目标阶段
- 事件冒泡阶段

### addEventListener

- 是DOM 2级事件新增的指定事件处理程序的操作
- 有三个参数

	- 要处理的事件名 click mouseover
	- 触发事件需要执行的动作
	- 布尔值（定义元素触发顺序）

		- true

			- 表示在捕获阶段调用事件处理程序

				- 外部元素先触发

		- false

			- 表示冒泡阶段调用事件处理程序

				- 内部元素先触发

## [如何让事件先冒泡后捕获](http://caibaojian.com/javascript-capture-bubble.html)

### 基础

- event.stopPropagation()  可以阻止捕获和冒泡阶段中当前事件的进一步传播
- 如果对一个没有子元素的元素同时绑定冒泡和捕获，结果执行事件时遵循Javascript的执行顺序，如果有子元素，则是先执行捕获，然后执行冒泡
- 在冒泡事件和捕获事件同时存在的情况下，捕获事件的优先级高一点
- 在元素上同时绑定捕获事件和冒泡事件，如果通过此元素的子级元素触发，则优先触发捕获事件，若不通过洗元素的子级元素触发，则按照javascript执行顺序触发
- 在同一元素的绑定事件中，冒泡没有次序之分，遵循Javacript的执行顺序

### 解决

- 给同一个元素添加同一个点击事件，第一个事件的第三个个参数为false冒泡，第二个监听事件的第三个参数为true 捕获

### 事件委托

- 定义

	- 不在事件的发生地上设置监听函数，而是在其父元素上监听函数，通过事件冒泡，父元素可以监听子元素上的事件触发，通过判断事件发生元素DOM的类型，来做出不同的响应

- 例子

	- ul和li标签的事件监听

		- 比如我们添加事件的时候，采用事件委托机制，不在li标签上直接添加，而是在ul父元素上添加

- 好处

	- 比较适合动态元素绑定，新添加的子元素也会有监听函数，也可以有事件触发机制

## 图片懒加载和预加载

### 懒加载

- 用到时加载

	- 目的是作为服务器前端的优化，缓解服务器压力

### 预加载

- 提前把所有图片加载好

	- 增加服务器前端压力

## mouseover和mouseenter的区别

### mouseover

- 只要鼠标指针移入（或移出） 事件所绑定的元素或其子元素，都会触发mouseover或mouseout事件

### mouseenter

- 只有鼠标指针移入或移出事件所绑定的元素时，才会触发mouseenter或mouseleave事件

## [Js的new操作符做了哪些事情](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)

### new运算符

- 创建一个用户定义的对象类型的实例或具有构造函数的内置对象实例
- new constructor([argus])

### new关键字会进行如下操作

- 创建一个空的Javascript对象  即{}
- 为创建的空的对象添加属__proto__，将该属性链接至构造函数的原型对象
- 将创建的空对象作为this的上下文
- 如果该函数没有返回对象，则返回this

## 改变函数内部this指针的指向函数

### [Function.prototype.bind()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

- bind()方法创建一个新的函数，这个新函数的this被指定为bind()的第一个参数，而其余参数将作为新函数的参数，供调用时使用
- 返回一个原函数的拷贝，并且拥有指定的this值和初始值

### [Function.prototype.call()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

- 使用一个指定的this值和单独给出一个或多个参数来调用一个函数
- 返回值：使用调用者提供的this值和参数调用该函数的返回值，若 该方法没有返回值，则返回undefined
- 允许为不同的对象分配和调用属于一个对象的函数/方法
- 可以使用call()方法来实现继承
- 与apply()方法类似

### [Function.prototype.apply()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

- 调用一个具体给定this值的函数，以及一个数组形式提供的参数
- 用apply将数组各项添加到另一个数组中

### call()和apply()区别

- call()方法接受的是一个参数列表
- apply()方法接受的是一个包含多个参数的数组

## [js中的各种宽高以及位置](https://www.cnblogs.com/myzhibie/p/4256164.html?utm_source=tuicool)

### Dom对象（只读属性，DOM节点固有属性）

- clientWidth|clientHeight

	- 可视部分的宽高   padding+content
	- 如果没有滚动条，即为元素设定的宽高
	- 如果出现滚动条，滚动条会遮盖元素的宽高，那么该属性就是本来宽高减去滚动条的宽高

- offsetWidth|offsetHeigth

	- 可视部分宽高  border+padding+content的宽高
	- 与滚动条无关
	- 只和本来设定的border以及width和height有关

- clientTop|clientLeft

	- 读取元素的border的宽度和高度的

- offsetTop|offsetLeft

	- 当前元素，相对于其最近的带有定位的父元素的左边距离和上边距离，当前元素的border到包含它的offsetParent的border距离

- scrollHeight|scrollWidth

	- 针对有滚动条的才有意义，就是当元素内部的内容超出其宽度或高度的时候，元素内部内容的实际宽度和高度，注意：滚动条也占宽度

- scrollTop|scrollLeft

	- 指当前元素其中内容超出宽高的时候，元素被卷起的高度和宽度

### Event对象

- clientX|clientY

	- 当事件发生时，鼠标点击位置相对于浏览器（可视区）的坐标

- screenX|screenY

	- 事件发生时，鼠标相对于屏幕的坐标

- offsetX|offsetY

	- 当事件发生时，鼠标点击位置相对于该事件源的位置

- pageX|pageY

	- 事件发生时鼠标点击位置相对于页面的位置
	- 通常浏览器窗口没有出现滚动条时，该属性和event.clientX以及event.clientY是等价的
	- 但是浏览器出现滚动条时，pageX通常会大于clientX 因为页面还存下被卷起来的宽度和高度

### window对象

- Window.innerWidth

	- 窗口内部宽度
	- 如果有滚动条，包含滚动条的宽度

## [js原生拖拽的实现](https://blog.csdn.net/weixin_41910848/article/details/82218243)

### mousedown

### mousemove

### mouseup

## [JS文件异步加载](https://cloud.tencent.com/developer/article/1687951?from=14588)

### defer

- 只适用于外联脚本
- 加载多个，按顺序加载
- 会在DOMContentLoaded和onload事件之前执行

### async

- 只适用于外联脚本
- 异步执行，多个脚本，不能保证顺序
- 在onload之前执行，但不能保证在DOMContentLoaded之前或是之后执行
- 会阻塞load事件

### Script dom element  动态插入一个<script> 标签来加载外部js脚本文件

- 将作为onload事件的回调函数，在页面加载完成后再执行
- 不会阻塞渲染线程

### [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event)

- 当纯HTML被完全加载以及解析时，DOMContentLoaded事件会被触发，而不必等待样式表，图片或者子框架

### [Load](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/load_event)

- 当整个页面以及所有依赖资源入样式表和图片都已经加载完成时，将触发load事件

### 图例

- 

## [防抖和节流和RequestAnimationFrame](https://www.cnblogs.com/coco1s/p/5499469.html)

### 防抖

- 在事件被触发n秒后再执行回调函数，如果在这n秒内又被 触发，则重新计时
- debounce(func,wait)
- 场景应用

	- window的resize
	- scroll
	- 不断的调整浏览器的窗口大小
	- input输入监听

### 节流

- 只允许一个函数在 n 毫秒内执行一次，只有当上一次函数执行后超过了你规定的时间间隔，才能进行下一次该函数 的调用
- throttle(func,wait,mustRun)

### requestAnimationFrame(callback)

- 告诉浏览器您希望执行动画，请求浏览器在下一次重绘之前调用指定的函数来更新动画，该方法使用一个回调函数作为参数，这个回调函数会在浏览器重绘之前被调用
- 16.7ms触发一次handler，降低了可控性，但是提升了性能和精确度
- 用于更复杂的场景时，rAF可能效果更佳

## 垃圾回收机制

### 必要性

- 由于字符串、对象和数组没有固定大小，所以当他们的大小已知时，才能对他们进行动态的分配内存
- Javascript程序每次创建字符串、数组或对象时，解释器都必须分配内存来存储那个实体
- 只要像这样动态的分配了内存，最终都要释放这些内存以便他们能够再用，否则JavaScript的解释器将会消耗完系统中所有可用的内存

### 标记清除

- 垃圾回收器，在运行时会给存储在内存中的所有变量都加上标记
- 当变量进入环境时，将这个变量标记为“进入环境”，当变量离开环境时，则将其标记为“离开环境"并收回内存

### 引用次数

- 当这个引用形变量的次数为0时，就会被垃圾收集器运行时，释放掉

## eval()是做什么的

### 功能

- 将字符串解析成Js并执行

### 为什么不推荐使用

- 可读性差
- 会增加性能优化
- 不安全，可能会引起XXS攻击

## [前端模块化](https://www.cnblogs.com/chenwenhao/p/12153332.html)

### 一个文件就是一个模块，有自己的作用域，只向外暴露特定的变量和函数，提高代码的复用率

### commonJs

- nodeJS是commonJs规范的主要实践者
- module、exports、require、global
- 实际用module.exports定义当前模块对外输出的接口
- 在服务端，模块文件都存放在本地磁盘，读取非常快
- 但是在浏览器端，限于网络原因，更合理的方案是使用异步加载

### AMD

- require.js
- 采用异步方式加载模块，模块的加载不影响它后面语句的运行
- 所有依赖这个模块的语句，都定义在一个回调函数中。等加载完之后，这个回调函数才会运行
- 使用require.config()指定引用路径
- 用definde()定义模块
- 用require()加载模块
- 依赖前置，提前执行

### CMD

- seaJS
- 与AMD类似  依赖就近，延迟执行

### ES6 Module

- ES6在语言标准层面上，实现了模块化功能
- 实现得相当简单，旨在成为浏览器和服务器通用的模块解决方案
- export用于规定模块的对外接口
- import命令用于输入其它模块提供的功能

### AMD和CMD的区别

- 都是并行加载js文件
- AMD是预加载，一开始就把所有要用到的模块加载完
- CMD是懒加载，用到再加载
- AMD优点：加载快速，尤其遇到多个大文件，因为并行解析，同一时间可以解析多个文件
- AMD缺点：并行加载，异步处理，加载顺序不一定
- CMD优点：只有在使用时才加载，每个JS文件的执行顺序是可控的
- CMD执行等待时间会叠加，每个文件执行时是同步执行，因此时间是所有文件解析执行时间之和

### ES6模块与CommonJS模块的差异

- CommonJs模块输出的是一个值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值
- ES6模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在模块，原始值变了，加载的值也会跟着变
- commonJs运行时加载

	- commonJS模块就是对象，即在输入时是先加载整个模块，生成一个对象，然后从这个对象上面读取方法

- ES6模块是编译时输出接口

	- ES6模块不是对象，是通过export命令显示指定输出的代码，而不是加载整个模块，模块内部引用的变化，会反映在外部

## [Js对象深度克隆实现](https://blog.csdn.net/u014607184/article/details/52749332)

### js中的数据类型

- 原始类型

	- 数值
	- 字符串
	- 布尔值
	- null
	- undefined

- 对象类型

	- 函数

		- 函数对象克隆之后会单独复制一次并存储实际数据，不会影响之前的对象，可采用简单的 =即可完成克隆

	- 对象（Object） 只是简单的数组和对象   不包含包装对象
	- 数组（Array）

### 实现js中所有对象的深度克隆

- 对象

	- 包装对象

		- Number
		- String
		- Boolean

	- Date对象
	- 正则对象

- 基础知识

	- [valueOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/valueOf)

	- 所有对象都有一个valueOf()方法
	- 返回被某种类型包装的原始值
	- 如果存在任意原始值，它就默认将对象转换为表示它的原始值

### 代码

- 

## [js监听属性的改变](https://www.jianshu.com/p/fce3a6a9f920)

### [ES5](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

- Object.defineProperty(obj,prop,descriptor)

### [ES6](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

- new Proxy(target,handler)

## [如何实现一个私有变量，用 getName 方法可以访问，不能直接访问](https://www.cnblogs.com/ff-upday/p/15146403.html)

## js中的==和===和Object.is

### ==等同

- 在判断是否相等之前，先进行类型转换  “”==false   为true 

### ===全等

- 不会进行类型转换，类型不同就是false
- 先判断类型，再判断值是否相同  +0=-0
- 注意：如果两值至少有一个是NaN那么不相等  NaN===NaN 为false

### Object.is(value1,value2)

- 判断机制和===相似
- 不过有两处不同

	- Object.is(-0,+0)  false
	- Object.is(Number.NaN=NaN) true

## [null和undefined的区别](https://www.jianshu.com/p/7514e2d56661#:~:text=null%20%E5%92%8C%20undefined%20%E5%9F%BA%E6%9C%AC%E5%90%8C%E4%B9%89%EF%BC%8C%E4%BA%8C%E8%80%85%E5%8F%88%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB%E5%91%A2%EF%BC%9F%20null%E8%A1%A8%E7%A4%BA%E6%B2%A1%E6%9C%89%E5%AF%B9%E8%B1%A1%EF%BC%8C%E5%8D%B3%E8%AF%A5%E5%A4%84%E4%B8%8D%E5%BA%94%E8%AF%A5%E6%9C%89%E5%80%BC,1%EF%BC%89%20%E4%BD%9C%E4%B8%BA%E5%87%BD%E6%95%B0%E7%9A%84%E5%8F%82%E6%95%B0%EF%BC%8C%E8%A1%A8%E7%A4%BA%E8%AF%A5%E5%87%BD%E6%95%B0%E7%9A%84%E5%8F%82%E6%95%B0%E4%B8%8D%E6%98%AF%E5%AF%B9%E8%B1%A1%202%EF%BC%89%20%E4%BD%9C%E4%B8%BA%E5%AF%B9%E8%B1%A1%E5%8E%9F%E5%9E%8B%E9%93%BE%E7%9A%84%E7%BB%88%E7%82%B9%20undefined%E8%A1%A8%E7%A4%BA%E7%BC%BA%E5%B0%91%E5%80%BC%EF%BC%8C%E5%8D%B3%E6%AD%A4%E5%A4%84%E5%BA%94%E8%AF%A5%E6%9C%89%E5%80%BC%EF%BC%8C%E4%BD%86%E6%B2%A1%E6%9C%89%E5%AE%9A%E4%B9%89%201%EF%BC%89%E5%AE%9A%E4%B9%89%E4%BA%86%E5%BD%A2%E5%8F%82%EF%BC%8C%E6%B2%A1%E6%9C%89%E4%BC%A0%E5%AE%9E%E5%8F%82%EF%BC%8C%E6%98%BE%E7%A4%BA)

### null

- 表示没有对象，即该处不应该有值
- 作为函数参数，表示该函数的参数不是对象
- 作为对象原型链的终点

### undefined

- 表示缺少值，即此处应该有值，但没有定义
- 类型检测到它是Number类型
- 定义了形参，没有传实参，显示undefined
- 对象属性名不存在时，显示undefined
- 函数没有写返回值，即没有写return 拿到的是undefined
- 写了return 但没有赋值，拿到的是undefined

### null和undefined比较==

- 在javascript规范中提到，要比较相等之前，不能将null和undefined转换成其它值，并且规定null和undefined是相等的

## [不同数据类型的值比较，是怎么转换的，有什么规则](https://blog.csdn.net/wulove52/article/details/84972152)

## 

自身做布尔运算的时候

- 除了“” 0 NaN null undefined false为false其它都为true
- 会先把后面的值去布尔，然后再取反，最后比较

## [暂时性死区 （ temporal dead zone，简称TDZ ）](https://blog.csdn.net/nicexibeidage/article/details/78144138)

> 当我们先访问一个变量，再声明这个变量，使用let和var申明的变量控制台报的结果前者是错误，后者返回一个undefined

> 当一个新的作用域进行实例化时，在此作用域中用let/const声明的变量会先在作用域中被创建，但因此还未进行词法绑定，所以是不能访问的，如果访问就会抛出错误，因此在变量创到词法绑定的过程就称为暂时性死区

> 总结：变量的声明必须在使用之前

## [Symbol](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

- 是一种基本数据类型

- 代表用给定的名称作为唯一标识

- 就算给定的名称一样生成的值也不一样

每个从Symbol()返回的symbol值都是唯一的

一个symbol值能作为对象属性的标识符

直接使用Symbol()来创建一个新的symbol类型

## 箭头函数的特性

- this的指向与函数执行无关只与声明有关，也就是说，箭头函数的this值指向声明它的非箭头函数的this

- this的值就是函数创建时所在的词法作用域

- this指向的是定义时的this不是执行时的this

- 箭头函数没有自己的aruguments对象，但是可以访问外围的函数的arguments

- 不能通过new关键字调用

## [DOM0~3事件区别](https://blog.csdn.net/weixin_41054156/article/details/88850585)

### DOM0级事件具有极好的跨浏览器优势

- 通过on+监听事件直接对元素绑定
- 可以写在script标签里面，也可以直接给dom元素添加
- 相同事件会被覆盖
- 删除DOM0事件处理程序，只要将对应事件属性设为null即可

### DOM1中一般只有设计规范没有具体实现

### DOM2事件通过addEventListener绑定事件

- 可以给同一个元素绑定多个相同类型事件，先绑定的先执行，后绑定的后执行，不会覆盖前面的
- 通过removeEventListener删除事件处理程序
- 函数的最后一个参数可以执行事件执行顺序为冒泡还是捕获，默认false冒泡执行(内部元素执行完再执行外部元素)，true为事件捕获（外部元素执行完，再执行内部元素）

### DOM3

- 在DOM2事件的基础上添加了更多的事件类型，同时也允许自定义事件类型

	- keydown
	- keypress
	- blur
	- focus
	- load
	- scroll

## 怎样获取对象上的属性

- Object.keys()

- Object.getOwnPropertyNames()

- for(let item in obj)

### 获取数组的值

- for(let item of arr)

## [ES6常用新特性](https://zhuanlan.zhihu.com/p/26589735)

### 函数默认值

- 可以直接在形参中赋值，即为默认值

### 模板字符串

- ``结合${变量使用}

### 解构赋值

### 块级作用域

- let/const

### 新的数据类型

- symbol

### 新的数据结构

-  new Set
- new Map
- new Symbol

### 新增库函数

- Number

	- isInteger() 判断是否是整数
	- isNaN() 判断是否为NaN

- String

	- includes() 判断一个字符串中是否存在指定的字符串
	- repeat() 重复一个字符串生成一个新的字符串
	- startWith() 判断一个字符串是否以指定字符串开头  可以传入一个整数作为第二个参数，用来设置查找的起点
	- endWith() 与startWith相反

- Array

	- from()方法  

		- 可将一个类数组对象转换成一个真正的数组

	- fill()方法

		-  用来填充一个数组，第一个参数为将要被填充的值，可选第二个参数为填充起始索引（默认为0），可选第三个参数为填充终止索引（默认填充到数组的末端）

	- findIndex() 

		- 用来查找指定元素的索引值，参数为函数，输出符合该条件的元素索引值

	- entries()

		- 返回对应键值对遍历器

	- keys()

		- 放回键遍历器

	- values()

		- 放回值遍历器

- Object

	- assign()

		- 合并两个对象（这种合并是浅拷贝）

- Math

	- sign()

		- 判断一个函数的正负

	- trunc()

		- 取数值的整数部分

### 箭头函数

- 共享父级this对象
- 共享父级arguments
- 不能当做构造函数
- 语法

	- 当箭头函数的入参只有一个可以省略入参括号
	- 当入参多于一个或没有入参时必须写括号
	- 当函数体只有一个return语句时可以省略函数体的花括号与return 关键字

### rest参数

- ...args，用于获取多余的参数

### 解决异步回调问题

- promise
- generator

### 类&继承

- 通过class可以很好的面向对象编程

### 模块

- export 用于规定模块的对外接口
- import  用于输入其它模块提供的功能

## 事件代理

> 利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的事件

> 把事件添加到本来要添加事件的父元素上，将事件委托给父元素来触发处理函数，如果这个父元素下有大量同级元素需要添加同一事件，这个样的话就可以减少事件绑定

> 可以用于动态添加多个同级元素

> 减少内存消耗，动态绑定事件

## setTimeout和setInterval和rAF（requestAnimationFrame）

### [setInterval](https://www.cnblogs.com/joe235/p/13402282.html#:~:text=%E5%BD%93%E7%84%B6%E4%B9%9F%E5%8F%AF%E4%BB%A5%E7%94%A8%20setInterval%20%28%29%20%E6%9D%A5%E6%A8%A1%E6%8B%9F%20setTimeout%20%28%29%20%EF%BC%8C%E5%85%B7%E4%BD%93%E4%BD%BF%E7%94%A8%E9%82%A3%E4%B8%AA%EF%BC%8C%E4%BB%A5%E5%85%B7%E4%BD%93%E7%9A%84%E9%9C%80%E6%B1%82%E5%92%8C%E5%9C%BA%E6%99%AF%E5%85%B7%E4%BD%93%E5%88%86%E6%9E%90%EF%BC%8C%E5%B0%B1%E5%83%8Ffor%E5%BE%AA%E7%8E%AF%E5%8F%AF%E4%BB%A5%E6%A8%A1%E6%8B%9F%E6%89%80%E6%9C%89%E7%9A%84%E5%BE%AA%E7%8E%AF%E4%B8%80%E6%A0%B7,%28%E5%8C%85%E6%8B%AC%E5%88%86%E6%94%AF%EF%BC%8C%E4%BB%A5%E5%8F%8Ado%20while%E4%B8%80%E6%A0%B7%29%E3%80%82.%20%E4%B8%80%E8%88%AC%E6%83%85%E5%86%B5%E4%B8%8B%20setTimeout%20%28%29%20%E7%94%A8%E4%BA%8E%E5%BB%B6%E8%BF%9F%E6%89%A7%E8%A1%8C%E6%9F%90%E6%96%B9%E6%B3%95%E6%88%96%E5%8A%9F%E8%83%BD%EF%BC%9BsetInterval%20%28%29%20%E5%88%99%E4%B8%80%E8%88%AC%E7%94%A8%E4%BA%8E%E5%88%B7%E6%96%B0%E8%A1%A8%E5%8D%95%EF%BC%8C%E5%AF%B9%E4%BA%8E%E4%B8%80%E4%BA%9B%E8%A1%A8%E5%8D%95%E7%9A%84%E5%81%87%E5%AE%9E%E6%97%B6%E6%8C%87%E5%AE%9A%E6%97%B6%E9%97%B4%E5%88%B7%E6%96%B0%E5%90%8C%E6%AD%A5%E3%80%82.)

- 按照指定的时间来调用函数计算表达式
- 直到clearInterval()被调用或窗口关闭
- 循环执行的
- 定时器指定的时间间隔，表示的是何时将定时器的代码添加到消息队列中，而不是何时执行代码
- 图例

	- 

- 由于Js引擎的单线程，可能会网络延迟，进程阻塞，导致，真正执行代码的时间有偏差
- 取决于何时被主线程的事件循环渠道，并执行
- 一般用于刷新表单

### setTimeout

- 在指定毫秒数后再调用函数或者计算表达式
- 只执行一次
- 一般用于延迟执行某方法或功能

### [requestAnimationFrame](https://www.cnblogs.com/xiaohuochai/p/5777186.html)

- 不需要设置时间间隔，采用系统时间间隔
- 保持最佳绘制效率，不会因为间隔时间过短，造成过度绘制，
- 也不会因为间隔时间太长，使用动画卡顿不流畅
- 用法和setTimeout相似，就是不用设置时间
- 特点

	- 会把每一帧中的所有DOM操作集中起来，再一次重绘或回流中完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率
	- 在隐藏或不可见的元素中，将不会进行重绘或回流
	- 如果页面不是激活状态下，动画会自动暂停，有效节省了CPU的开销

### 浏览器是个多应用进程

- Browser进程

	- 浏览器的主线程
	- 作用

		- 负责浏览器界面显示，与用户交互，如前进后退
		- 负责各个页面管理，创建和销毁其它进程
		- 将Renderer进程存到内存中的Bitmap，绘制到用户界面
		- 网络资源的管理，下载等

- 第三方插件进程

	- 每种类型的插件对应一个进程，仅使用该插件时，才创建

- GPU进程

	- 最多一个，用于3D绘制等

- 浏览器内核

	- 浏览器渲染进程，它内部是多线程的，默认每个tab页面一个进程，互不影响
	- 作用

		- GUI渲染线程
		- JS引擎线程

			- 负责解析JS脚本，运行代码

		- 事件触发线程

			- 归属于浏览器而不是JS引擎，用来控制事件循环，当JS引擎执行代码如setTimeout时，会将对应任务添加到事件线程中，由于js单线程的关系，所以这些待处理队列中的事件都得排队等待js引擎处理

		- 定时器触发线程

			- 因为js引擎是单线程的，如果处于阻塞线程状态就会影响计时的准确，计时完毕，添加到事件队列中，等待JS引擎空闲后执行

		- 异步http请求线程

## [自己实现个bind函数](https://blog.csdn.net/lovefengruoqing/article/details/80186401#:~:text=%E7%AE%80%E5%8D%95%E7%82%B9%E7%90%86%E8%A7%A3%EF%BC%8Cbind%20%E5%B0%B1%E6%98%AF%E7%94%A8%E6%9D%A5%E7%BB%91%E5%AE%9A%E4%B8%8A%E4%B8%8B%E6%96%87%E7%9A%84%EF%BC%8C%E5%BC%BA%E5%88%B6%E5%B0%86%E5%87%BD%E6%95%B0%E7%9A%84%E6%89%A7%E8%A1%8C%E7%8E%AF%E5%A2%83%E7%BB%91%E5%AE%9A%E5%88%B0%E7%9B%AE%E6%A0%87%E4%BD%9C%E7%94%A8%E5%9F%9F%E4%B8%AD%E5%8E%BB%E3%80%82%20%E4%B8%8E%20call%20%E5%92%8C,apply%20%E5%85%B6%E5%AE%9E%E6%9C%89%E7%82%B9%E7%B1%BB%E4%BC%BC%EF%BC%8C%E4%BD%86%E6%98%AF%E4%B8%8D%E5%90%8C%E7%82%B9%E5%9C%A8%E4%BA%8E%EF%BC%8C%E5%AE%83%E4%B8%8D%E4%BC%9A%E7%AB%8B%E5%8D%B3%E6%89%A7%E8%A1%8C%EF%BC%8C%E8%80%8C%E6%98%AF%E8%BF%94%E5%9B%9E%E4%B8%80%E4%B8%AA%E5%87%BD%E6%95%B0%E3%80%82%20%E5%9B%A0%E6%AD%A4%E6%88%91%E4%BB%AC%E8%A6%81%E6%83%B3%E8%87%AA%E5%B7%B1%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%20bind%20%E5%87%BD%E6%95%B0%EF%BC%8C%E5%B0%B1%E5%BF%85%E9%A1%BB%E8%A6%81%E8%BF%94%E5%9B%9E%E4%B8%80%E4%B8%AA%E5%87%BD%E6%95%B0%EF%BC%8C%E8%80%8C%E4%B8%94%E8%BF%99%E4%B8%AA%E5%87%BD%E6%95%B0%E4%BC%9A%E6%8E%A5%E6%94%B6%E7%BB%91%E5%AE%9A%E7%9A%84%E5%8F%82%E6%95%B0%E7%9A%84%E4%B8%8A%E4%B8%8B%E6%96%87%E3%80%82)

### <img src="http://tva1.sinaimg.cn/large/007WWC4aly1gxh3tn5ezij30pw0mcjwz.jpg" alt="image-20211217202823655.png" style="zoom: 50%;" />

## [自己实现call()和apply方法](https://zhuanlan.zhihu.com/p/83523272)

### call和 apply是用来做什么的

- 改变this指向
- 调用别的对象的方法
- 调用函数，因为apply,call方法会立即执行

## 

## [this](https://zhuanlan.zhihu.com/p/82504422)

### 默认绑定

- 非严格模式下，this就是全局对象
- 如果是（use strict）严格模式下this就是undefined

### 隐式绑定

- 谁调用这个方法，this就指向谁

### 显示绑定

- call()
- apply()
- bind()

### 关键字new

- 创建一个空对象
- 把这个对象链接到原型对象上
- this指向这个对象
- 如果函数不返回任何东西，那么默认返回this

### 箭头函数

- 会无视以上所有规则，this的值就是函数创建所在的词法作用域（lexical scope）,和调用方式无关
- 箭头函数中的this指向的是定义时的this，而不是执行时的this

## setTimeout相互实现setInterval

## js控制一次加载一张图片，加载完成后再加载下一张

### 基础知识

- [new Image()](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLImageElement/Image)

	- 功能等价于document.createElement('img)

- [GlobalEventHandlers.onload](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers/onload)

	- 事件处理程序，用于处理window XMLHttpRequest ,<img>等元素的加载事件，当资源已被加载时被触发
	- window.onload=func
	- img.onload=func

### 方法

- onload()
- [onreadystatechange()与readyState  (经测试，似乎行不通)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/readyState)

## 代码执行顺序

### 基础知识

- event loop(事件循环)

	- 是指主线程从任务队列中循环读取任务

- 首先执行主线程中的同步任务，当主线程任务执行完毕后，再从事件循环中读取任务
- 事件循环中的执行顺序

	- 宏任务macro-task

		- script(主程序代码)
		- setTimeout
		- setInterval
		- setImmediate
		- I/O
		- UI rendering

	- 微任务micro-task

		- process.nextTick
		- promise
		- Object.observe
		- MutationObserver

	- 首先执行macro-task队列开头的任务
	- 再执行微任务里的所有任务
	- 执行顺序

		- script(主程序代码)
		- process.nextTick
		- Promise
		- setTimeout
		- setInterval
		- setImmediate
		- I/O
		- UI rendering

## [简单实现一个promise](https://github.com/forthealllight/blog/issues/4)

### [基础知识](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

- 是一个对象
- 用于表示一个异步操作的最终完成（或失败）及其结果值
- promise的三种状态

	- 
	- pending 待定

		- 初始转态，既没有被兑现，也没有被拒绝

	- fullfilled 已兑现 

		- 意味着操作成功完成

	- rejected 已拒绝

		- 意味着操作失败

- [then()方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

	- 最多接受两个参数

		- promise的成功情况的回调函数

			- then(fullfilled)

		- promise的失败情况的回调函数

			- then(rejected)

	- 返回一个promise

- Promise/A+规范

	- 术语

		- promise是一个对象或者函数，该对象或者函数有一个then()方法
		- thenable是一个对象或者函数，用来定义then()方法
		- value是promise状态成功时的值
		- reason是promise状态失败时的值

	- 要求

		- 一个promise必须有三个状态

			- pending
			- fulfilled
			- rejected
			- 当处于pending状态的时候，可以转移到fulfilled或者rejected状态
			- 当状态处于fulfilled或者rejected就不可变了
			- promise的中文以为承诺，也就是说promise的状态一旦发生改变，就永远是不可逆的

		- 一个promise必须要有一个then()方法
		- then()方法接受两个参数
		- then()方法必须放回一个promise

- 实现代码

	- 

## [async和await](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Asynchronous/Async_await#asyncawait_%E5%9F%BA%E7%A1%80)

### async

- 放到函数声明之前，使其成为异步函数
- async关键字将函数转换为promise
- 调用该异步函数会返回一个promise

### await

- 只在异步函数中才起作用
- 可以放在任何异步的基于promise的函数之前
- 会暂停代码在该行上，直到promise完成，然后返回结果值
- 在暂停的同时，其它正在等待执行的代码就有机会执行了

## Function._proto_(getPrototypeOf)是什么？

### 基础知识

- [Object.create()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

	- 创建一个新的对象
	- 使用现有的对象来提供新创建的对象的__proto__

- __proto__（隐式原型）

	- 隐式原型指向创建这个对象的函数（constructor）的prototype(显示原型)
	- 作用：构成原型链，同样用于实现基于原型的继承，例如：当我们访问obj这个对象的x属性时，如果在ob找不到，那么就会沿着__proto__一次查找
	- 是每个对象都有的属性

- prototype (显示原型)

	- 每个函数在创建之后会拥有一个名为prototype的属性，这个属性指向函数的原型对象
	- 用来实现基于原型的继承与属性的共享
	- 函数才会有的属性
	- 原型也是一个对象，这个对象里面有个constructor的属性

- Object.getPrototypeOf()

	- 返回指定对象的原型

- 测试

	- Function.prototype还是Function
	- Function.prototype.__proto__是对象
	- Object.prototype是对象
	- Object.__proto__是函数
	- 对象的原型是null

### prototype和__proto__区别

- 图例

	- 

## JS判断类型的方式

### typeof

### instanceof

### [Object.prototype.toString.call(obj)](https://blog.csdn.net/hanyanshuo/article/details/104620122)

- 可以精准的判断所传入参数的数据类型
- 这句代码的意思是让我们用Object原型上的toString方法作用在传入的obj的上下文中(通过call将this指向obj)
- 其实不同的数据类型都有其自身的toString()方法
- 各数据类型使用toString()后的结果不一的原因在于：所有类在继承Object的时候，改写了toString()方法

## 数组

### 数组常用方法

- pop()
- push()
- shift()
- unshift()
- splice()
- slice
- [map()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

	- 创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值
	- 返回值：一个由原数组每个元素执行回调函数的结果组成的新数组

- [forEach()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

	- 对数组每个元素执行一次给定的函数
	- 返回值：undefined

- [reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

	- 对数组中的每个元素执行一个由您提供的reducer函数，将其结果汇总为单个返回值
	- 接受四个参数

		- accumlator 累机器
		- current value 当前值
		- current Index 当前索引 (可选)
		- source array 源数组（可选）

	- 返回值：函数累计处理结果

- [filter()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

	- 创建一个新数组，其包含通过所提供函数实现测试的所有函数

- [every()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

	- 测试一个数组内的所有元素是否都能通过某个指定函数测试，放回一个布尔值

- [find()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

	- 返回数组中满足提供测试函数的第一个元素的值，否则返回undefined

- [findIndex()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

	- 返回数组中提供的测试函数的第一个元素的索引，若没有找到对应的元素则返回-1

- [indexOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

	- 返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1

- [includes()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

	- 用来判断数组是否包含一个指定的值，如果包含返回true否则返回false

### [数组去重方法](https://zhuanlan.zhihu.com/p/93453613#:~:text=%E7%AC%AC%E4%B8%80%E7%A7%8D%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D%E7%9A%84,%E4%B8%8A%E6%9D%A5%E8%AF%B4%E8%82%AF%E5%AE%9A%E6%98%AF%E5%BE%88%E4%BD%8E)

- 基础知识

	- [Array.from()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

		- 从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例

	- [new Set()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/Set)

		- 创建set对象，可以存储任意类型的唯一值
		- 如果传递一个可迭代对象，它的所有元素将不重复地添加到新的Set中
		- 如果不指定此参数或其值为null则新的set为空

- 去重

	- 对数组本身遍历

		- 
		- 
		- 

	- indexOf

		- 
		- 

	- Object[]

		- 

	- 新特性

		- Array.from(new Set(arr))
		- [...new Set(arr)]

## 事件代理在捕获阶段的实际应用

### 在父元素层面阻止事件向子元素传播

### 代替子元素执行某些操作

## 去除首尾空格

### [String.prototype.trim()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/Trim)

### 正则式

- 基础知识

	- 方法

		- test()

			- 检查一个匹配模式是否存在于字符串中

		- match()

			- 提取找到的实际匹配项

	- |

		- 匹配多个内容

	- .

		- 通用符，匹配任何内容

	- []

		- 与多种可能性匹配

	- -   

		- 连字符，定义要匹配的字符或数字范围（）包含边界
		- 还可以单个字符集中组合一系列字母和数字[a-z0-9]

	- [^]

		- 匹配单个未指定的字符

	- +

		- 匹配连续出现一次或多次的字符或字符组

	- *

		- 匹配出现零次或多次的字符（不需要修饰符）

	- ？

		- 懒惰匹配（会抵消[]*的作用）

	- /^abc/

		- 搜寻字符串的开始位置

	- /abc$/

		- 搜寻字符串末尾的位置

	- \w

		- 匹配所有的字母和数字包括下划线_
		- 相当于[a-zA-Z0-9_]

	- \W

		- 搜寻和\w相反的匹配模式
		- 相当于[^A-Za-z0-9_]

	- \d

		- 查找数字字符的缩写
		- 等同于[0-9]

	- \D

		- 查找非数字字符的缩写
		- 等同于[^0-9]

	- \s

		- 搜寻空格
		- 匹配空格、回车符、制表符、换页符和换行符

	- \S

		- 搜寻非空白字符
		- 此匹配模式将不匹配空格回车符制表符和换行符

	- {数字(上限),数字()下限}

		- 匹配出现上限到下限次字母

	- {数字，}

		- 只指定匹配的下限

	- {数字}

		- 子主题 1

			- 指定匹配的确切数量

	- ？

		- 想要搜寻的匹配模式可能有不确定是否存在的部分
		- 可以使用问号?指定可能存在的元素    
		- 检查前面的零个或一个元素

	- ?=...

		- 查看并确保搜索匹配模式中元素存在，其中...就是需要存在但不会被匹配的部分
		- 先行断言会查看并确保搜索匹配模式中的元素存在

	- ?!...

		- 负向断言---查看并确保搜索匹配模式中的元素不存在

	- ()

		- 检查混合字符组
		- 如果想在字符串找到 Penguin 或 Pumpkin，可以用这个正则表达式：/P(engu|umpk)in/g。

	- [使用捕获组重用模式](https://chinese.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/reuse-patterns-using-capture-groups)

	- [使用捕获组搜索和替换](https://chinese.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/use-capture-groups-to-search-and-replace)

	- [删除开头和结尾的空白](https://chinese.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions/remove-whitespace-from-start-and-end)

		- 

	- 标志（flag）

		- i

			- 匹配时，忽略大小写

		- g

			- 全局匹配（多次搜索或提取匹配模式）

## js语言特性

### 运行环境包括客户端浏览器和Node.js两个

### 基于对象

- 可以创建对象或者使用现有的对象

### 弱类型语言，更加灵活

- 定义变量的时候，并没有指定变量的类型是什么，赋什么样的值，变量就是什么类型的

### 脚本语言，解释性语言

- 不用预编译，直接解析执行代码

### 动态

- 可以直接对用户的输入作出响应，而无须经过客户端，响应是通过事件驱动的方式进行的

### 跨平台性

- 只要能运行支持JS浏览器，那就能运行JS

## 如何判断一个数组

### Object.prototype.toString.call(obj)

### instanceof

### Array.isArray()

### [typeof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

- 不能直接判断是否是数组
- 可以加上限制条件，可以判断一下是否拥有数组的方法
- undefined--"undefined"
- null--"Object"
- Boolean--"bollean"
- Number--"number"
- String--"string"
- Symbol--"symbol"
- function对象--“function”
- 其它任何对象--“object”

## javascript数据类型

### 基本数据类型

- 字符串String
- 数字Number
- 布尔Boolean
- null
- 未定义undefined
- Symbol（ES6引入的原始数据类型，表示独一无二的值）

### 引用数据类型

- 对象（Object）
- 数组Array
- 函数Function

### 区别

- 是否可以添加方法

	- 基本数据类型不可以添加属性和方法
	- 引用类型可以

- 赋值

	- 基本数据类型的赋值是简单的赋值，如果从一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上
	- 引用数据类型的赋值是对象的引用

- 比较

	- 基本数据类型的比较就是值比较
	- 引用类型的比较是引用的比较，比较对象的内存地址是否相同

- 存放位置

	- 基本数据类型存放在栈区
	- 引用数据类型同时存放在栈区和堆区

- 修改值

	- 引用类型的值可以改变
	- 基本数据类型的值不可变的（任何方法都无法改变一个基本数据类型的值，当这个变量重新赋值看起来变量的值是改变了，但是这里的变量名只是指向变量的一个指针，所以改变的是指针的指向改变，该变量是不变的）

## [Js的全排列](https://blog.csdn.net/qq_32682301/article/details/108361463)



## 跨域

### 跨域的原理

- 跨域是指浏览器不能执行其它网站的脚本
- 它是由浏览器的同源策略造成的，是浏览器对javascrip实施的安全限制
- 只要协议、域名、端口有任何一个不同，都被当做是不同的域
- 跨域原理：通过各种方式，避开浏览器的安全限制

### [实现跨域的方法](https://blog.csdn.net/qq_34306360/article/details/80801377)

- 基于script标签
- jquery封装好的ajax
- 内联框架iframe

## 资源加载问题

> 问题：有一个游戏叫做 Flappy Bird，就是一只小鸟在飞，前面是无尽的沙漠，上
>
> 下不断有钢管生成，你要躲避钢管。然后小明在玩这个游戏时候老是卡顿
> 甚至崩溃，说出原因（3-5 个）以及解决办法（3-5 个）

### 内存溢出

- 应该在钢管离开可视区后，销毁钢管，让垃圾回收器回收钢管，因为不断生成的钢管如果不及时清理容易导致内存溢出游戏奔溃

### 资源过大

- 选择图片文件大小更小的文件格式 比如使用webp  png

### 资源加载问题

- 在可视区域之前就预加载好资源，如果在可视区域生成钢管的话，用户就会认为钢管是卡顿后才生成的

### canvas绘制频率问题

- 大部分显示器刷新频率为60次/s，因此游戏的每一帧绘制间隔时间需小于1000/60=16.7ms，才能让用户不觉得卡顿

## 什么是按需加载

> 用户触发了动作时，才加载对应的功能

触发的动作需要看具体业务场景而言

包括，鼠标点击、输入文字、下拉加载内容、鼠标移动，窗口大小更改等

可以是js、css、html、图片等

## 什么是 virtual dom(虚拟DOM)

本质上就是在JS和DOM之间做了一个缓存

用javascript对象结构表示DOM树结构；然后用这个树构建一个真正的DOM树

插到文档中

当状态发生改变的时候，重新构造一颗新的对象树

然后用新的树和旧的树进行比较，记录两棵树的差异，把所记录的差异应用到所构造的真正DOM树上，视图就更新了

### 作用

- 减少DOM操作引起的回流和重绘
- 通过diff 算法，减少 JavaScript 操作真实 DOM 的带来的性能消耗

## webpack

是一个前端构建工具

本质上是一个用于现代javascript应用程序的静态模块打包工具

当webpack处理应用程序时，

它会在内部构建一个依赖图

此依赖图对应映射到项目所需的每个模块

并生成一个或多个包

简单来说，webpack就是一个打包器，他能将多个文件打包成一个文件

解决面向对象开发的模块化带来的页面加载速度慢和js文件加载顺序问题

