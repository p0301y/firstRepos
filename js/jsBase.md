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