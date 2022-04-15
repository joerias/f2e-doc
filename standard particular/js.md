### JS 部分

#### - 变量

- 总是使用 const 或 let 声明变量，避免全局变量污染

- 每个变量在声明时，都要使用 const 或 let

```javascript
// bad
const items = "rede",
  goSportsTeam = true,
  dragonball = "z";

export { items, goSportsTeam, dragonball };
// good
const items = "rede";
const goSportsTeam = true;
const dragonball = "z";

export { items, goSportsTeam, dragonball };
```

- 将所有的 const 和 let 的定义分组

```javascript
// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

- 在需要的地方再对变量进行分配

```javascript
// bad
// 这里的checkName中name会调用getName函数，但是name并不是总会返回，如果hasName为test时，并不会返回，所以，应该把对name的定义延后
const getName = function backName() {
  return "rede";
};

function checkName(hasName) {
  const name = getName();

  if (hasName === "test") {
    return false;
  }

  return name;
}
// good
const getName = function backName() {
  return "rede";
};

function checkName(hasName) {
  if (hasName === "test") {
    return false;
  }
  const name = getName();

  return name;
}
```

- 禁止使用连续赋值

```javascript
// bad
const a = (b = c = 1);
// good
const a = 1;
const b = a;
const c = a;
```

- 避免使用++或--运算符

```javascript
// bad
let num = 1;
num++;
--num;
// good
let num = 1;
num += 1;
num -= 1;
```

- 在=号前后要避免进行换行，如果变量名超过最长限制，要统一换行方式

```javascript
// bad
// 此时的换行是没有必要的
const foo = "superLongLongLongLongLongLongLongLongString";
// good
const foo = "superLongLongLongLongLongLongLongLongString";
// bad
const foo = superLongLongLongLongLongLongLongLongFunctionName();
// good
const foo = superLongLongLongLongLongLongLongLongFunctionName();
```

#### - 变量提升

#### - 引用

- 对变量的声明不要使用 var，如果是声明后不再重现分配的变量要使用 const，如果是重现分配的变量要使用 let。
  注意 let 和 const 的块级作用域

#### - 对象

- 使用对象直接量创建对象

```javascript
const item = new Object(); //bad
const item = {}; //good
```

- 如果一个对象的 key 值包含动态属性，要保证对象的所有属性都是在一个地方进行定义

```javascript
function getKey(k) {
  return `a key named ${k}`;
}
// bad
const obj = {
  id: 5,
  name: "San Francisco"
};
obj[getKey("enabled")] = true;
// good
const obj = {
  id: 5,
  name: "San Francisco",
  [getKey("enabled")]: true
};
// 从上面的代码我们可以看出，这个建议的是要我们把与对象相关的属性，都在一个地方定义，便于维护
```

- 在定义方法时，使用简写的方式进行定义

```javascript
// bad
const atom = {
  value: 1,
  addValue: function(value) {
    return atom.value + value;
  }
};
// good
const atom = {
  value: 1,
  addValue(value) {
    return atom.value + value;
  }
};
```

- 在定义对象属性时，如果 key 值和 value 值同名，要使用简写形式

```javascript
const lukeSkywalker = "Luke Skywalker";
// bad
const obj = {
  lukeSkywalker: lukeSkywalker
};
// good
const obj = {
  lukeSkywalker
};
```

- 在定义对象时，简写的属性和非简写的属性要按顺序写，不要混着写

```javascript
const anakinSkywalker = "Anakin Skywalker";
const lukeSkywalker = "Luke Skywalker";
// bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker
};
// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4
};
```

- 在定义对象时，key 值只有在无效识别时添加单引号

```javascript
// bad
const bad = {
  foo: 3,
  bar: 4,
  "data-blah": 5
};
// good
const good = {
  foo: 3,
  bar: 4,
  "data-blah": 5
};
```

- 不允许直接使用 Object.prototype 的相关方法，比如 hasOwnProperty, propertyIsEnumerable, 和 isPrototypeOf.因为在定义对象时，有可能会覆盖了这些方法

```javascript
const item = {
  name: "rede"
};
// bad
console.log(item.hasOwnProperty("name"));
// good
console.log(Object.prototype.hasOwnProperty.call(item, "name"));
// best
const has = Object.prototype.hasOwnProperty;
console.log(has.call(item, "name"));
```

- 使用对象展开符浅复制对象，不要使用 Object.assign

```javascript
// very bad
// 本意是复制一个对象，在从复制出的对象上删除某个值，但实际上原始对象的值也会被影响
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 });
delete copy.a;
// bad
// 可以达到预期目的，但在写法上可读性不好
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }
delete copy.a;
// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }
const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

#### - 数组

- 在定义数组时，使用数组直接量，不要使用 new Array 的形式

```javascript
// bad
const items = new Array();
// good
const items = [];
```

- 在向数组添加元素时，不要直接赋值，通过 push 添加(注意指的是添加，并不包括修改的情况)

```javascript
const items = [];
// bad
items[items.length] = "test";
// good
items.push("test");
```

- 复制数组时，使用展开操作符

