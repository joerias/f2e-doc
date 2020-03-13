### CSS 部分（airbnb 规范标准）

#### - 格式

- 使用 2 个空格作为缩进

- 类名建议使用破折号代替驼峰法。如果你使用 BEM，也可以使用下划线

- 不要使用 ID 选择器

- 在一个规则声明中应用了多个选择器时，每个选择器独占一行

- 在规则声明的左大括号 { 前加上一个空格；在属性的冒号 : 后面加上一个空格，前面不加空格；规则声明的右大括号 } 独占一行；规则声明之间用空行分隔开。

#### - 注释

- 建议使用行注释 (在 Sass 中是 //) 代替块注释。

- 建议注释独占一行。避免行末注释。

- 给没有自注释的代码写上详细说明，比如：

```javascript
- 为什么用到了 z-index
- 兼容性处理或者针对特定浏览器的 hack
```

- 不建议使用 ID 选择器。ID 选择器会带来不必要的优先级，而且 ID 选择器是不可复用的

- JavaScript 钩子。避免在 Css 和 JavaScript 中绑定相同的类，不利于后续维护，因为写定后就相当于样式和 js 文件绑定了，改样式名词会造成页面逻辑出错。如果要涉及到与样式有关的操作，添加.js-前缀

- 定义边框无样式时，使用 0 代替 none

- 不要让嵌套选择器深度超过 3 层

### Google HTML/CSS 代码风格

#### - HTML 规则

- 标签，属性，属性值，css 选择器，属性，和属性值只使用小写

- 指定页面编码为 utf-8

- 添加合理的注释，说明相关代码是做什么的，只在关键代码处添加相关注释，避免过多添加增加 HTML 和 CSS 的代码量

- 使用 TODO 注释，说明代码功能

- 文档类型首选 HTML5 标准

- 根据 HTML 元素的语义使用相关元素

- 将行为和表现分开。严格遵循结构，表现和行为的分离，尽量保证三者交互保持最低，确保所有表现都放到样式表中，所有行为都放到脚本中，要尽量减少外链

- 引用属性值时，使用双引号

- 对 class 命名时要能保证光从名字就能看出是干什么用的，命名也要简短易懂

#### - CSS 规则

- 避免使用 CSS 类型选择器

```javascript
// bad
div.error {}
// good
.error {}
```

- 写属性值时尽量使用缩写

```javascript
// bad
padding-bootom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
...
// good
padding: 0 1em 2em;
```

- 除非必要，否则省略 0 后面的单位

```javascript
flex: 0px;
flex: 1 1 0px; /* IE11下会要求添加单位 */
```

- 省略 0 开头小数前面的 0

```javascript
// bad
font-size: 0.8em;
// good
font-size: .8em;
```

- 十六进制尽可能使用 3 个字符

```javascript
// bad
color: #eebbcc;
// good
color: #ebc;
```

- 用-连接命名，增进对名字的理解和查找

```javascript
// bad
.demoimage {}
.error_status {}
// good
.video-id {}
```

- 避免使用 css hacks

- 选择器在大括号前要添加一个空格

```javascript
// bad
.test{
    ...
}
// good
.test {
    ...
}
```

- 在每个声明尾部都加上分号

```javascript
// bad
.test {
    display: block;
    height: 100px
}
// good
.test {
    display: block;
    height: 100px;
}
```

- 在属性名冒号结束后添加一个空格

```javascript
// bad
h3 {
    font-size:16px;
}
// good
h3 {
    font-size: 16px;
}
```

- 当有多个选择器时，每个选择器都要独立新行

```javascript
// bad
h1, h2, h3 {

}
// good
h1,
h2,
h3 {

}
```

- 多个规则之间要隔行

```javascript
// bad
html {
    ...
}
body {
    ...
}
// good
html {
    ...
}

body {
    ...
}
```

- 按模块功能写注释
