# vue

## vue-loader

### .vue文件，是如何被编译然后运行到浏览器中的

### 作用

- 解析和转换.vue文件，提取出其中的逻辑代码 script,样式代码style，以及HTML模板template，再分别把他们交给对应的loader处理
- css-loader加载由vue-loader提取出的css代码
- vue-template-compiler:把vue-loader提取出来的html模板编译成可执行的javascript代码

## vue组件中的data为什么必须是个函数

### 每个vue组件都是一个vue实例，通过new Vue()实例化，引用同一个对象，如果data是一个对象的话，那么一旦修改其中一个组件中的数据，其它组件相同数据就会被改变

### 而data是函数的话，每个vue组件的data都因为函数有了自己的作用域，互不干扰

## vue的生命周期是什么

### 就是vue从开始创建到销毁的过程

### 分为四大部

- 创建

	- beforeCreate
	- created

- 挂载

	- beforeMounte

		- 在beforeMount前，虚拟dom已经创建完成，

	- mounted

		- 之后在mounted前，将vm.$el渲染页面，,mounted将虚拟dom挂载到真实页面（此时页面已经全部渲染完成）

- 更新

	- beforeUpdate
	- updated

- 销毁

	- beforeDestroy

		- 最后函数主动调用销毁函数或者组件自动销毁时beforeDestroy，手动撤销监听事件，计时器等

	- destroyed

		- 仅存在Dom节点，其它所有东西自动销毁

## vue中key的作用和工作原理

### 高效的更新虚拟dom

### 其原理是vue在patch过程中通过key可以精准的判断两个节点是否是同一个，从而避免频繁更新不同元素，使得整个patch过程更加高效，减少Dom操作量，提高性能

