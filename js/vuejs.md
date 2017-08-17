## 理解vuejs
传统的方法：修改某个对象的属性，就选取这个属性对应的html上的dom，如果添加一个对象
或者说是node节点，使用的是append方法
vuejs的思路是不再需要操作dom了，你只要操作数据对象就可以了，对应的html会自动更新
，所以使用vue的时候，基本可以隔离dom操作，代码中的大部分操作对象或者数组

总结：“数据驱动的组件系统”，“dom操作封装在指令中”

## vuejs的双向绑定
访问器属性（es5 的新增，所以不支持ie8）：访问器属性是一种特殊的属性，他不能直接在对象中设置
，而必须通过Object.defineProperty()单独定义：
```javascript
Object.defineProperty(obj,prop,descriptor)
var obj = {}
Object.defineProperty(obj,"key",{
    enumerable: false,
    configurable: false,
    writable: false,
    value: "static",
    set: function(val){
        this.key = val
    },
    get: function(){
        return this.key
    }
})
```
最重要的是set方法：在改变属性的值的时候，需要通过set函数

- view数据改变，以input为例子，添加change事件，值改变的时候设置obj的prop
- obj的prop中的set方法添加一个watcher，值改变触发watcher【发布者】
- 所有有关prop的dom用都是一个对象【订阅者】，包含更改prop值的方法，将所有对象添加到dep【主题对象】
- watcher通过主题对象使所有的观察者更新数据

## vuejs的自定义指令
在vue2.0中，代码的抽象和重用的主要形式是以组件的形式，但是可能在某些情况下，还是需要
对普通元素进行一些底层的dom访问，这是自定义指令仍然使用的场景之处，可以说是“数据驱动视图”的
一种有效补充或者说是扩展，不仅可用于定义任何的dom操作，并且是可以复用的

自定义指令的方法是：Vue.directive("focus",{各种钩子函数})
钩子函数（全部可选）：
bind: 在指令第一次绑定到元素调用，只会调用一次
unbind: 在指令从元素上解除绑定时调用，只会调用一次
inserted: 在已绑定的元素插入到父节点时调用
update:
componentUpdate:

钩子函数的参数：
el: 指令绑定的元素，可以用于直接的dom操作
binding: 一个对象（name,value,oldValue,expression,arg,modifiers）
vnode: 由vue编译器生成的虚拟dom
oldVnode: 之前的虚拟dom

