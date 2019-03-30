
# vw, vh 适配
这俩单位就是为适配而生的

`vw`: `viewport's width`  `1vw` = `视口宽度的 1%`
`vh`:` viewport's height` `1vh` = `视口高度的 1%`
`vmax`: 取 `vw`, `vh` 中的最大值
`vmin`: 取 `vw`, `vh` 中的最小值

支持情况: ` ios >= 8; android >= 4.4`


浏览器将任何屏幕都分成 100 份, 只要使用此单位, 就不会翻车

### 两种方案

方案一: 通篇使用` vw` 
```scss
@function vw($px){
    @return $px / 750 * 100vw;
}
```
为方便切图, 写了一个如上函数, 以 `750` 为基准, 在任何屏幕上都可以看做是`'750'`
因为例如此函数传 `250` 进去, 会被转换成 `33.33333vw`, 三个这样的大小将占满屏幕宽度, 在任何尺寸屏幕上的都是这样.

方案二: 通过 `vw` 设置根节点的字体大小, 页面尺寸依然使用 `rem`

一个很暴力的方式, 还是以 `750` 为基准. `375(css像素) / 750(设计稿宽度) * 100` 这是 `rem` 适配的原理所在
这个值最终是 `50`, 这个值就是 `rem` 适配中, `html` 的字体大小 . 
那通过 `vw` 适配, 要达到 `rem` 同样的适配效果, 是不是应该让 `?vw = 50px` ? 
所以 `50 / 3.75 ` = `13.333333333333334` (15位小数)
然后: 
```css
html {
    font-size: 13.333333333333334vw;
}
```
然后, `rem` 适配需要的 `js` 代码可以删除了. 然后在任意尺寸的屏幕上也是可以横着走的.
整个屏幕 `7.5rem`. 与 `rem` 适配的结果都是一样的 
需要注意一些问题: 
1. `css` 尺寸写 `rem`, 比如 `1/4` 屏幕大小的 `div`, `width: 1.875rem;`
2. `html` 的 `font-size` 会带来负面影响. 很多有文本属性`(受font-size影响)`的标签里面的内容会继承 `html` 的字体大小, `13.33vw` 字体其实是非常大的, 所以不处理的话, 页面将会乱套. `img` 的` display `属性默认是 `inline-block`, 它会根据字体来对齐. 如果字体继承了 `html`. 图片就会跑到一个匪夷所思的地方. 这个时候需要将` img `的包裹层的 `font-size` 做出相应的调整
3. 比较一劳永逸的方法, 在该设置的字体的地方设置字体大小, 然后最主要的是, 在` body `里面, 将 `font-size` 设置为`chrome`最小字体 `12px`, 阻止页面的元素去继承`html`的字体大小. 即现在 `html` 的字体大小只能影响 `rem` 这个单位.

这些问题逐一解决之后, 这也是一个很好的方案.



## bug

在 `ios` 中, `input` 输入唤醒键盘的时候, 固定顶部的元素 `fixed` 属性失效
1. 通过绝对定位模拟固定定位
将需要滚动的元素全部放进一个标签里面, 让需要滚动的元素在这个标签里面滚动, 整个页面不会滚动.
`-webkit-overflow-scrolling: touch;` 给滚动的元素设置这个属性让滚动变得流畅一些


2. 事件


## 1px 的问题

#### 伪类 + transform 解决方案
```css
    e{
        position: relative;
    }
    e::after {
        content: '',
        position: absolute;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 1px;
        background: #000;
        transform-origin: 0 0;
        transform: scaleY(0.5)
    }
```
#### 4 边框解决方案
```css
    e{
        position: relative;
    }
    e::after {
        content: '',
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
        border: 1px solid #000;
        transform-origin: 0 0;
        transform: scaleY(0.5)
    }
```