## 闭包的用途，换句话说是什么时候需要使用闭包
1. 可以读取函数的内部变量
2. 可以让这些变量的值始终保存在内存中
注意：立即执行函数中定义函数也是闭包，立即执行函数封装了一个作用域，将参数传递
进去就相当于传值，内部定义的函数引用了，就会使这些变量保存在内存中
```javascript
var arr = []
for(var i=0;i<=3;i++){
   arr[i] = (function (j){
    console.log(j)
   })(i)
}
```
[连接地址]{http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html}

## 媒体查询的总结
响应式设计的核心是媒体查询
1. 设置Meta标签
```html
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">
//width = device-width: 宽度等于当前设备的宽度
//initial-scale: 初始的缩放比例（默认值设置为1.0）
//minimum-scale/maximum-scale: 允许用户缩放的最小和最大的比例
//user-scalable: 是否允许手动缩放
```
2. 加载兼容文件js
因为ie8既不支持html5，也不支持css3 Media,所以需要加载两个文件
```
<!--[if it IE 9]>
<script src = "https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
<script src = "https://oss.maxcdn.com/libs/response.js/1.3.0/respond.min.js"></script>
<![endif]-->
```
3. 设置ie的渲染方式默认为最高【换句话说，ie9的就不要使用ie8的渲染方式了】（可选）
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
//建议使用
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
//chrome=1:如果用户电脑中装了chrome插件，就可以让电脑中的ie不管是哪个版本都可以使用webkit引擎以及v8引擎来运算
```

4. media的写法
第一种，直接在link标签中的Media属性
第二种，在css中的条件中写
5. media所有参数
width/height/device-width/device-height/orientation/color/aspect-ratio/device-aspect-ratio/color-index/grid/resolution/monochrome

## 响应式布局的几种方式
- 媒体查询 Media css
- bootstrap的栅格布局
- flex的弹性盒子模型

## 响应式的图片
1. 最常用的矢量图；矢量图是图形，通过数学公式画出来的，放大和缩小不失真；图像一般是拍摄出来的，缩放比例不是100%，从某种程度上是失真
2. img标签，图片随着容器自动放缩，保持宽高比，max-width:100%;
3. 背景图片，background-size:contain【没有裁切】,background-size:cover【可能有裁切】
4. 设置固定的高宽比，有利于适应不同的屏幕，如轮播图组，可以通过padding和margin的放缩，建议使用百分比【相对于父容器的width】
```css
.test{
    height:0;
    padding-top:50%;
    background: red;
}
```

## 响应式布局的字体
rem

## html5的API
1. 语义化
- html5的节段和提纲：section,article,nav,header,footer,aside,hgroup,figure标签
- 音视频：audio，video
- 表单和兼容性解释器
2. 通信
- websocket全双工通信
3. 离线存储
- indexDB,浏览器端的数据库，存储大量结构化数据，并且能够在这些数据上使用索引进行高性能检索
- localStorage，键值对存储数据，js操作进行操作和销毁的对象
4. 多媒体
- audio和video
5. 图像和3D
- canvas和webGL
6. 性能
- web worker
- XMLHttpRequest2
- history API
- contentEditable 富文本操作
- drag和drop 拖拽
- 动画 requestAnimationFrame
7. 设备访问
- 检测设备方向
- 使用地理位置

## 理解BOM和DOM
1. BOM: 浏览器对象模型(browser)，BOM提供了很多对象，用于访问浏览器功能，核心对象是window
2. DOM: 文档对象模型(documnet),是针对html和xml文档的一个API（应用程序编程接口），DOM描绘了一个层次化的
节点树，允许开发人员添加和移除和修改页面的某一个部分
补充：
- 最基本的节点类型是Node,用于抽象的表示文档中一个独立的部分；所有其他类型都是继承自Node
- document类型表示整个文档，是一组分层节点的根节点，在javascript中，document对象是Document的一个实例
- element节点表示文档中所有html和xml元素，可以用来操作这些元素的类容和特性