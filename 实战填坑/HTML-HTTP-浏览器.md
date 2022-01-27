# HTML|HTTP|浏览器

## 浏览器

### [浏览器的渲染原理](https://github.com/ljianshu/Blog/issues/51)

- 页面加载过程

	- 浏览器根据DNS服务器得到域名的ip地址
	- 向这个IP的机器发送HTTP请求
	- 服务器收到、处理并返回HTTP请求
	- 浏览器得到返回内容

		- 一堆HTML格式的字符串（因为只有HTML格式，浏览器才会正确解析）

- 页面渲染

	- HTML/SVG/XHTML解析

		- DOM树

			- 构建DOM

				- 字节数据
				- 字符串
				- Token
				- Node
				- DOM

	- CSS解析

		- CSS规则树

			- 构建CSSOM

				- 字节数据
				- 字符串
				- Token
				- Node
				- CSSOM

	- javascript解析

		- DOM API

			- 操作DOM Tree

				- 引起阻塞

		- CSSOM API

			- 操作CSSOM

				- 

			- 必须等CSSOM加载构建完毕

				- 为构建完，阻塞

	- 构建渲染树

		- 通过DOM Tree和CSS Rule Tree来构造渲染树  在GUI渲染线程

			- 渲染树只包括需要显示的节点和这些节点的样式信息
			- layout布局和reflow回流

		- 遇到javascript  在js引擎线程

			- 没有defer或async

				- 遇到就加载并执行

			- defer 延迟执行引入的javascript

				- js文件加载与html解析并行
				- html解析完毕且js加载完成后
				- 在DOMContentLoaded事件之前执行
				- 加载多个脚本是有顺序的

			- async 异步执行

				- 加载好了，就会开始执行
				- 加载过程和HTML解析互不干扰
				- 一定会在load触发之前执行  会阻塞load事件 
				- 可能会在DOMContentLoaded触发之后或之前执行
				- 加载多个脚本的时候，是无顺序的

	- 页面绘制

		- 页面重绘

			- 对DOM元素修改导致样式的变化
			- 未影响其几何属性
			- 例如

				- 修改字体颜色
				- 修改背景色

		- 页面重排

			- 对DOM的修改引发了DOM几何尺寸的变化
			- 引起重排

				- 添加或删除可见的DOM元素
				- 内容发生改变
				- 窗口大小发生改变
				- 计算offsetWidth offsetHeight
				- 设置style属性的值

			- 浏览器需要重新计算元素的几何属性
			- 将计算结果绘制出来

		- 重排必重绘，重绘不一定重排

	- 减少重排和重绘

		- 脱离标准流

			- 隐藏属性设置display:none
			- 创建文档片段创建一个子树，然后拷贝到文档中
			- 克隆原始元素，在克隆的元素上进行操作，在用克隆的元素替换原始元素

		- 缓存布局信息
		- 使用transform替代top
		- 不使用table布局

### [浏览器存储](https://github.com/ljianshu/Blog/issues/25)

- cookie

	- 功能

		- 并非存储而是维持状态

	- 产生

		- 使无状态的http保存稳定信息成为可能
		- http是无状态的，服务器不知道用户做了什么
		- 绕开http无状态的额外手段之一
		- 服务器可以设置 读取cookie中包含的信息

	- 介绍

		- 某些网站为了辨别用户身份而存储在用户本地终端上的数据
		- 服务端产生的，客户端进行维护和存储

	- 用途

		- 会话状态用户登录状态、购物车、游戏份数等）
		- 个性化设置（用户自定义设置、主题等）
		- 浏览器行为跟踪（跟踪分析用户行为）

	- 原理及其构成

		- 原理

			- 首次访问网站

				- 浏览器发出请求

					- 服务器生成cookie在响应中通过Set-Cookie头部传递多个值

						- 客户端得到cookie

							- 再次请求  将cookie头部携带至请求中发送给服务器

		- 构成

			- name

				- 唯一标识cookie名称，不区分大小写，必须经过url编码

			- value

				- 存储在cookie中的字符串，必须经过url编码

			- Domain

				- cookie有效域

			- Path

				- 请求url中包含这个路径才会把cookie发送到服务器中

			- Expires/Max-Age

				- cookie过期时间
				- max-age>expires

			- Secure

				- 只在使用SSL安全连接的情况下才会把cookie发送到服务器

			- HttpOnly

				- 不能使用javascript经由 document.cookie属性、XMLHttpRequest和Request APIs进行访问，防止跨站脚本攻击

			- 例：

				- Set-Cookie: name=value; domain=.wrox.com; path=/; secure

	- 生成方式

		- 通过Set-Cookie告知客户端
		- 使用javascript（document.cookie）

			- document.cookie='myname=xiaomin;path=/;domain=.baidu.com'

	- 缺陷

		- 不够大

			- 每个cookie的大小为4kb
			- 每个站点的cookie一般来说不超过300个

		- 过多的cookie会带来巨大的性能问题

			- cookie是与特定的域绑定的
			- 同一个域下的所有请求，都会携带cookie

		- 在http中cookie是明文传递，安全性问题，除非用https

	- cookie与安全

		- value

			- 如果用于保存用户登录转态，应该将该值进行加密，不能使用明文的用户标识

		- http-only

			- 不能通过js访问，减少跨站攻击XSS攻击

		- secure

			- 只能在协议为https的请求中携带

		- same-site

			- 规定浏览器不能在跨域请求中携带cookie.减少CSRF攻击

