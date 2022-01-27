#### 文本超出隐藏 [参考文章](https://www.cnblogs.com/libo-web/p/15398682.html)

```
1. 单行文本超出显示省略号🎯
div{
    /* 设置单行文本只需要三行代码即可搞定 */
    overflow:hidden;
    white-space: nowrap;
    text-overflow: ellipsis;  
}
```

```
 2. 多行文本超出显示省略号🎯
 注意：多行文本超出显示省略号只有-webkit内核才有作用

复制代码
div{
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
}    
```

#### 居中

```
top: 50%;
left: 50%;
transform: translate(-50%,-50%)
```

```
margin: auto //在有定位的元素中是无效的
```

#### 阴影

```
box-shadow: 1px 2px 10px 1px rgba(14,252,255,0.53), inset 5px 4px 100px 1px rgba(14,252,255,0.34);
background-color="rgba(11,76,151,0.10)"
```

