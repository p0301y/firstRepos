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

