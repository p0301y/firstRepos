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

     补充：
     - 什么是循环依赖：在a执行到require("b")的地方停下来去调用b，当去执行b的时候
     执行到一半require("a")，就停下来去调用a，就这么形成了循环依赖，死循环
     - require.js如何处理的：require.js只会执行到相互引用的部分，下面的代码不再过问
     ，也就是写再多也调不到
     - 循环导致的问题：开发时，在a中调用b的某个方法会报错，"xxx is not function" ,原因是b还没执行到该
     方法，得到的是null值
     - 解决办法：当出现循环依赖的时候，就不要依赖前置加载了，在a需要调用b的某个地方就近加载
     var b = require("b"),然后再去调用b的方法
     - 其他：循环依赖不会出现在ES6的import中，因为ES6中执行到import的时候并不会去执行import代码
     ，只是返回一个引用，等到真正用到的时候才会去执行

## 说说移动端与pc端的区别
- 移动端的网络考虑，3G4G而且没有pc端稳定，这就考虑到加载问题，懒加载和按需加载
- 移动端的分辨率各不先同，所以考虑到的是响应式布局
- 兼容性问题，移动端的浏览器的内核几乎都是webkit，所以css3和html5都可以使用，不像pc端考虑的兼容性很多，各种内核
- 交互模式pc端更加复杂，移动端基本是触摸、滑动和感应

## HTML的Doctype作用？严格模式与混杂模式如何区分？它们有何意义？
1. <!Doctype>声明位于文档的最前面，处于<html>标签之前，告知浏览器的
解析器以什么文档类型规范来解析规范
2. 严格模式的排版和js的运作模式是以该浏览器的最高标准运行。在混杂模式中，页面以宽松的
的向后兼容的方式显示。防止老的站点无法工作
3. DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现

## http2.0带来的前端优化
1. 请求头压缩：http每次请求会携带大量的冗余信息，浪费了很多宽带资源，压缩之后节省流量
2. 多路复用技术，直白的说就是所有的请求都是通过一个tcp连接完成并发的，提高了下载的效率
3. http2.0采用二进制格式传输数据，而非http1.0的文本格式，二进制在协议的解析和优化扩展上
带来了更多的优势和性能
4. server push:服务器端能够更快的把资源推送给客户端
## html5带来的前端优化
1. service worker:处理网络请求的后台服务。适用于离线和后台同步数据或者推送信息。不能直接和dom
交互，通过postMessage方法交互（出于安全考虑，目前只能在https的环境中使用service worker）
2. web worker:模拟多线程，允许复杂计算功能的脚本在后台运行而不会阻碍其他的脚本的运行，适用于处理器
占用量大而又不阻碍的情形，不能直接与dom交互，通过postMessage交互

## 前端静态资源的缓存和更新问题解析
浏览器缓存主要有两类
缓存协商：last-midified,Etag
彻底缓存：cache-control,Expires
200状态：当浏览器本地没有缓存或者下一层失效时，或者用户点击了CTL+F5时，浏览器直接去服务器下载新的数据
304状态：这一层是由last-modified/etag控制，当下一层失效时或者用户点击fresh，F5时，浏览器就会发送请求给服务器
，如果服务器端没有变化，则返回304给浏览器
200状态（from cache）：这一层由expires/cache-control控制；expires（http1.0版有效）是绝对时间；cache-control（http1.1版有效）
相对时间，两者都存在的时候，cache-control覆盖expires，只要是没有失效，浏览器只访问自己的缓存
1. last-modify
在浏览器第一次请求某一个url的时候，服务器端返回的状态码会是200，内容是你请求的资源，同时有一个last-modified的属性标记（HttpResponse Header)
此文件在服务器端最后被修改的时间，格式类似这样：
Last-Modify：Tue,24 Feb 2009 08:01:04 GTM
客户端在第二次请求此URL的时候，根据http协议规定，浏览器会像服务器传送If-Modify
-Since报头（HttpRequestHeader),询问该时间之后文件是否有被修改过：
If-Modify-Since:Tue,24 Feb 2009 08:01:04 GMT
如果服务器端的资源没有变化，则自动返回HTTP304(NotChanged)状态码，内容为空，这样就节省了传输数据量。
当服务器代码发生改变或者重启服务时，则重新发出资源，返回和第一次请求时类似。从而保证不向客户端重新
发出资源，也保证服务器有变化时，客户端能够得到最新的资源
注：如果If-Modified-Since的时间比服务器当前时间（当前的请求时间request_time）还晚，会认为是个非法请求
2. Etag工作原理
http协议规格说明定义ETag为“被请求变量的实体标记”。简单点即服务器响应时给请求URL标记，并在htpp请求头中
将其传送到客户端，类似服务器端返回的格式：
Etag:"ajfldajkfldajlf:3239"
客户端的查询更新格式是这样的：
If-None-Match: "jfjaklfjklajf:3239"
如果ETag没有改变，则返回状态304
注意：Etag在使用时候需要注意相同资源多台web服务器的Etag的一致性
3. expires
expires是用来控制请求文件的有效时间，一般是由服务器端设置的，如果带有expires
则在expire过期前不会发生htpp请求，直接从缓存中读取，用户强制F5例外
4. 区别
last-modify和expires针对浏览器，而Etag与客户端无关，所以可以适合REST架构
两者都应用在浏览器端的区别是：expires如期到达之前，浏览器不会发出新的请求
，除非用户按浏览器的刷新，所以last-Modified和expires基本是降低浏览器向服务器
发送的请求次数，而Etag更侧重于客户端与服务器之间的联系
5. last-modify,Etag,Expire混合
通常last-Modify,Etag,Expire是一起混合使用的，特别是last-Modify和Expire经常一起使用
因为Expire可以让浏览器不发起http请求，而浏览器强制F5的时候又有Last-Modify,这样就很好
的达到了浏览器端缓存的效果
Etag和Expire一起使用的时候，先判断Expire，如果已经过期，再发起http请求，如果Etag也过期了
，则返回200响应，如果没有过期则返回304响应
三者同时使用，先判断Expire，然后发送http请求，服务器先判断last-modified,再判断Etag，
必须都没有过期，才能返回304响应