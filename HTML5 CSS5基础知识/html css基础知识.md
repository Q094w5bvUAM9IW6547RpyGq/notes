## nth-child与nth-of-type的区别

### nth-child

> 会把所有的盒子都排列序号
>
> 执行的时候首先看:nth-child(1)   之后回去看前面的div 如果匹配不上就不会执行

nth-of-type

> 会把指定的元素的盒子排列序号
>
> 执行时首先看 div 指定的元素  之后回去看 :nth-of-type(1)

伪类选择器

> ::before 

> ::after

- 所创建的的元素是行内元素
- 必须有content属性
- 权重是1

## 清除浮动的方式

- 额外标签法 也称为隔墙法，是W3C推荐的做法，就是在浮动的元素后面加上一个块级盒子

- 父级添加overflow属性

- 父级添加双伪元素

  > 由于伪类会创建一个新元素，类似于额外标签法

  ```js
  .clearfix::after{
      content:"";  //伪元素必须写的属性
      display:block; //插入的元素必须是块级元素
      height:0;  //不要看见这个元素
      clear:both; //核心代码清除浮动
      visibility:hidden; //不要看见这个元素
  }
  ```

  ```css
  .clearfix:before,.clearfix::after{
      content:"";
      display:table; //转换为块级元素并在一行显示
  }
  .clearfix::after{
      clear:both;
  }
  ```

## 2D转换置

### 移动translate

  > translate里面的参数可以是%

  > 移动的距离是相对于自身元素的
  >
  > 对行内标签没有效果

常用技巧：让元素垂直居中

```css
p {
    position:absolute;
    top:50%;
    left:50%;
    width:200px;
    height:200px;
    transform:translate(-50%,-50%);
}
```

### rotate

设置转换中心点

语法：

```css
transform-origin:x y;
```

重点：

- 注意后面的参数x,y是用空格隔开
- x,y 默认转换中心点是元素的中心点（50%，50%）
- 还可以给x,y设置像素或者方位名词（top bottom left right center）

综合写法：

```css
transform:translate(150px,50px) rotate(1.1)
```

注意：

- 当我们同时有位移和其它属性的时候，记得要将位移放到最前面
- 中间用空额隔开就好

## 动画：

动画简写属性

```css
animation:动画名称 持续时间 动画曲线 何时开始播放 播放次数 是否反方向 动画起始或者结束的状态
animation:my 5s linear 2s infinite alternate
```

**transition 过渡动画，有4个属性**：

(1) transition-property：属性名称
(2) transition-duration: 间隔时间
(3) transition-timing-function: 动画曲线
(4) transition-delay: 延迟

**animation 关键帧动画，有7个属性**：

(1) animation-name：动画名称
(2) animation-duration: 间隔时间
(3) animation-timing-function: 动画曲线
(4) animation-delay: 延迟
(5) animation-iteration-count：n | infinite；动画播放次数

(6) animation-direction: normal | alternate;
normal： 正常播放动画
alternate: 轮流反向播放动画，奇数次正向播放，偶数次反向播放

(7) animation-fill-mode:
none 表示 等待期和完成期，元素样式都为初始状态样式，不受动画定义（@keyframes）的影响。
both 表示 等待期样式为第一帧样式，完成期保持最后一帧样式。
backwards 表示等待期为第一帧样式，完成期跳转为初始样式
forwards 表示等待期保持初始样式，完成期间保持最后一帧样式

## 3D转换

### 透视perspective

- 在2D平面产生近大选小，但是只是效果是二维的

- 透视是写在被观察元素的父盒子上面

  > d:就是视距，视距就是一个距离人眼睛到屏幕的距离
  >
  > z:就是z轴，物体距离屏幕的距离，z轴越大（正值）我们看到的物体就越大

### translateZ

> 值越大，显示的图像也会越大

### transform-style

- 控制子元素是否开启三维立体环境
- transform-style:flat子元素默认不开启3d空间
- transform-style:perserve-3d 子元素开启3d立体空间
- 代码写给父级，但是影响的是子盒子

