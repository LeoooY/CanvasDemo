### 简介
`<canvas>`是一个可以使用脚本(通常为JavaScript)来绘制图形的 HTML 元素

- Canvas 的默认大小为300像素×150像素（宽×高，像素的单位是px）
  - 可以使用HTML的高度和宽度属性来自定义Canvas 的尺寸
  - 三种定义宽高的方法
    - html元素上定义width 和 height
    - Js定义
    - css定义（`不推荐`）css定义会拉伸画布

### 基本用法
`<canvas>`标签只有两个属性
`width`和`height`,默认为宽300*高500
 
 - 替换内容
   - 直接在`<canvas></canvas>`标签内部写替换的内容
   - 不支持canvas的浏览器会直接忽略canvas容器，并渲染`<canvas></canvas>`标签内的内容  
示例：
```
<canvas id="stockGraph" width="150" height="150">
  current stock price: $3.15 +0.15
</canvas>

<canvas id="clock" width="150" height="150">
  <img src="images/clock.png" width="150" height="150" alt=""/>
</canvas>
```
- `</canvas>`标签不可省

- 渲染上下文
  - canvas标签有个getContext()方法，用于获得渲染上下文和绘画功能
```
var canvas = document.getElementById('tutorial');
var ctx = canvas.getContext('2d'); 
//ctx变量即为渲染上下文，可以进行绘图操作等
```
- 检查支持性（浏览器是否支持canvas）
  
```
    var canvas = document.getElementById('tutorial');
    if (canvas.getContext){
        var ctx = canvas.getContext('2d');
        // drawing code here
    } else {
        // canvas-unsupported code here
    }
```

### 绘制形状
- 栅格 Canvas grid画布栅格

- 绘制矩形
  - 不同于SVG，HTML中的元素canvas只支持一种原生的图形绘制：矩形。所有其他的图形的绘制都至少需要生成一条路径。不过，我们拥有众多路径生成的方法让复杂图形的绘制成为了可能。

- canvas提供了三种方式生成矩形
  - fillRect(x,y,width,height) 绘制一个填充的矩形
  - srokeRect(x,y,width,height) 绘制一个矩形的边框
  - clearRect(x,y,width,height) 清除矩形区域让清除部分完全透明

### 绘制路径
图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。使用路径绘制图形需要一些额外的步骤。

- 创建路径起始点
- 使用画图命令画出路径
- 把路径封闭
- 路径完成，使用描边或者填充路径来渲染

用到的函数
- beginPath()
  - 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径
- closePath()
  - 闭合路径之后图形绘制命令有重新指向到上下文
- stroke()
  - 通过线条来绘制图形路径
- fill()
  - 通过填充路径的内容区域生成实心的图形
  
生成路径的`第一步`叫做beginPath()。本质上，路径是由很多子路径构成，这些子路径都是在一个列表中，所有的子路径（线、弧形、等等）构成图形。而每次这个方法调用之后，列表清空重置，然后我们就可以重新绘制新的图形。
- moveTo()
  - 注意：当前路径为空，即调用beginPath()之后，或者canvas刚建的时候，第一条路径构造命令通常被视为是moveTo（），无论实际上是什么。出于这个原因，你几乎总是要在设置路径之后专门指定你的起始位置。

`第二步`就是调用函数指定绘制路径  
`第三`，就是闭合路径closePath(),不是必需的。这个方法会通过绘制一条从当前点到开始点的直线来闭合图形。如果图形是已经闭合了的，即当前点为开始点，该函数什么也不做。  
  - 调用fill()会自动闭合不必使用closePath()来闭合
  - 调用stroke()不会自动闭合  

Example:绘制一个三角形

- 移动笔触
  - moveTo(x, y) 将笔触移动到指定的坐标x以及y上。
  - 当canvas初始化或者beginPath()调用后，你通常会使用moveTo()函数设置起点。
  - 用于绘制不连续的路径
  - 
- 线
  - lineTo(x,y)
  - 绘制直线，绘制一条从当前位置到指定x以及y位置的直线。
  - 开始点和之前的绘制路径有关，之前路径的结束点就是接下来的开始点
  - 开始点也可以通过moveTo()函数改变  
  
例子 填充三角形和描边三角形
    - 注意到填充与描边三角形步骤有所不同。正如上面所提到的，因为路径使用填充（fill）时，路径自动闭合，使用描边（stroke）则不会闭合路径。如果没有添加闭合路径closePath()到描述三角形函数中，则只绘制了两条线段，并不是一个完整的三角形。
