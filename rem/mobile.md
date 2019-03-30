# meta
## 禁用电话和邮箱
真机中出现疑似手机号码或者邮箱的字符串的时候, 点击会去调用电话或者邮箱. 但是邮箱没效果
```html
 <meta name="format-detection" content="telephone=no,email=no"/>
```
# 移动端样式重置


`-webkit-user-select: none;`: 禁止用户选中文字, 安卓无效, 需要通过事件解决
`-webkit-touch-callout: none;`: 禁止长按弹出系统菜单
`-webkit-tap-highlight-color: rgba(0,0,0,0)`: 去除安卓下 a / button / input 被点击时产生的边框 & 去除 ios 下 a 被点击时候的半透明灰色背景
`-webkit-tap-highlight-color: rgba(0,0,0,0)`: 阻止切换横竖屏或者用户设置浏览器, 字体大小会自动改变
` -webkit-appearance: none; border-radius: 0;`: 去除 button 与 input的默认背景, 按钮在 ios 下都是默认圆角
```css
    /* 修改 placeholder 的默认样式 */
    input::-webkit-input-placeholder{
        color: #000;    /* 默认样式 */
    }
    input:focus::-webkit-input-placeholder{
        color: #f00;    /* 点击之后的样式 */
    }
```
### 移动端重置样式 css 文件
```css
 body {
            font-family: helvetica;
            margin: 0;
        }
        body *{
            -webkit-user-select: none;
            -webkit-text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
        }
        a, button, input {
            -webkit-tap-highlight-color: rgba(0,0,0,0)
        }
        button, input{
            -webkit-appearance: none;
            border-radius: 0;
        } 
        input::-webkit-input-placeholder{
            color: #000;
        }
        input:focus::-webkit-input-placeholder{
            color: #f00;
        }
```

## 默认字体
### ios
    中文: HeiTi SC
    英文: Helvetica
    数字: HelveticaNeue
    无微软雅黑
### android
    中文: Droidsansfallback
    英文&数字: Droid Sans
    无微软雅黑

font-family: helvetica

### 非得要自己定义字体 ?
    引入字体, 流量加载字体库, 耗流量






===== 适配  





# 适配
在不同尺寸的移动设备上, 页面相对性的达到合理的展示(自适应), 或者保持同一效果的等比缩放(看起来差不多)
## 适配的元素
 1. 字体
 2. 宽高
 3. 间距
 4. 图像(图标, 图片)

## 适配的方法
 1. 百分比适配
 2. viewport 缩放适配
 3. DPR 缩放适配
 4. rem 适配
 5. vw, wh 适配

### 百分比适配
    `360 `手机站
    拉钩 `H5` 页面 顶部底部, 职位列表 都是高度定死, 宽度 `100%` 自适应
    高度固定, 宽度百分比, 在高度不能定死的状况下, 不是很好用, 一般都是配合其他是适配使用
    当元素为奇数或者某个元素占比不均匀的时候, 不是很好算

    `360`顶部模拟
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="format-detection" content="telephone=no,email=no"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body {
            font-family: helvetica;
            margin: 0;
        }
        body *{
            -webkit-user-select: none;
            -webkit-text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
        }
        a, button, input {
            -webkit-tap-highlight-color: rgba(0,0,0,0)
        }
        button, input{
            -webkit-appearance: none;
            border-radius: 0;
        } 
        input::-webkit-input-placeholder{
            color: #000;
        }
        input:focus::-webkit-input-placeholder{
            color: #f00;
        }
        .header {
            width: 100%;
            height: 48px;
            background: #23ac38;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-sizing: border-box;
            padding: 0 10px;
        }
        .logo img{
            width: 80px;
        }
        .list img{
            width: 20px;
        }
    </style>
</head>
<body>
    <header class="header">
        <span class="logo"><img src="http://p2.qhmsg.com/t01ecc3b6b24e7bdbd8.png" alt=""></span>
        <span class="list"><img src="http://p9.qhmsg.com/t010fa93a99715aad32.png" alt=""></span>
    </header>