- webStorage

	- localeStorage

		- 数据可长期存储，除非手动删除
		- 要访问同一个localStorage对象，页面必须来自同一个域，同一个端口上使用相同协议

	- sessionStorage

		- 只存储会话数据，浏览器关闭就会释放
		- 相同端口 域名 不同窗口是无法进行数据共享
		- 存储数据 sessionStorage.setItem('user_name','xiaobai')
		- 读取数据 sessionStorage.getItem('user_name')
		- 删除某一键名对应的数据 sessionStorage.removeItem('user_name')
		- 清空数据记录  sessionStorage.clear()

- webStorage和cookie区别

	- 共同点

		- 都保存在浏览器端，且都遵循同源策略

	- 不同点

		- 数据的生命周期

			- cookie 可设置失效时间，否则默认为关闭浏览器后失效
			- sessionStorage 仅在当前浏览器会话下有效，关闭浏览器后失效
			- localStorage 一直有效，除非手动删除

		- 作用域不同

			- cookie和localeStorage在所有同源窗口都是共享的
			- sessionStorage不在不同的浏览器窗口共享

		- 存储数据大小不同

			- cookie数据不能超过4K
			- webStorage虽然也有限制，但是比cookie大得多，可以达到5M或更大

		- http请求

			- cookie每次都会携带在http头部中，过多的使用，会带来性能问题
			- webStorage保存在浏览器中，不参与服务器的通信

		- 易用性

			- cookie需要程序员自己封装，原生的cookie接口不友好
			- webStorage可以采用原生的接口，也可再次封装

