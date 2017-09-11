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
