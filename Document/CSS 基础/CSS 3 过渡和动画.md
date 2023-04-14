## CSS3 过渡和动画
CSS3 引入了过渡和动画，用于创建平滑的元素状态变化。以下是一些常见的 CSS 过渡和动画属性：

*   `transition`：指定元素在状态变化时应该如何平滑过渡。
*   `animation`：指定元素应该如何动画化。

## **transition** 有以下几个属性：

*   `transition-property`：指定要过渡的 CSS 属性。
*   `transition-duration`：指定过渡的时间。
*   `transition-timing-function`：指定过渡函数，控制过渡速度的变化。
*   `transition-delay`：指定过渡的延迟时间。

以下是一个实现鼠标悬停时 div 元素变暗的 `transition` 效果的 CSS 代码：

代码如下（[CodePen](https://codepen.io/webharry/pen/zYmrmyX)示例）:
```css
.transition_div {
  width: 100px;
  height: 100px;
  background: #92B901;
  color: #ffffff;
  padding: 10px;
  margin: 5px;
  
  transition: filter 0.5s ease; // 核心代码是这一行
}

.transition_div:hover {
  filter: brightness(70%);
}
```

`cubic-bezier`函数可以用来自定义过渡效果。它接受四个参数，分别表示贝塞尔曲线的两个控制点的坐标。例如：

```css
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1.0);
```

这个值会创建一个缓慢启动、快速结束的过渡效果。

`transition`只能用于可以进行过渡的CSS属性。这些属性包括：

*   background-color
*   background-position
*   border-color
*   border-width
*   border-spacing
*   bottom
*   clip
*   color
*   font-size
*   font-weight
*   height
*   left
*   letter-spacing
*   line-height
*   margin
*   max-height
*   max-width
*   min-height
*   min-width
*   ...

## **animation** 属性包含以下子属性：

*   `animation-name`：指定要应用的动画的名称。
*   `animation-duration`：指定动画持续的时间。
*   `animation-timing-function`：指定动画的速度曲线。
*   `animation-delay`：指定动画开始之前的延迟时间。
*   `animation-iteration-count`：指定动画应该重复的次数。
*   `animation-direction`：指定动画应该在循环中反向播放。
*   `animation-fill-mode`：指定动画在执行之前和之后如何应用样式。
*   `animation-play-state`：指定动画是否正在运行或已暂停。

`keyframes` 规则用于定义动画的每个阶段。通过 keyframes 规则，您可以指定动画的每个关键帧，即动画在执行过程中应该呈现的状态。每个关键帧都包含一个动画状态，例如元素的位置、颜色、透明度等。

keyframes 规则从 0%-50%-100% 定义了动画的整个过程，您可以在其中指定任意帧的状态。
例如，以下代码定义一个简单的动画，使元素从左侧移动到右侧：

代码如下（[CodePen](https://codepen.io/webharry/pen/vYVLVoX)示例）:

```css
@keyframes example {
  0%   {left: 0; top:0px;}
  50%  {left:200px; top:200px;}
  100% {left: 0px; top:0px;}
}
```

在上面的代码中，`@keyframes` 规则定义了一个名为 example 的动画，并指定该动画应该从 0%-50%-100% 进行一次循环。在这个动画中，元素的 left 属性从 0 变化到 200px，实现了从左上角移动到右下角，再回到左上角的效果。

您可以在 `animation` 属性中使用 `animation-name` 子属性来应用 `keyframes` 规则：

```css
div {
  animation-name: example;
  animation-duration: 5s;
  animation-iteration-count: infinite;
  animation-direction:alternate;
	animation-play-state:running;
}
```

在上面的代码中，animation-name 子属性指定应用名为 example 的 keyframes 规则的动画效果，animation-duration 子属性指定动画持续时间为 5s。animation-iteration-count 子属性指定动画应该无限次重复。animation-direction 指定动画应该在循环中反向播放。animation-play-state 指定动画是否正在运行。

`animation-timing-function` 属性用于控制动画的速度曲线。它可以使动画加速、减速、匀速或呈现弹性效果。

`animation-direction` 属性用于控制动画在循环中的方向。它可以使动画反向播放，或者在每个循环中交替正向和反向播放。

## 📢 update 同步更新

[掘金专栏](https://juejin.cn/column/7218749269896970299) | [知乎专栏](https://www.zhihu.com/column/c\_1627260575263817728) | [Github](https://github.com/webharry/fe-interview) | [简书专栏](https://www.jianshu.com/c/8ee0e31d826e) | [CSDN](https://blog.csdn.net/web_harry) | [segmentfault](https://segmentfault.com/u/yangjie\_5f0c1f890b88a/articles)
