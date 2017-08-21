## 面试题
1. canvas上的图形可以使用诸如getElementById()之类的方法获得吗？如果不行该
怎么获取？
canvas是通过js绘制的图形，图形是一个个像素画上去的，不可以获取到；但是svg是
基于xml的格式，内部是一个个节点，可以用dom获取节点；canvas可以通过原生的
toDataURL()方法获取图像的Base64编码
2. ES6中的箭头函数可以用作构造函数吗？
不可以，因为箭头函数中没有绑定this，所以不可以使用new操作符调用
3. null和undefined区别？
null是一个表示无的对象，转化为数值时为0；undefined是一个表示“无”
的原始值，转化为数值时为NaN：
- 变量声明了，但是没有赋值时就等于undefined
- 函数调用时，应该提供的函数没有提供，为undefined
- 对象没有赋值的属性，该属性的值为undefined
- 函数没有返回值时，默认返回undefined
- null表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象
- 对象原型链的终点是null
4. js延时加载的方式有哪些？
script的defer和async、动态创建dom（创建script，插入到dom中，加载完毕后callback）
按需异步加载js(requirejs\webpack)
5. 如何删除cookie？
设置cookie过期即可
6. 实现一个函数clone，可以对javascript的5种主要的数据类型（包括Number、String、Object
Array。Boolean）进行赋值
```javascript
Object.prototype.clone = function(){
    var o = this.constructor === Array ? [] : {}
    for(var e in this){
        o[e] = typeof this[e] === "object" ? this[e].clone() : this[e]
    }
    return o
 }
 ```
7. <strong>,<em>,<b>,<i>标签
strong和em是表达要素(phrase elements),都是用于强调文本，但是strong的强调程度更强一些
b和i是视觉要素，分别表示无意义的加粗和斜体