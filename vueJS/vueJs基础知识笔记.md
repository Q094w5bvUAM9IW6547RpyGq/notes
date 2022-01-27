邂逅Vuejs

#### 认识Vuejs

* 为什么学习Vuejs
  - 招聘前端的需求中，10个有8个都对Vue有或多或少的要求
  - 作为学习者我们知道Vuejs目前非常火，可以说是前端必备的一个技能
* Vue的读音
  - Vue (读音 /vjuː/，类似于 view)，不要读错
* Vue的渐进式
  - 渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。
  - 或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。
  - 比如Core+Vue-router+Vuex，也可以满足你各种各样的需求。
* Vue的特点
  - 解耦视图和数据
  - 可复用的组件
  - 前端路由技术
  - 状态管理
  - 虚拟DOM

#### 安装Vue

**可以参考 Vue 官网地址 https://cn.vuejs.org/教程**

* CDN引入

  - 你可以选择引入开发环境版本还是生产环境版本

  - ```javascript
    <!-- 开发环境版本，包含了有帮助的命令行警告 --> 
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- 生产环境版本，优化了尺寸和速度 -->
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    ```

* 下载引入

  - ```javascript
    //开发环境 
    https://vuejs.org/js/vue.js 
    //生产环境 
    https://vuejs.org/js/vue.min.js
    ```

* npm安装

  - npm install vue
  - npm install -g @vue/cli-service-global  //全局安装 vue serve
  
* 运行  

  - vue serve 项目名称

####  Vue的初体验

* Hello Vuejs

  * mustache -> 体验vue响应式

    ```javascript
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <div id="app">
          <h1>{{message}}</h1>
          <h2>{{name}}</h2>
        </div>
        <script src="../vue.js"></script>
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "helloVuejs",
              name: "你好",
            },
          });
        </script>
      </body>
    </html>
    
    ```

    

* Vue列表展示

  * v-for

  * 后面给数组追加元素的时候, 新的元素也可以在界面中渲染出来

    ```javascript
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <div id="app">
          <ul>
            <!-- v-for 指令 响应式的-->
            <!-- 可以在控制台输入 app.movies.push('电影名称') html 页面会动态的生成你添加的数据 -->
            <li v-for="item in movies">{{item}}</li>
          </ul>
        </div>
        <script src="../vue.js"></script>
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "电影名称",
              movies: ["不能说的秘密", "我的姐姐", "盗梦空间", "普法栏目"],
            },
          });
        </script>
      </body>
    </html>
    
    ```

    

* Vue计数器小案例

  * 事件监听: click -> methods

    ```javascript
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <div id="app">
          <h1>当前计数： {{counter}}</h1>
          <button v-on:click="add">+</button>
          <button v-on:click="sub">-</button>
        </div>
    
        <script src="../vue.js"></script>
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              counter: 0,
            },
            methods: {
              add: function () {
                console.log("add被执行了");
                this.counter++;
              },
              sub: function () {
                console.log("sub被执行了");
                this.counter--;
              },
            },
          });
        </script>
      </body>
    </html>
    
    ```

    

#### Vue中的MVVM