</body>
</html>
```
    


# viewport 适配
把所有机型的`css`像素设置成一致的
1. viewport 需要使用 js 动态设置, (不能直接把 device 的值设置为数值)
2. 通过设置比例(初始比例以及缩放比例), 把宽度缩放成一致
    缩放比 = css 像素 / 375
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="format-detection" content="telephone=no,email=no" />
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, minimum-scale=1.0" id="view">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body {
            font-family: helvetica;
            margin: 0;
        }

        body * {
            -webkit-user-select: none;
            -webkit-text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
        }
        a, button, input {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0)
        }
        button, input {
            -webkit-appearance: none;
            border-radius: 0;
        }

        input::-webkit-input-placeholder {
            color: #000;
        }
        input:focus::-webkit-input-placeholder {
            color: #f00;
        }
        div {
            width: 75px;
            height: 100px;
            float: left;
        }
        div:nth-child(1) {
            background: #f00;
        }
        div:nth-child(2) {
            background: #ff0;
        }
        div:nth-child(3) {
            background: #f0f;
        }
        div:nth-child(4) {
            background: #0ff;
        } 
        div:nth-child(5) {
            background: #0f0;
        }
    </style>
    <script>
        ; (function () {
            /* 获取 css 像素 (viewport没有缩放, initial-scale=1.0)*/
            var curWidth = document.documentElement.clientWidth
            var curWidth = window.innerWidth
            var curWidth = window.screen.width
            /* 以上三种方式都可以准确的获取到 html 的 width */
            var targetWidth = 375 // 目标值
            var scale = curWidth / targetWidth
            var meta = document.getElementById('view')
            var content = 'initial-scale=' + scale + ', user-scalable=no, maximum-scalable=' + scale + ', minimum-scalable=' + scale
            meta.content = content
        })()
    </script>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</body>
</html>
```

但是这种肯定是有问题的
在 `ipad` 上, 宽度为 `768`, `pro` 为 `1024`, 一张 `375` 的图片放上去 ... 


# DPR 适配
把 CSS 像素缩放成与设备像素一样大的尺寸
只有在 PC 端这两个值才是对应的

`iphone6` 的物理像素 `750 * 1334`. 通过缩放, 将 `CSS` 像素的 `375 * 667` 缩放, 按照设计稿 `750` 切图.
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="format-detection" content="telephone=no,email=no" />
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, minimum-scale=1.0" id="view">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body {
            font-family: helvetica;
            margin: 0;
        }

        body * {
            -webkit-user-select: none;
            -webkit-text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
        }
        a, button, input {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0)
        }
        button, input {
            -webkit-appearance: none;
            border-radius: 0;
        }

        input::-webkit-input-placeholder {
            color: #000;
        }
        input:focus::-webkit-input-placeholder {
            color: #f00;
        }
        div {
            width: 20%;
            height: 100px;
            float: left;
        }
        div:nth-child(1) {
            background: #f00;
        }
        div:nth-child(2) {
            background: #ff0;
        }
        div:nth-child(3) {
            background: #f0f;
        }
        div:nth-child(4) {
            background: #0ff;
        } 
        div:nth-child(5) {
            background: #0f0;
        }
    </style>
    <script>
        ; (function () {
            /*
                要将 375 => 750 就是 375 / 0.5 dpr = 2
                375 / ? = 750  这个 ? 就是 dpr 的倒数
            */
            var meta = document.querySelector('meta[name="viewport"]')
            var scale = 1 / window.devicePixelRatio
            if(!meta){ // 没有默认设置 viewport 的 meta, 创建
                meta = document.createElement('meta')
                meta.name = 'viewport'
                meta.content = 'width=device-width, initial-scale=' + scale + ', user-scalable=no, maximum-scalable=' + scale + ', minimum-scalable=' + scale
                document.head.appendChild(meta)
            } else { // 有默认设置 viewport 的 meta, 修改  
                meta.setAttribute('content', 'width=device-width, initial-scale=' + scale + ', user-scalable=no, maximum-scalable=' + scale + ', minimum-scalable=' + scale)
            }
        })()
    </script>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</body>
</html>
```
虽然一个` CSS` 像素对应了一个物理像素, 但是对于不同尺寸的设备, 依然不是一个好的解决方案, 需要 `rem` 进行配合

# rem 适配
把所有的设备分成相同的若干份, 再计算元素宽度所占的份数

`em:` 当意义为 `font-size` 的时候, `1em` 代表父元素的字体大小, 当作为其他单位(宽度高度)的时候, 代表自身字体大小
`chrome` 下有最小字体限制 `12px`, 字体小于 `12px` 无法再变小

`rem: r root`, 根元素的 `font-size` 将 `html` 的 `font-size` 设置为 `20px`, `1rem = 20px`

1. 元素适配的宽度 = 元素所占的列数 * 一列的宽度
2. 元素在设计稿里面的宽度 
3. 列数 (随便给的) 100
4. 一列的宽度 = 屏幕宽度(css像素) / 列数
5. 元素实际占的列数 = 设计稿里面的宽度 / 一列的宽度


```js
var colWidth = 0
var col = 100   // 假设 100 列
// 计算 iPhone5 iPhone6里面一列的宽度
colWidth = 375 / col // 3.75px 6
colWidth = 320 / col // 3.20px 5

