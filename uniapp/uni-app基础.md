

## 1.uni-app 初体验

### 1.1.开发方式

- 使用DCloud公司提供的HBuilderX来快速开发
- 使用脚手架来快速搭建和开发

### 1.2.脚手架搭建项目

```node
//1.全局安装  
    npm install -g @vue/cli  
//2.创建项目      
    vue create -p dcloudio/uni-preset-vue my-project     
//3.启动项目（微信小程序）   
    npm run dev:mp-weixin    
//4.微信小程序开发者工具导入项目      
```

#### 1.2.2 创建项目

```js
vue create -p dcloudio/uni-preset-vue my-project  
```

##### 问题  一直等待，拉取不到 dcloudio/uni-preset-vue

- 由于是去线上github中拉取到 dcloudio/uni-preset-vue
- 有时候会拉取不到

##### 解决

- 利用github下载  [dcloudio/uni-preset-vue](https://github.com/dcloudio/uni-preset-vue)

- 解压文件

- 执行命令

  ```js
  vue create -p 下载好文件的路径 myProject
  //如下
  vue create -p D:\code\uniapp\uni-preset-vue-master myProject
  ```

  

- 选择默认模板

![01](https://i0.hdslb.com/bfs/album/4932aa2d6832a9743a86bbe77cc3aa9ce16c1277.png)

![image-20210723101855622](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtwe2c8jj60ey083dhw02.jpg)

#### 1.2.4.微信小程序开发者工具导入项目     

- 打开微信开发者工具

- 导入项目

  项目根路径   D:\code\uniapp\my-project\dist\dev\mp-weixin

  ![image-20210723105140442](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtw5j18bj60jx0dcmyf02.jpg)

### 1.3.搭建过程中可能遇到的问题

vue 和 vue-template-complier版本不一致

![image-20210723102824167](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtvxlx0gj60fn0780w102.jpg)

解决

重新安转vue与 vue-template-complier版本一致

```node
npm install vue@2.6.10
```

然后再运行

```js
npm run dev:mp-weixin   
```

### 1.4.使用DCloud公司提供的HBuilderX来快速开发

官方文档很详细：[HBuilderX来快速开发](https://uniapp.dcloud.io/quickstart-hx)

#### 1.4.1.开发过程可能遇到的问题

##### 配置好了微信小程序的地址，但是打不开：

解决：[[Hbuild打开微信小程序失败](https://www.cnblogs.com/ff-upday/p/15054185.html)](https://www.cnblogs.com/ff-upday/p/15054185.html)

##### 引入sass

安装插件

![image-20210724082039739](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtvhptn3j60jj0brwhp02.jpg)

在style文件中使用 lang属性

![image-20210724082125595](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtv7xdalj60bi09wtat02.jpg)

## 2.项目结构介绍

#### 2.1.项目目录

![image-20210723105217955](http://ww1.sinaimg.cn/large/007WWC4agy1gsrtuzbolxj60dk07hwgn02.jpg)

## 3.样式和sass

#### 3.1.样式和sass

- 支持小程序的 rpx 和 h5 的 vw、vh

  - rpx  小程序中的单位   750rpx = 屏幕的宽度

  - vw  h5单位 100vw=屏幕的宽度  100vh = 屏幕的高度

- 内置有sass的配置了，只需要安装对应的依赖即可

  ```js
  npm install sass-loader node-sass
  ```

- vue 组件中 ，在style 标签上加入属性 

  ```css
  <style lang='scss'>  
  ```

问题   [解决](https://www.cnblogs.com/ff-upday/p/15054588.html)

![image-20210723133913147](http://ww1.sinaimg.cn/large/007WWC4agy1gsrt1osb04j60n8067q7y02.jpg)

## 4.基本语法

### 4.1.数据显示 data

- 在js的data中定义数据
- 在template中通过{{数据}}来显示
- 在标签的属性上通过  :data-index='数据' 来使用

```vue
data() {
  return {
     title: 'Hello',
	 mes:'你好，uniapp',
	 person:{
		name:'小灰',
		age:'18',
		sex:'男'
	},
	color:'blue'
}
},
```

```vue
<view class="data_show">
	{{mes}}
</view>
<view class="">
	{{person.name}}
</view>
<!-- 使用标签属性里面的变量 -->
<view class="" :data-color='color'>
	{{color}}
</view>
```

### 4.2.数据循环

- 通过 v-for 来指定要循环的数组
- item 和 index 分别为 循环项 和循环索引
- :key 指定唯一属性，用来提高循环效率

```vue
	<view v-for="(item,index) in list"
	:key="item.id"
	>
	  {{index}}----{{item.value}}
	</view>
```

### 4.3.条件编译

- 通过 v-if 来决定显示和隐藏  不适合做频繁的切换显示
  - 当它为 false是直接删掉了标签 样式
- 通过v-show来决定显示和隐藏 适合做频繁的切换和显示
  - 当它为false时，是自动添加了一个  display: none; 的样式
  - 相比于v-if频繁使用时，性能要好些   

```vue
<view class="show_hid" v-if="false">
	你好！if
</view>
<view class="">
	===============
</view>
<view class="show_hid" v-show="false">
	你好 v-show
</view>
```

![03](http://ww1.sinaimg.cn/large/007WWC4agy1gsrzwt2umjj60ey06dju602.jpg)

4.4.计算属性

- 可以理解为是对data中的数据提供了一种加工或者过滤的能力
- 通过computed 来定义计算属性

```vue
computed:{
  cmoney(){
	return '￥'+this.money;
  },
  filterList(){
	return this.list.filter(v=>v.id>0);
  }
}
```

```vue
<view class="">
	{{cmoney}}
</view>
<view class="" v-for="(item,index) in filterList" :key="item.id">
	{{index}}----{{item.value}}
</view>
```

## 6.事件

### 6.1.事件的使用

- 注册事件 @click="handleClick"
- 定义事件监听函数 需要在 methods 中定义

```vue
methods:{
	handleClick(){
		console.log('满怀希望 就会所向披靡');
	}
}
```

```js
	<view class="" @click="handleClick">
		点击有惊喜哦
	</view>
```

### 6.2.事件传参

函数内部传参

- @click="handletap(参数)"
- handletap(参数){}

传递标签内部参数 (把事件源对象传递过去)

- @click="handletap(参数，$event)"
- handletap(参数，event){}

```js
<view class="" data-index="11" @click="handletap(1,$event)">
	事件传参
</view>
```

```vue
handletap(index,event){
	console.log(index);
	console.log(event)
}
```

## 7.组件

### 7.1.组件的定义

- 在 src 目录下新建文件夹 components 用来存放组件

- 在components 目录下直接新建组件 *.vue

  ![image-20210724145000542](http://ww1.sinaimg.cn/large/007WWC4agy1gss1isrhazj605k03nt8y02.jpg)

### 7.2.组件引入

- 在页面中引入组件 "import 组件名 from '组件路径' "

  ```vue
  import {imgBorder} from "@/components/img-border/img-border.vue"
  ```

### 7.3.组件注册

- 在页面中的实例中，新增一个对象，把组件放进去注册

  ```js
  components:{
  	imgBorder
  }
  ```

### 7.4组件的使用

- 在页面的标签中，直接使用引入的组件 "<组件></组件>"

### 7.5.组件传递参数

#### 父组件向子组件传递参数

```js
data(){
  return{				    src1:"https://i0.hdslb.com/bfs/album/bc86ac2b514572a8d93a086af7d51de4431ef3d5.jpg",
				src2:"https://i0.hdslb.com/bfs/album/c0d912211788d4ef3fcaf0144088d76b29cf2e04.jpg"
			}
		}
```

```js
<view class="content">
  <img-border :src="src1"></img-border>
  <img-border :src="src2"></img-border>
</view>
```

```vue
export default {
		props:{
			src:String
		}
	}
```

```js
<view class="img_wrap">
  <image :src="src" mode="widthFix"></image>
</view>
```

#### 子组件向父组件传递参数

- 子组件通过 触发事件 的方式向父组件传递参数 this.$emit("子组件自定义事件",参数)

  ```js
  <view class="img_wrap">
  	<image :src="src" mode="widthFix" @click="handleClick"></image>
  </view>
  
  
  methods:{
  	handleClick(){
  		this.$emit("srcChange",this.src);
  	}
  }
  ```

  

- 父组件通过监听事件的方式来接受数据  @子组件自定义事件 = "父组件自定义事件"

   

  ```js
  <view class="content">
  	<img-border @srcChange="handleSrcChange" :src="src1"></img-border>
  	<img-border @srcChange="handleSrcChange" :src="src2"></img-border>
  </view>
  
  methods:{
    handleSrcChange(e){
  	console.log(e);
    }
  }
  ```

#### 全局共享数据

- 通过vue的原型共享数据（在main.js文件中）

  ```vue
  Vue.prototype.baseURL=''
  ```

- 通过globalData共享数据(微信小程序独有的)（在app.vue中）

  ```js
  globalData:{
  	base:"www.360.com"
  }
  ```

  ```vue
  console.log(getApp().globalData.base)
  ```

- vuex

- 本地存储

7.6.组件插槽（占位符）

<slot></slot>

### 8.生命周期

#### 8.1.介绍

- uni-app框架的生命周期结合了vue和微信小程序的生命周期函数
- 全局的APP中使用onLaunch表示应用启动时
- 页面中使用 onLoad 或者 onShow 分别表示 页面加载完毕时 和页面显示时
- 组件使用 mounted 组件挂载完毕时