![01](http://ww1.sinaimg.cn/large/007WWC4agy1gswet9lhfej60g208dab902.jpg)

- View层：
  视图层
  在我们前端开发中，通常就是DOM层。
  主要的作用是给用户展示各种信息。

- Model层：
  数据层
  数据可能是我们固定的死数据，更多的是来自我们服务器，从网络上请求下来的数据。
  在我们计数器的案例中，就是后面抽取出来的obj，当然，里面的数据可能没有这么简单。

- VueModel层：视图模型层
  视图模型层是View和Model沟通的桥梁。
  一方面它实现了Data Binding，也就是数据绑定，将Model的改变实时的反应到View中
  另一方面它实现了DOM Listener，也就是DOM监听，当DOM发生一些事件(点击、滚动、touch等)时，可以监听到，并在需要的情况下改变对应的Data。

  **计数器的MVVM:**

  - 我们的计数器中就有严格的MVVM思想

    - View依然是我们的DOM

    - Model就是我们我们抽离出来的obj

    - ViewModel就是我们创建的Vue对象实例

      **它们之间如何工作呢？**

      - 首先ViewModel通过Data Binding让obj中的数据实时的在DOM中显示。
      - 其次ViewModel通过DOM Listener来监听DOM事件，并且通过methods中的操作，来改变obj中的数据。
      - 有了Vue帮助我们完成VueModel层的任务，在后续的开发，我们就可以专注于数据的处理，以及DOM的编写工作了。

![01-计数器的MVVM](https://i0.hdslb.com/bfs/album/b552b7b643eef38c79e7e3f5658267056969cf8d.png)

####  创建Vue时, options可以放那些东西

- 你会发现，我们在创建Vue实例的时候，传入了一个对象options。

- 这个options中可以包含哪些选项呢？

  - 详细解析： https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE

    **目前掌握这些选项：**

    - el: 
      类型：string | HTMLElement
      作用：决定之后Vue实例会管理哪一个DOM。
    - data: 
      类型：Object | Function （组件当中data必须是一个函数）
      作用：Vue实例对应的数据对象。
    - methods: 
      类型：{ [key: string]: Function }
      作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用。

- Vue生命周期

  ![img](https://img-blog.csdnimg.cn/20200815191941397.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0NzUyOTc4,size_16,color_FFFFFF,t_70)

### 插值语法

* Mutache (胡须) 语法--->{{ }}

  ```javascript
  <body>
      <div id="app">
        <h2>{{message}}</h2>
        <h2>{{message}}, 你好</h2>
        <!-- Mustache 语法中不仅仅可以直接写变量，也可以写简单的表达式 -->
        <h2>{{firstname+lastname}}</h2>
        <h2>{{firstname+' '+lastname}}</h2>
        <h2>{{message}} {{lastname}}</h2>
      </div>
      <!-- 引入 vue 框架 -->
      <script src="../vue.js"></script>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "hello vuejs",
            firstname: "fan",
            lastname: "fei",
          },
        });
      </script>
    </body>
  </html>
  ```

* v-once

  - 但是，在某些情况下，我们可能不希望界面随意的跟随改变

    - 这个时候，我们就可以使用一个Vue的指令
      **v-once:** 
      该指令后面不需要跟任何表达式(比如之前的v-for后面是由跟表达式的)
      该指令表示元素和组件(组件后面才会学习)只渲染一次，不会随着数据的改变而改变。
      代码如下：

      ```javascript
      <body>
          <div id="app">
            <h2 v-once>{{message}}</h2>
            <h2>{{message}}</h2>
          </div>
          <script src="../vue.js"></script>
      
          <script>
            const app = new Vue({
              el: "#app",
              data: {
                message: "thankyou",
              },
            });
          </script>
        </body>
      ```

      

* v-html

  - 某些情况下，我们从服务器请求到的数据本身就是一个HTML代码
  - 如果我们直接通过{{}}来输出，会将HTML代码也一起输出。
  - 但是我们可能希望的是按照HTML格式进行解析，并且显示对应的内容。
    如果我们希望解析出HTML展示
  - 可以使用v-html指令
    - 该指令后面往往会跟上一个string类型
    - 会将string的html解析出来并且进行渲染

  ```javascript
  <body>
      <div id="app">
        <h2 v-html="url"></h2>
      </div>
      <script src="../vue.js"></script>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            url: '<a href="http://www.baidu.com">百度一下</a>',
          },
        });
      </script>
    </body>
  ```

  

* v-text

  - v-text作用和Mustache比较相似：都是用于将数据显示在界面中

  - v-text通常情况下，接受一个string类型

    ```javascript
    <body>
        <div id="app">
          <h2 v-once>{{message}}</h2>
          <!-- v-text 不是很灵活 会把后面的数据覆盖掉 -->
          <h2 v-text="message">111</h2>
        </div>
        <script src="../vue.js"></script>
    
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "你好啊",
            },
          });
        </script>
      </body>
    ```

    

* v-pre: {{}}

  - v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。
    **比如下面的代码：**
    - 第一个h2元素中的内容会被编译解析出来对应的内容
    - 第二个h2元素中会直接显示{{message}}

  ```javascript
  <body>
      <div id="app">
        <h2>{{message}}</h2>
        <h2 v-pre>{{message}}</h2>
      </div>
      <script src="../vue.js"></script>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
          },
        });
      </script>
    </body>
  ```

  

* v-cloak: 斗篷

  - 在某些情况下，我们浏览器可能会直接显然出未编译的Mustache标签。
    **cloak: 斗篷**

```javascript
<body>
    <!-- cloak--斗篷 -->
    <!-- 作用：就是防止浏览器因某些情况而直接在用户界面上显示出Mustache 标签 -->
    <div id="app">
      <h2 v-cloak>{{message}}</h2>
    </div>
    <script src="../vue.js"></script>

    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
      });
    </script>
  </body>
```



### v-bind

- 前面我们学习的指令主要作用是将值插入到我们模板的内容当中。
- 但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定。
  - 比如动态绑定a元素的href属性
  - 比如动态绑定img元素的src属性
  - 这个时候，我们可以使用v-bind指令：
    - 作用：动态绑定属性
    - 缩写：:
    - 预期：any (with argument) | Object (without argument)
    - 参数：attrOrProp (optional)

#### v-bind绑定基本属性

* v-bind:

  - v-bind用于绑定一个或多个属性值，或者向另一个组件传递props值

  - 在开发中，有哪些属性需要动态进行绑定呢？

  - 还是有很多的，比如图片的链接src、网站的链接href、动态绑定一些类、样式等等

  - v-bind有一个对应的语法糖，也就是简写方式

  - 在开发中，我们通常会使用语法糖的形式，因为这样更加简洁。

    ```java
    <body>
        <div id="app">
          <!-- <img v-bind:src="logourl" alt="" />
          <a v-bind:href="url">百度一下</a> -->
          <!-- v-bind语法糖 -->
          <!-- 可以直接简写为一个 冒号  ————>: -->
          <img :src="logourl" alt="" />
          <a :href="url">百度一下</a>
        </div>
        <script src="../vue.js"></script>
    
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "你好啊",
              logourl:
                "https://img.alicdn.com/imgextra/i1/2206686532409/O1CN01Soc3cc1TfMnbtDPXQ_!!2206686532409-0-lubanimage.jpg",
              url: "http://www.baidu.com",
            },
          });
        </script>
      </body>
    ```

    


####  v-bind动态绑定class

* 数组语法: 

  > ```<div v-bind:style="[baseStyles, overridingStyles]"></div>```
  >
  > style后面跟的是一个数组类型
  > 多个值以，分割即可

  ```javascript
  <body>
      <div id="app">
        <!-- 把size当成变量（不加引号），把skyblue直接当成字符串（加引号） -->
        <h2 :style="[baseStyle,addStyle]">{{message}}</h2>
  
        <!-- 如果闲太长，也可以单独设置一个函数 -->
        <h2 :style="getStyle()">{{message}}</h2>
      </div>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
            baseStyle: { color: "red" },
            addStyle: { fontSize: 50 + "px" },
          },
          methods: {
            getStyle: function () {
              return [this.baseStyle, this.addStyle];
            },
          },
        });
      </script>
    </body>
  ```

- 对象语法

  

  >```:style="{color: currentColor, fontSize: fontSize + 'px'}"```
  >style后面跟的是一个对象类型
  >对象的key是CSS属性名称
  >对象的value是具体赋的值，值可以来自于data中的属性

  

  ```javascript
  <body>
      <div id="app">
        <h2 :class="{active:isActive,line:isLine}">{{message}}</h2>
        <button v-on:click="btnclick">按钮</button>
      </div>
  
      <script src="../vue.js"></script>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
            isActive: true,
            isLine: true,
          },
          methods: {
            btnclick: function () {
              this.isActive = !this.isActive;
            },
            getClasses: function () {
              return { active: this.isActive, line: this.isLine };
            },
          },
        });
      </script>
    </body>
  ```

  

#### v-bind动态绑定style

> 我们可以利用v-bind:style来绑定一些CSS内联样式。
> 在写CSS属性名的时候，比如font-size
> 我们可以使用驼峰式 (camelCase)  fontSize 
> 或短横线分隔 (kebab-case，记得用单引号括起来) ‘font-size’



* 对象语法:

  ```javascript
  <body>
      <div id="app">
        <!-- 把size当成变量（不加引号），把skyblue直接当成字符串（加引号） -->
        <h2 :style="{fontSize:size+'px',color:'skyblue'}">{{message}}</h2>
  
        <!-- 如果闲太长，也可以单独设置一个函数 -->
        <h2 :style="getStyle()">{{message}}</h2>
      </div>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
            size: 100,
            color: "blue",
            yanse: "red",
          },
          methods: {
            getStyle: function () {
              return { color: this.yanse, fontSize: this.size + "px" };
            },
          },
        });
      </script>
    </body>
  ```

  

* 数组语法:

  ```javascript
  <body>
      <div id="app">
        <!-- 把size当成变量（不加引号），把skyblue直接当成字符串（加引号） -->
        <h2 :style="[baseStyle,addStyle]">{{message}}</h2>
  
        <!-- 如果闲太长，也可以单独设置一个函数 -->
        <h2 :style="getStyle()">{{message}}</h2>
      </div>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
            baseStyle: { color: "red" },
            addStyle: { fontSize: 50 + "px" },
          },
          methods: {
            getStyle: function () {
              return [this.baseStyle, this.addStyle];
            },
          },
        });
      </script>
    </body>
  ```

  

### 计算属性(computed)

- 我们知道，在模板中可以直接通过插值语法显示一些data中的数据。
- 但是在某些情况，我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示
  - 比如我们有firstName和lastName两个变量，我们需要显示完整的名称。
  - 但是如果多个地方都需要显示完整的名称，我们就需要写多个{{firstName}} {{lastName}}

- 我们可以将上面的代码换成计算属性：

  - OK，我们发现计算属性是写在实例的computed选项中的。

    ```js
     computed: {
              fullName: function () {
                return this.firstName + " " + this.lastName;
              },
              totalPrice: function () {
                let result = 0;
                for (let i = 0; i < this.books.length; i++) {
                  result += this.books[i].price;
                }
                return result;
              },
            },
    ```

* 案例一: firstName+lastName + 案例二: books -> price

  ```javascript
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <script src="../vue.js"></script>
      <title>Document</title>
    </head>
    <body>
      <div id="app">
        <h2>总价格：{{totalPrice()}}</h2>
      </div>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            books: [
              {
                id: 110,
                name: "Unix编程技术",
                price: 119,
              },
              {
                id: 111,
                name: "代码大全",
                price: 105,
              },
              {
                id: 112,
                name: "深入理解计算机原理",
                price: 98,
              },
              {
                id: 113,
                name: "现代操作系统",
                price: 87,
              },
            ],
          },
          methods: {
            totalPrice: function () {
              let result = 0;
              // for (let i = 0; i < this.books.length; i++) {
              //   result += this.book[i].price;
              // }
              // for (let i in this.books) {
              //   result += this.books[i].price;
              // }
  
              for (let book of books) {
                result += book.price;
              }
              return result;
            },
          },
        });
      </script>
    </body>
  </html>
  ```

  

#### 计算机属性的setter和getter

  * 每个计算属性都包含一个getter和一个setter
  * 在上面的例子中，我们只是使用getter来读取。
  * 在某些情况下，你也可以提供一个setter方法（不常用）
  * computed中的每一属性都有夜歌set函数和get函数，但是set函数几乎不用，get函数可以省略
    - 在需要写setter的时候，代码如下：

  ```javascript
  <body>
      <div id="app">
        <h2>{{fullName}}</h2>
      </div>
  
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
            firstName: "fan",
            lastName: "fei",
          },
          computed: {
            fullName: {
              get() {
                console.log("------调用了fullName的get");
                return this.firstName + " " + this.lastName;
              },
              set(newValue) {
                console.log("-----调用了fullNamede set");
                const names = newValue.split(" ");
                this.firstName = names[0];
                this.lastName = names[1];
              },
            },
          },
        });
      </script>
    </body>
  ```

#### 计算属性缓存

- 我们可能会考虑这样的一个问题：

- methods和computed看起来都可以实现我们的功能，

- 那么为什么还要多一个计算属性这个东西呢？
  - 原因：计算属性会进行缓存，如果多次使用时，计算属性只会调用一次。
  
  - 我们来看下面的代码：
  
    ```js
    <body>
        <div id="app">
          <h2>{{getFullName}}</h2>
          <h2>{{getFullName}}</h2>
          <h2>{{getFullName}}</h2>
        </div>
        <script>
          var app = new Vue({
            el: "#app",
            data: {
              firstName: "fan",
              lastName: "fei",
            },
            // methods: {
            //   getFullName: function () {
            //     return firstName + " " + lastName;
            //     console.log("我被调用了");
            //   },
            // },
            computed:{
              getFullName:function(){
                return firstName+' '+ lastName;
                console.log("我被调用了");
              }
            }
          });
        </script>
      </body>
    ```
  
- methods中的属性方法会被调用三次

- 而computed中的属性方法只会被调用一次

- 所以计算属性要比方法属性性能要高

### ES6语法的补充

#### let/var

- 事实上var的设计可以看成JavaScript语言设计上的错误. 但是这种错误多半不能修复和移除, 以为需要向后兼容.大概十年前, Brendan Eich就决定修复这个问题, 于是他添加了一个新的关键字: let.
- 我们可以将let看成更完美的var
  - 块级作用域
    - JS中使用var来声明一个变量时, 变量的作用域主要是和函数的定义有关.
    - 针对于其他块定义来说是没有作用域的，比如if/for等，这在我们开发中往往会引起一些问题。

```js
<script>
  // ES5中的var是没有块级作用域的(if/for)
  // ES6中的let是由块级作用的(if/for)

  // ES5之前因为if和for都没有块级作用域的概念, 所以在很多时候, 我们都必须借助于function的作用域来解决应用外面变量的问题.
  // ES6中,加入了let, let它是有if和for的块级作用域.
  // 1.变量作用域: 变量在什么范围内是可用.
  // {
  //   var name = 'why';
  //   console.log(name);
  // }
  // console.log(name);

  // 2.没有块级作用域引起的问题: if的块级
  // var func;
  // if (true) {
  //   var name = 'why';
  //   func = function () {
  //     console.log(name);
  //   }
  //   // func()
  // }
  // name = 'kobe'
  // func()
  // // console.log(name);

  var name = 'why'
  function abc(bbb) { // bbb = 'why'
    console.log(bbb);
  }
  abc(name)
  name = 'kobe'

  // 3.没有块级作用域引起的问题: for的块级
  // 为什么闭包可以解决问题: 函数是一个作用域.
  // var btns = document.getElementsByTagName('button');
  // for (var i=0; i<btns.length; i++) {
  //   (function (num) { // 0
  //     btns[i].addEventListener('click', function () {
  //       console.log('第' + num + '个按钮被点击');
  //     })
  //   })(i)
  // }


//函数是一个异步回调   异步操作，而for是同步操作 需要等for循环全部执行完成后，才会执行函数，所以函数里面你的 i=5
  const btns = document.getElementsByTagName('button')
  for (let i = 0; i < btns.length; i++) {
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击'); //不管点击的是哪个按钮  显示的都是 第5个按钮被点击了
    })
  }

//而闭包中相当于执行五次按钮

</script>

```

块级作用域（es5没有闭包-有闭包）

```js
<body>
<button>按钮1</button>
<button>按钮2</button>
<button>按钮3</button>
<script>
  // 1.没有块级作用域引起的问题: for的块级
  // 为什么闭包可以解决问题: 函数是一个作用域.
  var btns = document.getElementsByTagName('button');
  for (var i=0; i<btns.length; i++) {
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  // 1.情况一: ES5中没有使用闭包(错误的方式)
  // 由于没有作用域，当 i被改变的时候，那所有的i都会被改变
  i = 2
  {
    // i = 0
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  {
    i = 1
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  {
    // i = 2
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  // 2.情况二: ES5中使用闭包
  // 闭包有作用域
  var btns = document.getElementsByTagName('button');
  for (var i=0; i<btns.length; i++) {
    (function (i) { // 0
      btns[i].addEventListener('click', function () {
        console.log('第' + i + '个按钮被点击');
      })
    }) (i)
  }

  i = 100000000
  function (i) { // i = 0
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }(0)

  function (i) { // i = 1
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }(1)

  function (i) { // i = 2
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }(2)

  // ES6中的let
  //let本身就有块级作用域
  const btns = document.getElementsByTagName('button')
  for (let i = 0; i < btns.length; i++) {
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }
  i = 10000000
  { i = 0
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  { i = 1
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

  { i = 2
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }

</script>
```



#### const的使用

- const关键字
- 在很多语言中已经存在, 比如C/C++中, 主要的作用是将某个变量修饰为常量.
- 在JavaScript中也是如此, 使用const修饰的标识符为常量, 不可以再次赋值.
  - 什么时候使用const呢?
  - 当我们修饰的标识符不会被再次赋值时, 就可以使用const来保证数据的安全性.
  - 建议: 在ES6开发中,优先使用const, 只有需要改变某一个标识符的时候才使用let. 

#### 对象字面量的增强写法

- ES6中，对对象字面量进行了很多增强。

- 属性初始化简写和方法的简写：


```js
<body>

<script>
  // const obj = new Object()

  // const obj = {
  //   name: 'why',
  //   age: 18,
  //   run: function () {
  //     console.log('在奔跑');
  //   },
  //   eat: function () {
  //     console.log('在次东西');
  //   }
  // }

  // 1.属性的增强写法
  const name = 'why';
  const age = 18;
  const height = 1.88

  // ES5的写法
  // const obj = {
  //   name: name,
  //   age: age,
  //   height: height
  // }

  // const obj = {
  //   name,
  //   age,
  //   height,
  // }
  //
  // console.log(obj);


  // 2.函数的增强写法
  // ES5的写法
  // const obj = {
  //   run: function () {
  //
  //   },
  //   eat: function () {
  //
  //   }
  // }
  const obj = {
    run() {

    },
    eat() {

    }
  }
</script>

</body>
```

#### for 遍历方式

```js
  totalPrice() {
      // 1.普通的for循环
      // let totalPrice = 0
      // for (let i = 0; i < this.books.length; i++) {
      //   totalPrice += this.books[i].price * this.books[i].count
      // }
      // return totalPrice

      // 2.for (let i in this.books)
      // let totalPrice = 0
      // for (let i in this.books) {
      //   const book = this.books[i]
      //   totalPrice += book.price * book.count
      // }
      //
      // return totalPrice

      // 3.for (let i of this.books)
      // let totalPrice = 0
      // for (let item of this.books) {
      //   totalPrice += item.price * item.count
      // }
      // return totalPrice
      
      //将数组中的每个对象遍历出来，再进行操作
      return this.books.reduce(function (preValue, book) {
        return preValue + book.price * book.count
      }, 0)
    }
```

#### 函数调用

函数执行时，会把需要的数据进行压栈，一旦函数执行完成后，数据会被弹出，若没有其它变量指向这个函数产生的值，那么就会被回收掉，等待下一次函数执行，再把数据压栈，若要保留函数中的数据，那需要在函数被销毁之前，使用一个外部变量指向数据

### 事件监听

在前端开发中，我们需要经常和用于交互。

这个时候，我们就必须监听用户发生的时间，比如点击、拖拽、键盘事件等等

在Vue中如何监听事件呢？

#### 使用v-on指令

- 作用：绑定事件监听器

- （语法糖）缩写：@
- 预期：Function | Inline Statement | Object
- 参数：event
  - 这里，我们用一个监听按钮的点击事件，来简单看看v-on的使用
  - 面的代码中，我们使用了v-on:click="counter++”
  - 另外，我们可以将事件指向一个在methods中定义的函数

```javascript
<body>
    <div id="app">
      <h2>{{counter}}</h2>
      <!-- <button v-on:click="increment">+</button>
      <button v-on:click="decrement">-</button> -->
      <!-- 语法糖  v-on： 可简写为 @ -->
      <button @click="increment">+</button>
      <button @click="decrement">-</button>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          counter: 0,
        },
        methods: {
          increment() {
            this.counter++;
          },
          decrement() {
            this.counter--;
          },
        },
      });
    </script>
  </body>
```

> **注：v-on也有对应的语法糖：**
> **v-on:click可以写成@click**

#### v-on参数

- 情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。
  - 但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去
- 情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件。

```javascript
<body>
    <div id="app">
      <!-- btn1如果不用传参的话，可以直接省略括号 -->
      <button @click="btnclick1">按钮一</button>

      <!-- 加上括号，并传值 则打印值和event事件 -->
      <button @click="btnclick2('2')">按钮二</button>
      <!-- 2 就是需要传递一个参数 若不加括号，则会把event的值复制给参数-->
      <button @click="btnclick2">按钮小二</button>
      <!-- 2.1 若加了括号，但是没有传参数 则会显示一个 undefined-->
      <button @click="btnclick2()">按钮小小二</button>
      <!-- 有时候我们需要把event事件作为一个参数传值，但若直接就写event的话，会报错 -->
      <button @click="btnclick3(111,event)">按钮三</button>

      <!-- 解决办法就是在event前加一个 $ 符号 -->
      <button @click="btnclick3(111,$event)">按钮三</button>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        methods: {
          btnclick1() {
            console.log("按钮一");
          },
          btnclick2(a) {
            console.log("按钮二");
            console.log(a, event);
          },
          btnclick3(a, event) {
            console.log("按钮三");
            console.log("++++", a, event);
          },
        },
      });
    </script>
  </body>
```

#### v-on修饰符

- 在某些情况下，我们拿到event的目的可能是进行一些事件处理。
- Vue提供了修饰符来帮助我们方便的处理一些事件：
  - .stop - 调用 event.stopPropagation()。
  
  - .prevent - 调用 event.preventDefault()。
  
  - .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。
  
  - .native - 监听组件根元素的原生事件。(如果你要监听自己创建的组件)
  
    我们需要监听一个组件的原生事件时，必须给对应的事件加上.native修饰符，才能进行监听
  
  - .once - 只触发一次回调。

```javascript
<body>
    <div id="app">
      <!-- stop -->
      <!-- 1.会产生冒泡行为，当我只点击按钮的时候，由于冒泡行为，导致div也被执行了 -->
      <!-- <div @click="divclick">
        aaaaa
        <button @click="btnclick">按钮</button>
      </div> -->
      <!-- 阻止冒泡行为 .stop修饰符 -->
      <div @click="divclick">
        aaaaa
        <button @click.stop="btnclick">按钮</button>
      </div>

      <!-- 2.prevent -->
      <br />
      <form action="baidu">
        <!-- 这里会自动提交数据 -->
        <!-- <input type="submit" value="提交" @click="submitclick" /> -->
        <!-- 但是有时候我们不需要他自动提交数据，方便我们收集数据  加上修饰符prevent 就不会自动提交-->
        <input type="submit" value="提交" @click.prevent="submitclick" />
      </form>

      <!-- 3.keyup -->
      <br />
      <!-- 按键松开时就会触发条件 -->
      <!-- <input type="text" @keyup="keyup" /> -->
      <!-- 但是有时候我们需要限定什么时候才触发则 -->
      <input type="text" @keyup.enter="keyup" />

      <!-- 4.once修饰符 就是事件只执行一次-->
      <br />
      <input type="text" />
      <input type="submit" value="提交" @click.once="onceclick" />
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        methods: {
          btnclick() {
            console.log("我是按钮");
          },
          divclick() {
            console.log("我是div");
          },
          submitclick() {
            console.log("提交了");
          },
          keyup() {
            console.log("keyup");
          },
          onceclick() {
            console.log("执行了");
          },
        },
      });
    </script>
  </body>
```

#### 条件判断（v-if、v-else-if、v-else）

- v-if、v-else-if、v-else
- 这三个指令与JavaScript的条件语句if、else、else if类似。
- Vue的条件指令可以根据表达式的值在DOM中渲染或销毁元素或组件

```javascript
<body>
    <div id="app">
      <h2 v-if="isShow">
        <div>111</div>
        <div>111</div>
        <div>111</div>
        <div>111</div>
        {{message}}
      </h2>
      <h1 v-else="isShow">isShow为false时，显示</h1>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          isShow: true,
        },
      });
    </script>
  </body>
```

- v-if的原理：
- v-if后面的条件为false时，对应的元素以及其子元素不会渲染。
- 也就是根本没有不会有对应的标签出现在DOM中。

```java
<body>
    <div id="app">
      <!-- 这种方式不太推荐可以直接在计算属性里面写个函数 -->
      <!-- <h2 v-if="score>=90">优秀</h2>
      <h2 v-else-if="score>=80">良好</h2>
      <h2 v-else="score>=60">及格</h2> -->

      <h2>{{result}} {{message}}111</h2>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          score: 90,
        },
        computed: {
          result() {
            let level = "";
            if (this.score >= 90) {
              return (level = "优秀");
            } else if (this.score >= 80) {
              return (level = "良好");
            } else {
              return (level = "及格");
            }
          },
        },
      });
    </script>
  </body>
```

#### 小案例（用户登录切换）

key 的用法

```java
<body>
    <div id="app">
      <!-- 案例小问题，就是如果用户已经输入了内容，但是又切换了方式，则由于Vue内部的原因，会进行一个复用，则会保留用户输入的内容 -->
      <!-- 解决方式：加上key="取值（俩个input里面的key值不一样，则表示不可复用）"-->
      <span v-if="isUser">
        <label for="email">用户邮箱</label>
        <input type="text" id="email" placeholder="用户邮箱" key="email" />
      </span>
      <span v-else>
        <label for="username">用户账号</label>
        <input
          type="text"
          id="username"
          placeholder="用户账号"
          key="username"
        />
      </span>
      <button @click="isUser=!isUser">切换类型</button>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          isUser: true,
        },
      });
    </script>
  </body>
```

#### 案例小问题

- 如果我们在有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。
- 但是按道理讲，我们应该切换到另外一个input元素中了。
- 在另一个input元素中，我们并没有输入内容。
- 为什么会出现这个问题呢？
  - 问题解答：
  - 这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。
  - 在上面的案例中，Vue内部会发现原来的input元素不再使用，直接作为else中的input来使用了。
    - 解决方案：
      如果我们不希望Vue出现类似重复利用的问题，可以给对应的input添加key
      并且我们需要**保证key**的**不同** 
      
      上面案例已经加上

#### v-show

- v-show的用法和v-if非常相似，也用于决定一个元素是否渲染：

  - v-if和v-show对比

    ```javascript
    <body>
        <div id="app">
          <!-- 区别：消失的方式不同，当为false时，v-if 是直接整个h2直接没了，而，v-show则是加了个display样式 -->
          <h2 v-if="isShow">{{message}}</h2>
          <h2 v-show="isShow">{{message}}</h2>
        </div>
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "你好啊",
              isShow: true,
            },
          });
        </script>
      </body>
    ```

    - v-if和v-show都可以决定一个元素是否渲染，那么开发中我们如何选择呢？
    - v-if当条件为false时，压根不会有对应的元素在DOM中。
    - v-show当条件为false时，仅仅是将元素的display属性设置为none而已。
    - 开发中如何选择呢？
    - 当需要在显示与隐藏之间切片很频繁时，使用v-show
    - 当只有一次切换时，通过使用v-if

#### v-for(对数组和对象的遍历)

- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。

- v-for的语法类似于JavaScript中的for循环。

- 官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性

- **key****的作用主要是为了高效的更新虚拟****DOM**

- 格式如下：item in items的形式。

- 我们来看一个简单的案例：

  > 如果在遍历的过程中不需要使用索引值
  > v-for="movie in movies"
  > 依次从movies中取出movie，并且在元素的内容中，我们可以使用Mustache语法，来使用movie
  > 如果在遍历的过程中，我们需要拿到元素在数组中的索引值呢？
  > 语法格式：v-for=(item, index) in items
  > 其中的index就代表了取出的item在原数组的索引值。

```javascript
<body>
    <div id="app">
      <ul>
        <li v-for="(item,index) in movies">{{index+1}}.{{item}}</li>
      </ul>
      <ul>
        <li v-for="(value,index,item) in show">{{item}}{{index}}-{{value}}</li>
      </ul>
    </div>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          movies: ["你好，乔恩", "成龙历险记", "悲伤逆流成河", "叶罗丽"],
          show: {
            name: "xiaofan",
            age: 20,
            sex: "女",
          },
        },
      });
    </script>
  </body>
```

### 小bug

![](http://ww1.sinaimg.cn/large/007WWC4agy1gswevjqoc0j60b30490to02.jpg)

- **手写的vue.js要在最后引入**

- **因为要先有id为vue-app的div,vue才能获取相应的元素。**

### vue内部会监听数据的变化，同时进行渲染

- 因为Vue是响应式的，所以当数据发生变化时，Vue会自动检测数据变化，视图会发生对应的更新。

- Vue中包含了一组观察数组编译的方法，使用它们改变数组也会触发视图的更新

```js
<body>
<div id="app">
  <ul>
    <li v-for="item in letters">{{item}}</li>
  </ul>
  <button @click="btnClick">按钮</button>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      letters: ['a', 'b', 'c', 'd']
    },
    methods: {
      btnClick() {
        // 1.push方法
        // this.letters.push('aaa')
        // this.letters.push('aaaa', 'bbbb', 'cccc')

        // 2.pop(): 删除数组中的最后一个元素
        // this.letters.pop();

        // 3.shift(): 删除数组中的第一个元素
        // this.letters.shift();

        // 4.unshift(): 在数组最前面添加元素
        // this.letters.unshift()
        // this.letters.unshift('aaa', 'bbb', 'ccc')

        // 5.splice作用: 删除元素/插入元素/替换元素
        // 删除元素: 第二个参数传入你要删除几个元素(如果没有传,就删除后面所有的元素)
        // 替换元素: 第二个参数, 表示我们要替换几个元素, 后面是用于替换前面的元素
        // 插入元素: 第二个参数, 传入0, 并且后面跟上要插入的元素
        // splice(start)
        // splice(start):
        this.letters.splice(1, 3, 'm', 'n', 'l', 'x')
        // this.letters.splice(1, 0, 'x', 'y', 'z')

        // 5.sort()
        // this.letters.sort()

        // 6.reverse()
        // this.letters.reverse()

        // 注意: 通过索引值修改数组中的元素 不能做到数据响应式
        // this.letters[0] = 'bbbbbb';
        // this.letters.splice(0, 1, 'bbbbbb')
        // set(要修改的对象, 索引值, 修改后的值)
        // Vue.set(this.letters, 0, 'bbbbbb')
      }
    }
  })


  // function sum(num1, num2) {
  //   return num1 + num2
  // }
  //
  // function sum(num1, num2, num3) {
  //   return num1 + num2 + num3
  // }
  // function sum(...num) {
  //   console.log(num);
  // }
  //
  // sum(20, 30, 40, 50, 601, 111, 122, 33)

</script>

</body>
```

### 购物车案例（过滤器的使用）

补充知识点：filters属性

使用：

```js
//showPrice是过滤器的名称
<td>{{item.price | showPrice}}</td>
```

```js
filters: {
    showPrice(price) {
      return '¥' + price.toFixed(2)
    }
  }
```

### 表单绑定v-model

#### 基本使用

使用v-model把data中的变量绑定到input中，作为value值

```js
<body>
<div id="app">
  <input type="text" v-model="message">
  {{message}}
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>
</body>
```

#### v-model的原理(双向绑定)

- 直接使用v-model就可以直接双向绑定
- 也可以通过v-bind 和v-on 两个指令来实现双向绑定

```js
<body>

<div id="app">
  <!--<input type="text" v-model="message">-->
  <!--<input type="text" :value="message" @input="valueChange">-->
  <input type="text" :value="message" @input="message = $event.target.value">
  <h2>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    methods: {
      valueChange(event) {
        this.message = event.target.value;
      }
    }
  })
</script>
```

#### v-model结合radio类型使用(单选框)

```js
<body>

<div id="app">
  <label for="male">
    <input type="radio" id="male" value="男" v-model="sex">男
  </label>
  <label for="female">
    <input type="radio" id="female" value="女" v-model="sex">女
  </label>
  <h2>您选择的性别是: {{sex}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      //可以直接给一个默认值
      sex: '女'
    }
  })
</script>

</body>
```

#### v-model结合checkbox类型使用（多选框）

- 注意单选框 v-model绑定的是一个布尔值
- 多选框绑定的是一个数组
- 在input 外面一层加上 label标签的好处：点击文字也可以被选择

```js
<body>

<div id="app">
  <!--1.checkbox单选框-->
  <!--<label for="agree">-->
    <!--<input type="checkbox" id="agree" v-model="isAgree">同意协议-->
  <!--</label>-->
  <!--<h2>您选择的是: {{isAgree}}</h2>-->
  <!--<button :disabled="!isAgree">下一步</button>-->

  <!--2.checkbox多选框-->
  <input type="checkbox" value="篮球" v-model="hobbies">篮球
  <input type="checkbox" value="足球" v-model="hobbies">足球
  <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
  <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
  <h2>您的爱好是: {{hobbies}}</h2>
  <label v-for="item in originHobbies" :for="item">
    <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
  </label>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isAgree: false, // 单选框
      hobbies: [], // 多选框,
      originHobbies: ['篮球', '足球', '乒乓球', '羽毛球', '台球', '高尔夫球']
    }
  })
</script>

</body>
```

#### v-mode l结和 select  类型使用

```js
<body>

<div id="app">
  <!--1.选择一个-->
  <select name="abc" v-model="fruit">
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是: {{fruit}}</h2>

  <!--2.选择多个  加上mutiple属性-->  
  <select name="abc" v-model="fruits" multiple>
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是: {{fruits}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      fruit: '香蕉',
      fruits: []
    }
  })
</script>

</body>
```

#### 值绑定 （动态的给value复制）

- 通过v-bind动态给value赋值

```js
 <!--2.checkbox多选框-->
  <input type="checkbox" value="篮球" v-model="hobbies">篮球
  <input type="checkbox" value="足球" v-model="hobbies">足球
  <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
  <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
  <h2>您的爱好是: {{hobbies}}</h2>

  <label v-for="item in originHobbies" :for="item">
    <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
  </label>
```

- 动态的绑定一个数组
- 不要把checkbox中的值写死

#### v-model修饰符的使用

lazy修饰符：

- 默认情况下，v-model默认是在input事件中同步输入框的数据的。

- 也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变。

- lazy修饰符可以让数据在失去焦点或者回车时才会更新：

nnumber修饰符：

- 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理。

- 但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。

- number修饰符可以让在输入框中输入的内容自动转成数字类型：

trim修饰符：

- 如果输入的内容首尾有很多空格，通常我们希望将其去除

- trim修饰符可以过滤内容左右两边的空格

```js
<body>

<div id="app">
  <!--1.修饰符: lazy--> 
  <input type="text" v-model.lazy="message">
  <h2>{{message}}</h2>


  <!--2.修饰符: number-->
  <input type="number" v-model.number="age">
  <h2>{{age}}-{{typeof age}}</h2>

  <!--3.修饰符: trim-->
  <input type="text" v-model.trim="name">
  <h2>您输入的名字:{{name}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      age: 0,
      name: ''
    }
  })

  var age = 0
  age = '1111'
  age = '222'
</script>

</body>
```

### 组件化开发

#### 认识组件化

- 人面对复杂问题的处理方式：
  任何一个人处理信息的逻辑能力都是有限的
  所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容。
  但是，我们人有一种天生的能力，就是将问题进行拆解。

- 如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解。

- 组件化也是类似的思想：

  - 如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展。

  - 但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了。

    

![02](http://ww1.sinaimg.cn/large/007WWC4agy1gswh63sslzj604s07ygm702.jpg)

- 我们将一个完整的页面分成很多个组件。

- 每个组件都用于实现页面的一个功能块。

- 而每一个组件又可以进行细分。

  

  ------------

  **组件化是Vue.js中的重要思想**

  ![03](http://ww1.sinaimg.cn/large/007WWC4agy1gswh6lkrcwj60hi06s3yv02.jpg)

  它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
  任何的应用都会被抽象成一颗组件树。

  组件化思想的应用：
  有了组件化的思想，我们在之后的开发中就要充分的利用它。
  尽可能的将页面拆分成一个个小的、可复用的组件。
  这样让我们的代码更加方便组织和管理，并且扩展性也更强。
  所以，组件是Vue开发中，非常重要的一个篇章，要认真学习。

  ---------------

  

#### 注册组件

组件的使用分成三个步骤：

- 创建组件构造器

- 注册组件

- 使用组件。
  我们来看看通过代码如何注册组件
  查看运行结果：

  ![04](http://ww1.sinaimg.cn/large/007WWC4agy1gswh7o19sqj607w0cojsw02.jpg)

  ```js
  <body>
  
  <div id="app">
    <!--3.使用组件-->
    <my-cpn></my-cpn>
    <my-cpn></my-cpn>
    <my-cpn></my-cpn>
    <my-cpn></my-cpn>
  
    <div>
      <div>
        <my-cpn></my-cpn>
      </div>
    </div>
  </div>
  
  <my-cpn></my-cpn>
  
  <script src="../js/vue.js"></script>
  <script>
    // 1.创建组件构造器对象
    const cpnC = Vue.extend({
      template: `
        <div>
          <h2>我是标题</h2>
          <p>我是内容, 哈哈哈哈</p>
          <p>我是内容, 呵呵呵呵</p>
        </div>`
    })
  
    // 2.注册组件
    Vue.component('my-cpn', cpnC)
  
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      }
    })
  </script>
  
  </body>
  ```
  
  
  
  和直接使用一个div看起来并没有什么区别。
  但是我们可以设想，如果很多地方都要显示这样的信息，我们是不是就可以直接使用<my-cpn></my-cpn>来完成呢？
  
- 这里的步骤都代表什么含义呢？

  **1.Vue.extend()：**

  调用Vue.extend()创建的是一个组件构造器。 
  通常在创建组件构造器时，传入template代表我们自定义组件的模板。
  该模板就是在使用到组件的地方，要显示的HTML代码。
  事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。

  **2.Vue.component()：**

  调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。
  所以需要传递两个参数：1、注册组件的标签名 2、组件构造器

  **3.组件必须挂载在某个Vue实例下，否则它不会生效。**

  我们来看下面我使用了三次<my-cpn></my-cpn>
  而第三次其实并没有生效：

  ![05](http://ww1.sinaimg.cn/large/007WWC4agy1gswhae53v2j60v60ctwm302.jpg)

####  全局组件和局部组件

- 当我们通过调用Vue.component()注册组件时，组件的注册是全局的

- 这意味着该组件可以在任意Vue示例下使用。

- 如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

  ```javascript
  <body>
      <div id="app"></div>
  
      <script>
        //1.创建组件构造器
        const cpnC = Vue.extend({
          template: `
          <div>
          <h2>我是标题</h2>
          <p>我是内容,哈哈哈哈啊</p>
        </div>
          `,
        });
  
        //   2.注册组件(全局组件)
        //   Vue.component("cpn", cpnC);
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
          },
          // 局部组件
          components: {
            cpn: cpnC,
          },
        });
      </script>
    </body>
  ```
  

#### 父组件和子组件

在前面我们看到了组件树：
组件和组件之间存在层级关系
而其中一种非常重要的关系就是父子组件的关系


- 父子组件错误用法：以子标签的形式在Vue实例中使用

- 因为当子组件注册到父组件的components时，Vue会编译好父组件的模块

- 该模板的内容已经决定了父组件将要渲染的HTML（相当于父组件中已经有了子组件中的内容了）

- <cpnC1></cpnC1>是只能在父组件中被识别的。

- 类似这种用法，<cpnC1></cpnC1>是会被浏览器忽略的。

- **组件注册的位置决定了组件是父组件还是子组件**

  ```javascript
  <body>
      <div id="app">{{message}}</div>
      <script src="../vue.js"></script>
      <script>
        // 1.创建第一各组件（子组件）
        const cpnC1 = Vue.extend({
          template: `
        <div>
          <h2>我是标题1</h2>
          <p>我是内容, 哈哈哈哈</p>
        </div>
      `,
        });
        //   2.创建第二个组件(父组件)
  
        const cpnC2 = Vue.extend({
          template: `
        <div>
          <h2>我是标题2</h2>
          <p>我是内容, 呵呵呵呵</p>
          <cpn1></cpn1>
        </div>
        `,
          components: {
            cpn1: cpnC1,
          },
        });
  
        // root组件
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
          },
          components: {
            cpn2: cpnC2,
          },
        });
      </script>
    </body>
  ```

  

#### 注册组件语法糖

- 在上面注册组件的方式，可能会有些繁琐。

- Vue为了简化这个过程，提供了注册的语法糖。

- 主要是省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替。

  - 语法糖注册全局组件和局部组件：

    ```html
    <body>
        <div id="app">
          <cpn1></cpn1>
          <cpn2></cpn2>
        </div>
        <script src="../vue.js"></script>
        <script>
          // 1.创建组件构造器
          // const cpn1=Vue.extend()
    
          // 注册组件(语法糖)(全局组件)
          Vue.component("cpn1", {
            template: `
          <div>
            <h2>我是标题1</h2>
            <p>我是内容, 哈哈哈哈</p>
          </div>
        `,
          });
        </script>
        <script>
          const app = new Vue({
            el: "#app",
            data: {
              message: "你好啊",
            },
              //局部组件（语法糖）
            components: {
              cpn2: {
                template: `
              <div>
                <h2>我是标题2</h2>
                <p>我是内容, 呵呵呵</p>
              </div>
        `,
              },
            },
          });
        </script>
      </body>
    ```

    

#### 模板的分离写法

刚才，我们通过语法糖简化了Vue组件的注册过程，另外还有一个地方的写法比较麻烦，就是template模块写法。
如果我们能将其中的HTML分离出来写，然后挂载到对应的组件上，必然结构会变得非常清晰。
Vue提供了两种方案来定义HTML模块内容：

- 使用<script>标签
- 使用<template>标签

```javascript
<body>
    <div id="app">
      <cpn></cpn>
    </div>
    <!-- 1.script标签 -->
    <!-- <script type="text/x-template" id="cpn">
      <div>
          <h2>我是标题</h2>
          <p>我是内容</p>
      </div>
    </script> -->

    <!-- 2.template标签 -->
    <template id="cpn">
      <div>
        <h2>我是标题</h2>
        <p>我是内容,呵呵呵</p>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      // 注册一个全局组件
      Vue.component("cpn", {
        template: "#cpn",
      });
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
      });
    </script>
  </body>
```



#### 组件数据存放

##### 组件可以访问Vue实例里面的数据吗

组件是一个单独功能模块的封装：
这个模块有属于自己的HTML模板，也应该有属性自己的数据data。
组件中的数据是保存在哪里呢？顶层的Vue实例中吗？
我们先来测试一下，组件中能不能直接访问Vue实例中的data

![05](http://ww1.sinaimg.cn/large/007WWC4agy1gswjzyv06nj60e80ahju502.jpg)

我们发现不能访问，而且即使可以访问，如果将所有的数据都放在Vue实例中，Vue实例就会变的非常臃肿。
**结论：Vue组件应该有自己保存数据的地方**

组件自己的数据存放在哪里呢?
组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)
只是这个data属性必须是一个函数
而且这个函数返回一个对象，对象内部保存着数据

![image-20210523232952935](D:\vuejs学习笔记\image-20210523232952935.png)

##### vue组件中的data为什么是个函数呢

为什么data在组件中必须是一个函数呢?

- 首先，如果不是一个函数，Vue直接就会报错。
- 其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。



#### 父子组件通信

- 子组件是不能引用父组件或者Vue实例的数据的。
- 但是，在开发中，往往一些数据确实需要从上层传递到下层：
- 比如在一个页面中，我们从服务器请求到了很多的数据。
- 其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示。
- 这个时候，并不会让子组件再次发送一个网络请求，而是直接让大组件(父组件)将数据传递给小组件(子组件)。
  **如何进行父子组件间的通信呢？Vue官方提到**
  - 通过props向子组件传递数据
  - 通过事件向父组件发送消息

![06](http://ww1.sinaimg.cn/large/007WWC4agy1gswk2897orj60fp06xwfq02.jpg)

##### 父组件向子组件传递函数（props）

**props的值有两种方式：**

- 方式一：字符串数组，数组中的字符串就是传递时的名称。
- 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等
- 具体下面代码展示

```javascript
<body>
    <div id="app">
      <cpn :cmessage="message" :cmovies="movies"></cpn>
    </div>
    <template id="cpn">
      <div>
        <ul>
          <li v-for="item in cmovies">{{item}}</li>
        </ul>
        <h2>{{cmessage}}</h2>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      // 父传子：props
      const cpn = {
        template: "#cpn",
        props: {
          //1.类型限制
          // 2.提供一些默认值，以及必传值

          cmovies: {
            type: Array,
            default() {
              return [];
            },
          },
          cmessage: {
            type: String,
            default: "aaaaaa",
            required: true,
          },
        },
      };
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          movies: ["你好", "海贼王", "悲伤逆流成河"],
        },
        components: {
          cpn,
        },
      });
    </script>
  </body>
```

**props数据验证**

> 在前面，我们的props选项是使用一个数组。
> 我们说过，除了数组之外，我们也可以使用对象，当需要对props进行类型等验证时，就需要对象写法了。
> 验证都支持哪些数据类型呢？
> String
> Number
> Boolean
> Array
> Object
> Date
> Function
> Symbol
> 当我们有自定义构造函数时，验证也支持自定义的类型

![image-20210523233618843](D:\vuejs学习笔记\image-20210523233618843.png)

![image-20210523233625051](D:\vuejs学习笔记\image-20210523233625051.png)

##### 子组件向父组件传递（$emit）

props用于父组件向子组件传递数据，还有一种比较常见的是子组件传递数据或事件到父组件中。
我们应该如何处理呢？这个时候，我们需要使用自定义事件来完成。
**什么时候需要自定义事件呢？**

- 当子组件需要向父组件传递数据时，就要用到自定义事件了。
- 我们之前学习的v-on不仅仅可以用于监听DOM事件，也可以用于组件间的自定义事件。
  **自定义事件的流程：**
  - 在子组件中，通过$emit()来触发事件。
  - 在父组件中，通过v-on来监听子组件事件。
  - 我们来看一个简单的例子：
  - 我们之前做过一个两个按钮+1和-1，点击后修改counter。
  - 我们整个操作的过程还是在子组件中完成，但是之后的展示交给父组件。
    这样，我们就需要将子组件中的counter，传给父组件的某个属性，比如total。

```javascript
<body>
    <div id="app">
      <cpn @item-click="cpnClick"></cpn>
    </div>
    <template id="cpn">
      <div>
        <button v-for="item in categories" @click="btnClick(item)">
          {{item.name}}
        </button>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      const cpn = {
        template: "#cpn",
        data() {
          return {
            categories: [
              { id: "aaa", name: "热门推荐" },
              { id: "bbb", name: "手机数码" },
              { id: "ccc", name: "家用家电" },
              { id: "ddd", name: "电脑办公" },
            ],
          };
        },
        methods: {
          btnClick(item) {
            //   发射事件：自定义事件
            this.$emit("item-click", item);
          },
        },
      };
      //   2.父组件
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        components: {
          cpn,
        },
        methods: {
          cpnClick(item) {
            console.log("cpnClick", item);
          },
        },
      });
    </script>
  </body>
```



##### 父子组件的访问方式

有时候我们需要父组件直接访问子组件，子组件直接访问父组件，或者是子组件访问根组件。

- 父组件访问子组件：使用$children或$refs

  > $children的缺陷：
  >
  > - 通过$children访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值。
  >   但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化。
  >   有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用$refs
  >
  >   $refs的使用：
  >   $refs和ref指令通常是一起使用的。
  >
  > - 首先，我们通过**ref**给某一个子组件绑定一个特定的ID。
  > - 其次，通过**this.$refs.ID**就可以访问到该组件了。
  >

  ```js
   <body>
      <div id="app">
        <cpn ref="aaa"></cpn>
        <cpn></cpn>
        <cpn></cpn>
        <button @click="btnClick">按钮</button>
      </div>
      <template id="cpn">
        <div>我是子组件</div>
      </template>
      <script src="../vue.js"></script>
      <script>
        const app = new Vue({
          el: "#app",
          data: {
            message: "你好啊",
          },
          methods: {
            btnClick() {
              // console.log(this.$children);
              // for (let c of this.$children) {
              //   console.log(c.name);
              //   c.showMessage();
              // }
              // console.log(this.$children[0].showMessage);
              console.log(this.$refs);
              console.log(this.$refs.aaa.name);
            },
          },
          components: {
            cpn: {
              template: "#cpn",
              data() {
                return {
                  name: "我是子组件的name",
                };
              },
              methods: {
                showMessage() {
                  console.log("showMessage");
                },
              },
            },
          },
        });
      </script>
    </body>
  ```

- 子组件访问父组件：使用$parent

  - 尽管在Vue开发中，我们允许通过$parent来访问父组件，但是在真实开发中尽量不要这样做。
  
  - 子组件应该尽量避免直接访问父组件的数据，因为这样耦合度太高了。
  
  - 如果我们将子组件放在另外一个组件之内，很可能该父组件没有对应的属性，往往会引起问题。
  
  - 另外，更不好做的是通过$parent直接修改父组件的状态，那么父组件中的状态将变得飘忽不定，很不利于我的调试和维护。

#### 插槽（slot）

- slot翻译为插槽

   在生活中很多地方都有插槽，电脑的USB插槽，插板当中的电源插槽。
  插槽的目的是让我们原来的设备具备更多的扩展性。
  比如电脑的USB我们可以插入U盘、硬盘、手机、音响、键盘、鼠标等等。

- 组件的插槽：
  组件的插槽也是为了让我们封装的组件更加具有**扩展性**和组件的**复用性**。

  这样就可以同一个组件在多个地方使用，同时也可以通过插槽修改其不同的地方

  让使用者可以决定组件内部的一些内容到底展示什么。

##### 插槽的基本使用

- 如何封装这类组件呢

  它们也很多区别，但是也有很多共性。
  如果，我们每一个单独去封装一个组件，显然不合适：比如每个页面都返回，这部分内容我们就要重复去封装。但是，如果我们封装成一个，好像也不合理：有些左侧是菜单，有些是返回，有些中间是搜索，有些是文字，等等。

- 如何封装合适呢？抽取共性，保留不同。
  最好的封装方式就是将共性抽取到组件中，将不同暴露为插槽。
  一旦我们预留了插槽，就可以让使用者根据自己的需求，决定插槽中插入什么内容。
  是搜索框，还是文字，还是菜单。由调用者自己来决定。
  
  ![image-20210524225724862](http://ww1.sinaimg.cn/large/007WWC4agy1gswkgic1r4j60fu09bwie02.jpg)

```javascript
<body>
    <div id="app">
      <cpn><button>按钮</button></cpn>
      <cpn></cpn>
    </div>
    <template id="cpn">
      <div>
        <h2>我是组件</h2>
        <p>我是组件哈哈哈</p>
        <slot></slot>
        <!-- <button>按钮</button> -->
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        components: {
          cpn: {
            template: "#cpn",
          },
        },
      });
    </script>
  </body>
```

##### 具名插槽(给每个插槽取个名字)
- 当子组件的功能复杂时，子组件的插槽可能并非是一个。
  比如我们封装一个导航栏的子组件，可能就需要三个插槽，分别代表左边、中间、右边。
  那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？

- 这个时候，我们就需要给插槽起一个名字
如何使用具名插槽呢？

- 非常简单，只要给slot元素一个name属性即可
  ```<slot name='myslot'></slot>```

  

  

  ![image-20210524231206507](http://ww1.sinaimg.cn/large/007WWC4agy1gswkhnqorej60j907xn0l02.jpg)

```javascript
<body>
    <div id="app">
      <cpn><span slot="mid">如果</span></cpn>
    </div>
    <template id="cpn">
      <div>
        <slot name="left"><span>左边</span></slot>
        <slot name="mid"><span>中间</span></slot>
        <slot name="right"><span>右边</span></slot>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        components: {
          cpn: {
            template: "#cpn",
          },
        },
      });
    </script>
  </body>
```



##### 什么是编译作用域

- 父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。

- 父组件不能引用子组件中的数据，子组件也不能引用父组件中的数据

  ![image-20210524232734364](http://ww1.sinaimg.cn/large/007WWC4agy1gswkiunakcj60kv0h8wk502.jpg)

![image-20210524233040293](http://ww1.sinaimg.cn/large/007WWC4agy1gswkjwg3dcj60gj0e2tde02.jpg)

```javascript
 <body>
    <div id="app">
      <cpn v-show="isShow"></cpn>
    </div>
    <template id="cpn">
      <div>
        <h2>你看到我了吗</h2>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
          isShow: true,
        },
        components: {
          cpn: {
            template: "#cpn",
            data() {
              return {
                isShow: false,
              };
            },
          },
        },
      });
    </script>
  </body>
```

##### 小案例（作用域插槽使用）

> 作用域插槽是slot一个比较难理解的点，而且官方文档说的又有点不清晰。
> 这里，我们用一句话对其做一个总结，然后我们在后续的案例中来体会：
> 父组件替换插槽的标签，但是内容由子组件来提供。
> 我们先提一个需求：
> 子组件中包括一组数据，比如：pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']
> 需要在多个界面进行展示：
> 某些界面是以水平方向一一展示的，
> 某些界面是以列表形式展示的，
> 某些界面直接展示一个数组
> 内容在子组件，希望父组件告诉我们如何展示，怎么办呢？
> 利用slot作用域插槽就可以了
> 我们来看看子组件的定义：
>
> 在父组件使用我们的子组件时，从子组件中拿到数据：
> 我们通过<template slot-scope="slotProps">获取到slotProps属性
> 再通过slotProps.data就可以获取到刚才我们传入的data了

```javascript
<body>
    <!-- 我想要以和子组件规定的不同方式来显示数据 -->
    <div id="app">
      <cpn></cpn>
      <cpn>
        <template slot-scope="slot">
          <span>{{slot.data.join('-')}}</span>
        </template>
      </cpn>
    </div>
    <template id="cpn">
      <div>
        <slot :data="pLanguages">
          <ul>
            <li v-for="item in pLanguages">{{item}}</li>
          </ul>
        </slot>
      </div>
    </template>
    <script src="../vue.js"></script>
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "你好啊",
        },
        components: {
          cpn: {
            template: "#cpn",
            data() {
              return {
                pLanguages: [
                  "JavaScript",
                  "C++",
                  "Java",
                  "C#",
                  "Python",
                  "Go",
                  "Swift",
                ],
              };
            },
          },
        },
      });
    </script>
  </body>
```

## 模块化开发

### 为什么要模块化

- 在网页开发的早期，js制作作为一种脚本语言，做一些简单的表单验证或动画实现等，那个时候代码还是很少的。
- 那个时候的代码是怎么写的呢？直接将代码写在<script>标签中即可
- 随着ajax异步请求的出现，慢慢形成了前后端的分离
- 客户端需要完成的事情越来越多，代码量也是与日俱增。
- 为了应对代码量的剧增，我们通常会将代码组织在多个js文件中，进行维护。
- 但是这种维护方式，依然不能避免一些灾难性的问题。
  - 比如全局变量同名问题
  - 另外，这种代码的编写方式对js文件的依赖顺序几乎是强制性的
  - 但是当js文件过多，比如有几十个的时候，弄清楚它们的顺序是一件比较难的事情。
  - 而且即使你弄清楚顺序了，也不能避免上面出现的这种尴尬问题的发生。

-  小明后来发现代码不能正常运行，去检查自己的变量，发现确实true
- 最后杯具发生了，小明加班到2点还是没有找到问题出在哪里(所以，某些加班真的是无意义的)

### 匿名函数的解决方案

- 我们可以使用匿名函数来解决重名问题

- 在aaa.js文件中，我们使用匿名函数

  ```js
  (function() {
      var flag =true
  })()
  ```

- 但是如果我们希望在main.js文件中，用到flag，应该如何处理呢？
- 显然，另外一个文件中不容易使用，因为flag是一个局部变量。

### 使用模块作为出口

- 我们可以使用将需要暴露到外面的变量，使用一个模块作为出口，什么意思呢？
  来看下对应的代码：

```js
var ModuleA =(function() {
    //定义一个对象
    var obj={};
    //在对象内部添加变量和方法
    obj.flag=true;
    obj.myfunc=function(info){
        console.log(info);
    }
    //将对象返回
    return obj
})()
```

```js
if(ModuleA.flag) {
    console.log('小明是个天才');
    ModuleA.myfunc('小明长得真帅');
    console.log(ModuleA);
}
```



- 我们做了什么事情呢？
- 非常简单，在匿名函数内部，定义一个对象。
- 给对象添加各种需要暴露到外面的属性和方法(不需要暴露的直接定义即可)。
- 最后将这个对象返回，并且在外面使用了一个MoudleA接受。
- 接下来，我们在man.js中怎么使用呢？
- 我们只需要使用属于自己模块的属性和方法即可
- 这就是模块最基础的封装，事实上模块的封装还有很多高级的话题：
  - 但-是我们这里就是要认识一下为什么需要模块，以及模块的原始雏形。
  - 幸运的是，前端模块化开发已经有了很多既有的规范，以及对应的实现方案。
  - 常见的模块化规范：
    CommonJS、AMD、CMD，也有ES6的Modules

### CommonJs

模块化有两个核心：导出(export)和导入(require)
CommonJS的导出：

```js
module.exports={
    flag:true,
    test(a,b) {
        return a+b
    },
    demo(a,b) {
        return a-b
    }
}
```



CommonJS的导入

```js
//CommonJs模块
let {test,demo,flag}=require("moduelA")

//等同于
let _mA=require('moduleA');
let test=_mA.test;
let demo=_mA.demo;
let flag=_mA.flag;
```



### ES6的export基本使用

export指令用于导出变量，比如下面的代码：

```js
//info.js
export let name='why'
export let age=18
export let height=1.88
```

上面的代码还有另外一种写法：

```js
let name='why'
let age=18
let height=1.88

export {name,age,height}
```

```javascript
var name = '小明'
var age = 18
var flag = true

function sum(num1, num2) {
  return num1 + num2
}

if (flag) {
  console.log(sum(20, 30));
}

// 1.导出方式一:
export {
  flag, sum
}

// 2.导出方式二:
export var num1 = 1000;
export var height = 1.88


// 3.导出函数/类
export function mul(num1, num2) {
  return num1 * num2
}

export class Person {
  run() {
    console.log('在奔跑');
  }
}

// 5.export default
// const address = '北京市'
// export {
//   address
// }
// export const address = '北京市'
// const address = '北京市'
//
// export default address

export default function (argument) {
  console.log(argument);
}
```

#### export default

某些情况下，一个模块中包含某个的功能，我们并不希望给这个功能命名，而且让导入者可以自己来命名
这个时候就可以使用export default

```js
//info.js
export default function(){
    conosle.log('default funciton')
}
```

我们来到main.js中，这样使用就可以了
这里的myFunc是我自己命名的，你可以根据需要命名它对应的名字

```js
import myFunc from './info.js'
myFunc()
```

另外，需要注意：
export default在同一个模块中，不允许同时存在多个(有且仅有一个)

#### import使用

我们使用export指令导出了模块对外提供的接口，下面我们就可以通过import命令来加载对应的这个模块了
首先，我们需要在HTML代码中引入两个js文件，并且类型需要设置为module

```js
<script src='info.js' type="module"></script>
<script src='main.js' type="module"></script>
```

import指令用于导入模块中的内容，比如main.js的代码

```js
import {name,age,height} from './info.js'
console.log(name,age,height)
```

如果我们希望某个模块中所有的信息都导入，一个个导入显然有些麻烦：
通过可以导入模块中所有的export变量
但是通常情况下我们需要给起一个别名，方便后续的使用

```js
import * as info from './info.js'
console.log(info.name,info.height,info.friends);
```

```javascript
// 1.导入的{}中定义的变量
import {flag, sum} from "./aaa.js";

if (flag) {
  console.log('小明是天才, 哈哈哈');
  console.log(sum(20, 30));
}

// 2.直接导入export定义的变量
import {num1, height} from "./aaa.js";

console.log(num1);
console.log(height);

// 3.导入 export的function/class
import {mul, Person} from "./aaa.js";

console.log(mul(30, 50));

const p = new Person();
p.run()

// 4.导入 export default中的内容
import addr from "./aaa.js";

addr('你好啊');

// 5.统一全部导入
// import {flag, num, num1, height, Person, mul, sum} from "./aaa.js";

import * as aaa from './aaa.js'

console.log(aaa.flag);
console.log(aaa.height);

```

## webpack

### webpack安装步骤 

  [博客地址](https://www.cnblogs.com/ff-upday/p/14819395.html)

### webpack配置 

  [博客地址](https://www.cnblogs.com/ff-upday/p/14819482.html)

### webpack的扩展loader  

[博客地址](https://www.cnblogs.com/ff-upday/p/14843444.html)

### url-loader 

首先，我们在项目中加入两张图片：

放一张较小的图片test01.jpg(小于8kb)，一张较大的图片test02.jpeg(大于8kb)

待会儿我们会针对这两张图片进行不同的处理

如果我们现在直接打包，会出现如下问题

![image-20210608194424290](D:\vuejs学习笔记\image-20210608194424290.png)

图片处理，我们使用url-loader来处理，依然先安装url-loader

```cmd
npm install url-loader --save-dev  
```

修改webpack.config.js配置文件

```json
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/i,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192,
            },
          },
        ],
      },
    ],
  },
};
```

再次打包，运行index.html，就会发现我们的背景图片选出了出来。

而仔细观察，你会发现背景图是通过base64显示出来的

OK，这也是limit属性的作用，当图片小于8kb时，对图片进行base64编码

那么问题来了，如果大于8kb呢？我们将background的图片改成test02.jpg

这次因为大于8kb的图片，会通过file-loader进行处理，但是我们的项目中并没有file-loader

所以，我们需要安装file-loader

```cmd
npm install file-loader --save-dev
```

```json
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpe?g|gif)$/i,
        use: [
          {
            loader: 'file-loader',
          },
        ],
      },
    ],
  },
};
```

再次打包，就会发现dist文件夹下多了一个图片文件

![image-20210608194458456](D:\vuejs学习笔记\image-20210608194458456.png)

#### **图片文件处理** **–** **修改文件名称**

我们发现webpack自动帮助我们生成一个非常长的名字

这是一个32位hash值，目的是防止名字重复

但是，真实开发中，我们可能对打包的图片名字有一定的要求

比如，将所有的图片放在一个文件夹中，跟上图片原来的名称，同时也要防止重复 

```js
options:{
    limit:8192,
    name:'img/[name].[hash:8].[ext]'
}
```

> 所以，我们可以在options中添加上如下选项：
>

> img：文件要打包到的文件夹
>

> name：获取图片原来的名字，放在该位置
>

> hash:8：为了防止图片名称冲突，依然使用hash，但是我们只保留8位
>

> ext：使用图片原来的扩展名
>

但是，我们发现图片并没有显示出来，这是因为图片使用的路径不正确

默认情况下，webpack会将生成的路径直接返回给使用者

但是，我们整个程序是打包在dist文件夹下的，所以这里我们需要在路径下再添加一个dist/

```js
//出口：通常是一个对象，里面至少包含两个重要属性，path 和 filename
output:{
    path:path.resolve(_dirname,'dist'),//注意path通常是一个绝对路径
    filename:'dist/'
},
```



### webpack配置vue

[博客地址](https://www.cnblogs.com/ff-upday/p/14864573.html)

#### **.****vue****文件封装处理**

但是一个组件以一个js对象的形式进行组织和使用的时候是非常不方便的

一方面编写template模块非常的麻烦

另外一方面如果有样式的话，我们写在哪里比较合适呢？

现在，我们以一种全新的方式来组织一个vue的组件

但是，这个时候这个文件可以被正确的加载吗？

必然不可以，这种特殊的文件以及特殊的格式，必须有人帮助我们处理。

谁来处理呢？vue-loader以及vue-template-compiler。

安装vue-loader和vue-template-compiler

```cmd
npm install vue-loader vue-template-compiler --save-dev
```

修改webpack.config.js的配置文件：

![image-20210608195815755](D:\vuejs学习笔记\image-20210608195815755.png)

### **认识****plugin**

#### plugin是什么？

plugin是插件的意思，通常是用于对某个现有的架构进行扩展。

webpack中的插件，就是对webpack现有功能的各种扩展，比如打包优化，文件压缩等等。

#### loader和plugin区别

loader主要用于转换某些类型的模块，它是一个转换器。

plugin是插件，它是对webpack本身的扩展，是一个扩展器。

#### plugin的使用过程：

步骤一：通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)

步骤二：在webpack.config.js中的plugins中配置插件。

下面，我们就来看看可以通过哪些插件对现有的webpack打包过程进行扩容，让我们的webpack变得更加好用。

##### **添加版权的****Plugin**

按照下面的方式来修改webpack.config.js的文件：

![image-20210608230545694](http://ww1.sinaimg.cn/large/007WWC4agy1gswmdehjwxj60l60d3wje02.jpg)

重新打包程序：查看main.js.LICENSE文件的头部，看到如下信息

![image-20210608230622645](http://ww1.sinaimg.cn/large/007WWC4agy1gswme7dqvhj60e506adhl02.jpg)

##### **打包****html****的****plugin**

- 目前，我们的index.html文件是存放在项目的根目录下的。

- 我们知道，在真实发布项目时，发布的是dist文件夹中的内容，但是dist文件夹中如果没有index.html文件，那么打包的js等文件也就没有意义了。

- 所以，我们需要将index.html文件打包到dist文件夹中，这个时候就可以使用HtmlWebpackPlugin插件

**HtmlWebpackPlugin插件可以为我们做这些事情：**

- 自动生成一个index.html文件(可以指定模板来生成)

- 将打包的js文件，自动通过script标签插入到body中

- 安装HtmlWebpackPlugin插件

```cmd
npm install html-webpack-plugin --save-dev
```

**使用插件，修改webpack.config.js文件中plugins部分的内容如下：**

- 这里的template表示根据什么模板来生成index.html

- 另外，我们需要删除之前在output中添加的publicPath属性

- 否则插入的script标签中的src可能会有问题

  ![image-20210608231552270](http://ww1.sinaimg.cn/large/007WWC4agy1gswmg3fb44j60j805v76g02.jpg)

##### **js****压缩的****Plugin**

在项目发布之前，我们必然需要对js等文件进行压缩处理

这里，我们就对打包的js文件进行压缩

我们使用一个第三方的插件uglifyjs-webpack-plugin

```cmd
npm install uglifyjs-webpack-plugin --save-dev
```

修改webpack.config.js文件，使用插件：

![image-20210608235709298](D:\vuejs学习笔记\image-20210608235709298.png)

查看打包后的main.js文件，是已经被压缩过了

## **搭建本地服务器**

webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

不过它是一个单独的模块，在webpack中使用之前需要先安装它

```cmd
npm install --save-dev webpack-dev-server
```

devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：

contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist

port：端口号

inline：页面实时刷新

historyApiFallback：在SPA页面中，依赖HTML5的history模式

webpack.config.js文件配置修改如下

![image-20210608235955950](D:\vuejs学习笔记\image-20210608235955950.png)

我们可以再配置另外一个scripts：

![image-20210609001350740](http://ww1.sinaimg.cn/large/007WWC4agy1gswmhie059j60jx04ddhf02.jpg)

--open参数表示直接打开浏览器



## Vue CLI

- 在开发大型项目, 那么你需要, 并且必然需要使用Vue CLI

- 使用Vue.js开发大型应用时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情。

- 如果每个项目都要手动完成这些工作，那无疑效率比较低效，所以通常我们会使用一些脚手架工具来帮助完成这些事情。

**CLI****是什么意思****?**

- CLI是Command-Line Interface, 翻译为命令行界面, 但是俗称脚手架.

- Vue CLI是一个官方发布 vue.js 项目脚手架

- 使用 vue-cli 可以快速搭建Vue开发环境以及对应的webpack配置.

#### Vue CLI使用前提 - Node

**安装****NodeJS**

可以直接在官方网站中下载安装.

网址: http://nodejs.cn/download/

**检测安装的版本**

默认情况下自动安装Node和NPM

Node环境要求8.9以上或者更高版本

**什么是****NPM****呢****?**

NPM的全称是Node Package Manager

是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。

后续我们会经常使用NPM来安装一些开发过程中依赖包.

> cnpm安装
>
> 由于国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。
>
> 你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:
>
> npm install -g cnpm --registry=https://registry.npm.taobao.org
>
> 这样就可以使用 cnpm 命令来安装模块了：
>
> cnpm install [name]

#### **Vue** **CLI****使用前提** **-** **Webpack**

Vue.js官方脚手架工具就使用了webpack模板

对所有的资源会压缩等优化操作

它在开发过程中提供了一套完整的功能，能够使得我们开发过程中变得高效。

Webpack的全局安装

```javascript
npm install webpack -g
```

#### **Vue** **CLI****的使用**

安装Vue脚手架

https://cli.vuejs.org/zh/guide/installation.html

```javascript
npm install -g @vue/cli
```

注意：上面安装的是Vue CLI3的版本，如果需要想按照Vue CLI2的方式初始化项目是不可以的。

如果你想使用Vue CLI2：

![image-20210609235545488](http://ww1.sinaimg.cn/large/007WWC4agy1gswmorydnij60li07977302.jpg)

###### Vue CLI2初始化项目

```javascript
vue init webpack my-project
```

###### Vue CLI3初始化项目

```javascri
vue create my-project
```

#### Vue CLI2初始化项目解析

![image-20210614120552204](http://ww1.sinaimg.cn/large/007WWC4agy1gswmp413d8j60s40dcwmo02.jpg)

![image-20210614121357471](http://ww1.sinaimg.cn/large/007WWC4agy1gswmplqtbnj60iu0hmwkv02.jpg)

#### **Runtime-Compiler****和****Runtime-only****的区别**

简单总结

如果在之后的开发中，你依然使用template，就需要选择Runtime-Compiler

如果你之后的开发中，使用的是.vue文件夹开发，那么可以选择Runtime-only

#### **render****和****template**

Runtime-Compiler

![image-20210614122858330](http://ww1.sinaimg.cn/large/007WWC4agy1gswmqln2vmj60ai04kgm502.jpg)

Runtime-Only

![image-20210614122917760](http://ww1.sinaimg.cn/large/007WWC4agy1gswmr5k20aj60ac03kt9002.jpg)

为什么存在这样的差异呢？

我们需要先理解Vue应用程序是如何运行起来的。

Vue中的模板如何最终渲染成真实DOM。

我们来看下面的一幅图。

Vue程序运行过程：

![image-20210614123006979](http://ww1.sinaimg.cn/large/007WWC4agy1gswmrlpu3sj60r60enjuc02.jpg)

![image-20210614123624554](D:\vuejs学习笔记\image-20210614123624554.png)

![image-20210614123631432](D:\vuejs学习笔记\image-20210614123631432.png)

![image-20210614123638055](D:\vuejs学习笔记\image-20210614123638055.png)

#### npm run build

![image-20210614124915389](http://ww1.sinaimg.cn/large/007WWC4agy1gswmsbe3jqj60vr0fljx602.jpg)

#### npm run dev

![image-20210614124938402](http://ww1.sinaimg.cn/large/007WWC4agy1gswmsmd4dvj60x60g2jxp02.jpg)

#### **修改配置：****webpack.base.conf.js****起别名**

![image-20210614125003785](http://ww1.sinaimg.cn/large/007WWC4agy1gswmt0ia92j60lp09zjua02.jpg)

#### **认识****Vue CLI3**

- vue-cli 3 与 2 版本有很大区别

- vue-cli 3 是基于 webpack 4 打造，vue-cli 2 还是 webapck 3

- vue-cli 3 的设计原则是“0配置”，移除的配置文件根目录下的，build和config等目录

- vue-cli 3 提供了 vue ui 命令，提供了可视化配置，更加人性化

- 移除了static文件夹，新增了public文件夹，并且index.html移动到public中

![image-20210614145110367](http://ww1.sinaimg.cn/large/007WWC4agy1gswmtlqas7j60xm0dtn7n02.jpg)

![image-20210614145553464](http://ww1.sinaimg.cn/large/007WWC4agy1gswmu1v2e1j60fi0ag0vr02.jpg)

#### **配置去哪里了？**

1、UI方面的配置

启动配置服务器：vue ui

![image-20210614145745492](http://ww1.sinaimg.cn/large/007WWC4agy1gswmula8qxj60ru0eb78202.jpg)

2、直接到node_modules找

![image-20210614145831502](http://ww1.sinaimg.cn/large/007WWC4agy1gswmv1oqu9j60af0dzjtm02.jpg)

3、**自定义配置：起别名**

![image-20210614145951059](http://ww1.sinaimg.cn/large/007WWC4agy1gswmvdva2ij60gz0fwaeu02.jpg)

## 什么是路由？

说起路由你想起了什么？

- 路由是一个网络工程里面的术语。

- **路由**（**routing**）就是通过互联的网络把信息从源地址传输到目的地址的活动. --- 维基百科

额, 啥玩意? 没听懂

在生活中, 我们有没有听说过路由的概念呢? 当然了, 路由器嘛.

路由器是做什么的? 你有想过吗?

- 路由器提供了两种机制: 路由和转送.

- 路由是决定数据包从**来源**到**目的地**的路径.

- 转送将**输入端**的数据转移到合适的**输出端**.

- 路由中有一个非常重要的概念叫路由表.

- 路由表本质上就是一个映射表, 决定了数据包的指向.

#### **后端路由阶段**

早期的网站开发整个HTML页面是由服务器来渲染的.

服务器直接生产渲染好对应的HTML页面, 返回给客户端进行展示.

但是, 一个网站, 这么多页面服务器如何处理呢?

一个页面有自己对应的网址, 也就是URL.

URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理.

Controller进行各种处理, 最终生成HTML或者数据, 返回给前端.

这就完成了一个IO操作.

上面的这种操作, 就是后端路由.

当我们页面中需要请求不同的**路径**内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户顿.

这种情况下渲染好的页面, 不需要单独加载任何的js和css, 可以直接交给浏览器展示, 这样也有利于SEO的优化.

后端路由的缺点:

一种情况是整个页面的模块由后端人员来编写和维护的.

另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码.

而且通常情况下HTML代码和数据以及对应的逻辑会混在一起, 编写和维护都是非常糟糕的事情.



![01-后端路由阶段](http://ww1.sinaimg.cn/large/007WWC4agy1gswmybjavbj60xn0o242w02.jpg)

#### **前端路由阶段**

前后端分离阶段：

随着Ajax的出现, 有了前后端分离的开发模式.

后端只提供API来返回数据, 前端通过Ajax获取数据, 并且可以通过JavaScript将数据渲染到页面中.

这样做最大的优点就是前后端责任的清晰, 后端专注于数据上, 前端专注于交互和可视化上.

并且当移动端(iOS/Android)出现后, 后端不需要进行任何处理, 依然使用之前的一套API即可.

目前很多的网站依然采用这种模式开发.

![02-前端后端分离阶段](http://ww1.sinaimg.cn/large/007WWC4agy1gswmyp61xij60xn0o2aez02.jpg)

**单页面富应用阶段****:**

其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由.

也就是前端来维护一套路由规则.

前端路由的核心是什么呢？

改变URL，**但是页面不进行整体的刷新。**

如何实现呢？

![03-SPA页面页面的阶段](http://ww1.sinaimg.cn/large/007WWC4agy1gswmz0fmlbj60xn0o2goo02.jpg)

**前端路由中url和组件的关系**

![04-前端路由中url和组件的关系](http://ww1.sinaimg.cn/large/007WWC4agy1gswmzbfzixj60m509f75j02.jpg)

#### **URL****的****hash**

URL的hash

URL的hash也就是锚点(#), 本质上是改变window.location的href属性.

我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

![image-20210616151155772](http://ww1.sinaimg.cn/large/007WWC4agy1gswop5nstlj60ib06smym02.jpg)

#### HTML5的history模式：**pushState**

history接口是HTML5新增的, 它有五种模式改变URL而不刷新页面.

history.pushState()  //可以返回

![image-20210616223557894](http://ww1.sinaimg.cn/large/007WWC4agy1gswoptdxa4j60c20budha02.jpg)

#### HTML5的history模式：**replaceState**

history.replaceState()  //不可以返回

![image-20210616223846245](http://ww1.sinaimg.cn/large/007WWC4agy1gswoq7zqe9j60cj042q3c02.jpg)

#### HTML5的history模式：go

history.go()

> 因为 history.back() 等价于 history.go(-1)
>
> history.forward() 则等价于 history.go(1)
>
> 这三个接口等同于浏览器界面的前进后退

### **认识****vue****-router**

vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。

我们可以访问其官方网站对其进行学习: https://router.vuejs.org/zh/

vue-router是基于路由和组件的

路由用于设定访问路径, 将路径和组件映射起来.

在vue-router的单页面应用中, 页面的路径的改变就是组件的切换.

#### **安装和使用****vue****-router**

**步骤一: 安装vue-router**

```cmd
npm install vue-router --save
```

**步骤二: 在模块化工程中使用它(因为是一个插件, 所以可以通过Vue.use()来安装路由功能)**

第一步：导入路由对象，并且调用 Vue.use(VueRouter)

![image-20210616232202327](http://ww1.sinaimg.cn/large/007WWC4agy1gsworoo77qj60g1077wi102.jpg)

第二步：创建路由实例，并且传入路由映射配置

![image-20210616232552667](http://ww1.sinaimg.cn/large/007WWC4agy1gswosmxqdzj60h50ccn2k02.jpg)

第三步：在Vue实例中挂载创建的路由实例

![image-20210616232906161](http://ww1.sinaimg.cn/large/007WWC4agy1gswotf4jofj60hk0ayaeh02.jpg)

**使用vue-router的步骤:**

第一步: 创建路由组件

![image-20210616233342327](http://ww1.sinaimg.cn/large/007WWC4agy1gswoztk72vj60h50ccn2k02.jpg)

第二步: 配置路由映射: 组件和路径映射关系

![image-20210616233436965](http://ww1.sinaimg.cn/large/007WWC4agy1gswp2drr1zj60fj0dodk802.jpg)

第三步: 使用路由: 通过<router-link>和<router-view>

![image-20210616233514175](http://ww1.sinaimg.cn/large/007WWC4agy1gswp1miwncj60ux0b7q9x02.jpg)

- <router-link>: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个<a>标签.

- <router-view>: 该标签会根据当前的路径, 动态渲染出不同的组件.

- 网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和<router-view>处于同一个等级.

- 在路由切换时, 切换的是<router-view>挂载的组件, 其他内容不会发生改变.

#### **路由的默认路径**

我们这里还有一个不太好的实现:

默认情况下, 进入网站的首页, 我们希望<router-view>渲染首页的内容.

但是我们的实现中, 默认没有显示首页组件, 必须让用户点击才可以.

如何可以让**路径**默认跳到到**首页**, 并且<router-view>渲染首页组件呢?

非常简单, 我们只需要配置多配置一个映射就可以了.

![image-20210616233657871](http://ww1.sinaimg.cn/large/007WWC4agy1gswp2yyb55j60a505n3z002.jpg)

**配置解析:**

我们在routes中又配置了一个映射. 

path配置的是根路径: /

redirect是重定向, 也就是我们将根路径重定向到/home的路径下, 这样就可以得到我们想要的结果了.

#### **HTML5****的****History****模式**

我们前面说过改变路径的方式有两种:

- URL的hash

- HTML5的history

默认情况下, 路径的改变使用的URL的hash.

如果希望使用HTML5的history模式, 非常简单, 进行如下配置即可:

![image-20210616233831693](http://ww1.sinaimg.cn/large/007WWC4agy1gswp41wrr6j60hp05zgo802.jpg)

#### **router-link****补充**

在前面的<router-link>中, 我们只是使用了一个属性: to, 用于指定跳转的路径.

<router-link>还有一些**其他属性**:

- tag: tag可以指定<router-link>之后渲染成什么组件, 比如上面的代码会被渲染成一个<li>元素, 而不是<a>

- replace: replace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中

- active-class: 当<router-link>对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.

在进行高亮显示的导航菜单或者底部tabbar时, 会使用到该类.

但是通常不会修改类的属性, 会直接使用默认的router-link-active即可. 

#### **修改****linkActiveClass**

该class具体的名称也可以通过router实例的属性进行修改 

![image-20210616234036470](http://ww1.sinaimg.cn/large/007WWC4agy1gswp5dugg9j60ir07v77t02.jpg)

> exact-active-class
>
> 类似于active-class, 只是在精准匹配下才会出现的class.
>
> 后面看到嵌套路由时, 我们再看下这个属性.

#### **路由代码跳转**

有时候, 页面的跳转可能需要执行对应的JavaScript代码, 这个时候, 就可以使用第二种跳转方式了

```this.$router.push('/home')```

比如, 我们将代码修改如下:

![](http://ww1.sinaimg.cn/large/007WWC4agy1gswp8x98bij60do08d41002.jpg)

#### **动态路由**

在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：

/user/aaaa或/user/bbbb

除了有前面的/user之外，后面还跟上了用户的ID

这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)。

1、路由配置

![image-20210617105551519](http://ww1.sinaimg.cn/large/007WWC4agy1gswpb72ia6j609g094q4m02.jpg)

2、在App.vue文件中动态拼接用户ID(v-bind: 动态绑定 简写  ：)

![image-20210617105929685](http://ww1.sinaimg.cn/large/007WWC4agy1gswpd8k8ugj60qp0axted02.jpg)

![image-20210617110021606](http://ww1.sinaimg.cn/large/007WWC4agy1gswpe9l8zzj608i04dt9102.jpg)

3、User.vue文件中显示获取的userId

![image-20210617110402098](http://ww1.sinaimg.cn/large/007WWC4agy1gswpejygkgj60fl0g543702.jpg)

**注意$route和$router**

这里的$router相当于创建的router实例(即调用router实例里面的方法)

![image-20210617110724880](http://ww1.sinaimg.cn/large/007WWC4agy1gswpf2szmlj60cp09k41902.jpg)

这里的$route是获取当前活跃的路由

![image-20210617110754407](http://ww1.sinaimg.cn/large/007WWC4agy1gswpfsjejfj60hd0693zj02.jpg)

### 路由懒加载

**官方解释：**

当打包构建应用时，Javascript 包会变得非常大，影响页面加载。

如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了

**官方在说什么呢?**

首先, 我们知道路由中通常会定义很多不同的页面.

这个页面最后被打包在哪里呢? 一般情况下, 是放在一个js文件中.

但是, 页面这么多放在一个js文件中, 必然会造成这个页面非常的大.

如果我们一次性从服务器请求下来这个页面, 可能需要花费一定的时间, 甚至用户的电脑上还出现了短暂空白的情况.



如何避免这种情况呢? 使用路由懒加载就可以了.

路由懒加载做了什么?

路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.

**只有在这个路由被访问到的时候, 才加载对应的组件**

![image-20210617122130867](D:\vuejs学习笔记\image-20210617122130867.png)

#### **懒加载的方式**

方式一: 结合Vue的异步组件和Webpack的代码分析.

```vue
const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};
```

方式二: AMD写法

```vue
const About = resolve => require(['../components/About.vue'], resolve);
```

方式三: 在ES6中, 我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割.

```vue
const Home = () => import('../components/Home.vue')
```

**推荐使用第三种方式**

### **嵌套路由**

嵌套路由是一个很常见的功能

比如在home页面中, 我们希望通过/home/news和/home/message访问一些内容.

一个路径映射一个组件, 访问这两个路径也会分别渲染两个组件.

路径和组件的关系如下:

![image-20210617130410371](http://ww1.sinaimg.cn/large/007WWC4agy1gswph9sm15j609d09e74y02.jpg)

实现嵌套路由有两个步骤:

创建对应的子组件, 并且在路由映射中配置对应的子路由.

在组件内部使用<router-view>标签.

#### **嵌套路由实现**

1、定义两个组件

![image-20210617130621571](http://ww1.sinaimg.cn/large/007WWC4agy1gswpl9gehlj60yv0hidqw02.jpg)

2、导入组件和定义路由

![image-20210617130907437](http://ww1.sinaimg.cn/large/007WWC4agy1gswpmbuasdj60ne09ntff02.jpg)

![image-20210617130812835](http://ww1.sinaimg.cn/large/007WWC4agy1gswplqobadj60hf0ikwju02.jpg)

3、使用路由

![image-20210617131012815](http://ww1.sinaimg.cn/large/007WWC4agy1gswpmuwvgej60lx0dpn2v02.jpg)

**嵌套路由也可以配置默认的路径, 配置方式如下: **

![image-20210617131138031](http://ww1.sinaimg.cn/large/007WWC4agy1gswpn6k6rkj60av0ejgny02.jpg)

### 传递参数

第一步: 创建新的组件Profile.vue 

![image-20210617135908399](http://ww1.sinaimg.cn/large/007WWC4agy1gswpnl42y4j60mp0e0jxs02.jpg)

第二步: 配置路由映射 

![image-20210617135943341](http://ww1.sinaimg.cn/large/007WWC4agy1gswpo3eva0j60ci0au41202.jpg)

第三步: 添加跳转的```<router-link>```

![image-20210617140042590](http://ww1.sinaimg.cn/large/007WWC4agy1gswponrj25j60xq0bb10802.jpg)

#### **传递参数的方式**

**URL解析：**

协议：//主机：端口/路径？查询

scheme://host:port/path?query#fragment

fragment是指片段的意思

例：

![image-20210617141130356](http://ww1.sinaimg.cn/large/007WWC4agy1gswppe8k2bj60en05y76c02.jpg)

传递参数主要有两种类型: params和query

**params****的类型****:**

- 配置路由格式: /router/:id

- 传递的方式: 在path后面跟上对应的值

- 传递后形成的路径: /router/123, /router/abc

**query****的类型****:**

- 配置路由格式: /router, 也就是普通配置

- 传递的方式: 对象中使用query的key作为传递方式

- 传递后形成的路径: /router?id=123, /router?id=abc

如何使用它们呢? 也有两种方式: <router-link>的方式和JavaScript代码方式

router-link

![image-20210617141249990](http://ww1.sinaimg.cn/large/007WWC4agy1gswppreg6uj60vt053jwd02.jpg)

JavaScript代码

![image-20210617141940074](http://ww1.sinaimg.cn/large/007WWC4agy1gswpr1md5gj60ha02pmym02.jpg)

![image-20210617141958923](http://ww1.sinaimg.cn/large/007WWC4agy1gswprhkg6lj60h50c6jtt02.jpg)

#### **获取参数**

![image-20210617142100753](http://ww1.sinaimg.cn/large/007WWC4agy1gswpryzc1vj60e005p40p02.jpg)

#### **$route****和****$router****是有区别的**

打印$router

![image-20210617151027770](http://ww1.sinaimg.cn/large/007WWC4agy1gswpsvzmxbj60jf09fq6602.jpg)

打印$route(显示的是当前活跃的路由)

![image-20210617151139992](http://ww1.sinaimg.cn/large/007WWC4agy1gswpt8zsimj60kd07zta902.jpg)

### **导航守卫**

我们来考虑一个需求: 在一个SPA应用中, 如何改变网页的标题呢?

网页标题是通过<title>来显示的, 但是SPA只有一个固定的HTML, 切换不同的页面时, 标题并不会改变.

但是我们可以通过JavaScript来修改<title>的内容.window.document.title = '新的标题'.

那么在Vue项目中, 在哪里修改? 什么时候修改比较合适呢?

**普通的修改方式:**

我们比较容易想到的修改标题的位置是每一个路由对应的组件.vue文件中.

通过mounted声明周期函数, 执行对应的代码进行修改即可.

但是当页面比较多时, 这种方式不容易维护(因为需要在多个页面执行类似的代码).

有没有更好的办法呢? 使用导航守卫即可.

**什么是导航守卫?**

vue-router提供的导航守卫主要用来监听监听路由的进入和离开的.

vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发.

#### **导航守卫使用**

我们可以利用beforeEach来完成标题的修改.

首先, 我们可以在钩子当中定义一些标题, 可以利用meta来定义

![image-20210617163500150](http://ww1.sinaimg.cn/large/007WWC4agy1gswpty7qsej60as0fyacq02.jpg)

其次, 利用导航守卫,修改我们的标题.

![image-20210617163528371](http://ww1.sinaimg.cn/large/007WWC4agy1gswpubx2n9j60h804jjt402.jpg)

**导航钩子的三个参数解析:**

- to: 即将要进入的目标的**路由对象.**

- from: 当前导航即将要离开的**路由对象**.

- next: 调用该方法后, 才能进入下一个钩子.（必须要有）

#### **导航守卫补充**

补充一:如果是后置钩子, 也就是afterEach, 不需要主动调用next()函数.

补充二: 上面我们使用的导航守卫, 被称之为**全局守卫**.

路由独享的守卫.

组件内的守卫.



更多内容, 可以查看官网进行学习:

[https://router.vuejs.org/zh/guide/advanced/navigation-guards.html#%E8%B7%AF%E7%94%B1%E7%8B%AC%E4%BA%AB%E7%9A%84%E5%AE%88%E5%8D%AB](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)

### **keep-alive**

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。

它们有两个非常重要的属性:

- include - 字符串或正则表达，只有匹配的组件会被缓存

- exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

  ```<keep-alive exclude="Profile,User"></keep-alive>```

router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

![image-20210617181452806](http://ww1.sinaimg.cn/large/007WWC4agy1gswpwckvvtj60hk056mzq02.jpg)

通过create声明周期函数来验证

![image-20210617181607494](http://ww1.sinaimg.cn/large/007WWC4agy1gswpxy4p4hj60d50ea43502.jpg)

![image-20210617181959471](http://ww1.sinaimg.cn/large/007WWC4agy1gswq0fb953j60pq0bnq6f02.jpg)

为了实现一个能保留上一个页面记录的效果

```javascript
<script>
 export default {
   data () {
     return {
        //固定一个初始路径
       path:'/home/news'
     }
   },
   name:'Home',
       //生命周期函数，一旦组件被调用就会调用此函数
   created() {
     console.log('home created');
   },
       //生命周期函数，一旦路由改变，上一个组件就会被摧毁
   destroyed() {
     console.log('home destoryed');
   },
       //生命周期函数，活跃，调用某个组件，则此组件活跃
   activated() {
     this.$router.push(this.path);
     console.log('activated');
   },
   deactivated() {
     console.log('deactivated');
   },
      // 组件内的守卫
      //beforeRouteLeave(to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
 // }
   beforeRouteLeave(to,from,next) {
     console.log(this.$route.path);
     this.path=this.$route.path;
     next()
   }


 }
</script>
```

### 小案例（**TabBar**）：

实现思路：

如果在下方有一个单独的TabBar组件，你如何封装

自定义TabBar组件，在APP中使用

让TabBar出于底部，并且设置相关的样式

2.TabBar中显示的内容由外界决定

定义插槽

flex布局平分TabBar

3.自定义TabBarItem，可以传入 图片和文字

定义TabBarItem，并且定义两个(具名)插槽：图片、文字。

给两个插槽外层包装div，用于设置样式。（防止样式被替换掉）

填充插槽，实现底部TabBar的效果

![image-20210618142716655](http://ww1.sinaimg.cn/large/007WWC4agy1gswq1790q3j608s0fc0sx02.jpg)

.传入 高亮图片

定义另外一个插槽，插入active-icon的数据

定义一个变量isActive，通过v-show来决定是否显示对应的icon

5.TabBarItem绑定路由数据

安装路由：npm install vue-router —save

完成router/index.js的内容，以及创建对应的组件

main.js中注册router

APP中加入```<router-view>```组件

6.点击item跳转到对应路由，并且动态决定```isActive```

监听item的点击，通过this.$router.replace()替换路由路径

通过```this.$route.path.indexOf(this.link) !== -1```来判断是否是```active```

7.动态计算active样式

![image-20210619090832196](http://ww1.sinaimg.cn/large/007WWC4agy1gswq27b49ij60a507lwg002.jpg)

封装新的计算属性：```this.isActive ? {'color': 'red'} : {}```

#### 小技巧（给路径起别名）

在```webpack.base.conf.js```里

![image-20210619090922310](http://ww1.sinaimg.cn/large/007WWC4agy1gswq2lfitzj60gv07p76v02.jpg)

在src中使用别名时要加上```~```

![image-20210619091117384](http://ww1.sinaimg.cn/large/007WWC4agy1gswq2zb13jj60o205vtbr02.jpg)

## Promise

#### **什么是****Promise****呢？**

> ES6中一个非常重要和好用的特性就是Promise
>
> Promise是异步编程的一种解决方案。

> 那什么时候我们会来处理异步事件呢？
>
> 一种很常见的场景应该就是网络请求了。
>
> 我们封装一个网络请求的函数，因为不能立即拿到结果，所以不能像简单的3+4=7一样将结果返回。
>
> 所以往往我们会传入另外一个函数，在数据请求成功时，将数据通过传入的函数回调出去。
>
> 如果只是一个简单的网络请求，那么这种方案不会给我们带来很大的麻烦。
>
> 但是，当网络请求非常复杂时，就会出现回调地狱。

OK，我以一个非常夸张的案例来说明。

> 我们来考虑下面的场景(有夸张的成分)：
>
> 我们需要通过一个url1从服务器加载一个数据data1，data1中包含了下一个请求的url2
>
> 我们需要通过data1取出url2，从服务器加载数据data2，data2中包含了下一个请求的url3
>
> 我们需要通过data2取出url3，从服务器加载数据data3，data3中包含了下一个请求的url4
>
> 发送网络请求url4，获取最终的数据data4

![image-20210619121857400](D:\vuejs学习笔记\image-20210619121857400.png)

> 上面的代码有什么问题吗？
>
> 正常情况下，不会有什么问题，可以正常运行并且获取我们想要的结果。
>
> 但是，这样额代码难看而且不容易维护。
>
> 我们更加期望的是一种更加优雅的方式来进行这种异步操作。
>
> 如何做呢？就是使用Promise。
>
> Promise可以以一种非常优雅的方式来解决这个问题。

#### **定时器的异步事件**

我们先来看看Promise最基本的语法。

这里，我们用一个定时器来模拟异步事件：

假设下面的data是从网络上1秒后请求的数据

console.log就是我们的处理方式。

```js
setTimeout(function() {
    let data='Hello World'
    console.log(content);
},1000)
```

这是我们过去的处理方式，我们将它换成Promise代码

这个例子会让我们感觉脱裤放屁，多此一举

首先，下面的Promise代码明显比上面的代码看起来还要复杂。

其次，下面的Promise代码中包含的resolve、reject、then、catch都是些什么东西？

```js
new Promise((resolve,reject)=>{

  setTimeout(fucntion (){

   resolve('Hello World')

    reject('Error Data')

 },1000)

 }).then(data=>{
     console.log(data)
 }).catch(error=>{
     console.log(error)
 })
```

我们先不管第一个复杂度的问题，因为这样的一个屁大点的程序根本看不出来Promise真正的作用。

#### **定时器异步事件解析**

我们先来认认真真的读一读这个程序到底做了什么？

- new Promise很明显是创建一个Promise对象

- 小括号中((resolve, reject) => {})也很明显就是一个函数，而且我们这里用的是之前刚刚学习过的箭头函数。

但是resolve, reject它们是什么呢？

- 我们先知道一个事实：在创建Promise时，传入的这个箭头函数是固定的（一般我们都会这样写）

- resolve和reject它们两个也是函数，通常情况下，我们会根据请求数据的成功和失败来决定调用哪一个。

成功还是失败？

- 如果是成功的，那么通常我们会调用resolve(messsage)，这个时候，我们后续的then会被回调。

- 如果是失败的，那么通常我们会调用reject(error)，这个时候，我们后续的catch会被回调。 

OK，这就是Promise最基本的使用了。

#### **Promise****三种状态**

![image-20210619122611680](http://ww1.sinaimg.cn/large/007WWC4agy1gswqh4kob7j60f605m3zj02.jpg)

pending：等待状态，比如正在进行网络请求，或者定时器没有到时间。

fulfill：满足状态，当我们主动回调了resolve时，就处于该状态，并且会回调.then()

reject：拒绝状态，当我们主动回调了reject时，就处于该状态，并且会回调.catch()

![image-20210619122740751](http://ww1.sinaimg.cn/large/007WWC4agy1gswqhnlg3oj60dn0dawir02.jpg)

#### **Promise****链式调用**

我们在看Promise的流程图时，发现无论是then还是catch都可以返回一个Promise对象。

所以，我们的代码其实是可以进行链式调用的：

这里我们直接通过Promise包装了一下新的数据，将Promise对象返回了

Promise.resovle()：将数据包装成Promise对象，并且在内部回调resolve()函数

Promise.reject()：将数据包装成Promise对象，并且在内部回调reject()函数

![image-20210619122837832](http://ww1.sinaimg.cn/large/007WWC4agy1gswqir206ij60fm0f1gqn02.jpg)

#### **链式调用简写**

如果我们希望数据直接包装成Promise.resolve，那么在then中可以直接返回数据

注意下面的代码中，return Promise.resovle(data)改成了return data

结果依然是一样的

![image-20210619122934015](http://ww1.sinaimg.cn/large/007WWC4agy1gswqjdefvvj60fk0fl0wz02.jpg)

## Vuex

#### **Vuex****是做什么的****?**

- 官方解释：Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。

> 它采用 集中式存储管理 应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
>
> Vuex 也集成到 Vue 的官方调试工具 [devtools](https://github.com/vuejs/vue-devtools)[ extension](https://github.com/vuejs/vue-devtools)，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

- **状态管理**到底是什么？

> **状态管理模式、集中式存储管理**这些名词听起来就非常高大上，让人捉摸不透。

> 其实，你可以简单的将其看成把需要多个组件共享的变量全部存储在一个对象里面。
>
> 然后，将这个对象放在顶层的Vue实例中，让其他组件可以使用。
>
> 那么，多个组件是不是就可以共享这个对象中的所有变量属性了呢？
>
> 等等，如果是这样的话，为什么官方还要专门出一个插件Vuex呢？难道我们不能自己封装一个对象来管理吗？
>
> 当然可以，只是我们要先想想VueJS带给我们最大的便利是什么呢？没错，就是响应式。
>
> 如果你自己封装实现一个对象能不能保证它里面所有的属性做到响应式呢？当然也可以，只是自己封装可能稍微麻烦一些。
>
> 不用怀疑，Vuex就是为了提供这样一个在多个组件间共享状态的插件，用它就可以了。

#### **管理什么状态呢****?**

但是，有什么状态时需要我们在多个组件间共享的呢？

如果你做过大型开放，你一定遇到过多个状态，在多个界面间的共享问题。

比如用户的登录状态、用户名称、头像、地理位置信息等等。

比如商品的收藏、购物车中的物品等等。

这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的

#### **单界面的状态管理**

我们知道，要在单个组件中进行状态管理是一件非常简单的事情

什么意思呢？我们来看下面的图片。

这图片中的三种东西，怎么理解呢？

State：不用多说，就是我们的状态。（你姑且可以当做就是data中的属性）

View：视图层，可以针对State的变化，显示不同的信息。（这个好理解吧？）

Actions：这里的Actions主要是用户的各种操作：点击、输入等等，会导致状态的改变。

![image-20210619144240900](http://ww1.sinaimg.cn/large/007WWC4agy1gswqkharnmj60c5088dgh02.jpg)

**小案例：**

![image-20210619145758051](http://ww1.sinaimg.cn/large/007WWC4agy1gswqlauzcsj60g30ew78002.jpg)

在这个案例中，我们有木有状态需要管理呢？没错，就是个数counter。

counter需要某种方式被记录下来，也就是我们的State。

counter目前的值需要被显示在界面中，也就是我们的View部分。

界面发生某些操作时（我们这里是用户的点击，也可以是用户的input），需要去更新状态，也就是我们的Actions

这不就是上面的流程图了吗？

#### **多界面状态管理**

Vue已经帮我们做好了单个界面的状态管理，但是如果是多个界面呢？

多个试图都依赖同一个状态（一个状态改了，多个界面需要进行更新）

不同界面的Actions都想修改同一个状态（Home.vue需要修改，Profile.vue也需要修改这个状态）

也就是说对于某些状态(状态1/状态2/状态3)来说只属于我们某一个视图，但是也有一些状态(状态a/状态b/状态c)属于多个试图共同想要维护的

状态1/状态2/状态3你放在自己的房间中，你自己管理自己用，没问题。

但是状态a/状态b/状态c我们希望交给一个大管家来统一帮助我们管理！！！

没错，Vuex就是为我们提供这个大管家的工具。

全局单例模式（大管家）

我们现在要做的就是将共享的状态抽取出来，交给我们的大管家，统一进行管理。

之后，你们每个视图，按照我**规定好的**规定，进行访问和修改等操作。

这就是Vuex背后的基本思想。

![image-20210619160234733](http://ww1.sinaimg.cn/large/007WWC4agy1gswqmayhwwj60u40gn7fd02.jpg)



Devtools插件需要到谷歌商店里下载。

**小案例2：**

在之前案例的基础上：

安装vuex

```cmd
npm install vuex --save
```

首先，我们需要在某个地方存放我们的Vuex代码：

这里，我们先创建一个文件夹store，并且在其中创建一个index.js文件

在index.js文件中写入如下代码：

```javascript
import Vuex from 'vuex'
import Vue from 'vue'

//2、使用插件
Vue.use(Vuex)

//3.new一个Vuex.store对象出来
const store=new Vuex.Store({
  state:{
    count:0
  },
  mutations:{
    increment(state) {
      state.counte++
    },
    decrement(state) {
      state.counte--
    }

  },
})
//4.导出
export default store
```

**挂载到****Vue****实例中**

其次，我们让所有的Vue组件都可以使用这个store对象

来到main.js文件，导入store对象，并且放在new Vue中

这样，在其他Vue组件中，我们就可以通过this.$store的方式，获取到这个store对象了

![image-20210619152151588](http://ww1.sinaimg.cn/large/007WWC4agy1gswqn06latj60dk0cdtbv02.jpg)



**使用****Vuex****的****count**

使用方法：

1、可以直接```$store.state.count```

就是通过组件直接修改状态，但是不建议，这样无法保留状态修改记录，跳过了Devtools，一旦出错，很难找到

2、使用mutations

先定义对应的方法，再到对应组件里使用该方法

```javascript
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

const store=new Vuex.Store({
  state:{
    count:0
  },
  mutations:{
    increment(state) {
      state.count++
    },
    decrement(state) {
      state.count--
    }

  },
})

export default store
```

```javascript
<template>
  <div id="app">
    <p>{{ count }}</p>
    <button @click="increment">+1</button>
    <button @click="decrement">-1</button>
    <h2>-----------hello---------</h2>
    <hello-world></hello-world>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
  },

  computed: {
    count: function () {
      return this.$store.state.count;
    },
  },
  methods: {
    increment: function () {
      this.$store.commit("increment");
    },
    decrement: function () {
      this.$store.commit("decrement");
    },
  },
};
</script>

<style>
</style>
```

小结：

1.提取出一个公共的store对象，用于保存在多个组件中共享的状态

2.将store对象放置在new Vue对象中，这样可以保证在所有的组件中都可以使用到

3.在其他组件中使用store对象中保存的状态即可

通过this.$store.state.属性的方式来访问状态

通过this.$store.commit('mutation中方法')来修改状态

注意事项：

我们通过提交mutation的方式，而非直接改变store.state.count。

这是因为Vuex可以更明确的追踪状态的变化，所以不要直接改变store.state.count的值。

#### **Getters****基本使用**

有时候，我们需要从store中获取一些state变异后的状态，就像之前我们学的组件里面的computed属性一样

我们可以在Store中定义getters

案例：

index.js

```javascript
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

const store=new Vuex.Store({
  state:{
    count:0,
    students:[
      {id:110,name:'Why',age:18},
      {id:111,name:'kobe',age:21},
      {id:112,name:'luck',age:25},
      {id:113,name:'lilei',age:30},
    ]
  },
  getters:{
    more20stu(state) {
      return state.students.filter(s=>s.age>=20)
    },
    agefilter(state) {
      return function(age){
        return state.students.filter(s=>s.age>age)
      }
    }
      
  },
  mutations:{
    increment(state) {
      state.count++
    },
    decrement(state) {
      state.count--
    }

  },
})

export default store
```
组件使用

```javascript
<template>
  <div class="test">
    <div>当前计数：{{ $store.state.count }}</div>
    <h2>{{ $store.getters.more20stu }}</h2>
    <h2>{{ $store.getters.agefilter(25) }}</h2>
    <!-- <button @click="increment">+</button>
    <button @click="decrement">-</button> -->
  </div>
</template>
<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      counter: 0,
    };
  },
  components: {},
};
</script>

<style>
</style>

```

总结：

通过getters属性，定义两个函数

1、无参数

```javascript
 more20stu(state) {
      return state.students.filter(s=>s.age>=20)
    }
```

2、用户可以动态的决定筛选的年龄范围

```java
agefilter(state) {
      return function(age){
        return state.students.filter(s=>s.age>age)
      }
    }
```

**注意：getters默认是不能传递参数的, 如果希望传递参数, 那么只能让getters本身返回另一个函数.**

组件使用方法：```$store.getters.方法名```

1、

```{{ $store.getters.more20stu }}```

2、

```{{ $store.getters.agefilter(25) }}```

#### **Mutation****使用**

##### 基本更新

Vuex的store状态的更新唯一方式：**提交****Mutation**

Mutation主要包括两部分：

- 字符串的**事件类型（****type****）**

- 一个**回调函数（****handler****）**,该回调函数的第一个参数就是state。

mutation的定义方式：

```js
mutations:{
    increament(state) {
        state.count++
    }
}
```

通过mutation更新

```js
increament:function() {
    this.$store.commit('increament')
}
```

##### **Mutation****传递参数**

在通过mutation更新数据的时候, 有可能我们希望携带一些**额外的参数**

参数被称为是mutation的载荷(Payload)

Mutation中的代码:

```js
decrement(state,n) {
    state.count-=n
}

decrement:function() {
    this.$store.commit('decrement',2)
}
```

如果有多个参数：

```javascript
changeCount(state,payload){
      state.count=payload.count;
    }
```

```javascript
 changeCount: function () {
      this.$store.commit("changeCount", { count: 0 });
    },
```

##### **Mutation****提交风格**

上面的通过**commit**进行提交是一种普通的方式

Vue还提供了另外一种风格, 它是一个包含type属性的对象

```javascript
this.$store.commit({
    type:'changecount',
    count:100
})
```

##### **Mutation****响应规则**

Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新.

这就要求我们必须遵守一些Vuex对应的规则:

提前在store中初始化好所需的属性.

当给state中的对象添加新属性时, 使用下面的方式:

方式一: 使用Vue.set(obj, 'newProp', 123)

方式二: 用新对象给旧对象重新赋值

```js
mutations:{
    updateInfo(state,ppayload) {
      //方式一：Vue.set()
        Vue.set(state.info,'height',payload.height)
      //方式二：给info赋值一个新对象
        state.info={...state.info,'height':payload.height}
    }
}
```

方式一和方式二都可以让state中的属性是响应式的，Vue组件会自动更新

删除一个属性(响应式)：

```javascript
Vue.delete(state.info,'age')
```

注意：通过以下方式是不能实现响应式的

```javascript
state.info.name='ff'
```

##### **Mutation****常量类型** **–** **概念**

我们来考虑下面的问题:

> 在mutation中, 我们定义了很多事件类型(也就是其中的方法名称).
>
> 当我们的项目增大时, Vuex管理的状态越来越多, 需要更新状态的情况越来越多, 那么意味着Mutation中的方法越来越多.
>
> 方法过多, 使用者需要花费大量的经历去记住这些方法, 甚至是多个文件间来回切换, 查看方法名称, 甚至如果不是复制的时候, 可能还会出现写错的情况.

如何避免上述的问题呢?

> 在各种Flux实现中, 一种很常见的方案就是使用**常量**替代Mutation**事件的类型****.**
>
> 我们可以将这些常量放在一个单独的文件中, 方便管理以及让整个app所有的事件类型一目了然.

具体怎么做呢?

> 我们可以创建一个文件: mutation-types.js, 并且在其中定义我们的常量.
>
> 定义常量时, 我们可以使用ES2015中的风格, 使用一个常量来作为函数的名称.

1、在store文件下建一个mutation_types.js文件

```javascript
export const INCREMENT ='increment'
```

2、使用

（1）导入

```javascript
import * as types from './mutation-types.js'
```

  (2)muation中使用

```javascript
 [types.INCREMENT](state) {
      state.count++
    },
```

​      组件中使用

```javascript
increment: function () {
      this.$store.commit(INCREMENT);
    },
```

##### **Mutation****同步函数**

通常情况下, Vuex要求我们Mutation中的方法必须是同步方法.

主要的原因是当我们使用devtools时, 可以devtools可以帮助我们捕捉mutation的快照.

但是如果是异步操作, 那么devtools将不能很好的追踪这个操作什么时候会被完成.

#### **Action****的基本定义**

> 我们强调, 不要再Mutation中进行异步操作.
>
> 但是某些情况, 我们确实希望在Vuex中进行一些异步操作, 比如网络请求, 必然是异步的. 这个时候怎么处理呢?
>
> Action类似于Mutation, 但是是用来代替Mutation进行异步操作的.

Action的基本使用代码如下:

> context是什么?
>
> context是和store对象具有相同方法和属性的对象.
>
> 也就是说, 我们可以通过context去进行commit相关的操作, 也可以获取context.state等.
>
> 但是注意, 这里它们并不是同一个对象, 为什么呢? 我们后面学习Modules的时候, 再具体说.
>
> 这样的代码是否多此一举呢?
>
> 我们定义了actions, 然后又在actions中去进行commit, 这不是脱裤放屁吗?
>
> 事实上并不是这样, 如果在Vuex中有异步操作, 那么我们就可以在actions中完成了.



**在Vue组件中, 如果我们调用action中的方法, 那么就需要使用dispatch**

**同样的, 也是支持传递payload**

```javascript
 aUpdateInfo(context, payload) {
   setTimeout(() => {
   context.commit('updateInfo')
   console.log(payload.message);
   payload.success()
   }, 1000)
},
```

```javascript
 this.$store.dispatch("updateInfo", "我是携带的信息")
```

##### **Action****返回的****Promise**

前面我们学习ES6语法的时候说过, Promise经常用于异步操作.

在Action中, 我们可以将异步操作放在一个Promise中, 并且在成功或者失败后, 调用对应的resolve或reject.

```javascript
actions:{
    updateInfo(context,payload) {
      return new Promise((resolve,reject)=>{
        setTimeout(()=>{
          context.commit('updateInfo');
          console.log(payload);

          resolve('1111')
        },1000)
      })
    }
  }
```

```javascript
updateInfo() {
      this.$store.dispatch("updateInfo", "我是携带的信息").then((res) => {
        console.log("里面完成了提交");
        console.log(res);
      });
    },
```

结果：

![image-20210619203633644](http://ww1.sinaimg.cn/large/007WWC4agy1gswqyct36hj60ek08xwgp02.jpg)

#### **认识****Module**

Module是模块的意思, 为什么在Vuex中我们要使用模块呢?

Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理.

当应用变得非常复杂时,store对象就有可能变得相当臃肿.

为了解决这个问题, Vuex允许我们将store分割成模块(Module), 而每个模块拥有自己的state、mutations、actions、getters等

modulesA.js

```javascript
export default {
  state:{
    name:'fanfei'
  },
  mutations:{
    updateName(state,payload) {
      state.name=payload
    }
  },
  getters:{
    fullname(state) {
      return state.name+'111'
    },
    fullname2(state,getters){
      return getters.fullname+'222'
    },
    fullname3(state,getters,rootState) {
      return getters.fullname2+rootState.count
    }
  },
  actions:{
    aUpdtateName(coontext) {
      console.log(context);
      setTimeout(()=>{
        context.commit('updateName','wangwu')
      },1000)
    }
  }
}
```

index.js

```javascript
import modulesA from './modules/moduleA'

const store=new Vuex.Store({
  state,
  getters,
  mutations,
  actions,

  modules:{
    a:modulesA
  }
})
```

使用app.js

```javascript
$.store.state.a.属性 //->moduleA的状态
$.store.state.b.属性 //->moduleB的状态
```





![image-20210619203923428](http://ww1.sinaimg.cn/large/007WWC4agy1gswr3lqjp7j60ez0e876q02.jpg)

##### **Module****局部状态**

上面的代码中, 我们已经有了整体的组织结构, 下面我们来看看具体的局部模块中的代码如何书写.

我们在moduleA中添加state、mutations、getters

mutation和getters接收的第一个参数是局部状态对象

![image-20210619204027630](http://ww1.sinaimg.cn/large/007WWC4agy1gswr3yut6gj609t0bj75d02.jpg)

![image-20210619204035090](http://ww1.sinaimg.cn/large/007WWC4agy1gswr47zitvj60cs0b275u02.jpg)

注意:

虽然, 我们的doubleCount和increment都是定义在对象内部的.

但是在调用的时候, 依然是通过this.$store来直接调用的.

##### **Actions****的写法**

actions的写法呢? 接收一个context参数对象

局部状态通过 context.state 暴露出来，根节点状态则为 context.rootState

![image-20210619204202736](http://ww1.sinaimg.cn/large/007WWC4agy1gswr4k0ni6j60ha069jso02.jpg)

如果getters中也需要使用全局的状态, 可以接受更多的参数

![image-20210619204232882](http://ww1.sinaimg.cn/large/007WWC4agy1gswr4wmmn4j60cy052dgn02.jpg)

#### **项目结构**

当我们的Vuex帮助我们管理过多的内容时, 好的项目结构可以让我们的代码更加清晰.

![image-20210619204324131](http://ww1.sinaimg.cn/large/007WWC4agy1gswr5cbf02j60ik097q5402.jpg)

### axios

> Axios 是一个基于 *[promise](https://javascript.info/promise-basics)* 网络请求库，作用于[`node.js`](https://nodejs.org/) 和浏览器中。 它是 *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

#### 下载：

```cmd
npm install axios --save
```

引入(main.js)：

```javascript
import axios from 'axios'
```

#### 基本使用：

```javasc
//axios里面是支持Promise
axios({
  method:'get',
  url:'http://123.207.32.32:8000/home/multidata'
  //专门针对get请求的参数拼接的信息
}).then(res=>{
  console.log(res)
})
```

#### 虚拟网络服务器：

[服务器](https://httpbin.org/)

#### **发送并发请求**

有时候, 我们可能需求同时发送两个请求

使用axios.all, 可以放入多个请求的数组.

axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

```javascript
axios.all([axios.get('http://123.207.32.32:8000/category'),
axios.get('http://123.207.32.32:8000/home/multidata',{params:{type:'sell',page:1}})])
.then(axios.spread((res1,res2)=>{
  console.log(res1);
  console.log(res2);
}))
```

#### **全局配置**

在上面的示例中, 我们的BaseURL是固定的

事实上, 在开发中可能很多参数都是固定的.

这个时候我们可以进行一些抽取, 也可以利用axiox的全局配置

```java
// 提取全局的配置
//这样所有的axios请求都会有默认配置baseURL
axios.defaults.baseURL='http://123.207.32.32:8000'

// 发送并发请求
axios.all([axios.get('/category'),axios.get('/home/data',{params:{type:'sell',page:1}})])
.then(axios.spread((res1,res2)=>{
  console.log(res1);
  console.log(res2);
}))
```

##### **常见的配置选项**

> 请求地址
>
> url: '/user',

> 请求类型
>
> method: 'get',

> 请求根路径
>
> baseURL: 'http://www.mt.com/api',

> 请求前的数据处理
>
> transformRequest:[function(data){}],

> 请求后的数据处理
>
> transformResponse: [function(data){}],

> 自定义的请求头
>
> headers:{'x-Requested-With':'XMLHttpRequest'},

> URL查询对象
>
> params:{ id: 12 },

> 查询对象序列化函数
>
> paramsSerializer: function(params){ }
>
> request body
>
> data: { key: 'aa'},

> 超时设置s
>
> timeout: 1000,

> 跨域是否带Token
>
> withCredentials: false,

> 自定义请求处理
>
> adapter: function(resolve, reject, config){},

> 身份验证信息
>
> auth: { uname: '', pwd: '12'},

> 响应的数据格式 json / blob /document /arraybuffer / text / stream
>
> responseType: 'json',

#### **axios****的实例**

为什么要创建axios的实例呢?

当我们从axios模块中导入对象时, 使用的实例是默认的实例.

当给该实例设置一些默认配置时, 这些配置就被固定下来了.

但是后续开发中, 某些配置可能会不太一样.

比如某些请求需要使用特定的baseURL或者timeout或者content-Type等.

这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息.

创建新的实例：

```javascript
// 创建新的实例
const axiosInstance=axios.create({
  baseURL:'http://123.207.32.32:8000',
  timeout:5000,
  headers:{
    'Content-Type':'application/x-www-form-urllencoded'
  }
})
```

发送网络请求：

```javascript
// 发送网络请求
axiosInstance({
  url:'/category',
  methods:'get'
}).then(res=>{
  console.log(res);
}).catch(err=>{
  console.log(err);
})
```

#### **axios****封装**

1、首先需要在scr中创建一个新的文价夹（network）里面再新建一个request.js文件夹

2、代码(1)request.js

```javascript
import axios from 'axios'
export function request(config) {
    // 1.创建axios的实例
     const instance = axios.create({
       baseURL: 'http://123.207.32.32:8000',
       timeout: 5000
     })

     // 发送真正的网络请求  因为返回的实例本身就是一个promise
      return instance(config)
   })
 
```

main.js

```javascript
request({
  url: '/home/multidata'
}).then(res => {
  console.log(res);
}).catch(err => {
  // console.log(err);
})
```

方式二：

request.js

```javascript
 export function request(config) {
   // 1.创建axios的实例
   const instance = axios.create({
     baseURL: 'http://123.207.32.32:8000',
     timeout: 5000
   })

   // 发送真正的网络请求
   instance(config.baseConfig)
     .then(res => {
       // console.log(res);
       config.success(res);
     })
     .catch(err => {
       // console.log(err);
       config.failure(err)
     })
 }
```

main.js

```javascript
request({
   baseConfig: {

   },
   success: function (res) {

   },
   failure: function (err) {

  }
})

```

方式三：

request.js

```javascript
export function request(config, success, failure) {
   // 1.创建axios的实例
   const instance = axios.create({
     baseURL: 'http://123.207.32.32:8000',
     timeout: 5000
   })

  // 发送真正的网络请求
   instance(config)
     .then(res => {
       // console.log(res);
       success(res);
     })
     .catch(err => {
      // console.log(err);
      failure(err)
     })
 }
```

main.js

```javascript
request({
   url: '/home/multidata'
 }, res => {
   console.log(res);
 }, err => {
   console.log(err);
 })

```

#### **如何使用拦截器？**

1、请求式拦截

```javascript
// 请求拦截
  instance.interceptors.request.use(config=>{
     //可以对拦截下来的信息进行相应的操作
    console.log(config);
    return config;
  },err=>{
    console.log(err);
  })
```

2、响应式拦截

```javascript
// 响应式拦截
  instance.interceptors.response.use(res=>{
    console.log(res);
    return res.data;
  },err=>{
    console.log(err);
  })
```

#### 引入axios的第二种方式

 [vue add axios](https://segmentfault.com/a/1190000020506968)

### 项目

使用最新版脚手架

#### 使用github与项目连接起来

- 首先在github中创建一个仓库

- 复制仓库地址

- 到终端中 cd 到相应的目录

- 执行

  ```cmd
  git clone 拷贝的仓库地址
  ```

- 会在对应的目录中出现一个与仓库名相同的文件夹

- 拷贝之前在本地创建的脚手架到生成的文件夹内

- 打开后，拷贝过来的文件都是绿色的

- 执行

  ```cmd
  git add .
  ```

  ```cmd
  git commit -m '初始化项目'
  ```

  ```cmd
  git push
  ```

  如何通过不拷贝的方式直接将项目远程连接到仓库：

  ```cmd
  git remote add origin 仓库地址
  git push -u origin master
  ```

  ```cmd
  
  git add .  //把当前项目中的所有东西载入到本地缓存
  git commit -m "first commit"
  git branch -M main
  git remote add origin https://github.com/smile-feifan/supermall.git
  git push -u origin main
  ```
  
  直接与远程仓库进行连接
  ```cmd
  git remote add origin https://github.com/smile-feifan/supermall.git
  git branch -M main
  git push -u origin main
  ```
  
  

#### 函数调用的生命周期：

> 调用函数时，内存会把所有的数据进行压栈，函数调用完后，会把数据弹出。也就是说函数调用完后，数据就会被销毁，为了在数据被销毁之前，我们能取得请求到的数据，并且令其不被销毁做了如下操作：
>
> 1.在组件中定义两个data数据。
>
> 2.把函数中请求过来的数据赋值给定义好的数据，这样请求过来的数据有了新的指向，就不会被销毁啦

```javascript
export default {
  name: "Home",
  components: { NavBar },
  data() {
    return {
      banners: [],
      recommends: [],
    };
  },
  created() {
    getHomeMultidata().then((res) => {
      // console.log(res);
      // this.result = res;
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  },
};
```



#### 滚动框架：better-scroll



1.可以直接下载源码，通过script引入

2.通过 npm install

```cmd
npm install better-scroll --save
```

3.使用

引入：

```javascript
import BScroll from "better-scroll";
```

基本使用：

```javascript
<div class="wrapper" ref="aaa">
    <ul class="content">
      <li>分类列表1</li>
      <li>分类列表2</li>
      <li>分类列表3</li>
      ....
    </ul>
  </div>
```

```javascript
let wrapper = document.querySelector(".wrapper")
let bs = new BScroll(wrapper, {})
```

增强型滚动（如果你还需要其它的滚动类型）：

```javascript
import BScroll from 'better-scroll'

let bs = new BScroll('.wrapper', {
  // ...
  pullUpLoad: true,//上拉加载操作
  click:true,
  wheel: true,
  scrollbar: true,
  // and so on
})
```

```javascript
// 1.创建BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      observeDOM: true,
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
    });

// 2.监听滚动的位置
    this.scroll.on("scroll", (position) => {
      // console.log(position);
      this.$emit("scroll", position);
    });
// 3.监听上拉事件
    this.scroll.on("pullingUp", () => {
      this.$emit("pullingUp");
    });
  },

  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp();
    },
  },
```



##### 配置项：

click:

- **类型**：`boolean`
- **默认值**：`false`
- **作用**：BetterScroll 默认会阻止浏览器的原生 click 事件。当设置为 true，BetterScroll 会派发一个 click 事件，我们会给派发的 event 参数加一个私有属性 `_constructed`，值为 true。

observe-dom

开启对 content 以及 content 子元素 DOM 改变的探测。当插件被使用后，当这些 DOM 元素发生变化时，将会触发 scroll 的 refresh 方法。 observe-dom 插件具有以下几个特性：

- 针对改变频繁的 CSS 属性，增加 debounce
- 如果改变发生在 scroll 动画过程中，则不会触发 refresh

pullUpLoad:

```javascript
import BScroll from '@better-scroll/core'
import PullUp from '@better-scroll/pull-up'

BScroll.use(PullUp)

const bs = new BScroll('.bs-wrapper', {
  pullUpLoad: true
})

bs.finishPullUp()
bs.openPullUp({})
bs.closePullUp()
```

解析：

finishPullUp()

- 结束下拉加载
- 每次触发 `pullingUp` 钩子后，你应该**主动调用** `finishPullUp()` 告诉 BetterScroll 准备好下一次的 pullingUp 钩子
- 这样才能进行下一次的下拉加载动作，如果没有的话，就只能加载一次

##### 注意：

> 自己建的组件是不能监听点击事件的
>
> 如果需要监听的话必须：
>
> 加上.native修饰符
>
> @click.native

> 父组件访问子组件的方式：
>
> 通过设置ref属性:
>
> ref="属性名"
>
> 访问方式：
>
> this.$refs.属性名.子组件里面的方法

> 父组件向子组件传递数据
>
> 通过在子组件中设置props对象
>
> ```javascript
> props:{
>  名称：{
>  type:
>  dafault:
>  }
> }
> ```

解决首区域页中better-scroll课滚动的问题

- Better-scroll在决定有多少区域可以滚动时，是根据scrollerHeight属性决定的
- scrollerHeight属性是根据放better-scroll的content中的子组件的高度
- 但是我们在首页中，刚开始在计算scrollerHeight属性时，时没有将图片计算在内的
- 所以，计算出来的高度是错误的
- 后来图片加载进来之后有了新的高度，但是scrollerHeight属性并没有更新
- 所以滚动出现了问题

解决：

- 监听每一张图片是否加载完成，图片加载完成了，就执行一次refresh()
- 如何监听加载完成呢：
- - img.onload=function(){}