```javascript
const items = [1, 2, 4, 8, 16];
// bad
const itemsCopy = [];
for (let i = 0; i < items.length; i += 1) {
  itemsCopy[i] = items[i];
}
// good
const itemsCopy = [...items];
```

- 在把类数组对象转为数组对象时，使用展开操作符来替代 Array.from

```javascript
const foo = document.querySelectorAll(".foo");
// good
const nodes = Array.from(foo);
// best
const nodes = [...foo];
```

- 使用 Array.from 代替展开操作符来处理针对数组的映射操作，可以避免操作创建中间数组

```javascript
const foo = [1, 2, 3];
// bad
const baz = [...foo].map(x => x + x);
// good
const baz = Array.from(foo, x => x + x);
```

#### - 解构

- 优先使用对象解构来访问对象属性

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
  return `${firstName} ${lastName}`;
}
// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}
// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

- 优先使用数组解构从数组索引创建变量

```javascript
const arr = [1, 2, 3, 4];
// bad
const first = arr[0];
const second = arr[1];
// good
const [first, second] = arr;
```

- 用对象解构去处理多个返回值

```javascript
const input = {
  left: "0px",
  right: "0px",
  top: "0px",
  bottom: "0px"
};
// bad
function processInput(input) {
  const left = input.left;
  const right = input.right;
  const top = input.top;
  const bottom = input.bottom;
  return [left, right, top, bottom];
}
const [left, __, top] = processInput(input);
// good
function processInput({ left, right, top, bottom }) {
  return {
    left,
    right,
    top,
    bottom
  };
}
const { left, top } = processInput(input);
```

#### - 字符串

- 字符串使用单引号

```javascript
// bad
const name = "Capt. Janeway";
// bad
const name = `Capt. Janeway`;
// good
const name = "Capt. Janeway";
```

- 当字符串过长时，不要使用字符串连接符写成多行

```javascript
// bad
// 此时报的检查错误是no-multi-str，保证字符串不分两行书写
const errorMessage =
  "This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.";
// bad
// 此时运行代码检查并不会报错，针对这种写法应该是建议不要这么写
const errorMessage =
  "This is a super long error that was thrown because " +
  "of Batman. When you stop to think about how Batman had anything to do " +
  "with this, you would get nowhere fast.";
// good
// 要是感觉代码过长不方便看时，可以在编译器上做相关设置，设置自动换行
const errorMessage =
  "This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.";
```

- 当字符串和变量要进行连接时，要使用模版字面量