- [Cookie和Session](https://www.jianshu.com/p/2f7031a69f43)

	- 存储位置不同

		- cookie数据存放在客户端的浏览器上
		- session数据放在服务器上

	- 存储容量不同

		- cookie保存的数据不能超过4K
		- session并没有上限

	- 存储方式不同

		- cookie只能保管ASCII字符串，并需要通过编码方式存储为Unicode字符或二进制数据
		- session中能存储任何类型的数据

	- 安全性

		- session相对于cookie要安全些
		- cookie对客户端是可见的
		- session存储在服务器，客户端无法看到

	- 有效期不同

		- 可以通过设置cookie属性，达到使cookie长期有效的效果
		- session只需要关闭窗口就会失效

	- 服务器压力不同

		- cookie不占用服务器资源
		- session是保管在服务器中 占用服务器资源

- indexedDB

### 浏览器的缓存机制

- 缓存位置

	- Services Worker 

		- 运行在浏览器背后的独立线程
		- 传输协议必须是https
		- 缓存功能

			- 注册
			- 监听install
			- 拦截请求

		- 没有在service worker中命中请求的话，会根据缓存查找优先级去查找数据，不管是从哪里获取道德，浏览器都会显示是从service worker中获取的内容

	- Memory Cache

		- 内存中缓存
		- 关闭tab页面，内存中的缓存就被释放了
		- 包含

			- 当前页面已经抓取到的资源
			- 页面已下载的样式、脚本、图片

		- 读取数据快
		- 缓存持续时间短

	- Disk Cache

		- 硬盘中的缓存
		- 读取速度慢
		- 什么都能存储到磁盘中
		- 容量大

	- Push Cache

		- 是http2中的内容
		- 以上三种情况都没有命中时，才会被使用
		- 只在会话中存在，一旦会话结束就别释放
		- 缓存时间短

- 缓存过程

	- 

- 强缓存

	- 不会向服务器发送请求，直接从缓存中读取资源
	- http header

		- Expires

			- 缓存过期时间，指定资源到期时间
			- 是http1.0产物

		- Cache-Control

			- 是http1.1产物
			- public

				- 响应可以被客户端和代理服务器缓存

			- private

				- 响应只可以被客户端缓存

			- max-age=30

				- 缓存30秒后就过期

			- s-maxage=30

				- 覆盖max-age，只在代理服务器中生效，和max-age作用一样

			- no-store

				- 不缓存任何响应

			- no-cache

				- 资源被缓存，但是立即失效，下次会发起请求验证资源是否过期

			- min-fresh=30

				- 希望30s内获取最新响应

			- max-stale=30

				- 30秒该缓存内，即使缓存过期，也使用

		- 对比

			- expires是http1.0的产物
			- cache-control是http1.1的产物
			- 同时存在的话，cache-control的优先级高于expires

- 协商缓存

	- 强制缓存失效
	- 浏览器携带缓存标识，向服务器发起请求
	- 由服务器根据缓存标识决定是否使用缓存
	- 协商缓存的过程

		- 生效，返回304和not modified

			- 

		- 失效，放回200和请求结果

			- 

		- http header

			- Last-Modified和If-Modified-Since

				- 服务器在返回资源的同时，在response header中添加Last-Modified的header,值是这个资源在服务器最后修改的时间

					- 

				- 弊端

					- 仅仅只是打开缓存文件，未修改文件，还是会造成Last-Modified被修改
					- 以秒计时，无果在不可感知的时间内修改完成文件，那么服务器会认为资源还是命中了，不会返回正确的资源
					- 根据最后一次修改时间计算

			- ETag和If-None-Match

				- 是服务器响应请求时，返回当前资源文件的唯一标识（服务器生成）
				- 只有资源变化，Etag就会重新生成
				- 过程

					- 

			- 对比

				- 精度上

					- Etag要优于Last-Modified

				- 性能上

					- Etag要逊于Last-Modified，Last-Modified只需记录时间，而Etag需要服务器通过算法来计算出一个hash值

				- 优先级上

					- 服务器校验优先考虑Etag

- 缓存机制

	- 强制缓存优先于协商缓存
	- 若强制缓存Expires和Cache-Control生效则直接使用缓存，不生效则进行协商缓存
	- 协商缓存由服务器决定是否生效

		- 资源有更新

			- 重新返回资源和缓存标识，并存入缓存中

		- 资源无更新

			- 304，继续使用缓存

	- 图解

		- 

- 实际场景应用缓存策略

	- 频繁变动的资源

		- Cache-Control:no-cache

	- 不常变化的资源

		- Cache-Control:max-age=3153600

- 用户行为对浏览器缓存的影响

	- 用户在浏览器如何操作时，会触发怎样的缓存策略

		- 打开网页

			- 地址栏输入地址，查找disk cache中是否有匹配。有 则使用，无则发送网络请求

		- 普通刷新（F5）

			- Tab没有关闭，memory cache是可用的,会被优先使用，其次才是 disk cache

		- 强制刷新 Ctrl+F5

			- 浏览器不是使用缓存
			- 发送请求头都带有Cache-Control：no-cache
			- 服务器直接返回200和最新内容

### 从输入url到页面渲染到底发生了什么

- url组成

	- scheme://host.domain:port/path/filename
	- scheme:协议
	- host-主机，http默认主机是www
	- domain-定义因特网的域名
	- port-定义主机上的端口
	- path-定义服务器上的路径
	- filename-定义文档/资源的名称

- 过程

	- DNS解析（域名解析）

		- 产生原因

			- 浏览器不能直接通过域名找到对应的服务器,而是要通过ip地址
			- ip地址由32位二进制组成
			- 域名是ip的伪装，是为了方便记忆和理解
			- 域名解析成ip地址->DNS

		- 域名解析

			- 浏览器把域名发送给DNS服务器，DNS服务器通过域名查找ip地址，返回给浏览器

		- 浏览器如何通过域名去查询对应的IP

			- 浏览器缓存
			- 操作系统缓存
			- 路由缓存
			- ISP(Internet Service Provice)互联网服务提供商
			- 根服务器

		- 图解

			- 

	- TCP连接（TCP三次握手）

		- 图解

			- 

		- 过程

			- 第一次握手，浏览器发起，告诉服务器我要发送请求了
			- 第二次握手，服务器发起，告诉浏览器，我准备接收了，你赶紧发送吧
			- 第三次握手，浏览器发起，告诉服务器，我马上就发了，准备接收吧

		- 为啥要三次握手

			- 为了防止已经失效的连接请求报文段又传送到了服务端，因而产生错误

	- 发送http请求

		- 请求报文

			- 请求行

				- 请求方法

					- get
					- post
					- put
					- delete
					- patch
					- head
					- options
					- trace

				- url
				- 协议版本

			- 请求头

				- 请求的附加信息

					- keepalive 持久连接（一个连接可以发多次请求）

			- 请求体

				- 请求参数数据
				- 并不是所有请求都具有请求数据
				- name=tom&password=123456&realName=aaa

	- 服务器处理请求并返回http报文

		- 服务器

			- 网络环境中的高性能计算机
			- 侦听网络上其它计算机（客户机）提交的服务请求
			- 提供相应的服务
			- 处理请求的应用web server

				- apache
				- nginx
				- IIS
				- Lighttpd

		- MVC后台处理阶段

			- 是一种设计模式  
			- 模型 model

				- 主要负责数据交互，一个模型能为多个视图提供数据

			- 视图 view

				- 提供给用户的操作界面

			- 控制器 controller

				- 根据用户从视图层输入的指令
				- 选取模型中的数据
				- 对其进行相应的操作
				- 产生最终结果

		- http响应报文

			- 响应行

				- 协议版本号
				- 状态码

					- 1xx:指示信息--表示请求已接受，继续处理
					- 2xx:成功--表示请求已被成功接收、理解、接受
					- 3xx:重定向--要完成请求必须进行更进一步的操作
					- 4xx:客户端渲染错误--请求有语法错误或请求无法实现
					- 5xx:服务器端错误--服务器未能实现合法请求

			- 响应头

				- 包含响应报文的附加信息，由名/值对组成

			- 响应体

				- 包含回车符、换行符和响应返回数据（并不是所有响应报文都有响应数据）

	- 浏览器解析渲染页面

		- 根据html解析出DOM树
		- 根据css解析生成css规则树
		- 结合DOM树和CSS规则树，生成渲染树
		- 根据渲染树计算每个节点信息

			- 布局
			-  重排

		- 根据计算好的信息绘制页面

			- 重绘
			- 重排

				- 几何属性改变

			- 重排必重绘
			- 重绘不一定重排

	- 断开连接TCP四次挥手

		- 数据传送完毕
		- 断开tcp连接
		- 发起tcp四次挥手

			- 图解

				- 

			- 第一次挥手：浏览器发起，发给服务器，我请求报文发送完毕了，你准备关闭把
			- 第二次挥手：服务器发起，告诉浏览器，我请求报文接收完了，我准备关闭了，你也准备把
			- 第三次挥手：服务器发起，告诉浏览器，我响应报文发送完了，你准备关闭吧
			- 第四次挥手：浏览器发起，告诉服务器，我响应报文接收完了，我准备关闭了，你也准备吧

### 一个图片url访问后直接下载

- html5新增属性 download

	- <a href="url" download="文件名加后缀"></a>

- 修改响应头的相关参数

	- x-oss-object-type :Normal
	- x-oss-required-id:
	- x-oss-storage-class:Standard

### 网络攻击及防范

- xss

	- 什么是XSS

		- 跨站脚本攻击 cross-site script
		- 攻击者通过注入恶意脚本
		- 在用户浏览网页时进行攻击，获取cookie或者用户的其它身份信息

	- 分类

		- 存储型

			- 攻击者输入一些数据并且存储到了数据库中，其它浏览器看到的时候进行攻击

		- 反射型

			- 不存储在数据库中
			- 将攻击代码放到url地址请求参数中

	- 防御

		- cookie

			- 设置httpOnly属性，可以防止XSS,它会禁止javascript脚本来访问cookie
			- secure 

				- 告诉浏览器仅在请求为https的时候发送cookie

		- 对用户输入进行检验
		- 进行特殊字符过滤

- [CSRF](https://tech.meituan.com/2018/10/11/fe-security-csrf.html)

	- 什么是CSRF

		- 跨站请求伪造  Cross-site request forgery
		- 攻击者引诱受害者进入第三方网站，在第三方网站中，向攻击网站发送跨站请求
		- 利用受害者在被攻击的网站已经获取的注册凭证，绕过后台用户验证，达到冒充用户对被攻击网站执行某项操作

	- 特点

		- 攻击一般发起在第三方网站
		- 攻击者利用受害者在被攻击网站的登录凭证，冒充受害者提交操作；不是直接窃取数据
		- 攻击者不能获取到受害者的登录凭证，仅仅是冒用
		- 通常是跨域的

	- 防护策略

		- 阻止不明外域访问

			- 同源检测
			- Samesite Cookie

				- Set-Cookie响应头新增属性
				- Strict

					- 严格模式

						- 这个cookie在任何情况下都不可能作为第三方cookie

				- Lax

					- 宽松模式

						- 用户在不同网页之间的跳转不受影响了

		- 提交要求附加本域才能获取的信息

			- CSRF Token

				- 用户打开页面，服务器需要给这个用户生成一个Token
				- 存放在服务器中的Session中

			- 双重Cookie验证

				- 无须使用Session，适用面更广，易于实施
				- 可以在前后端统一拦截，不需要一个个接口和页面添加
				- 如果有其它漏洞，如XSS 将会失效

			- 验证码和密码

### [一句话概括RESTFUL](https://www.zhihu.com/question/28557115)

- 就是用URL定位资源，用HTTP动词（get post put delete等）描述操作
- REST -- REpresentational State Transfer 直接翻译：表现层状态转移

### [click在移动端上有300ms延迟](https://zhuanlan.zhihu.com/p/69522350#:~:text=%E8%BF%99%E5%BD%93%E4%B8%AD%E6%9C%80%E5%87%BA%E5%90%8D%E7%9A%84%EF%BC%8C%E5%BD%93%E5%B1%9E%E5%8F%8C%E5%87%BB%E7%BC%A9%E6%94%BE%20%28double%20tap%20to%20zoom%29%EF%BC%8C%E8%BF%99%E4%B9%9F%E6%98%AF%E4%BC%9A%E6%9C%89%E4%B8%8A%E8%BF%B0,300%20%E6%AF%AB%E7%A7%92%E5%BB%B6%E8%BF%9F%E7%9A%84%E4%B8%BB%E8%A6%81%E5%8E%9F%E5%9B%A0%E3%80%82%20%E5%8F%8C%E5%87%BB%E7%BC%A9%E6%94%BE%EF%BC%8C%E9%A1%BE%E5%90%8D%E6%80%9D%E4%B9%89%EF%BC%8C%E5%8D%B3%E7%94%A8%E6%89%8B%E6%8C%87%E5%9C%A8%E5%B1%8F%E5%B9%95%E4%B8%8A%E5%BF%AB%E9%80%9F%E7%82%B9%E5%87%BB%E4%B8%A4%E6%AC%A1%EF%BC%8CiOS%20%E8%87%AA%E5%B8%A6%E7%9A%84%20Safari%20%E6%B5%8F%E8%A7%88%E5%99%A8%E4%BC%9A%E5%B0%86%E7%BD%91%E9%A1%B5%E7%BC%A9%E6%94%BE%E8%87%B3%E5%8E%9F%E5%A7%8B%E6%AF%94%E4%BE%8B%E3%80%82)

- 原因

	- 为了能把PC端大屏幕的页面以较好的效果展示在小屏幕上，使用了双击缩放

- 解决

	- 禁止缩放

		- <meta name="viewport" content="width=device-width,user-scalable=no">

	- 使用fastClick

		- 原理：在检测到touchend事件后，立即触发一个模拟click事件，并把浏览器300ms之后真正触发的click事件阻断掉

### 性能优化

- 减少http请求
- 添加本地缓存
- 压缩资源文件
- 将css样式表放在顶部，把javascript放在底部
- 避免重定向
- 图片懒加载
- 减少重绘和重排

## HTTP

### http协议

- 定义

	- 超文本传输协议
	- 基于TCP/IP通信协议传输数据
	- 属于应用层面向对象的协议

- 特点

	- 支持客户/服务器模式

		- 浏览器作为HTTP客户端 通过URL向http服务端即web服务器发送所有请求

	- 简单快速

		- 只需传送请求方法和路径

	- 灵活

		- 允许传输任意类型的数据对象，由Content-type标记

	- 无连接

		- 每次连接只处理一个请求

	- 无状态

		- 对事物处理没有记忆能力

### [http2.0](https://zhuanlan.zhihu.com/p/89471776)

- 什么是http2.0协议

	- 建立在https协议的基础上
	- 通过二进制分帧来进行数据传输
	- 对http1.x语义完全兼容
	- 性能的大幅提升（对终端用户感知延迟、网络及服务器资源的使用等性能优化）

- 优化内容

	- 提升访问速度
	- 二进制分帧

		- 请求优先级

			- 最高-主要是html
			- 高-css文件
			- 中-js文件
			- 底-图片

		- 帧frame包含部分

			- 类型 type
			- 长度 length
			- 标记 flags
			- 流标识符 stream
			- 有效载荷 stream payload

		- 消息message

			- 一个完整的请求或者响应
			- 由一个或多个frame组成

		- 流

			- 连接中的虚拟通道
			- 每个流由唯一的整数标识符
			- 防止两端流冲突

				- 客户端发起的流具有奇数ID
				- 服务器发起的流具有偶数ID

			- 是描述二进制frame的格式

	- 多路复用

		- 允许同时通过单一的http/2连接发起多重数据请求-响应消息
		- 每个数据都拆分成很多互不影响的帧
		- 最后在另一端把他们重新组合起来
		- http2连接是持久的
		- 来自很多流的数据包能够混合在一起通过同样的连接传输
		- 到达终点时，根据不同 帧首部的流标识符重新连接 将不同的数据流进行组装

	- 头部压缩

		- 使用encoder来减少需要传输的header大小
		- 相同的数据，不通过每次请求和响应发送
		- 如果首部发生变化，只需将变化的部分加入到header中
		- 首部表在http2.0的连接存续期间内始终存在，由客户端和服务器共同渐进的更新

	- 服务器推送

		- 可以缓存
		- 在同源的情况下，不同页面之间可以共享缓存资源
		- 推送遵循同源策略
		- 基于客户端的请求确定响应
		- 可以对一个客户端请求 发送多个响应
		- 服务器向客户端推送资源无须客户端明确的请求
		- 把客户端所需要的资源伴随着index.html一起发送到客户端，省去了客户端重复请求的步骤
		- 没有发起请求，没有建立连接等操作，速度大大提高

### 响应状态码

- 1.x.x 
- 2.x.x 请求成功

	- 200

		- 请求已成功，返回请求所需要的请求头和请求体，返回的数据为全量数据，如果文件不通过GZIP压缩的话，文件是多大，则要有多大的传输量

- 3.x.x 资源移动

	- 301

		- Move Permanently 永久移动，请求的资源已被永久移动到新URL,返回信息会包括新的URL，浏览器会自动定向到新的URL,今后任何新的请求都应使用新的URL代替

			- 除非额外指定，否则这个响应是可缓存的
			- 比较常用的场景是使用域名跳转
			- 永久重定向

	- 302

		- Found 临时移动,与301类似，但资源只是临时移动，客户端应继续使用原有URL

			- 只有在Cache-Control或Expires中进行了指定的情况下，这个响应才是可缓存的
			- 302用来做域名临时跳转
			- 比如未登录的用户返回用户中心重定向到登录页面
			- 临时重定向

	- 304

		- Not Modified 未修改，所有请求资源未修改，服务器返回此状态码时，不会返回任何资源。

			- 客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回指定日期之后修改的资源

		- 如果客户端发送了一个带条件的get请求且该请求已被允许，而文档内容自上次请求以来并没有改变，则服务器返回这个状态码

			- 客户端和服务器只需要传输很少的数据量来做文件校验，如果文件没有修改过，则不需要返回全量数据

- 4.x.x 客户端发生错误

	- 401

		- 前端提交的数据字段名称和字段类型与后台的实体没有保持一致

			- 前端提交到后台的数据应该是json字符串类型，但是前端没有将对象JSON.stringify转换成字符串
			- 解决

				- 对照字段名称，保持一致性
				- 将obj对象通过JSON,stringify实现序列化

	- 402

		- 当前请求需要得到用户验证

	- 403

		- 服务器已经得到请求，但是拒绝执行

- 5.x.x服务器发生错误

### http请求方法

- [get和post的区别](https://zhuanlan.zhihu.com/p/135454697)

	- 功能

		- get用于获取资源

			- 类似于查找过程，用户获取数据，可以不用每次都和数据库连接，可以使用缓存

		- post用于更新资源

			- 一般是修改和删除的工作，所以必须与数据库交互，所以不能使用缓存

	- 区别

		- 浏览器（平时大部分见到的还是基于浏览器的请求）

			- 无论是get或是post本质上都是不安全的

				- 原因

					- 由于http本身就是明文协议
					- 每个http请求和返回的数据再网络上都是明文传播

				- 解决

					- 使用https（用ssl协议商出的秘钥加密明文http数据）

			- get请求时URL的长度是有限制的(浏览器或web服务器对get的限制)

				- 原因

					- 浏览器要对url解析
					- 解析时要分配内存
					- url必须当做一个整体看待，无法一块一块的处理
					- 必须分配一个足够大的内存
					- 如果url太长，而且并发性又很高，容易挤爆服务器

			- get只有header没有请求体而post都有

				- 问题

					- post是发送两个请求吗

						- http协议中并没有明确说明post会产生两个数据包
						- 原因

							- 和post完全没有关系,只是基于两端的一种优化手段

					- 同时发送还是先后发送

						- 先发送请求头

							- 服务器校验

								- 通过

									- 服务器回复100 - Continue

										- 客户端再把请求体发送给服务器

								- 不通过

									- 服务器回复400之类的错误

										- 交互终止

		- 使用http作为接口进行传输

			- 都只是http协议上的两种请求方式
			- 由于http协议是基于TCP/IP的应用层协议
			- get和post用的都是同一个传输层协议，在传输上没什么区别
			- 最大的区别就是报文格式上的不同
			- get也可以有body,post不一定非要用body 前提是需要客户端和服务器确定好规范

- get

	- 请求指定页面信息，并返回实体主体

- post

	- 向服务器提交数据，进行处理请求

- heade

	- 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头

- options

	- 允许客户端查看服务器的性能，返回服务器针对特定资源所支持的http方法

- delete

	- 请求服务器删除指定页面

- put

	- 从客户端向服务器传送数据取代指定的文档内容

- trace

	- 回显服务器收到的请求，主要用于测试或诊断

- connect

	- http1.1协议中能够将连接改为管道方式的代理服务器

### [常见的http头部](https://juejin.cn/post/6844903745004765198#:~:text=%E4%B8%80%E3%80%81%E5%B8%B8%E7%94%A8%E7%9A%84http%E8%AF%B7%E6%B1%82%E5%A4%B4%201.Accept%20Accept%3A%20text%2Fhtml%20%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%AF%E4%BB%A5%E6%8E%A5%E5%8F%97%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%9B%9E%E5%8F%91%E7%9A%84%E7%B1%BB%E5%9E%8B%E4%B8%BA,text%2Fhtml%E3%80%82%20Accept%3A%20%2A%2F%2A%20%E4%BB%A3%E8%A1%A8%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%AF%E4%BB%A5%E5%A4%84%E7%90%86%E6%89%80%E6%9C%89%E7%B1%BB%E5%9E%8B%2C%20%28%E4%B8%80%E8%88%AC%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%91%E7%BB%99%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%83%BD%E6%98%AF%E5%8F%91%E8%BF%99%E4%B8%AA%29%E3%80%82)

- 通用首部首部

	- Date

		- 表示报文创建时间

- 请求首部（请求报文中的通用信息）

	- Accept

		- Accept:text/html  浏览器可以接受服务器返回的类型为text/html
		- Accept:*/* 代表浏览器可以处理所有类型

	- Accept-Encoding:gzip|deflate

		- 浏览器你声明自己接受编码的方法，通常指压缩方法，是否支持压缩方法，（不止是字符编码）

	- Accept-Language:zh-cn,zh;q=0.9

		- 浏览器声明自己接受的语言

	- connection

		- keep-alive

			- 当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接

		- close

			- 代表一个request请求完成后，客户端和服务器之间用于传输HTTP数据的TCP连接会关闭，再次发起请求时，需要重新建立TCP连接

	- Host

		- 发送请求时，该报头域是必须的---请求报头域主要用于指定被请求资源的Internet主机和端口号，通常从http URL中提取出来

	- Referer

		- 告诉服务器我是从哪个页面来的

	- User-Agent

		- 告诉HTTP服务器，客户端使用的操作系统和浏览器名称和版本号

	- Cache-Control

		- 缓存控制

	- Cookie

		- 用来存储一些用户信息，让服务器辨别用户的身份

	- Range（用于断点续传）

- 响应首部（响应报文中的通用信息）

	- Cache-Control
	- Server

		- 服务器和相对应的版本号

	- Transfer-Encoding:chunked

		- 告诉客户端，服务器发送资源的方式，chunked代表分块发送

	- Expires

		- 设置缓存有效期，因为客户daunt和服务器的时间不一定都是相同的，如果时间不同就会导致问题，没有Cache-Control响应头的max-age准确

	- Last-Modified

		- 所有请求对象最后修改日期

	- Connection

		- keep-alive，告诉客户端服务器的tcp连接是一个长连接，客户端可以继续使用这个tcp连接发送http请求

	- Etag

		- 判断一个对象是否被修改了

	- Refresh

		- 用于重定向

	- Access-Control-Allow-Origin

		- 指定哪些网站可以跨域资源共享
		- * 代表所有网站可以跨域资源共享

	- Access-Control-Allow-Credentials：true

		- 是否允许发送cookie
		- 默认 cookie不包括在CORS请求中
		- 设为true，表示cookie可以包含在请求中

- 实体首部（描述实体部分）

	- Content-Range

		- 指定整个实体中的一部分的插入位置
		- 指示了整个实体的长度

	- Content-Encoding

		- 告诉客户端服务器发送的资源编码格式

	- Content-Type

		- 告诉客户端，资源文件的类型，还有字符编码

## HTML

### web Quality(应用无障碍)

- 定义

	- 网站开发中，可访问性是指网页内容和与用户界面可以被用户理解、浏览并与之交互
	- 用户包括有视觉障碍、听觉障碍或认知障碍的用户

- 如何提升网站的可访问性

	- img标签中使用alt属性为视觉障碍用户添加替代的文本，若是装饰性图片可在alt属性中添加空白字符串
	- h1-h6 使用标题显示内容的层级关系  不同标题之间也应该有具有层级关系
	- 使用main标签呈现网页的主题内容，每个页面应只有一个
	- 语义化标签

		- 网页布局

			- main
			- header
			- section
			- article
			- nav
			- aside

		- 视频

			- audio

		- 图表

			- figure  

				- 包含在图表外面

			- figcaption

				- 图表的描述信息
				- 可嵌套在figure中也可是其它标签中组合使用

		- 表单

			- label

				- 每个单选按钮都有一个包含for属性的labe标签,这些属性直指相关选项的id

			- fieldset

				- 包裹整组单选按钮
				- 使用legend标签提供分组描述
				- 以便屏幕阅读器用户会阅读fieldset元素中的每个选项

		- 日期

			- input标签里的type=date
			- time标签 和datetime属性

		- 使用css让元素仅对屏幕阅读器可见
		- 添加accesskey属性，让用户可以在链接之间快速导航

			- 用于指定激活元素或者使元素获得焦点的快捷键

		- 使用tabindex将键盘焦点添加到元素中

			-  tab 键来获得焦点

		- 使用tabindex指定多个元素的键盘焦点顺序

### drag api

- 事件主体是被拖放元素

	- ondragstart
	- ondragend

- 事件主体是目标元素

	- ondragenter
	- ondragover
	- ondragleave
	- ondrop

- e.dataTransfer

	- 用来保存drag and drop过程中的数据
	- dataTransfer.clearData()--删除给定类型关联数据
	- dataTransfer.getData() 检索给定的类型数据
	- dataTransfer.setDate() 用于设定自定义的拖动图像
	- dataTransfer.files 文件资源列表

### iframe

- iframe是什么

	- <iframe>标签规定一个内联框架
	- 可用此标签在当前HTML文档中嵌入另一个文档
	- <iframe src="要嵌入的html网页地址"></iframe>

- 缺点

	- 会阻塞页面的onload事件
	- 搜索引擎无法解读这种页面，不利于SEO(搜索引擎优化)
	- iframe和主页共享连接池，而浏览器对相同区域有限制，会影响性能

### [doctype](https://www.cnblogs.com/wuqiutong/p/5986191.html)

- 作用

	- 告诉浏览器该文件的类型，让浏览器解析器知道他们应该用哪个规范来解析文档

- 严格模式

	- 又称标准模式，是指浏览器按照W3C标准解析代码

- 混杂模式

	- 又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码

- 如何区分

	- 与网页中的DTD直接相关
	- 如果文档包含严格的DTD,那么它一般以严格模式呈现  (严格DTD-严格模式)
	- 包含过渡DTD和URL的DOCTYPE，也以严格模式呈现
	- 但有过渡DTD而没有URL(统一资源标识符，就是声明最后的地址) 会导致页面以混杂模式出现
	- DOCTYPE不存在或形式不正确会导致文档以混杂模式呈现
	- HTML5没有DTD,因此也就没有严格模式与混杂模式的区别，HTML5有相对宽松的语法，实现时 已经尽可能大的向后兼容
	- 严格模式的排版和JS运作模式是以该浏览器支持的最高标准运行
	- 混杂模式，向后兼容，模拟老式浏览器，防止浏览器无法兼容页面

### BOM

- 什么事BOM

	- BOM是浏览器对象

- 有哪些常用的属性

	- location对象

		- location.href--返回或设置当前文档的url
		- location.search--返回当前url中的查询字符串部分
		- location.hash-- 返回url  #后面的内容 若没有# 返回空
		- location.host--返回url域名部分
		- location.hostname--返回url中的主域名部分
		- location.pathname--返回url中域名后面的部分
		- location.port--返回url中端口部分
		- location.protocol--返回url中的协议部分
		- loaction.assign--设置当前文档的url
		- location.replace()--设置当前文档的url,并在history对象的地址列表中移除这个url,(不能返回)
		- location.reload()--重新加载当前页面

	- history对象

		- history.go(num)--前进或后退指定的页面数
		- history.back()--后退一页
		- history.forwad()--前进一页

	- navigator对象

		- navigator.cookieEnabled--返回用户代理头的字符串是否支持(启用)cookie
		- navigator.appCodeName--浏览器代号
		- navigator.appName--浏览器名称
		- navigator.appVersion--浏览器版本
		- navigator.platform--硬件平台
		- navigator.userAgent--用户代理
		- navigator.language--用户代理语言

	- 弹窗

		- 警告框

			- window.alert("sometext")

		- 确认框

			- window.confirm("sometext")

		- 提示框

			- window.prompt("sometext","defaultvalue")

		- 换行

			- 使用 \n

	- 计时事件

		- setInterval
		- clearInteval
		- setTimeout
		- clearTimeout

	- cookie

		- 记录客户端的用户信息

			- 登录的用户名 密码等
			- 用户自定义

		- 设置cookie  document.cookie="username=  ;password=   ;expires=  path=/"

	- screen

		- screen.availWidth --可用屏幕宽度
		- screen.availHeight --可用屏幕高度

	- Window对象

		- innerHeight 浏览器的内部高度（包括滚动条）
		- innerWidth
		- window.open()-打开新窗口
		- window.close()-关闭当前窗口
		- window.moveTo()-移动当前窗口
		- window.resizeTo()-调整当前窗口的尺寸

### addEventListener参数

- event  指定事件名称

	- click
	- mousedown
	- mouseover
	- mouseout
	- resize

- function  指定事件触发时执行的函数
- useCapture  指定事件是否在捕获或冒泡阶段执行

	- true  捕获传递

		- 外部元素的事件会先被触发

	- false 冒泡传递 (默认)

		- 内部元素的事件会被先触发

- removeEventListener()方法

	- 移除有addEventListener()方法添加的事件句柄

