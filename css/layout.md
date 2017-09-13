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

## flex布局-弹性布局
任何一个元素都可以指定为flex，行内元素也可以指定为flex布局，webkit内核的浏览器
必须加上-webkit前缀
```
.box{
    display: flex;
}
.box{
    display: inline-flex;
}
.box{
    display: -webkit-flex;
    display: flex;
}
```
注意设置为flex布局之后，子元素的float、clear、vertical-align属性将失效
父元素display: flex之后成为伸缩容器，子元素（除了position: absolute和fixed）
无论是display:block或者display: inline都将称为伸缩项目；伸缩项目之间，没有inline-block
元素之间的空隙；伸缩项目自动box-sizing:border-box;
1. 采用flex布局的元素称为flex容器(flex container),简称“容器”。他的所有
子元素自动成为容器成员，称为flex项目(flex item),简称项目
2. 容器的属性
    - flex-direction: 决定主轴的方向（即项目排列的方向）
    ```
    .box{
        flex-direction: row | row-reverse | column | column-reverse
    }
    ```
    - flex-wrap: 决定容器中的项目是否换行，默认是不换行的
    ```
    .box{
        flex-wrap: nowrap | wrap | wrap-reverse
    }
    ```
    - flex-flow: 是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
    - justify-content: 定义项目在主轴上的对齐方式
    ```
    .box{
        justify-content: flex-start | flex-end | center | space-between | space-around
    }
    ```
    - align-items: 定义项目在交叉轴上如何对齐
    ```
    .box{
        align-items: flex-start | flex-end | center | baseline | strench;
    }
    ```
    - align-content: 定义多根轴线的对齐方式
3. 项目属性
    - order: 定义项目的排列顺序，数值越小越靠前，默认值为0
    ```
    .item{
        order: <Integer>;//可以为负数
    }
    ```
    - flex-grow: 定义放大比例，默认值为0，即如果存在剩余空间，也不放大，通常用来响应式布局，填充剩余的部分
    ```
    .item{
        flex-grow: <number>;/*default 0*/
    }
    ```
    如果所有的项目flex-grow属性都为1，则它们将等分剩余的空间；如果为其他数>0,则按比例分配剩余的空间
    - flex-shrink: 定义了项目的缩小比例，默认为1，即空间不足，该项目将缩小，不想项目缩小则设置为0
    ```
    .item{
        flex-shrink: <number>; /*default 1 不能为负数*/
    }
    ```

    - flex-basis: 定义了在分配多余的空间之前，项目占据的主轴空间(main size)，浏览器根据这个属性计算主轴是否有多余的空间，它的默认值为auto，即项目的本来大小
    ```
    .item{
        flex-basis: <length> | auto; /* default auto */
    }
    ```
    它可以设置为跟width或height属性一样的值(比如350px)，则项目将占据固定空间
    - flex: 是flex-grow\flex-shrink\flex-basis的简写，默认值为0 1 auto
    - align-self: 允许单个项目与其他项目不一样的对齐方式，可以覆盖align-items属性，默认值为auto，
    表示继承了父元素的align-items属性
[参考连接]{http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html}

