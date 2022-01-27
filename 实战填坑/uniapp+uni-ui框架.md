## 当前页面分享

```
<button type="default" @click="canvasImage2.printReport">分享</button>
```

[html2canvas](https://html2canvas.hertzen.com/getting-started)

> 使用canvas把当前页面绘制

```
npm install html2canvas
```

```
import html2canvas from 'html2canvas';
```

```
printReport(e,ownerFunc) {
				ownerFunc.callMethod('popupClose')
				setTimeout(()=>{
					const viewDom = window.document.querySelector('#view')
					const tableDom = window.document.querySelector('#table2')
					html2canvas(viewDom, {
					  backgroundColor: 'white',
					  useCORS: true, //支持图片跨域
					  scale: 4, //设置放大的倍数
						height: viewDom.scrollHeight,
						width: tableDom.scrollWidth,
						windowHeight: viewDom.scrollHeight,
						windowWidth: tableDom.scrollWidth
					}).then((canvas) => {
						  // 生成图片导出
							ownerFunc.callMethod('receiveRenderData', canvas.toDataURL('img/png'))
						})
				},300)
			},
```

**问题：**

绘制方法不执行

开始是以为没有加定时器，加上定时器还是不执行

网上说要使用[renderjs](https://uniapp.dcloud.io/frame?id=renderjs)

## renderjs

另加一个script标签 `lang="renderjs"`   `module="canvasImage"`命名改script为`canvasImage`

注意定时器必须加上，因为绘制需要时间，如果不加定时器，还是绘制完成就执行了下一步，导致绘制失败

```
<script lang="renderjs" module="canvasImage">
  import html2canvas from 'html2canvas'
  export default {
		methods:{
			printReport(e,ownerFunc) {
				ownerFunc.callMethod('popupClose')
				setTimeout(()=>{
					const viewDom = window.document.querySelector('#view')
					const tableDom = window.document.querySelector('#table2')
					html2canvas(viewDom, {
					  backgroundColor: 'white',
					  useCORS: true, //支持图片跨域
					  scale: 4, //设置放大的倍数
						height: viewDom.scrollHeight,
						width: tableDom.scrollWidth,
						windowHeight: viewDom.scrollHeight,
						windowWidth: tableDom.scrollWidth
					}).then((canvas) => {
						  // 生成图片导出
							ownerFunc.callMethod('receiveRenderData', canvas.toDataURL('img/png'))
						})
				},300)
			},
		}
  }
</script>
```

### renderjs视图层与逻辑层通信

> - APP 端可以使用 dom、bom API，不可直接访问逻辑层数据，不可以使用 uni 相关接口（如：uni.request）
> - H5 端逻辑层和视图层实际运行在同一个环境中，相当于使用 mixin 方式，可以直接访问逻辑层数据。

```
```



[uni-share](https://ext.dcloud.net.cn/plugin?id=4860)

```
import uniShare from '@/uni_modules/uni-share/js_sdk/uni-share.js';
```

```
uniShare (path) {
      uniShare.show({
        content: { //公共的分享参数配置  类型（type）、链接（herf）、标题（title）、summary（描述）、imageUrl（缩略图）
          type: 2,
					imageUrl:path,
        },
        menus: [{
          "img": "/static/app-plus/sharemenu/wechatfriend.png",
          "text": "微信好友",
          "share": { //当前项的分享参数配置。可覆盖公共的配置如下：分享到微信小程序，配置了type=5
              "provider": "weixin",
              "scene": "WXSceneSession"
            }
          },
          {
            "img": "/static/app-plus/sharemenu/wechatmoments.png",
            "text": "微信朋友圈",
            "share": {
                "provider": "weixin",
                "scene": "WXSceneTimeline"
            }
          },
          // {
          //    "img": "/static/app-plus/sharemenu/mp_weixin.png",
          //    "text": "微信小程序",
          //    "share": {
          //        provider: "weixin",
          //        scene: "WXSceneSession",
          //        type: 5,
          //        miniProgram: {
          //            id: '123',
          //            path: '/pages/list/detail',
          //            webUrl: '/#/pages/list/detail',
          //            type: 0
          //        },
          //    }
          // },
          {
              "img": "/static/app-plus/sharemenu/weibo.png",
              "text": "微博",
              "share": {
                  "provider": "sinaweibo"
              }
          },
          {
              "img": "/static/app-plus/sharemenu/qq.png",
              "text": "QQ",
              "share": {
                  "provider": "qq"
              }
          },
          {
              "img": "/static/app-plus/sharemenu/copyurl.png",
              "text": "复制",
              "share": "copyurl"
          },
          {
              "img": "/static/app-plus/sharemenu/more.png",
              "text": "更多",
              "share": "shareSystem"
          }
        ],
        cancelText: "取消分享",
      }, e => { //callback
        console.log(uniShare.isShow);
        console.log(e);
      })
    },
```

> 注意使用uni-share这个jdk，在发布之前，一定要在manifest文件app模块配置中勾选share

<img src="D:\FfWork\notes\实战填坑\uniapp+uni-ui框架.assets\image-20220114111016382.png" alt="image-20220114111016382" style="zoom:50%;" />

[base64ToPath](https://ask.dcloud.net.cn/article/35512)

> base64格式图片转换为路径

```
npm i image-tools --save
```

```
import { pathToBase64, base64ToPath } from 'image-tools'
```

```
loadBase64Url() {
  const imageStr = this.path;
  base64ToPath(imageStr).then(path => {
	this.uniShare(path)
  }).catch(error => {
    console.error('临时路径转换出错了：', error);
  })  
},
```

```
receiveRenderData(val) {
  this.path = val.replace(/[\r\n]/g, ''); // 去除base64位中的空格
  this.loadBase64Url()
},
```

## html2canvas跨域问题

> Uncaught (in promise) SecurityError: Failed to execute 'toDataURL' on 'HTMLCanvasElement': Tainted canvases may not be exported. at app-view.js:8194

官方方法：

```
useCORS: true
```

但是好像没用，还是报错

解决办法：直接把图片转换成base64图片格式

## uni-app中直接获取dom元素报错

```
const viewDom = window.document.querySelector('#allView')
```

![image-20220114140150805](D:\FfWork\notes\实战填坑\uniapp+uni-ui框架.assets\image-20220114140150805.png)

```
const viewDom = uni.createSelectorQuery().select('#allView')
const tableDom = uni.createSelectorQuery().select('#table2')
```

这样不会报错

> 但是最好不要随意操作Dom元素
>
> 可以使用renderjs这样可以直接获取