- 圆弧
  - 绘制圆弧或者圆，我们使用arc()方法。当然可以使用arcTo()，不过这个的实现并不是那么的可靠，所以我们这里不作介绍。
  - arc(x,y,radius,startAngle,endAngle,anticlockwise)
    - 画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。
    - 注意：arc()函数中表示角的单位是弧度，不是角度。角度与弧度的js表达式:弧度=(Math.PI/180)*角度
  - arcTo(x1, y1, x2, y2, radius)
    - 根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点。
- [贝塞尔曲线](https://github.com/hujiulong/blog/issues/1)
  - 二次贝塞尔曲线及三次贝塞尔曲线
  - 二次及三次贝塞尔曲线都十分有用，一般用来绘制`复杂`有规律的图形。
  - 绘制复杂的曲线
  - quadraticCurveTo(cp1x, cp1y, x, y)
    - 绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点。
  - bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
    - 绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。
- path2D对象
    - 
    - 使用SVG paths
### 添加样式和颜色
- 颜色
如果我们想要给图形上色，有两个重要的属性可以做到：fillStyle 和 strokeStyle。
  - fillStyle = color
  - strokeStyle = color

  注意: 一旦您设置了 strokeStyle 或者 fillStyle 的值，那么这个新值就会成为新绘制的图形的默认值。如果你要给每个图形上不同的颜色，你需要重新设置 fillStyle 或 strokeStyle 的值。
  ```
  // 这些 fillStyle 的值均为 '橙色'
  ctx.fillStyle = "orange";
  ctx.fillStyle = "#FFA500";
  ctx.fillStyle = "rgb(255,165,0)";
  ctx.fillStyle = "rgba(255,165,0,1)";
  ```
- 透明度 Transparency
  - canvas提供一个API绘制半透明的图形
    - globalAlpha = transparencyValue
      - 这个属性影响到 canvas 里所有图形的透明度，有效的值范围是 0.0 （完全透明）到 1.0（完全不透明），默认是 1.0。
    - globalAlpha 属性在需要绘制大量拥有相同透明度的图形时候比较高效
  - 更具操作性的方法 设置rgba颜色  
因为 strokeStyle 和 fillStyle 属性接受符合 CSS 3 规范的颜色值，那我们可以用下面的写法来设置具有透明度的颜色。
```
// 指定透明颜色，用于描边和填充样式
ctx.strokeStyle = "rgba(255,0,0,0.5)";
ctx.fillStyle = "rgba(255,0,0,0.5)";
//0.0（完全透明）到 1.0（完全不透明）

```
- 线型 lineStyle
  - lineWidth = value
    - 设置线条宽度
  - lineCap = type
    - 设置线条末端样式
  - lineJoin = type
    - 设定线条与线条结合处的样式
  - lineLimit = value
    - 限制当两条线相交时交接处最大长度;指的是线条交接出内角顶点到外角顶点的长度
  - getLineDash()
    - 返回一个包含当前虚线样式，长度为非负偶数的数组。
  - setLineDash(segments)
    - 设置当前虚线样式。
  - lineDashOffset = value
    - 设置虚线样式的起始偏移量。


- 渐变 Gradients
  - 线性渐变 LinearGradient
    - createLinearGradient(x1, y1, x2, y2)
    - 方法接受 4 个参数，表示渐变的起点 (x1,y1) 与终点 (x2,y2)。
  - 球形渐变 RadiaGradient
    - createRadialGradient(x1, y1, r1, x2, y2, r2)
    - createRadialGradient 方法接受 6 个参数，前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆。
  - gradient.addColorStop(position, color)
    - 创建颜色梯度
    - 
- 图案样式 Patterns
  - 类似于渐变
  - patterns使用img图片对象作为填充的颜色
  - 可以赋给fillStyle和strokeStyle
- 阴影 Shadow
  - shadowOddsetX = float
  - shadowOddsetY = float
  - shadowBlur = float
  - shadowColor = color
- Canvas 填充规则
### 绘制文本

- fillText(text, x, y [, maxWidth])
  - 在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的.
- strokeText(text, x, y [, maxWidth])
  - 在指定的(x,y)位置绘制文本边框，绘制的最大宽度是可选的.