```javascript
// bad
function sayHi(name) {
  return "How are you, " + name + "?";
}
// bad
// 检查的错误template-curly-spacing，禁止模版字符串前后使用空格
function sayHi(name) {
  return `How are you, ${name}?`;
}
// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

- 针对字符串不要使用 eval

- 在字符串中只在有意义的地方使用转义字符

```javascript
// bad
const foo = "'this' is \"quoted\"";
// good
const foo = "'this' is \"quoted\"";
```

#### - 函数

- 在定义函数时，使用指定名词的函数表达式，而不是匿名表达式

```javascript
// bad
function add(a, b) {
  return a + b;
}
// bad
const add = function(a, b) {
  return a + b;
};
// good
const add = function myAdd(a, b) {
  return a + b;
};
```

- 立即执行函数要用大括号包裹起来

```javascript
// bad
const x = (function() {
  return { y: 1 };
})();
// not bad
// 随着现在模块的普及立即执行函数使用的应该不多了
const x = (function() {
  return { y: 1 };
})();
```

- 禁止循环中出现函数，如果需要在循环中定义函数，最好把相关函数使用变量定义好再使用，避免形成闭包

- 禁止在代码块中使用函数声明，不过可以使用函数表达式

```javascript
// bad
const currentUser = true;
if (currentUser) {
  function test() {
    console.log("Nope.");
  }
}
// good
const currentUser = true;
let test;
if (currentUser) {
  test = () => {
    console.log("Nope.");
  };
}
```

- 函数接收的形参不可以使用 argumenst

```javascript
// bad
function foo(name, options, arguments) {
  // ...
}
```

- 使用默认参数语法，不要去使用存在变化的函数参数

```javascript
// bad
// 这个会报no-param-reassign，禁止对 function 的参数进行重新赋值
function handleThings(opts) {
    opts = opts || {};
    ...
}
// bad
// 报的错误同上
function handleThings(opts) {
    if (opts === 0) {
        opts = {};
    }
}
// good
function handleThings(opts = {}) {
    // ...
}
```

- 避免对函数默认参数进行不可预期的操作

```javascript
// bad
// 检查时会报no-plusplus，禁用++
// 这个例子应该是要说明，不对默认参数设置不确定的因素，就比如这里的b值，两次调用返回值都不同，会令人费解
let b = 1;
function count(a = b++) {
  console.log(a);
}
count(); // 1
count(); // 2
```

- 始终将默认参数，放到最后

```javascript
// bad
function handleThings(opts = {}, name) {
  return { opts, name };
}
// good
function handleThings(name, opts = {}) {
  return { opts, name };
}
```

- 禁用 Function 构造函数创建函数

```javascript
// bad
const x = new Function("a", "b", "return a + b");
// good
const x = function backAdd(a, b) {
  return a + b;
};
```

- 强制在函数圆括号前和代码块之前使用统一的空格

```javascript
// bad
const f = function() {};
const g = function() {};
const h = function() {};
// good
const f = function() {};
const g = function() {};
const h = function() {};
```

- 禁止对函数参数再赋值

- 在函数括号内使用一致的换行，如果是多行会要求最后一项带逗号

```javascript
// normal
// 不使用换行
function foo(bar, baz, quux) {
  // ...
}
// bad
// 会报function-paren-newline要求使用一致的换行
function foo(bar, baz, quux) {
  // ...
}
// good
// 最后一行添加了逗号
function foo(bar, baz, quux) {
  // ...
}
```

#### - 箭头函数

- 当必须使用匿名函数时(比如回调函数)，可以使用箭头函数

```javascript
// bad
[1, 2, 3].map(function(x) {
  const y = x + 1;
  return x * y;
});
// good
[1, 2, 3].map(x => {
  const y = x + 1;
  return x * y;
});
```

- 如果回调函数只是简单的单行语句，可以省略 return

```javascript
// good
[1, 2, 3].map(x => {
  const y = x + 1;
  return x * y;
});
// good，提高可读性
[1, 2, 3].map(x => (x + 1) * x);
```

- 如果表达式垮多行，将其包裹在括号中，可以提高代码的可读性

```javascript
// not good
["get", "post", "put"].map(httpMethod =>
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod
  )
);
// good
["get", "post", "put"].map(httpMethod =>
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod
  )
);
```

- 箭头函数体只有一个参数时且不使用大括号，可以省略圆括号。其它任何情况，参数都应被圆括号括起来

```javascript
// bad
// arrow-parens
[1, 2, 3].map(x => x * x);
// good
[1, 2, 3].map(x => x * x);
// bad
// 因为此时使用了大括号，箭头函数后面跟随了代码块
[1, 2, 3].map(x => {
  const y = x + 1;
  return x * y;
});
```

- 禁止在可能与比较操作符相混淆的地方使用箭头函数

```javascript
// bad
// 此时的箭头符号和比较符号看起来很像
const itemHeight = item =>
  item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = item =>
  item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = item => {
  const { height, largeSize, smallSize } = item;
  return height > 256 ? largeSize : smallSize;
};
```

#### - 模块

- 使用模块 import／export 输入输出代码块

- 使用 import 时，不要使用通配符，最好明确要导入的代码块

```javascript
// 另外一个模块文件，比如是index.js
export const firstName = "rede";
export const lastName = "li";
// 引用该模块

// bad
// 按webpack 4+以上的版本会静态分析index.js只导入需要的代码块，所以明确导入的代码块会更有利于减少打包体积
import * as index from "./index";
console.log(index.firstName);
// best
// 原例子上还提到了一个good的写法，不过看了下，感觉这种写法最好，结合编译器，还能减小文件代码
import { firstName } from "./index";
console.log(firstName);
```

- 不要从 import 中直接导出(export)

```javascript
// bad
export { firstName as default } from "./index";
// good
// 这样更加明晰
import { firstName } from "./index";

export default firstName;
```

- 同一个路径的导入只在一个地方导入，禁止重复导入

```javascript
// bad
import { firstName } from "./index";
import { lastName } from "./index";

export default { firstName, lastName };
// good
import { firstName, lastName } from "./index";

export default { firstName, lastName };
```

- 不要 export 可变绑定

```javascript
// bad
let foo = 3;
export { foo };
// good
const foo = 3;
export { foo };
```

- 如果一个文件只导出一个模块，默认 export 优于命名 export

```javascript
// bad
const foo = 3;
export { foo };
// good
const foo = 3;
export default { foo };
```

- 将所有 import 导入放在非导入语句上面

```javascript
// bad
import { firstName, lastName, backName } from "./index";
backName();
import { name } from "./test";

export default { firstName, lastName, name };
// good
import { firstName, lastName, backName } from "./index";
import { name } from "./test";

backName();

export default { firstName, lastName, name };
```

- 多行导入应该像多行数组那样进行缩进

```javascript
// bad
import { firstName, lastName, year } from "./main";

export { firstName, lastName, year };
// good
import { firstName, lastName, year } from "./main";

export { firstName, lastName, year };
```

- 禁止在模块的 import 中使用 Webpack 加载语法

```javascript
// bad
import fooSass from "css!sass!foo.scss";
// good
import fooSass from "foo.scss";
```

#### - 属性

- 使用点语法来访问对象属性

```javascript
// bad
const luke = {
  jedi: true,
  age: 28
};
const isJedi = luke["jedi"];

export default { isJedi };
// good
const luke = {
  jedi: true,
  age: 28
};
const isJedi = luke.jedi;

export default { isJedi };
```

- 当通过变量访问属性时要使用中括号

```javascript
const luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

const isJedi = getProp("jedi");

export default { isJedi };
```
