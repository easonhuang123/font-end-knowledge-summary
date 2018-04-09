## CSS

### 盒子模型

- 总尺寸 = content + padding + border + magin 

- W3C标准盒子 content只等于内容（即width和height只包括content）

- IE盒子 content = padding + border（即width和height包括了content + padding + border）

- css3新属性 box-sizing（默认值 content-box）

    - box-sizing: content-box 设定的width只含内容宽度，不包括padding + border （相当于W3C标准盒子）

    - box-sizing: border-box 设定的width包括content + padding + border（相当于IE盒子）
        - 在IE8，box-sizing的值为border-box时，不能与min-width, max-width, min-height或max-height的一起使用，因为IE8对min-和max-的解析，仍是作用于content-box，不受box-sizing属性控制

    - 一般都直接全局设置
    ```
        *{
            box-sizing: border-box
        }
    ```
    - 兼容ff和移动端的话最好加上前缀-moz-,-webkit

    ```
        *, *:before, *:after {
        　　-moz-box-sizing: border-box;
        　　-webkit-box-sizing: border-box;
        　　box-sizing: border-box;
        }
    ```

    - 对于行级元素inline
        - 可置换行内元素，其展示的内容是通过元素的src、value等属性或CSS content属性从外部引用得到的，可被替换的。随着内容来源或内容数量的变化，可置换元素本身也会有水平和垂直方向上尺寸的变化。典型的可替换元素有 `img` ,`object`,`video`和 `embed`，表单类的可替换元素有 `textarea` 和 `input`（其实很多浏览器将其视为行内块状元素inline-block）
        - 不可置换行内元素，如`a`,`span`，对他们设置width，height，margin-top和margin-bottom无效，但是设置margin-left和margin-right有效
        - 当行级元素水平排列时，两两之间可能会出现大约6px的空白，这是由元素间的空白字符（换行符、空格或制表符）产生，我的解决方法是设置元素`font-size: 0`，再在内层设置字体大小。
    - 对于相邻的块级元素block，margin-bottom和margin-top 
        - 若都是正数，取最大值
        - 若都是负数，取最小值
        - 一正一负，正负相加

- Position 定位
    - absolute 脱离文档流，相对于已定位的父元素进行移动，当某个absolute定位元素的父元素具有position:relative/absolute/fixed时，定位元素都会依据父元素而定位，而父元素没有设置position属性或者设置了默认属性，那么定位属性会依据html元素来定位
    - relative 相对于自身位置移动，原位置还保留在文档流中，内容发生了移动
    - fixed 脱离文档流，相对于浏览器窗口，对于IE78需要DOCTYPE
    - static 默认值
    - sticky 粘性定位 必须设置上下左右其中一个值（达到阈值前会相对定位，达到后变成固定定位）
        - 挺好玩的，例如导航条什么的可以用上
        - 但是兼容性非常不乐观
    - z-index
        - 只对于absolute，relative，fixed三种定位有效
        - 父子元素设置z-index无法进行比较，但是可以通过设置子元素的z-index为负数来控制顺序
- 样式引入方式
    - link标签
        - 没有兼容性问题
        - 还可以引入图标等资源
        - 在页面加载的时候同时加载css文件
        - 可通过js控制dom操作样式
    - import引入
        - 兼容性问题 css2.1 IE5
        - 网页加载完后再加载css文件，所以会出现闪烁现象
        - 不可通过js修改样式
        - 只能引入样式文件，但是可以在css文件里再引入css文件
        - 推荐书写 @import url(style.css) 
- 伪类:before :after
    - ::before 和 :before 差别时前者是css3调整的写法，所以后者的兼容性更好，其实效果一样
    - 必须与content属性一起使用
    - 不能通过js控制，只能在css中使用
    - 用途：清除浮动，制造各种小形状，icon
* 块与内联
    * 块
        * 特点
            * 独占一行
            * 宽高边距都可控
            * 宽度默认父容器宽度
            * 可容纳块与内联
        * 元素
            * div
            * p
            * h
            * ul
            * dl
            * ol
            * form
    * 内联
        * 特点
            * 都在一行
            * 高，行高，上下内外边距不可改，左右内外边距可改变但是不影响左右元素
            * 宽度是内容宽度
            * 只能容纳内联和文本
        * 元素
            * a
            * span
            * input
            * img
            * textarea
