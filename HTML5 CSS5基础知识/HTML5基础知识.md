HTML5新增标签

## 1.新增语义化标签（部份） [菜鸟教程](https://www.runoob.com/html/html5-semantic-elements.html)

| <header>  | 头部标签         |
| --------- | ---------------- |
| <nav>     | 导航标签         |
| <article> | 内容标签         |
| <section> | 定义文本某个区域 |
| <aside>   | 侧边栏标签       |
| <footer>  | 尾部标签         |

注意：

- 这种语义化标准主要是针对搜索引擎的

- 这些新标签在页面中可以使用多次

- 在IE9中，需要把这些元素转换为块级元素

  ```js
  header, section, footer, aside, nav, article, figure
  {
      display: block;
  }
  ```

- 移动端更喜欢使用这些标签

- HTML5还增加了很多其它标签属性

## 2.新增多媒体标签

- 音频：<audio>

  ```js
  <video controls autoplay loop muted>
    <source src="https://www.runoob.com/try/demo_source/movie.mp4"></source>
  </video>
  ```

- 视频：<video>  [video](https://www.runoob.com/tags/tag-video.html)

- 俩者的使用方式都很类似

- 可以很方便的在页面中嵌入音频和视频，而不再去使用flash和其它浏览器插件

video

| 属性                                                         | 值                 | 描述                                                         |
| :----------------------------------------------------------- | :----------------- | :----------------------------------------------------------- |
| [autoplay](https://www.runoob.com/tags/att-video-autoplay.html) | autoplay           | 如果出现该属性，则视频在就绪后马上播放。                     |
| [controls](https://www.runoob.com/tags/att-video-controls.html) | controls           | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| [height](https://www.runoob.com/tags/att-video-height.html)  | *pixels*           | 设置视频播放器的高度。                                       |
| [loop](https://www.runoob.com/tags/att-video-loop.html)      | loop               | 如果出现该属性，则当媒介文件完成播放后再次开始播放。         |
| [muted](https://www.runoob.com/tags/att-video-muted.html)    | muted              | 如果出现该属性，视频的音频输出为静音。                       |
| [poster](https://www.runoob.com/tags/att-video-poster.html)  | *URL*              | 规定视频正在下载时显示的图像，直到用户点击播放按钮。         |
| [preload](https://www.runoob.com/tags/att-video-preload.html) | auto metadata none | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| [src](https://www.runoob.com/tags/att-video-src.html)        | *URL*              | 要播放的视频的 URL。                                         |
| [width](https://www.runoob.com/tags/att-video-width.html)    | *pixels*           | 设置视频播放器的宽度。                                       |

## 3.HTML5 新的 Input 类型

[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input)

|                                                              |                                                              |                                                              |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Type                                                         | 描述                                                         | Spec                                                         |
| [button](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/button) | 没有默认行为的按钮，上面显示 [value](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#value) 属性的值，默认为空。 |                                                              |
| [checkbox](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/checkbox) | 复选框，可设为选中或未选中。                                 |                                                              |
| [color](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/color) | 用于指定颜色的控件；在支持的浏览器中，激活时会打开取色器。   | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [date](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/date) | 输入日期的控件（年、月、日，不包括时间）。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [datetime-local](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/datetime-local) | 输入日期和时间的控件，不包括时区。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [email](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/email) | 编辑邮箱地址的区域。类似 `text` 输入，但在支持的浏览器和带有动态键盘的设备上会有确认参数和相应的键盘。 |                                                              |
| [file](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/file) | 让用户选择文件的控件。使用[accept](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#accept)属性规定控件能选择的文件类型。 |                                                              |
| [hidden](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/hidden) | 不显示的控件，其值仍会提交到服务器。举个例子，右边就是一个隐形的控件。 |                                                              |
| [image](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/image) | 带图像的 `submit` 按钮。显示的图像由 `src` 属性规定。如果 [src](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#src) 缺失，[alt](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#alt) 属性就会显示。 |                                                              |
| [month](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/month) | 输入年和月的控件，没有时区。                                 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [number](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/number) | 用于输入数字的控件。如果支持的话，会显示滚动按钮并提供缺省验证（即只能输入数字）。拥有动态键盘的设备上会显示数字键盘。 |                                                              |
| [password](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/password) | 单行的文本区域，其值会被遮盖。如果站点不安全，会警告用户。   |                                                              |
| [radio](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/radio) | 单选按钮，允许在多个拥有相同 [name](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#name) 值的选项中选中其中一个。 |                                                              |
| [range](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/range) | 此控件用于输入不需要精确的数字。控件是一个范围组件，默认值为正中间的值。同时使用[htmlattrdefmin](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#htmlattrdefmin)  和 [htmlattrdefmax](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#htmlattrdefmax)来规定值的范围。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [reset](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/reset) | 此按钮将表单的所有内容重置为默认值。不推荐。                 |                                                              |
| [search](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/search) | 用于搜索字符串的单行文字区域。输入文本中的换行会被自动去除。在支持的浏览器中可能有一个删除按钮，用于清除整个区域。拥有动态键盘的设备上的回车图标会变成搜索图标。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [submit](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/submit) | 用于提交表单的按钮。                                         |                                                              |
| [tel](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/tel) | 用于输入电话号码的控件。拥有动态键盘的设备上会显示电话数字键盘。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [text](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/text) | 默认值。单行的文本区域，输入中的换行会被自动去除。           |                                                              |
| [time](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/time) | 用于输入时间的控件，不包括时区。                             | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [url](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/url) | 用于输入 URL 的控件。类似 `text` 输入，但有验证参数，在支持动态键盘的设备上有相应的键盘。 | [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) |
| [week](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/week) | 用于输入以年和周数组成的日期，不带时区。                     |                                                              |
| 废弃的值                                                     |                                                              |                                                              |
| [datetime](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/datetime) | 用于输入基于UTC时区的日期和时间（时、分、秒及秒的小数部分）。 |                                                              |

## 4.HTML5 新的表单元素

- ```<datalist>```

  > <datalist> 元素规定输入域的选项列表。
  >
  > <datalist> 属性规定 form 或 input 域应该拥有自动完成功能。当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项：
  >
  > 使用 <input> 元素的列表属性与 <datalist> 元素绑定.

  ```js
  <form>
   <input list="happyness" name="happy">
   <datalist id="happyness">
      <option value="开心1">
      <option value="开心2">
      <option value="开心3">
      <option value="开心4"> 
   </datalist>
   <button type="submit">提交</button>
   </form>
  ```

  

- ```<keygen>``` IE浏览器不支持

  > <keygen> 元素的作用是提供一种验证用户的可靠方法。
  >
  > <keygen>标签规定用于表单的密钥对生成器字段。
  >
  > 当提交表单时，会生成两个键，一个是私钥，一个公钥。
  >
  > 私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）

  ```js
  <form action="demo_keygen.asp" method="get">
  用户名: <input type="text" name="usr_name">
  加密: <keygen name="security">
  <input type="submit">
  </form>
  ```

- ```<output>```  IE浏览器不支持

>  <output> 元素用于不同类型的输出，比如计算或脚本输出：

       ```js
       <form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
       <input type="range" id="a" value="50">100 +
       <input type="number" id="b" value="50">=
       <output name="x" for="a b"></output>
       </form>
       ```

## 5.HTML5 Web 存储

[菜鸟教程](https://www.runoob.com/html/html5-app-cache.html)

## 6.HTML5 Geolocation（地理定位）

用于定位用户的位置。