// 一个 div 占 10 列
var width = 10 * 3.75 // 37.5px 6
var width = 10 * 3.20 // 32.0px 5

// 一个 div 50px 
divCol = 50 / 3.75 // 13.333
divCol = 50 / 3.20 // 15.625

// 所以按照此方案, 50px 的 div, 在不同的设备里, 会占到不同的份数

```

屏幕已经被分成了若干份
那么 `width: 10rem;` 写入 CSS 文件的代码
元素适配的宽度 => `元素所占的列数 * 一列的宽`
元素适配的宽度 => `width 10 * 1rem`
元素所占的列数 => `10`
一列的宽 => `1rem`

**`1rem` = `html` 的 `font-size`**

栅格化系统的原理, 将屏幕分成若干份, 不同的屏幕被分成相同的份数, 所以一份的宽度会不一样
但是份数是一样的, 所以整体比例是一样的

```js
 ; (function (fs) {
            var html = document.documentElement
            var width = html.clientWidth    // css 像素
            html.style.fontSize = width / fs + 'px'
            // 分成 16 列, iPhone5 为例 320px 得到 1rem = 20px
         })(16)
```
 这种方式并没有一个基准点, 只是按照屏幕的增大, `html` 的 `font-size` 在变大
我们希望增加一个基准点, 这个点就是 `iPhone6`, 屏幕仍然分成 `16` 份
如果屏幕尺寸为 `375`, 那么就 `html` 字体也是` 16px`
如果屏幕小于 `375` 那 `font-size` 也会小于 `16px`
反之, 大于 `16px `
如下被注释了的代码:
```js
; (function (doc, win, designWidth) {
    const html = doc.documentElement
    const refreshDom = () => {
        const clientWidth = html.clientWidth
        if(clientWidth >= designWidth){
            html.style.fontSize = "100px"
        }else{
            // html.style.fontSize = 16 * clientWidth / 375 + 'px'
            html.style.fontSize = 100 * (clientWidth / designWidth) + 'px'
        }
    }
    doc.addEventListener('DOMContentLoaded', refreshDom)
})(document, window, 750)
```
但是这样做有一个弊端, 当计算出了 `rem` 值之后, 还要除以 `dpr`, 才是真正应该写的值
而且很多是除不尽的, 跟着一大串小数, 虽然有 `less sass` 去做这些事情, 但是还是觉得美中不足
# 最终方案
那么`html.style.fontSize = 100 * (clientWidth / designWidth) + 'px'` 又是什么意思呢 ?
基于 `iPhone6` 的尺寸, 将整个页面适配成` 7.5 rem`.
所以, 只要设计稿是` 750px`, 在切图的时候, 量出来出多少` px`, 直接将这个值除以 `100`, 加上`rem`就`ok`
如果设计图是 `640px`, 那么整屏的宽度就是 `6.4rem`, 只需要将参数修改一下就可以了
但是上面的代码是用到了 ` ES6 ` 的语法, `ios9` 不是原生支持的, 直接在上面跑会出现很大的问题, 就相当于适配没有做一样.
所以改写吧: 
```js
; (function (doc, win, designWidth) {
           var html = doc.documentElement
           function refreshDom(){
               var clientWidth = html.clientWidth
               if(clientWidth >= designWidth){
                   html.style.fontSize = "100px"
               }else{
                   html.style.fontSize = 100 * (clientWidth / designWidth) + 'px'
               }
           }
           doc.addEventListener('DOMContentLoaded', refreshDom)
         })(document, window, 750)
```
这种方案总体来说没什么大问题了. 如果在设计稿上量出来长度为`50px`, 那么实际写上去的长度应该是 `50 / 2 = 25px`. 因为 `750` 的设计稿, `375px`就会占满屏幕. 或者是写` .5rem`.

字体也要用标注的字体大小除以` 2 `, 如标注 `28px`, 实则应该写 `14px`, 或者`.28rem`

## 媒体查询设置 html 字体
苏宁易购的移动端
```css
@media screen and (min-width: 320px){
    html{
        font-size: 32px;
    }
    body{
        font-size: 15.36px;
    }
}
```
媒体查询会有一个区间, 320 - 375 之间的某个型号会是一种适配, 在另外一个区间又另外一种.

