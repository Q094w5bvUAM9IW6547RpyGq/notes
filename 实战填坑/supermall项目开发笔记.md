## 项目搭建工具-->vscode

使用插件

- Vetur
- 浏览器插件--->vue

## 接口：

最新接口地址：baseURL = "http://152.136.185.210:7878/api/m5" 

使用：

- baseURL/recommend
- baseURL/home/data?type=pop&page=1

## 项目基本配置搭建

### 1.使用脚手架3创建一个项目

```cmd
vue create supermall
```

> 注意：此项目使用的是vue2

项目目录结构

- assets/img 中最好把各个内容的组件的图片分别建一个个文件，方便找

![01](https://i0.hdslb.com/bfs/album/17a0c07360240d8f0384e770fd98a606e159d904.png)

### 2.使用github托管

```cmd
  git add .  //把当前项目中的所有东西载入到本地缓存
  git commit -m "first commit"
  git branch -M main
  git remote add origin https://github.com/smile-feifan/supermall.git
  git push -u origin main
```

  ```
  //直接与远程仓库进行连接
  git remote add origin https://github.com/smile-feifan/supermall.git
  git branch -M main
  git push -u origin main
  ```

### 3.放入相关资源assets文件夹下

- img 项目中用到的图片

- css初始化的css样式->normalize.css（第三方）、base.css（自己的）

  - 在base.css中引入normalize.css

    ```css
    @import "./normalize.css";
    ```

  - 在项目中引入base.css

    ```vue
    //在app.vue中引入，因为main.js引入了APP.js
    @import "./assets/css/base.css";
    ```

   - base.css 解定义变量解析

     ```css
     /* 伪类  :root -> 获取根元素html*/
     /* css中定义的一些变量 */
     /* 使用方式 var(--color-text) */
     :root {
       --color-text: #666;
       --color-high-text: #ff5777;
       --color-tint: #ff8198;
       --color-background: #fff;
       --font-size: 14px;
       --line-height: 1.5;
     }
     ```

### 4.vue.config .js和 editorconfig.js

>  需求：配置相关文件夹的别名->脚手架3

- vue.config

> 在与src文件夹同级的目录中新建一个 vue.config (对vue的一些相关配置)
>
> ```config
> //进行导出后，会自动和隐藏起来的公共配置进行合并
> //configureWebpack:{}表示准备配置webpack中的configure
> //alias->别名
> //默认会有一个别名配置 -> 'src':'@'
> module.exports = {
>   configureWebpack: {
>     resolve: {
>       alias: {
>         'assets': '@/assets',
>         'common': '@/common',
>         'components': '@/components',
>         'network': '@/network',
>         'views': '@/views',
>       }
>     }
>   }
> }
> ```

- editorconfig(对项目很重要)

  > 目的：对代码进行一个统一的风格
  >
  > ```js
  > root = true
  > 
  > [*]
  > charset = utf-8
  > indent_style = space
  > indent_size = 2
  > end_of_line = lf
  > insert_final_newline = true
  > trim_trailing_whitespace = true
  > ```

- 修改项目图标  public-->index.html

- <%= BASE_URL %>  表示动态的获取路径

  > <link rel="icon" href="<%= BASE_URL %>favicon.jpg">

## 项目开发

## 首页

### 1.分析

- 模块化思想

> 分析：应该从哪里入手呢？->模块化思想
>
> 先把底部的导航栏创建好，就可以直接根据底部导航栏进行一个模块化的划分开发

- TabBar(底部导航外框架)

- TabBarItem（底部导航内部元素）

  ```js
  <div class="tab_bar_item" @click="itemClick">
      <div v-if="!isActive"><slot name="tab_icon"></slot></div>
      <div v-else><slot name="tab_icon_active"></slot></div>
      <div :style="activeStyle"><slot name="tab_name"></slot></div>
   </div>
  ```

  - 具名插槽 (让用户自己传入图片和文字 ) 

  - 父组件传递过来的参数：path:String   还有选中后的文字颜色 isAcitveColor

    ```js
    props: {
        path: String,
        activeColor: {
          type: String,
          default: "rgb(255, 0, 128)",
        },
      },
    ```

  - 插槽前面需要加一层div避免样式被覆盖掉 在外层的div中，绑定相关样式和判断

    - 根据$route.path.indexOf(this.path)!==1 判断哪个路由活跃  返回 isActive

      ```js
       computed: {
          isActive() {
            return this.$route.path.indexOf(this.path) !== -1;
          },
          activeStyle() {
            return this.isActive ? { color: this.activeColor } : {};
          },
        },
      ```

  - 点击事件

    绑定点击事件，跳转到对应的组件

    ```js
     methods: {
        itemClick() {
          this.$router.push(this.path);
        },
      },
    ```

- router跳转  

   > 注意区分 this.$router 和 this.$route 的区别
   >
   > this.$router 代表的是所有路由信息
   >
   > this$route 代表的是当前活跃的路由信息
   
   ```js
    import Vue from 'vue'
    import VueRouter from 'vue-router'
    //懒加载
    const Home=()=>import('../views/home/Home.vue')
    const Category=()=>import('../views/category/Category.vue')
    const Cart = () => import('../views/cart/Cart')
    const Profile = () => import('../views/profile/Profile')
    const Detail =()=>import('../views/detail/Detail.vue')
    //使用插件
    Vue.use(VueRouter)
    //配置路由
    const routes = [
      {
        path:'',
        redirect:'/home',
      },
      {
        path:'/home',
        component:Home,
        meta:{
          title:'首页'
        }
      },
      {
        path: '/category',
        component: Category,
        meta:{
          title:'分类'
        }
      },
      {
        path: '/cart',
        component: Cart,
        meta:{
          title:'购物车'
        }
      },
      {
        path: '/profile',
        component: Profile,
        meta:{
          title:'我的'
        }
      },
      {
        path:'/detail/:iid',
        component:Detail,
        meta:{
          title:'详情页'
        }
      }
    ]
    //创建路由
    const router = new VueRouter({
      //路由模式
      //URL的hash模式
      //HTML5的history模式
      mode: 'history',
      base: process.env.BASE_URL,
      routes
    })
    router.beforeEach((to,from,next)=>{
      document.title=to.matched[0].meta.title;
      next()
    })
    
    export default router
    
    //在app.vue中使用
    //<router-view />
   ```
   
    > 路由模式
    >   URL的hash模式：
    >
    > 本质上是修改window.location的href属性的值，可以直接通过直接赋值给location.href来改变href，但页面不发生刷新
    >
    >   HTML5的history模式：
    >
    > history接口是HTML5新增的，有五种模式改变URL而不发生页面刷新
    >
    > history.pushState
    >
    > history.replaceState
   >
   > history.go
   >
   > history.back
   >
   > history.forward
  
  - 顶部导航栏封装NavBar  common
    - 具名插槽
    - 弹性布局
    
    ```js
    <div class="nav_bar">
        <div class="left"><slot name="left"></slot></div>
        <div class="center"><slot name="center"></slot></div>
        <div class="right"><slot name="right"></slot></div>
    </div>
    ```

### 2.请求页面多个数据（network）

  - axios的封装->request.js

    ```js
    import axios from 'axios'
    
    export function request(options){
      const instance1=axios.create({
        baseURL:'http://152.136.185.210:7878/api/m5',
        timeout:5000
      })
      return instance1(options);
    }
    ```

  - 由于一个页面可能会要请求多个数据，如果全部都面向request.js的话，耦合度就太高了

  - 所以多做了一层封装，让首页面向home进行数据请求

  - 其它页面也同样如此

  - 功能：降低耦合度

  - home首页面向home.js进行网络请求

    ```js
    import {request} from "./request"
    
    export function getHomeMultidata() {
      return request({
        url:'/home/multidata'
      })
    }
    ```
    
    - 在home.js中引入
    
    - 大括号不能去掉,只有导出时使用了 default 才能省掉大括号，不然会报错
    
      ```js
      import { getHomeMultidata } from "network/home.js";
      ```
    
    - 在生命周期函数created中请求数据
    
      ```js
      created() {
          getHomeMultidata().then((res) => {
            this.banners = res.data.data.banner.list;
            this.recommends = res.data.data.recommend.list;
          });
        },
      ```
    
    - 使用data中的数据保存请求过来的数据
    
      ```js
      data() {
          return {
            banners: [],
            recommends: [],
          };
        },
      ```

### 3.轮播图的展示

  - 使用封装好了的轮播图
  - 遍历list数组，把相应的东西拿出来展示item.link、item.image
  - 注意：由于数据是请求过来的，所以，可能定时器开启后，数据还没有请求完过来，就会造成，图片轮播失效
  - 到swiper.vue中把定时器，开启的时间设置长一点，就好了  400
  - 最好在home.vue同层级建一个childComps把轮播图展示封装成一个组件homeSwiper.vue
  - 通过父组件  :banners="banners" 把轮播图数据传递到homeSwiper.vue中

### 推荐数据封装 RecommendView

```js
<div class="home_recommend">
    <div class="recommend_item" v-for="item in recommends" :key="item.image">
      <a :href="item.link">
        <img :src="item.image" alt="" />
        <div>{{ item.title }}</div>
      </a>
    </div>
  </div>
```

### FeatureView.vue封装

```js
<div class="home_feature">
    <a href="https://act.mogujie.com/zzlx67">
      <img src="~assets/img/home/recommend_bg.jpg" alt="" />
    </a>
  </div>
```

### 4.TabControl

```js
<div class="tab_control">
    <div
      class="control_item"
      v-for="(item, index) in titles"
      :key="index"
      @click="handleControlItem(index)"
      :class="{ active: index === currentIndex }"
    >
      <span>{{ item }}</span>
    </div>
  </div>
```

props / data:

```js
props: {
    titles: {
      type: Array,
      default() {
        return [];
      },
    },
  },
data() {
    return {
      currentIndex: 0,
    };
  },
```

点击事件

```js
 methods: {
    handleControlItem(index) {
      this.currentIndex = index;
    },
  },
```

  ```javascript
  position: sticky;
  top: 44px;
  ```

### 5.商品数据请求

  保存商品的数据结构设计

  ```js
  goods:{
      'pop':{page:5,list:[100]}
      'new':{page:2,list:[30]}
      'sell':{page:1,list:[60]}
  }
  //当点击 流行 时，就会请求 pop 相关的数据 page list
  //当点击 新款 时，就会请求 new 相关的数据 page list
  //当点击 精选 时，就会请求 sell 相关的数据 page list
  ```

   home.js数据请求

             ```js
             //传入两个参数
             export function getHomeGoods(type,page) {
               return request({
                 url:'/home/data',
                 params:{
                   type,
                   page
                 }
               })
             }
             ```

  使用请求到的数据

  ```js
  getHomeGoods(type) {
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then((res) => {
          console.log(res);
          //如何把一个数组直接放到另一个数组里面
          // 1.遍历
          this.goods[type].list.push(...res.data.data.list);
          this.goods[type].page += 1;
        });
      },
  ```

  调用

  ```js
  this.getHomeGoods("pop");
  this.getHomeGoods("new");
  this.getHomeGoods("sell");
  ```

样式(goodsItem)：

- 图片占满了整个item
- 所以用定位把goods_info 定到了下方

```js
<style scoped>
.goods_item {
  width: 48%;
  padding-bottom: 40px;
  position: relative;
}
.goods_item img {
  width: 100%;
  height: 235px;
  border-radius: 5px;
}
.goods_info {
  font-size: 12px;
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  overflow: hidden;
}
.goods_info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}
.goods_info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}
.goods_info .collect {
  position: relative;
}

.goods_info .collect::before {
  content: "";
  position: absolute;
  left: -15px;
  top: -1px;
  width: 14px;
  height: 14px;
  /* background: no-repeat url("~assets/img/common/collect.svg"); */

  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
```



### 6.商品数据的展示

### 7.TabControl点击事件的监听

  - 首先把事件发到父组件home.vue中，告诉父组件我点击了，并且要传一个参数index,告诉父组件我点击的是哪个

    ```js
    handleControlItem(index) {
          this.currentIndex = index;
          this.$emit("tabClick", index);
        },
    ```

  - 通过索引值,判断是点击的类型,并保存在一个currentType的data变量

  - ```js
    tabClick(index) {
          switch (index) {
            case 0:
              this.currentType = "pop";
              break;
            case 1:
              this.currentType = "new";
              break;
            case 2:
              this.currentType = "sell";
              break;
          }
    ```

  - 展示点击类型的商品

  - ```js
    showGoods() {
          return this.goods[this.currentType].list;
        },
    ```

### 8.better-scroll的使用  

   [安装](https://better-scroll.oschina.io/docs/zh-CN/guide/how-to-install.html#npm)

```js
npm install better-scroll --save
```

#### 基本使用

- 原生局部滚动

  ```js
  <ul class="content">
        <li>分类列表51</li>
        <li>分类列表52</li>
        <li>分类列表53</li>
        <li>分类列表54</li>
        ..........100   
      </ul>
  
  <style scoped>
  .content {
    height: 150px;
    background-color: pink;
    overflow-y: scroll;
  }
  </style>
  ```

- 使用better-scroll

  > 注意：
  >
  > 1.created函数，是组件创建完，但是模板没有渲染过来
  >
  > 所以不能在created中使用
  >
  > 可以去mounted函数中
  >
  > 2.content内容下面不能有多个同级标签
  >
  > 3.content必须要有高度

  > 基本使用：
  >
  > ```js
  >  new BScroll(document.querySelector('.wrapper'),{
  >   //BetterScroll 默认会阻止浏览器的原生 click 事件。当设置为 true，BetterScroll 会派发一个 click 事件
  >     click:true,
  >    //默认是false 上拉加载操作
  >  pullUpLoad:true,
  >  //监测 默认是0，0和1表示不监测   2：在手指滚动过程中监测  3：只要是滚动都监测
  >     probeType:3
  >   })
  >   
  >   BScroll.on('scroll',(position) {
  >            console.log(position)
  >           })
  >   
  > BScroll.on('pullingUp',()=>{
  >  //默认只能调用一次
  >     //调用this.scroll.finishPullUp();可以上拉多次
  >     this.scroll.finishPullUp();
  >            })
  > ```

#### 对首页进行一个重构（better-scroll的封装）

- 使用better-scroll

- 多个地方都要使用->对better-scroll进行一个封装

  > 注意
  >
  > <style scoped>
  > </style>
  > 样式+上scoped就只针对当前这个组件起效果
  
- 当为一个普通的元素中添一个  ref="名称"  属性

- 那么使用this.$refs.名称就可以拿到整个标签对象

- observeDom  [官方介绍](https://better-scroll.oschina.io/docs/zh-CN/plugins/observe-dom.html#%E5%AE%89%E8%A3%85)

  > 开启对 content 以及 content 子元素 DOM 改变的探测。当插件被使用后，当这些 DOM 元素发生变化时，将会触发 scroll 的 refresh 方法。 observe-dom 插件具有以下几个特性：
  >
  > - 针对改变频繁的 CSS 属性，增加 debounce
  > - 如果改变发生在 scroll 动画过程中，则不会触发 refresh

- 监听组件滚动 [probetype](https://better-scroll.oschina.io/docs/zh-CN/guide/base-scroll-options.html#probetype)

  ```js
   contentScroll(position) {
        // console.log(position);
        this.isShowBackTop = -position.y > 1000;
      },
  ```

- 上拉加载更多 [pullUpLoad ](https://better-scroll.oschina.io/docs/zh-CN/plugins/pullup.html#%E4%BA%8B%E4%BB%B6)

- home.vue

  ```js
  loadMore() {
        // console.log("上拉加载更多");
        this.getHomeGoods(this.currenType);
      },
  ```

- 上拉加载更多，默认只加载一次，如果不告诉scroll你已经完成了上拉加载

- 所以需要在图片请求完之后getHomeData()中，加上

- ```this.scroll.finishPullUp()```

```js
<template>
  <div class="wrapper" ref="wrapper">
    <div class="content"><slot></slot></div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
// import ObserveDom from "better-scroll";
// BScroll.use(ObserveDom);
export default {
  components: {},
  data() {
    return {
      scroll: null,
    };
  },
  props: {
    probeType: {
      type: Number,
      default: 0,
    },
    pullUpLoad: {
      type: Boolean,
      default: false,
    },
  },
  mounted() {
    // 1.创建BScroll对象
    //不要通过document.querySelector来拿，可能会拿到其它地方相同的class
    // this.scroll = new BScroll(document.querySelector(".wrapper"),{
    // });
    // 通过ref可以直接拿到确定的元素
    this.scroll = new BScroll(this.$refs.wrapper, {
      // observeDOM: true,
      click: true,
      // 为了提高性能：因为位置监听可能有些地方需要用，
      //有些地方不需要用，还是让用户传入参数决定用不用
      // probeType: 3,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      observeDOM: true // 开启 observe-dom 插件
    });
    // 2.监听滚动的位置
    if (this.probeType === 2 || this.probeType === 3) {
      this.scroll.on("scroll", (position) => {
        // console.log(position);
        this.$emit("scroll", position);
      });
    }

    // 3.监听上拉加载更多
    if (this.pullUpLoad) {
      this.scroll.on("pullingUp", () => {
        this.$emit("pullingLoad");
      });
    }
  },
  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll && this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp();
    },
    refresh() {
      // console.log(1);
      this.scroll && this.scroll.refresh();
    },
    getScrollY() {
      return this.scroll ? this.scroll.y : 0;
    },
  },
};
</script>

<style scoped>
</style>

```



### 9.BackTop（返回顶部）

#### 监听

> 直接监听组件的点击,要加上 .native修饰符才可以监听到
>
> * scroll对象, scroll.scrollTo(x, y, time)
> * this.$refs.scroll.scrollTo(0, 0, 500)
>
> ```vue
> <back-top @click.native="backClick"></back-top>
> ```
>
> ```js
> //使用better-scroll中的scrollTo(x,y,time)
> //父组件如何访问子组件？
> //通过给元素设置ref
> //使用$ref.scroll
> backClick() {
>    // console.log(this.$refs.scroll);
>    //可以直接封装一个方法在scroll组件中
>    // this.$refs.scroll.scroll.scrollTo(0, 0, 300);
>    this.$refs.scroll.scrollTo(0, 0, 300);
>  },
> ```

#### 显示和隐藏

> 监听scroll的滚动
>
> :probeType="3"
>
>  @scroll="contentScroll"
>
> 通过比较offsetTop属性值和监听到的scroll中的position值和scrol决定l什么时候显示和什么时候隐藏
>
> ```js
>  contentScroll(position) {
>       // console.log(position);
>       // 1.判断BackTop是否显示
>       this.isShowBackTop = -position.y > 1000;
> 
>       // 2.决定tabControl是否吸顶(position:fixed)
>       this.isTabFixed = -position.y > this.tabOffsetTop;
>     },
> ```

### 10. 解决首页中可滚动区域的问题

* Better-Scroll在决定有多少区域可以滚动时, 是根据scrollerHeight属性决定
  * scrollerHeight属性是根据放Better-Scroll的content中的子组件的高度
  * 但是我们的首页中, 刚开始在计算scrollerHeight属性时, 是没有将图片计算在内的
  * 所以, 计算出来的告诉是错误的(1300+)
  * 后来图片加载进来之后有了新的高度, 但是scrollerHeight属性并没有进行更新.
  * 所以滚动出现了问题
  
* 如何解决这个问题了?
  * 监听每一张图片是否加载完成, 只要有一张图片加载完成了, 执行一次refresh()
  * 如何监听图片加载完成了?
    * 原生的js监听图片: img.onload = function() {}
    * Vue中监听: @load='方法'
  * 调用scroll的refresh()
  
* 如何将GoodsListItem.vue中的事件传入到Home.vue中

  > Better-scroll 2.0 版本可以使用，observeDom:"true",来解决动态获取图片，重新计算滚动区域
#### 事件总线

  * 因为涉及到**非父子组件的通信**, 所以这里我们选择了**事件总线**(也可以使用状态管理器 vuex)
    * bus ->总线
    
      (到main.js)在Vue对象原型中添加一个$bus属性
    
    * Vue.prototype.$bus = new Vue()
    
    * 发送事件
    
    * ```this.$bus.$emit('事件名称', 参数)```
    
    * 监听事件
    
    * ```this.$bus.$on('事件名称', 回调函数(参数))```
    
    * 取消监听事件
    
    * this.$bus.$off('事件名称',要取消的函数)


* 问题一: refresh找不到的问题
  * 第一: 在Scroll.vue中, 调用this.scroll的方法之前, 判断this.scroll对象是否有值
  * 第二: 在mounted生命周期函数中使用 this.$refs.scroll而不是created中
* 问题二: 对于refresh非常频繁的问题, 进行防抖操作
  * 防抖debounce/节流throttle(课下研究一下)
  * 防抖函数起作用的过程:
    * 如果我们直接执行refresh, 那么refresh函数会被执行30次.
    * 可以将refresh函数传入到debounce函数中, 生成一个新的函数.
    * 之后在调用非常频繁的时候, 就使用新生成的函数.
    * 而新生成的函数, 并不会非常频繁的调用, 如果下一次执行来的非常快, 那么会将上一次取消掉

```js
      debounce(func, delay) {
        let timer = null
        return function (...args) {
          if (timer) clearTimeout(timer)
          timer = setTimeout(() => {
            func.apply(this, args)
          }, delay)
        }
      },
```

debounce函数解析：

- 首先是可以传入俩个参数，一个是函数，一个是延迟时间
- 声明一个变量timer



### 11. 上拉加载更多的功能

- 监听什么时候滚动到底部

### 12. tabControl的吸顶效果

#### 1. 获取到tabControl的offsetTop

- 所有组件都有一个属性 $el:用于获取组件 中的元素

* 必须知道滚动到多少时, 开始有吸顶效果, 这个时候就需要获取tabControl的offsetTop
* 但是, 如果直接在mounted中获取tabControl的offsetTop, 那么值是不正确.
* 如何获取正确的值了?
  * 监听HomeSwiper中img的加载完成. @load="imageLoad"
  
  * 加载完成后, 发出事件, 在Home.vue中, 获取正确的值.
  
    ```js
     imageLoad() {
          if (!this.isLoad) {
            this.$emit("swiperImageLoad");
            this.isLoad = true;
          }
        },
    ```
  
  * 补充:
    * 为了不让HomeSwiper多次发出事件,
    * 可以使用isLoad的变量进行状态的记录.
    
  * 注意: 这里不进行多次调用和debounce的区别

#### 2. 监听滚动, 动态的改变tabControl的样式

- offsetTop的值与position.y比较

* 问题:动态的改变tabControl的样式时, 会出现两个问题:
  * 问题一: 下面的商品内容, 会突然上移
  * 问题二: tabControl虽然设置了fixed, 但是也随着Better-Scroll一起滚出去了.
  
* 其他方案来解决停留问题.
  * 在最上面, 多复制了一份PlaceHolderTabControl组件对象, 利用它来实现停留效果.
  * 当用户滚动到一定位置时, PlaceHolderTabControl显示出来.
  * 当用户滚动没有达到一定位置时, PlaceHolderTabControl隐藏起来.

  但是会出现一个小bug,就是复制出来的PlaceHolderTabContro和原来的路由跳转不一致

  - 解决：

  ```javascript
  tabClick(index) {
        switch (index) {
          case 0:
            this.currentType = "pop";
            break;
          case 1:
            this.currentType = "new";
            break;
          case 2:
            this.currentType = "sell";
            break;
        }
        this.$refs.tabControl1.currentIndex = index;
        this.$refs.tabControl2.currentIndex = index;
      },
  ```

  



### 13. 让Home保持原来的状态

#### 1. 让Home不要随意销毁掉

* keep-alive

#### 2. 让Home中的内容保持原来的位置

* 离开时, 保存一个位置信息saveY.
* 进来时, 将位置设置为原来保存的位置saveY信息即可.
* activated   deactivated
  * 注意: 最好回来时, 进行一次refresh()

##### 非父子组件通信:

https://www.jb51.net/article/132371.htm

## 详情页面

#### 1.设置路由跳转(router->index.js)

- 跳转详情页并携带id

- 每次点击详情页都需要重新加载数据，所以不需要 keep-alive  

- exclude="组件名  （name属性）"

  ```javascript
  <keep-alive exclude="Detail"></keep-alive>
  ```
  
  动态获取路由：
  
  ```js
   {
      // path:'/detail',
      // 动态获取路由
      path:'/detail/:iid',
      component:Detail,
      meta:{
        title:'详情页'
      }
    }
  ```
  
  ```js
  itemClick() {
        //详情页还需要返回，所以用push比较好些
        this.$router.push("/detail/" + this.goodsItem.iid);
      },
  ```
  
- 详情页获取到iid

- 注意是this.$route

  ```js
  created() {
      this.iid = this.$route.params.iid;
    },
  ```

#### 2.网络数据请求（network->detail.js）

```js
export function getDetail(iid){
  return request({
    url:'/detail',
    params:{
      iid
    }
  })
}
```

#### 3.导航栏布局（NavBar）

#### 4.轮播图

#### 5.商品基本信息的封装和展示

- 把所有商品信息封装成一个对象

  ```javascript
  //detail.js
  export class Goods {
    constructor(itemInfo,columns,services) {
      this.title=itemInfo.title
      this.desc=itemInfo.desc
      this.newPrice=itemInfo.price
      this.oldPrice=itemInfo.oldPrice
      this.discount=itemInfo.discountDesc
      this.columns=columns
      this.services=services
      this.realPrice=itemInfo.lowNowPrice
    }
  }
  //使用
  // 获取商品信息
       const data=res.data.result;
        this.goods = new Goods(
          data.itemInfo,
          data.columns,
          data.shopInfo.services
        );
  ```
  
  > 注意：
  >
  > 使用此方法是为了更好的去取得接口中的数据，把杂乱的数据整合到一起
  
- v-for="index in 10"

- 是从1遍历到10

#### 6.店铺信息的解析和展示同上

- 最好在数据渲染之前都加上
- 有数据再展示
- 没数据不展示

```js
  v-if="Object.keys(commentInfo).length !== 0"
```

#### 7.加入滚动效果

问题一：

底部导航(MainTabBar)栏脱离了标准流，会一直覆盖到详情页底部，但是，我们不需要所以需要同过层级样式来把底部导航栏覆盖掉

```css
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
}
```

加入滚动效果：

如果出现不能滚动的现象，参考前面Home首页的方式

- 监听图片加载@load="imgLoad"
- 执行refresh()函数

#### 8.获取时间

每当向服务器请求数据，服务器都会返回一个时间

只是服务器返回的的时间是以Unix时间元年为起点，返回对应的时间戳

如何将时间戳转成时间格式化字符串

时间戳：1535694719秒

1.将时间转成date对象

const date=newDate(1535694719*1000)

2.将date格式化，转成对应的字符串

date.getYear()+data.getMonth()+1

<img src="https://i0.hdslb.com/bfs/album/db2ad56df8b230505e54f95562d411d451c51132.png"  />



封装date格式化函数

```javascript
/**
 * 格式化函数 ， 给日期格式化
 * date为 new Date()对象， fmt为 'yyyy-MM-dd'的格式
 */
 export function formatDate(date, fmt) {
  //获取年份
  if (/(y+)/.test(fmt)) {
    let dateY = date.getFullYear() + "";
    //RegExp.$1 在判断中出现过，且是括号括起来的，所以 RegExp.$1 就是 "yyyy"
    fmt = fmt.replace(RegExp.$1, dateY.substr(4 - RegExp.$1.length));
  }

  //获取其他
  let o = {
    "M+": date.getMonth() + 1,
    "d+": date.getDate(),
    "h+": date.getHours(),
    "m+": date.getMinutes(),
    "s+": date.getSeconds()
  };
  for (const k in o) {
    if (new RegExp(`(${k})`).test(fmt)) {
      let str = o[k] + "";
      fmt = fmt.replace(
        RegExp.$1,
        RegExp.$1.length == 1 ? str : padLeftZero(str)
      );
    }
  }
  return fmt;
}
function padLeftZero(str) {
  return ("00" + str).substr(str.length);
}
```



> 注意理解正则表达式

#### 9.mixins（全局混入）

[全局混入官方]([https://cn.vuejs.org/v2/guide/mixins.html#%E5%85%A8%E5%B1%80%E6%B7%B7%E5%85%A5](https://cn.vuejs.org/v2/guide/mixins.html#全局混入))

```javascript
//mixins.js
import { debounce } from "./utils";

export const itemListenerMixin={
  data() {
    return {
      itemListenerMixin:null,
      refresh:null
    }
  },
  mounted() {
    this.refresh=debounce(this.$refs.scroll.refresh,500)
    this.itemImgListener=()=>{
      this.refresh()
    }
  }

}
```



使用：

1.导入

2.使用

```javascript
mixins: [itemListenerMixin],
```

小bug:

- 当我加上商品展示的组件(DetailGoodsInfo)后，DetailGoodsInfo组件直接覆盖掉了前面的组件

- 原因：
- css样式出现了问题
- 解决：
- 在DetailGoodsInfo组件中的最外层的样式加上一个相对定位，就可以啦

#### 10.点击标题，滚动到对应的主题

- 首先获取到对应主题的offsetTop值

- 如何获取，在哪获取？

  >  1.第一次在mounted中获取，值不对
  >
  >   原因：this.$ref.params.$el没有渲染
  >
  >  2.第二次在getDetail函数中直接使用，值还是不对
  >
  >  3.第三次获取在getDetail函数中使用this.$nextTick(()=>{})，值不对
  >
  >   原因：图片没有计算在内
  >
  >   根据最新的数据，对应的DOM是已经被渲染出来
  >
  >   但是图片依然是没有加载完（目前取到的offsetTop不包含在其中的图片）
  >
  >   offsetTop值不对的时候都是因为图片的问题

- 要获取offsetTop值，必须等到图片都加载完成后，才是正确的

- 之前我们有一个监听图片加载完成的方法，所以可以直接在imgLoad方法里面实现

  ```vue
  imageLoad() {
        this.refresh();
  
        this.themeTopYs = [];
  //通过$el来获取
        this.themeTopYs.push(0);
        this.themeTopYs.push(this.$refs.params.$el.offsetTop);
        this.themeTopYs.push(this.$refs.comment.$el.offsetTop);
        this.themeTopYs.push(this.$refs.recommend.$el.offsetTop);
        console.log(this.themeTopYs);
      },
  
      titleClick(index) {
  //使用scrollTo(x,y,time)来实现
        this.$refs.scroll.scrollTo(0, -this.themeTopYs[index], 200);
        console.log(this.$refs.scroll.scroll);
      },
  ```

#### 11.内容滚动，显示正确的标题

  方式一（普通做法）：

  ```vue
  let length = this.themeTopYs.length;
        for (let i = 0; i < this.themeTopYs.length; i++) {
          if (
            // positionY > this.themeTopYs[i] &&
            // positionY < this.themeTopYs[i + 1]
            // 会出现溢出问题，如果到了3,3+1，就会溢出了
            this.currentIndex !== i &&
            ((i < length - 1 &&
              positionY >= this.themeTopYs[i] &&
              positionY < this.themeTopYs[i + 1]) ||
              (i === length - 1 && positionY >= this.themeTopYs[i]))
          ) {
            this.currentIndex = i;
            console.log(this.currentIndex);
            this.$refs.nav.currentIndex = this.currentIndex;
          }
        }
  ```

  解析：

  ```vue
   (this.currentIndex !== i )&&
            ((i < length - 1 &&
              positionY >= this.themeTopYs[i] &&
              positionY < this.themeTopYs[i + 1]) ||
              (i === length - 1 && positionY >= this.themeTopYs[i]))
          
   条件一：this.currentIndex !== i
                防止赋值得过于频繁
   条件二： (i < length - 1 &&
              positionY >= this.themeTopYs[i] &&
              positionY < this.themeTopYs[i + 1]) ||
              (i === length - 1 && positionY >= this.themeTopYs[i])
             条件一：i < length - 1 &&
              positionY >= this.themeTopYs[i] &&
              positionY < this.themeTopYs[i + 1])
                   判断区间：在0和某个数字之间
              条件二： (i === length - 1 && positionY >= this.themeTopYs[i])
                    判断等于：i===length-1
  ```

  方式二（hack）:

  向themeTopYs数组里面多添加一个最大值

  ```vue
   this.themeTopYs.push(Number.MAX_VALUE);
  ```

  themeTopYs[0, 2871, 3716, 3931, 1.7976931348623157e+308]

  for 遍历的时候，要length-1，最后一个不需要遍历

  ```vue
  if (
            this.currentIndex !== i &&
            positionY >= this.themeTopYs[i] &&
            positionY < this.themeTopYs[i + 1]
          ) {
            this.currentIndex = i;
            this.$refs.nav.currentIndex = this.currentIndex;
          }
  ```

  

#### 12.底部导航栏的封装

- 注意其定位

#### 13.详情页回到顶部

- home.vue和detail.vue的回到顶部的：mixin

  ```js
  export const backTopMixin={
    data() {
      return{
        isShowBackTop:false
      }
    },
    components:{
      BackTop
    },
    methods:{
      backClick() {
        this.$refs.scroll.scrollTo(0,0,300)
      },
      ListenerShowBackTop(position) {
        this.isShowBackTop=-position.y>BACK_POSITION?true:false
      }
    }
  }
  ```

  

#### 14.直达顶部的backTop

使用mixin进行了混入

#### 15.点击加入购物车

- bottom-bar内部监听，把事件发出去

- detail.vue父组件监听

- 获取商品信息：iid/price/image/title/desc

  ```js
  addCart() {
        // 1.获取购物车需要展示的信息
        const product = {};
        product.image = this.topImages[0];
        product.title = this.goods.title;
        product.desc = this.goods.desc;
        product.price = this.goods.realPrice;
        product.iid = this.iid;
  
        // 将商品添加到购物车
        // this.$store.commit("addCart", product);
        this.$store.dispatch("addCart", product);
      },
  ```

使用vuex(状态管理器)对代码进行管理共同的变量

- 定义mutations,将商品添加到state.cartList

  ```js
   mutations: {
      addCounter(state,payload){
         payload.count++;
      },
      addToCart(state,payload) {
        state.cartList.push(payload)
      }
      
    },
  ```

- 把复杂的操作，放到actions中

  ```js
   actions: {
      addCart(context,payload) {
        // let oldProduct=null;
        //  for(let item of state.cartList) {
        //    if(item.iid===payload.iid){
        //      oldProduct=item;
        //    }
        //  }
        let oldProduct = context.state.cartList.find(item=>item.iid===payload.iid)
        //  2.判断oldProduct
        if(oldProduct){
          // oldProduct.count+=1
          context.commit('addCounter',oldProduct);
          
        }else{
          payload.count=1
          // state.cartList.push(payload)
          context.commit('addToCart',payload);
        }
      }
      
    },
  ```

- 再使用vuex对代码进行重构

  - 将mutations中的代码抽取到actions中
  
  - mutations-type （给函数名定义一个变量）
  
    ```js
    export const ADD_COUNTER='add_counter'
    export const ADD_TO_CART='add_to_cart'
    ```
  
    - 在mutations.js中使用，要加上[ADD_COUNTER]
    - 在actions.js中，直接使用
  
  - 将mutations/actions单独抽取到文件中
  

## 购物车

#### 1.导航栏实现

mapGetters[辅助函数](https://vuex.vuejs.org/zh/guide/getters.html)

```js
import { mapGetters } from "vuex";

 computed: {
    // cartLength() {
    //   return this.$store.getters.cartLength;
    // },
    ...mapGetters(["cartLength"]),
  },
```

vuex中getters里面的一个属性

#### 2.购物车商品列表展示

- CartList->Scroll(滚动问题)

  - 可能会出现滚动不了的问题

  - 又是因为content高度，所以我们需要refresh一下

    ```javascript
    activated() {
        this.$refs.scroll.refresh();
      },
    ```

    

- CartListItem->CheckButton

#### 3.item选中和不选中(CheckButton)

- 修改商品的模型对象，改变选中和不选中

- 在商品被添加到购物车的时候，让它多增加个属性

- ```js
  payload.checked=true//加入购物车默认是
  ```

- 监听按钮点击（直接在CartListItem中监听） @click.native="checkClick"

  ```javascript
   checkClick() {
       //直接修改商品模型中的属性checked
        this.item.checked = !this.item.checked;
      },
          
  ```

  

#### 4.底部工具栏的汇总（CartBottomBar->CheckButton）

- 全选按钮CheckButton

  - 注意调好样式

- 计算总价格

  ```vue
   totalPrice() {
        return (
          "￥" +
          this.$store.state.cartList
            .filter((item) => {
              return item.checked;
            })
            .reduce((preValue, item) => {
              return preValue + item.price * item.count;
            }, 0)
            .toFixed(2)
        );
      },
  ```

  

- 去计算（显示选中商品的数量）

  ```vue
  checkLength() {
        return this.$store.state.cartList.filter((item) => item.checked).length;
      },
  ```

  

#### 5.购物车全选按钮

- 显示的状态

  * 判断是否有一个不选中，全选按钮就是不选中

- 点击全选按钮

  - 如果原来都是选中，点击一次，全部不选中

  - 如果原来都是不选中（某些不选中），全部选中
  
    思路：就是比较cartlist.length和不被选中的长度

```js
isSelectAll() {
      // 1.使用filter
    //如果购物车列表长度为0表示没有商品加入购物车
      if (this.cartList.length === 0) return false;
      // 数字取反也是false!!!
      // 使用过滤函数返回一个不选中的数组的长度然后取反
      return !this.cartList.filter((item) => !item.checked).length;

      //当没有数据的时候
      // 2.使用find
      // return !this.cartList.find((item) => !item.checked);
      // 3.普通遍历
      // for (let item of this.cartList) {
      //   if (!item.checked) {
      //     return false;
      //   }
      //   return true;
      // }
    },
  },
```

```js
checkClick() {
      // console.log(1);
    //全选情况下
      if (this.isSelectAll) {
        this.cartList.forEach((item) => (item.checked = false));
      } else {
        //部分或全部不选中
        this.cartList.forEach((item) => (item.checked = true));
      }
    },
       //toast 
    calcClick() {
      let noSelect = this.cartList.filter((item) => !item.checked).length;
      if (this.cartList.length === 0 || noSelect == this.cartList.length) {
        this.$toast.show("请选择购买的商品", 2000);
      }
    },
```



#### 6.点击加入购物车弹出弹窗toast封装和vuex（Actions可以返回一个Promise）的两个补充

- vuex的补充
  - Actions可以返回一个Promise，这样可以通过 .then返回一个res告诉外界vue做了什么操作、
  
    ```js
    import {
      ADD_COUNTER,
      ADD_TO_CART
    }from './mutation-type'
    
    export default {
      addCart(context,payload) {
        return new Promise((resolve,reject)=>{
          let oldProduct=context.state.cartList.find(item=>{
            return item.iid===payload.iid;
          })
    
          if(oldProduct) {
            context.commit(ADD_COUNTER,oldProduct)
            resolve('当前商品数量+1')
          }else {
            payload.count=1;
            context.commit(ADD_TO_CART,payload);
            resolve('添加了新的商品')
          }
        })
      }
    }
    ```
  
    - Promise-mapAction（让外界知道内部做了什么操作）
  
    ```js
    // 将商品添加到购物车
          // this.$store.commit("addCart", product);
          this.$store.dispatch("addCart", product).then((res) => {
            console.log(res);
          });
    ```
  
  - mapActions的映射关系
  
    导入：import { mapActions } from "vuex";
  
    使用： ...mapActions(["addCart"]),

Toast(吐司)

- 普通封装方式

  ```js
  <template>
    <div class="toast">
      <div>{{ message }}</div>
    </div>
  </template>
  
  <script>
  export default {
    name: "",
    components: {},
    props: {
      message: {
        type: String,
        default: "",
      },
    },
    data() {
      return {};
    },
  };
  </script>
  
  <style scoped>
  .toast {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(0, 0, 0, 0.6);
    color: white;
    padding: 8px 10px;
    border-radius: 10px;
    z-index: 1;
  }
  </style>
  
  ```

  使用：(在详情页使用)；

  - 必须给个变量 isShow决定是否显示
  - 使用定时器让tost不显示

  ```js
    this.$store.dispatch("addCart", product).then((res) => {
          console.log(res);
          this.isShow = true;
          this.message = res;
  
          setTimeout(() => {
            this.isShow = false;
            this.message = "";
          }, 1000);
        });
  ```

  

- 插件方式的封装

  Toast.vue

  ```vue
  <template>
    <div class="toast" v-show="isShow">
      <div>{{ message }}</div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Toast",
    components: {},
    data() {
      return {
        message: "",
        isShow: false,
        // message2: "你好",
      };
    },
    methods: {
      show(message = "默认文字", duration = 2000) {
        this.isShow = true;
  
        this.message = message;
  
        console.log(this.message);
        setTimeout(() => {
          this.isShow = false;
          this.message = "";
        }, duration);
      },
    },
  };
  </script>
  
  <style scoped>
  .toast {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(0, 0, 0, 0.6);
    color: white;
    padding: 8px 10px;
    border-radius: 10px;
    z-index: 99;
  }
  </style>
  
  ```

  toast的index.js

  ```js
  import Toast from './Toast.vue'
  
  const obj={}
  obj.install=function(Vue) {
    // 1.创建组件构造器
    const toastConstructor=Vue.extend(Toast)
    
    // 2.new的方式，根据组件构造器，可以创建一个组件对象
    const toast =new toastConstructor()
  
    // 3.创建组件对象手动挂载到一个元素上
    toast.$mount(document.createElement('div'))
  
    // 4.toast.$el对应的就是div
    document.body.appendChild(toast.$el)
    Vue.prototype.$toast=toast
  }
  
  export default obj
  ```

  vue的main.js

  ```js
  import toast from './components/common/toast'
  // 安装toast插件
  Vue.use(toast)
  ```

### 项目优化：

### 1.fastClick减少移动端300ms的延迟

- 安装

```cmd
 npm install fastclick --save
```

- 导入

```js
import FastClick from 'fastclick'
```

- 调用attach函数

```js
FastClick.attach(document.body)
```

### 2.图片懒加载

- 图片需要显示在屏幕上再加载

- vue-lazyload  [官方地址](https://github.com/hilongjw/vue-lazyload)

  - 安装

  - ```cmd
     npm install vue-lazyload --save
    ```

  - 导入

  - ```js
    import VueLazyLoad from 'vue-lazyload'
    ```

  - 使用

    ```js
    Vue.use(VueLazyLoad)
    ```

    - 修改img :src 改成v-lazy
    - 如果想使用其它功效，参考官方options 值

### 3.单位装换（px->vp/rem）

（最好在开发过程中就选好单位）

插件：postcss-px-to-viewport

4.路由懒加载

```js
 const Home=()=>import('../views/home/Home.vue')
 const Category=()=>import('../views/category/Category.vue')
 const Cart = () => import('../views/cart/Cart')
 const Profile = () => import('../views/profile/Profile')
 const Detail =()=>import('../views/detail/Detail.vue')
```



### nginx-项目在window下的部署

公司没有自己的服务主机：租借阿里云、华为云、和腾讯云

主机->操作系统->window(.net)/Linux->tomcat/nginx(软件/反向代理)

第一：将自己的电脑作为服务器->window->nginx

第二：远程部署（Mac）



### 面试题

- 如何理解Vue的生命周期

- 如何进行非父子组件通信

- Vue的响应式原理

  - 不要认为数据发生改变，界面跟着更新，并不是理所当然

    

![](https://i0.hdslb.com/bfs/album/e7c1284ccc05136ec742608236974530ce08dbc2.png)