```html
<style>
  body{
    perspective: 500px;
  }
  .box {
    width: 200px;
    height: 200px;
    margin: 100px auto;
    position: relative;
    /* 让子元素保持3d立体空间 */
    transform-style: preserve-3d;
  }
  .box div {
    position:absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: pink;
  }
  .box div:last-child{
    background-color: purple;
    transform: rotateX(60deg);
  }
  .box:hover{
    transform: rotateY(60deg);
  }
</style>
<body>
  <div class="box">
    <div></div>
    <div></div>
  </div>
</body>
```

### 小盒子翻转案例：

- 注意两个盒子背靠背

```html
<style>
  .box{
    position: relative;
    width: 300px;
    height: 300px;
    margin: 100px auto;
    transform-style: preserve-3d;
    transition: all 3s;
  }
  .font,.back {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    font-size: 20px;
    color: white;
    line-height: 300px;
    text-align: center;
  }
  
  .font{
    background-color: skyblue;
    z-index: 1;
  }
  .back{
    background-color: pink;
    transform: rotateY(180deg);

  }
 .box:hover{
  transform: rotateY(180deg);
 }
</style>
<body>
  <div class="box">
    <div class="font">坠落深渊</div>
    <div class="back">向阳而生</div>
  </div>
</body>
```

### 3d导航栏

```js
<style>
    *{
      margin: 0;
      padding: 0;
      list-style: none;
    }
    ul {
      margin: 100px;
    }
    ul li {
      width: 120px;
      height: 35px;
      perspective: 500px;
      margin: 10px 0;
    }
    .box {
      width: 100%;
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transition: all 1s;
    }
    .box:hover{
      transform: rotateX(90deg);
    }
    .font,.bottom {
       position: absolute;
       left: 0;
       right: 0;
       width: 100%;
       height: 100%;
    }
    .font{
      background-color: pink;
      z-index: 1;
      transform: translateZ(17.5px);
    }
    .bottom{
      background-color: skyblue;
      transform: translateY(17.5px) rotateX(-90deg);
    }
  </style>
</head>
<body>
  <ul>
    <li>
      <div class="box">
        <div class="font"></div>
        <div class="bottom"></div>
      </div>
    </li>
    <li>
      <div class="box">
        <div class="font"></div>
        <div class="bottom"></div>
      </div>
    </li>
    <li>
      <div class="box">
        <div class="font"></div>
        <div class="bottom"></div>
      </div>
    </li>
    <li>
      <div class="box">
        <div class="font"></div>
        <div class="bottom"></div>
      </div>
    </li>
  </ul>
</body>
```

### 旋转木马案例：

```js
<style>
  body {
    perspective: 1000px;
  }
  section {
    width: 300px;
    height: 200px;
    margin: 150px auto;
    position: relative;
    transform-style: preserve-3d;
    animation: rotate 6s linear infinite;
    background: url("img/pig.jpg") no-repeat;
  }
  @keyframes rotate {
    0% {
      transform: rotateY(0);
    }
    100% {
      transform: rotateY(360deg);
    }
  }
  section:hover{
    animation-play-state: paused;
  }
  section div {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url("img/dog.jpg") no-repeat;
  }
  section div:nth-child(1){
    transform: translateZ(300px);
  }
  section div:nth-child(2){
    /* 先旋转好了再移动 */
    transform: rotateY(60deg) translateZ(300px);
  }
  section div:nth-child(3){
    /* 先旋转好了再移动 */
    transform: rotateY(120deg) translateZ(300px);
  }
  section div:nth-child(4){
    /* 先旋转好了再移动 */
    transform: rotateY(180deg) translateZ(300px);
  }
  section div:nth-child(5){
    /* 先旋转好了再移动 */
    transform: rotateY(240deg) translateZ(300px);
  }
  section div:nth-child(6){
    /* 先旋转好了再移动 */
    transform: rotateY(300deg) translateZ(300px);
  }

</style>

<body>
  <section>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </section>
</body>

```

## 浏览器的私有前缀：

浏览器私有前缀是为了兼容老版本的写法，比较新版本的浏览器无须添加

- -moz-:代表firefox浏览器私有属性
- -ms-:代表ie浏览器私有前缀
- -o-:代表Opera私有前缀
- -webkit-:代表safari、chrome私有前缀

提倡写法：

```js
-moz-border-radius:10px;
-webkit-border-radius:10px
-o-border-radius:10px
border-radius:10px
```



