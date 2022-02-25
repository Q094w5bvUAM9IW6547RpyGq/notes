# css预处理器

[官方地址](https://www.sass.hk/)

## 根据主题的变化 切换sass变量 达到根据不同主题，某一样式变化

[参考文章](http://www.teamsfy.com/html/r_0026737b6fe846fd944a492a010f2ba8.html)

> 定义好变量

```
/* 底部 取消、确定操作栏距离左侧的位置 */
$footer-panel-left: 270px; 
$footer-panel-left-vertical: 150px;
$footer-panel-left-horizontal: 0px;
```

> 混入样式

```
// footer-panel
@mixin footer-panel($footer-panel) {
  left: $footer-panel;

  [layout="vertical"] & {
    left: $footer-panel-left-vertical;
  }
  [layout="horizontal"] & {
    left: $footer-panel-left-horizontal;
  }
}
```

> 使用

```
.footer-panel{
    @include footer-panel($footer-panel-left);
    position: fixed;
    z-index: 1001;
    right: 10px;
    bottom: 0;
    padding: 16px 20px 0;
    min-height: 67px;
    box-sizing: border-box;
    background-color: #fff;
    border: 1px solid #ebedf2;
    box-shadow: 0 -4px 20px 0 rgba(71,107,179,.2);
    transition: left .2s;
  }
```

> js添加layout

```
/* 主题设置保存 */
handleSaveTheme() {
  this.handleSetTheme()                window.document.documentElement.setAttribute('layout',this.theme.layout)//设置属性名为 layout 的值为 this.theme.layout(变量)
        console.log('保存成功')
      },
```

