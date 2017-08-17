## 可维护性
- 可理解性：后期的维护人员容理解代码并且进行维护
- 直观性：不管操作或者说是业务有多么的复杂，代码中的东西一看就能够明白
- 可适应性：代码以一种数据上的变化，不要求完全重写方法
- 可扩展性：在代码架构上已经考虑到未来允许对核心功能进行扩展
- 可调试性：当有地方出错的时候，代码可以给予足够的信息直接确定问题的所在
## 代码约定
1. 可读性：必要的注释，良好的有意义的命名，代码的层次分明，代码简化，去除多余的代码
2. 松散耦合：解耦html/js，解耦css/js，解耦应用逻辑/事件处理程序，封装与重用
3. 安全：尊重对象所有权（对于js原生的固有对象，不要随便在原型上添加方法；对于自定义
局部使用对象可以使用，特别是在面向对象编程的时候）；避免全局变量（使用一个字面量对象存储
变量，或者使用立即执行函数）；对于不变的值使用常量const；避免与null进行比较，，可以使用
instanceof\typeof替换
4. 性能：避免内存溢出；避免全局查找（如果局部多次使用全局变量如document,可以使用一个局部变量
保存document）；避免使用with，with会创建自己的作用域，会增加其中执行代码的作用域链的长度
；循环的时候一定要确保终止循环的条件；原生方法比较快，switch比if-else快，位运算比较快；最小化
语句（比如声明多个变量，用一个var即可）；优化dom交互（如插入dom，避免多次插入，每次插入都会
造成reflow，使用documentFragment一次性插入；页面上创建dom节点的方法有createElement()\appendChild()
\innerHTML，对于大的dom更改，使用innerHTML要快得多【当innerHTML设置为某个值的时候，后台会创建
一个html解析器，然后使用内部dom调用来创建dom，而非基于javascript的dom调用，内部方法是编译好的
而非解释执行的，所以快的多】；使用事件代理（事件委托）；注意使用HTMLCollection）；js压缩和http压缩

## js中的new
- new一个函数隐藏的操作
 ```javascript
 function Animal(name){
   this.name = name
 }
 new Animal("cat") ==>{
    var obj = {}
    obj.__proto__ = Animal.prototype
    var result = Animal.call(obj,"cat")
    return result === 'object' ? result : obj
 }
 ```
 1. 创建一个空对象obj
 2. 把obj的__proto__指向了构造函数Animal的原型对象prototype
 此时便建立了原型链：obj - Animal.prototype - Object.prototype - null
 3. obj对象调用Animal的环境（很重要）
 4. 确定返回的对象
 - new的意义
 通过new创建的对象和构造函数之间建立了一条原型链，原型链的建立
 使得原本孤立的对象有了依赖和继承能力，体现了面向对象的本质

 ## 前端模块化
 1. 为什么需要模块化？

    代码量的骤增 => 分制管理的刚性需求
 2. 模块化方案需要解决的问题？

    要实现的问题：模块封装和模块加载
    - 如何定义模块以确保模块的作用域独立，避免命令冲突？
    - 如何管理模块之间的依赖关系，避免重复加载与循环引用？
    - 模块化代码如何部署，以降低http请求数？
    - 如何实现按需加载？
 3. 原始的解决方案以及局限性？
    命名空间+立即执行函数+script标签

    局限性：
    需要手动管理依赖，不具备可扩展性；无法实现按需加载
 4. 新的解决方案

     1.commonjs：module.exports暴露接口，require()获取资源；使用在服务器端的同步加载模块
     并不适合浏览器（网络延时、异步特性）
     ```javascript
     var math = require("math")
     math.add(2,3)
     ```
     如上述同步代码，第二行必须等待第一行require之后运行，换句话说必须等待math.js
     加载完成；浏览器的加载取决与网络，如果响应时间很长，真个应用都会停在那里；
     而服务器端不存在，所有模块都在本地硬盘，可以同步加载，等待时间短；因此，在浏览器
     端出现了各类模块加载器，以解决模块加载问题，各类模块加载器提出了各自的模块封装的规范
     ，其中sea.js提出/实现的封装规范，称为CMD规范；requirejs提出/实现的封装规范，就是AMD
     规范
     2.seajs：模块封装
     ```javascript
     define(function(require,exports,module){
         var a = require("./a") //模块加载
         a.dosomething()
         //...
         var b = require("./b") //依赖可以就近书写
         b.dosomething()
         //通过exports对外提供接口
         exports.doSomething
         //或者是通过module.exports提供整个接口
         module.exports = ...
     })
     ```
     模块加载：
     ```javascript
     var $ = require("jquery")
     ```
     3.requirejs
     模块封装
     ```javascript
     define(["./a","./b"],function(a,b){
        a.dosomething()
        //...
        b.dosomething()
        return function(){} //返回模块的值，可以是函数也可以是对象
     })
     ```
     模块加载
     ```javascript
     require(["./a","./b"],function(){
        //do something
     })
     ```
     区别：
     requirejs: 依赖前置，提前加载
     seajs: 依赖就近，延时加载