* 可继承属性
    * 可继承
        * 字体属性font
        * visibility
        * cursor
        * color
        * 部分文本属性
            * line-height
            * word-spacing字间距
            * letter-spacing字符间距
            * text-transform大小写
            * direction方向
            * 其中文本缩进text-indent，text-align只有块状元素可继承
    * 不可继承
        * 背景属性background
        * 布局属性margin
        * 定位属性position
        * display
        * 部分文本属性
            * vertical-align
            * text-decoration
            * text-shadow
            * white-space
            * unicode-dibi
* 选择器
    * 分类
        * *
        * .class
        * #id
        * div
        * div,p
        * div p
        * div>p
        * div+p
        * [attribute]
        * [attirbute=‘123']
        * [attribute~=‘123’]
        * [attritube|=‘123’]
        * :link :hover :active :visited :focus
        * :before :after
        * p:first-of-type (last, only，nth) 其父元素的第1/最后/唯一/n个p元素的所有p元素
        * p:nth-（-last-）child(n) 其父元素的（顺序，倒序）第n个元素的所有p元素
        * :root
        * p:empty
        * :disabled :checked
        * :not(p)
    * 优先级排序
        * 计算法则
            * 元素选择器： 1
            * 类选择器：10
            * ID选择器：100
            * 内联： 1000
        * !important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性
* 布局
    * 居中
        * 水平
            * 定宽 + margin: 0 auto
            * inline-block + text-align
            * display: table + margin: 0 auto
            * 父元素display: flex + justify-content: center
        * 垂直
            * display: table-cell + vertical-align: middle
            * 父元素display: flex + align-item: center
        * 万金油
            * position: absolute + top + left + transform: translate()
    * 图片 + 文字 对齐
        * 图片作为背景图片 background-image background-repeat background-size
        * 父容器 vertical-align: middle
    * 多列布局
        * float + overflow: hidden
        * columns-width columns-count（ IE10以下不支持，要写前缀）
            * 瀑布流布局
        * flex （兼容性也不好，需要加入兼容语法）
        ```
        {
            display: -webkit-box; 
            display: -webkit-flex; 
            display: -ms-flexbox; 
            display: flex;
        }
        ```
* flex
    * https://css-tricks.com/snippets/css/a-guide-to-flexbox/
* grid
    * https://juejin.im/entry/5894135c8fd9c5a19507f6a1
* 浮动
    * https://www.jianshu.com/p/07eb19957991
* 清除浮动
    * 原因
        * 浮动元素脱离文档流，影响页面结构
        * 父元素高度无法撑开
    *
    ```
    .clearfix { 
        zoom: 1; 
    }

    .clearfix::after { 
        content: ''; 
        clear: both; 
        height: 0; 
        visibility: hidden; 
        display: block; 
    }
    ```

* BFC
    * 块级格式化上下文
    * 触发条件
        * float不为none
        * overflow不为visible
        * display 为table-cell，table-caption，inline-block
        * position为absolute，fixed
        * fieldset元素
    * 功能
        * 自我独立，内部元素不会影响外部元素
        * 会包含浮动元素
        * 同一个BFC的margin重叠
* css3
    * 边框图片，圆角
        * Border-radius
        * &-image
    * 背景
        * Background-image
        * &-size
        * &-origin（位置区域content-box/border-box/padding-box）
        * &-clip（裁剪描绘区域）
        * 多重背景
    * 渐变色
        * Linear-gradient(angle,color1 10%,color2 30%,..)
        * Radial-gradient
        * 兼容性，添加前缀
    * 文本效果
        * Text-shadow
        * Box-shadow
        * Text-overflow
        * Word-wrap (break-word,强制断开分行）
        * Word-break（keep-all,break-all 是否换行）
        * 一行省略
        ```
        {
            display: block; 
            text-overflow: ellipsis; 
            white-space: nowrap; 
            overflow: hidden;
        }
        ```
        * N行省略
        ```
        {
            display: -webkit-box; 
            overflow: hidden; 
            text-overflow: ellipsis; 
            -webkit-box-orient: vertical; 
            -webkit-line-clamp: n;
        }
        ```
    * columns
    * flex
    * 2D/3D转换
        * transform
            * Matrix 矩阵变换
            * translate平移
            * scale缩放
            * rotate旋转
            * skew倾斜
    * 过渡
        * transition
    * 动画
        * @keyframes
        * animation
* 单位
    * px
    * em 当前字体大小
    * rem 根节点字体大小
    * vh, vw, vmin, vmax 视窗单位
    * ex, ch 给予特殊字体的单位
        * ex em的一半，字体的中间标志，可以上下用于微调
        * ch 数字0的宽度
* BEM
    * box--body
    * box__body
* 命名空间
    * .l- : 布局（layouts）
    * .o-: 对象（object）
    * .c-: 组件（componen）
    * .js: js钩子
    * .is- | .has-: 状态类
    * .t1 | .s1： 排版类
    * .u-: 实用类（utility）
* 媒体查询
    * 设置Meta标签
        * `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no”/>`
    * `@media (max-width: 960px) and (min-width: 600px) {…}`
* 响应式设计
    * rem适应屏幕大小
    * 媒体查询
    * flex流式布局
    * 响应式图片`<picture>`
* Css解析过程
    * CSS选择器的解析是从右向左解析的
        * 若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。
    * 而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。
* css优化
    * 雪碧图，利用背景图片位移
    * 对类名的设计与选择
        * 避免不必要的重复
        * 避免！important
        * 避免链式，后代选择符
    * 预处理
        * less，sass
    * 后处理
        * postCSS
* 兼容
    * *{margin:0 ; padding: 0;}
    * Hack 
        * _color ——IE6
        * *color ——IE6/7
        * color: red\9 ——IE8及以下
    * 24位PNG在IE6不支持
        * 用8位PNG
        * 准备专门的一套
    * A标签顺序
        * Link
        * visited
        * hover
        * Active 
    * 透明度
        * opacity： 0.8
        * filter: alpha(opacity=80) ——IE
        * filter:progid:DXImageTransform.Microsoft.Alpha(style=0,opacity=80); //IE6的写法
    * 盒子模型
    * 边距问题
        * 浮动双倍
        * Img图片存在边距
    * 各种前缀
    * flex
* css变量
    * https://mp.weixin.qq.com/s/wFz0PsOGaLb9KDGfEJuLaA

HTML
* html5
    * 语言规范
        * HTML5不基于sgml，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为。
        * 而HTML4.01基于sgml，所以需要DTD进行引用，才能告知浏览器文档所使用的文档类型。
    * DOCTYPE
        * doctype是声明文档类型，告诉浏览器以什么文档类型规范来解析这个文档。
        * 严格模式的排版和JS运作模式是以该浏览器支持的最高标准执行的。
        * 混杂模式中，页面以宽松的、向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
        * doctype不存在或不正确会导致文档以混杂模式呈现。
        * 严格模式与混杂模式存在的意义与其来源密切相关，如果说只存在严格模式，那么许多旧网站必然受到影响，如果只存在混杂模式，那么会回到当时浏览器大战时的混乱，每个浏览器都有自己的解析模式。
    * 语义化标签
        * 用正确的标签做正确的事
        * 让页面内容结构化，便于浏览器、搜索引擎解析
        * 在去掉或丢失样式的时候能让页面呈现出清晰的结构
        * 搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，有利于SEO
        * 便于团队开发和维护，语义化更具可读性，可以减少差异性
    * canvas，svg
    * 多媒体，音频视频
    * 地理定位 navigator.geolocation.getCurrentPosition
    * 拖拽API draggable
    * 陀螺仪
    * iframe
        * https://segmentfault.com/a/1190000004502619
    * head标签
        * https://zhuanlan.zhihu.com/p/34918296
    * 回流与重绘
        * http://www.css88.com/archives/4996













