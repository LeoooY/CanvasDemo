使用js+Canvas实现一个星空的效果(随机粒子)  
- [Preview](https://leoooy.github.io/CanvasDemo/)
## 相关
- Canvas
- ES6 class 私有有方法 symbol

## 思路
- 创建一个全屏Canvas画布
- 实现一个``` PointItem ``` 类,用于接收坐标,生成随机的粒子(随机位置、alpha值)
- 使用requestAnimation函数递归重绘更新

## 参考
- 掘金小册Canvas《如何使用Canvas制作出炫酷的网页背景特效》