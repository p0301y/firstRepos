## 两列布局
1. div的内联(inline-block)
```css
.left{
    display:inline-block;
    width: 200px;
}
.right{
    display:inline-block
}
```
2. 绝对定位(html代码的书写右边在前，左边在后，即右边先加载)【float也是可以的，脱离文档流】
```css
.right{
    width:100%
    margin-left: 200px
}
.left{
    position:absolute //脱离文档流，相对于父级非static元素
    width:200px
}
```
3. flex(flex-grow: 1)
4. calc()计算
5. 负margin（html代码的书写右边在前，左边在后，即右边先加载）【这种方式比较麻烦】
```html
<div class="leftWrap">
    <div class="left">就fda开始了</div>
</div>
<div class="right">hello</div>
<style>
    .leftWrap{
        width: 100%;
        float: left;
    }
    .left{
        /*width: 100%;*/
        background-color:#2b2b2b;
        margin-left: 200px;
        height: 100px;
    }
    .right{
        float: left;
        background-color: #00acd6;
        width: 200px;
        height: 100px;
        margin-left: -100%;
    }
</style>
```

## 常见的伪类与伪元素
1. 伪类，顾名思义，类似于在元素上添加一个class，对目标元素进行操作
    - :active 向被激活的元素添加样式
    - :focus 向拥有键盘输入焦点的元素添加样式
    - :hover 当鼠标悬浮的时候添加样式
    - :link 向未被访问的连接添加样式
    - :visited 向一杯访问的连接添加样式
    - :first-child 向第一个子元素添加样式
    - :lang 向带有lang属性的元素添加样式
2. 伪元素，顾名思义，添加新的元素标签
    - :first-letter 向文本的第一个字母添加特殊样式
    - :first-line 向文本首行添加特殊的样式
    - :before 在元素之前添加类容
    - :after 在元素之后添加类容

