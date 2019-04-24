# 移动端事件

 * touchstart
 * touchmove
 * touchend

移动端事件用事件监听添加, 不要使用 `on`, 使用`on`绑定的事件会发生覆盖.

## touchstart
```
var box = document.querySelector("#box")
box.addEventListener("touchstart", () => {
    console.log("touchstart")
})
```
ios10 中有一个奇怪的bug, 如下写会拿不到东西, 但是如果参为`class`选择器就没有问题
```
const box = document.querySelector("#box")

```

## touchmove 
```
var box = document.querySelector("#box")
box.addEventListener("touchmove", () => {
    console.log("touchmove")
})
```
当手指点在屏幕上, 不离开, 然后移动手指的时候, 会不停地触发这个事件, 即使当手指已经离开`box`, 依然会持续触发, 直到手指离开屏幕.

## touchend

手指抬起触发此事件. 当手指按下, 移动出了`box`, 然后抬起手指, 依然会触发.

## 移动端事件与 pc 端事件的不同之处
1. 回想在用原生 `js` 写拖动的时候, 是把 `mousemove` 和` mouseup` 放在 `mousedown `之中的, 因为 `move` 肯定是按下之后触发, 否则就监听不到, `up `也是一样, 但是移动端系统默认已经做了这个事情, 所以, 可以这么写:
```
box.addEventListener("touchstart", () => {
    console.log("touchstart")
})
box.addEventListener("touchmove", () => {
    console.log("touchmove")
})
box.addEventListener("touchend", () => {
    console.log("touchend")
})
```

2. 事件的触发点不同

```
box.addEventListener("mousedown", () => {
    console.log("鼠标按下")
})
box.addEventListener("mousemove", () => {
    console.log("鼠标移动")
})
box.addEventListener("mouseup", () => {
    console.log("鼠标抬起")
})


box.addEventListener("touchstart", () => {
    console.log("touchstart")
})
box.addEventListener("touchmove", () => {
    console.log("touchmove")
})
box.addEventListener("touchend", () => {
    console.log("touchend")
```

写法是一样的, 但是触发可不太一样. 
PC端: 
    鼠标在元素身上移动, 会触发move事件
    鼠标按下, 移动鼠标, 鼠标抬起, 依次触发 `mousedown` => `n次 mousemove` => `mouseup`, 如果鼠标移出元素, `mousemove` 停止触发.

    
移动端: 
    鼠标在元素身上移动, 不会触发` move `事件
    当手指按下, 移动手指, 抬起手指, 依次触发 `touchstart` => `n次 touchmove` => `touchend`









