# 层叠、优先级和继承

## 层叠

冲突解析规则：
样式表的来源：样式是从哪里来的，包括你的样式和浏览器默认样式等。
选择器优先级：哪些选择器比另一些选择器更重要。
源码顺序：样式在样式表里的声明顺序。

### 权重表

## CSS 选择器权重表

| 选择器                       | ID  | 类  | 标签 | 标记  |
| ---------------------------- | --- | --- | ---- | ----- |
| `html body header h1`        | 0   | 0   | 4    | 0,0,4 |
| `body header.page-header h1` | 0   | 1   | 3    | 0,1,3 |
| `.page-header .title`        | 0   | 2   | 0    | 0,2,0 |
| `#page-title`                | 1   | 0   | 0    | 1,0,0 |

### 建议

- 在选择器中不要使用ID。就算只用一个ID，也会大幅提升优先级。当需要覆盖这个选择
  器时，通常找不到另一个有意义的 ID，于是就会复制原来的选择器，然后加上另一个类，让它区别于想要覆盖的选择器。
- 不要使用!important。它比ID更难覆盖，一旦用了它，想要覆盖原先的声明，就需要再加上一个!important，而且依然要处理优先级的问题。

## 继承

- 如果一个元素的某个属性没有层叠值，则可能会继承某个祖先元素的值。比如通常会给<body>元素加上font-family，里面的所有祖先元素都会继承这个字体，就不必给页面的每个元素明确指定字体了。

继承关系：

```txt
<html>
└── <body>
    ├── <header>
    │   ├── <h1>
    │   └── <ul>
    │       ├── <li>
    │       ├── <li>
    │       ├── <li>
    │       └── <li>
    └── <main>
```

- 不是所有都可以被继承
  默认的属性，比如：color、font、font-family、font-size、
  font-weight、font-variant、font-style、line-height、letter-spacing、text-align、
  text-indent、text-transform、white-space 以及 word-spacing。 ，都是可以被继承的。
  还有一些其他的属性也可以被继承，比如列表属性：list-style、list-style-type、
  list-style-position 以及 list-style-image。表格的边框属性 border-collapse 和
  border-spacing 也能被继承。
  （显然没有人愿意将一个div传递到每个后代）

### 样式debug

f12 -> 检查 -> 样式 -> 查看元素的样式

## 特殊值

- inherit 继承父元素的值
- initial 初始值 大部分颜色初始值其实是黑色的
  - 优势是不用考虑太多 直接恢复原样即可
- 要注意，auto 不是所有属性的默认值，对很多属性来说甚至不是合法的值。比如
  border-width: auto 和 padding: auto 是非法的，因此不会生效。可以花点时间研究一下
  这些属性的初始值，不过使用initial更简单。
  声明display: initial 等价于 display: inline。不管应用于哪种类型的
  元素，它都不会等于display: block。这是因为initial重置为属性的初始值，而
  不是元素的初始值。inline才是display属性的初始值。元素的display有很多，但是这里是属性级别的

## 简写属性

大多数简写属性可以省略一些值，只指定我们关注的值。但是要知道，这样做仍然会设置省
略的值，即它们会被隐式地设置为初始值。

- font
  - font-style、font-weight、font-size、font-height 以及
    font-family。
    font: italic bold 18px/1.2 "Helvetica", "Arial", sans-serif;
- border
  - border-width、border-style、border-color
    border: 2px solid red;
- background
  - background-color、background-image、background-repeat、background-position、background-attachment
    background: red url("bg.jpg") no-repeat center center fixed;
- 部分简写存在顺序 margin padding：
  。如果声明结束时四个属性值还剩一个没指定，没有指定的一
  边会取其对边的值。指定三个值时，左边和右边都会使用第二个值。指定两个值时，上边和下边会
  使用第一个值。如果只指定一个值，那么四个方向都会使用这个值。因此下面的声明都是等价的。
- 水平 垂直
  - 括background-position、box-shadow、text-shadow

建议： 如果属性需要指定从一个点出发的两个方向的值，就想想“笛卡儿网格”。如果属性需要指
定一个元素四个方向的值，就想想“时钟”。
