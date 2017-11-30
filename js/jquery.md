## juery知识分类
1. $.ready(): 当dom已经加载，并且页面（包括图像）已经完全呈现时，会发生ready事件
```
$(document).ready(function(){
    ...js
})
```
2. $(" "): 选择器（重点无new构造）
```
(function(window,undefined){
    var rootjQuery = window.document
    var jQuery = (function(){
        var jQuery = function(selector,context){
            return new jQuery.fn.init(selector,context,rootjQuery)
        }

        jQuery.fn = jQuery.prototype = {
            constructor: jQuery,
            init: function(selector,context,rootjQuery){
                var that = this
                that.ele = null
                that.value = ''
                if(selector.charAt(0) === '#'){
                    this.ele = document.getElementById(selector.slice(1))
                }
                that.getValue = function(){
                    that.value = that.ele ? that.ele.innerHTML : 'no value'
                }
                that.showValue = function(){
                    return that.value
                }
            }
        }
        jQuery.fn.init.prototype = jQuery.fn
        return jQuery
    })()
    window.jQuery = window.$ = jQuery
})(window)
```
3. $("").html()\text()\val():读取选定元素的内容
- html()用来读取元素的html内容（包括html标签）
- text()用来读取表单元素的纯文本内容，包括后代元素
- val()是用来读取表单元素的value值
```
<div id="app">
    <h1>标题</h1>
    <p>段落</p>
    <input type="text" id="inp" value="表单">
</div>
<script>
    $(document).ready(function () {
        var pre = $("#app"),inp = $("#inp")
        console.log("html"+pre.html())
        console.log("text"+pre.text())
        console.log("val"+ inp.val())
    })
</script>

html
    <h1>标题</h1>
    <p>段落</p>
    <input type="text" id="inp" value="表单">
text
    标题
    段落
val
    表单
```
4. $("").attr()\prop()\addclass()...:属性操作（方法的重载）
```
$("#id").attr('title') //获取title属性的值
$("#id").attr("title","jquery") //设置title的属性
```
5. $("").css():样式操作（方法的重载）
```
$("").css("color") //获取color的值
$("").css("color","red") //设置color的值为red
```
6. $("").animate(): 动画
```
$("#id").animate({
    left: 100px  //向右移动100px
})
```
7. $("").data():取出保存的数据
```
<div data-type="jfiaoif"></div>
var type = $("").data("type")
```
8. $("").on()\trigger(): 事件
9. $.ajax({}): ajax请求
10. $.deffered(): 异步变同步，类似promise的写法
11. $("").eq(0).html(): 链式调用（每个方法返回jquery对象）
12. jquery.fn.extend(object): 给jquery对象添加实例方法，就是在原型prototype添加方法， 通过extend添加的新方法，实例化的jquery对象都可以使用，
即$("").functionName();jquery.extend(object): 给jquery添加静态方法，通过$.functionName()

## jquery源码部分知识
1. jquery.fn.css()的内部关键使用的js的getComputedStyle以及getPropertyValue方法
    - getComputedStyle()的用法：可以获取当前元素所有最终使用的css属性值，返回一个
    css样式声明对象（只读）
    ```
    var style = window.getComputedStyle("元素"，"伪类")
    var style = document.getComputedStyle(...)

    var dom = document.getElementById("test")
    style = window.getComputedStyle(dom,":after")
    ```
    - getComputedStyle与style的区别：
        1. 只读与可写：getComputedStyle只读，element.style可读可写
        2. 获取的对象范围：getComputedStyle方法获取的是最终应用在元素上的所有css属性对象（即使没有css代码，也会把默认的祖宗十八代都
        显示出来）；而lement.style只能获取元素style属性中的css样式
    - getComputedStyle与defaultView
        如果查看jquery源码，会发现css()使用的是document.defaultView.getComputedStyle;
        实际上defaultView更本没有必要，getComputedStyle本身就存在于window对象
    - ie中使用element.currentStyle,功能与getComputeStyle相似
    - getPropertyValue方法（与getAttribute()类似）可以获取css样式申明对象上的属性值（直接属性名称，ie9+浏览器都支持），如果不使用getPropertyValue方法，直接使用键值访问
    ```
    var style = document.getComputedStyle(dom,null)
    //以下三种写法是等价的
    style.getPropertyValue("float")
    style.float
    style.getAttribute("float")
    ```

2. jquery插件的写法
2.1 原型方法
    - $.fn.functionName = function([options]){};一次一个函数
    - $.fn.extend({functionName:function(){},..});一次声明多个函数
2.2 静态方法
    - $.extend(defaults,options);其中default为默认设置，options为传入的参数；
    这个函数的作用是用后面的参数与第一个参数进行合并然后返回它的值
    ```
    (function($){
        $.fn.color = function(options){
            var defaults = {color: "blue",size:"30px"}
            console.log($.extend(defaults,options))
            console.log(defaults)
            console.log(options)
            //return的作用是支持链式调用
            return $(this).each(function(){
                $(this).css({"color": options.color})
                $(this).css({"font-size": options.size})
            })
        }
    })(window.jQuery)
    ```
    - $.extend({},defaults,options),不会导致defaults被代替，所以一般选择使用这个