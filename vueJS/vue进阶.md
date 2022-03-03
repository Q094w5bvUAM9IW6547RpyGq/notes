## 混入和页面生命周期函数执行顺序

[参考文章](https://juejin.cn/post/6844904169824845832)

**1.** 组件内**data**是在**beforeCreate**和**created**之间执行

 **2.** 父子组件生命周期执行顺序：父组件创建完成后会等待子组件挂载完成才会挂载到页面上，所以父子组件生命周期执行顺序为：

> beforeCreate(父) -> created(父) -> beforeMount(父) -> beforeCreate(子) -> created(子) -> beforeMount(子) -> mounted(子) -> mounted(父)

 **3.** **data**执行**组件**先于**mixin**

> 数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。

 **4.** **生命周期**执行**mixin**先于**组件**

> 同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。

 **5.** 若组件和mixin的**methods**重名，则取组件的methods

> 值为对象的选项，例如 methods、components 和 directives，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。

