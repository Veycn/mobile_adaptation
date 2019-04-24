
# 响应式
### 响应式存在的问题: 
响应式的原理是: 一次设计,多屏适配.
在 PC 端, 所有的内容无疑都能显示, 当屏幕逐渐缩小, 某些元素开始隐藏
再次缩小, 某些元素也开始隐藏. 到了移动端, 大部分元素都会隐藏掉.
但是这并不意味着隐藏掉的元素不加载. 
移动端有可能又是使用的 3G, 4G 耗费网络流量. 去加载这些不需要显示的东西真的必要吗? 

### 特点
网页宽度自动调整 (不定死, 百分比)
字体大小使用相对单位(em rem)
布局尽量使用浮动(流式布局)

### 媒体查询(核心)
```
@media
    all     所有设备
    * print   打字机
    screen  彩色屏幕
    * speech  听觉设备(内容以声音的形式呈现)
    /* 其他的已经在媒体查询4中废弃 */
```

`(max)min-width`: 宽度最大/最小是某个值的时候里面的样式生效
`(max)min-height`: 高度最大/最小是某个值的时候里面的样式生效
`orientation`: 方向(w > h 横屏(lanscape); h > w 竖屏(portrait))
`aspect-ratio`: 宽高比(4/3, 16/9)
`-webkit-device-pixel-ratio`: 像素比
满足媒体查询的条件, 内部的 css 样式生效. 最新的样式都能覆盖旧的样式

逻辑运算符
* and   合并多个媒体类型
```
/* 所有设备 最小宽度大于 700  横屏 */
@media all and (min-width: 700px) and (orientation: landscape) {
    div {
        width: 100px;
    }
}
```
* ,     匹配某个媒体查询
```
/* 屏幕的宽度大于 800px, 或者小于 400px */
@media (min-width: 800px), (max-width: 400px) {
    div {
        background: red;
    }
}
```
* not   媒体查询结果取反
```

/* 屏幕最大宽度不小于 400px 生效 */
@media not all and (max-width: 400px){
    div{
        background: blue;
    }
}
```
* only  尽在某个媒体查询成功后应用样式
```
/* 仅仅是彩色屏幕且宽度大于1000px */
@media only screen and (min-width: 1000px){
    div{
        background: red;
    }
}
```


`@import` 引入 `css` 文件
```
    @import url('./css/200.css') (min-width: 200px);
    @import url('./css/400.css') (min-width: 400px);
    @import url('./css/600.css') (min-width: 600px);
    @import url('./css/800.css') (min-width: 800px);
    @import url('./css/1000.css') (min-width: 1000px);
```

# BootStrap4

1. 容器
`.container-fluid`: 流体容器
    * 100% 窗口宽度
`.container`: 固定容器
    * `width > 1200　?　1140px`
    * `width > 992 ? 960px`
    * `width > 768 ? 720px`
    * `width > 576 ? 540px`
    * `width < 576 ? auto (跟随屏幕, 占满 100%)`
默认 `padding` 左右 `15px`
二者不能嵌套

2. 行, 列
行 给 `div` 用 `.row` 标记为一行
列 
    - 12列, 超出将会换行
    - `.col-xl-*` 超大  1200+   1140
    - `.col-lg-*` 大    992 +   960
    - `.col-md-*` 中等  768 +   720
    - `.col-sm-*` 小    576 +   540
    - `.col-*`    超小  <576    
    - `.col` 创建 n 个等宽列, 在任一尺寸下, n 个列等宽

    