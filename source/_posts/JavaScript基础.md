---
title: JavaScript 基础
date: 
updated:
tags: javascript
categories: 前端
cover: https://s1.ax1x.com/2023/06/20/pC8UDRf.png
---



# JS 基础

JavaScript 包含很多内容，如类、期约、迭代器、代理、客户端检测、事件、动画、表单、错误处理以及JSON等。

## 1. JavaScript 概念

完整的 Javascript 包含3部分：

- 核心（ECMAScript）

- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

![image-20230605092717715](../FILES/JavaScript基础.md/image-20230605092717715.png)

script 标签属性：

- async 立即开始下载脚本【外部脚本】
- charset 字符集
- crossorigin CORS 跨域资源共享
- defer 脚本可以延迟到文档完全被解析和显示之后再执行（最好只包含一个这样的脚本）【外部脚本】
- src <b style="color: red">重要！！</b>
- type 脚本类型 type="text/javascript"

noscript 标签：满足以下两个条件，都会被浏览器渲染。否则不会渲染 noscript 标签里内容

- 不支持 JavaScript
- 禁用 JavaScript

```html
<!DOCTYPE html> 
<html> 
 <head> 
 <title>Example HTML Page</title> 
 <script defer="defer" src="example1.js"></script> 
 <script defer="defer" src="example2.js"></script> 
 </head> 
 <body> 
 <noscript> 
 <p>该页面不支持或者禁用JavaScript.</p> 
 </noscript> 
 </body> 
</html>
```

注意：对不推迟执行的脚本，浏览器必须解释完位于`<script>`元素中的代码，然后才能继续渲染页面

## 2. 语法基础

### 2.1 变量

标识符组成：（变量名建议：驼峰命名）

- 第一个字符必须是一个字母、下划线（_）或美元符号（$）
- 标识符由字母、下划线、$或数字组成

```javascript
// 有效名称 ： 合法名称
firstSecond 
myCar 
doSomethingImportant
```

开启严格模式：=="use strict"==。对于不安全的活动将抛出错误

```javascript
function doSomething() { 
 "use strict"; 
 // 函数体 
}
```

在 JavaScript 中建议 ==加分号（;）==，压缩代码不容易出现语法错误，在某些情况下可能会提升性能，因为解析器会尝试在合适的位置补上分号以纠正语法错误。

关键字如下：

| break    | do       | in         | typeof |
| -------- | -------- | ---------- | ------ |
| case     | else     | instanceof | var    |
| catch    | export   | new        | void   |
| class    | extends  | return     | while  |
| const    | finally  | super      | with   |
| continue | for      | switch     | yield  |
| debugger | function | this       | enum   |
| default  | if       | throw      | 等等   |
| delete   | import   | try        |        |

**var 声明提升**：都拉到函数作用域的顶部【let 声明的变量不会被提升，即必须先声明再使用，即“暂时性死区”】

```javascript
function foo() {
  console.log(age)
  // 变量声明在下面，不报错
  var age = 10
}
```

let 声明的范围是块作用域，而 var 声明的范围是函数作用域。

> ✨<span style="color: red">小技巧：</span>
> 建议使用 let 声明变量，如果变量确定不会发生变化，建议使用 const 声明变量。

全局声明时，let 声明变量不会成为 window 对象属性

```javascript
var name = "张三"
console.log(window.name); // "张三"
let age = 12
console.log(window.age); // undefined
```

{%note success %}

总结：const 优先，let 次之

{%endnote%}

### 2.2 数据类型（7种）

6中简单数据类型（原始类型）：

- Undefined（"undefined"）只有1个值 undefined
- Null（""）
- Boolean（"boolean"）
- Number（"number"）
- String（"string"）
- Symbol（符合）

还有复杂数据类型：Object（"object" 或 null）（键值对的集合）

确定变量类型： typeof 【操作符】，区分函数和其他对象

````javascript
let message = "some string"; 
console.log(typeof message); // "string" 
console.log(typeof(message)); // "string" 
console.log(typeof 95); // "number"
````

> ✨<span style="color: red">小技巧：</span>
> 声明变量时，建议初始化，避免不必要的错误

== 的使用：这个操作符会为了比较而转换它的操作数

```javascript
console.log(null == undefined); // true
```

一般来讲，不必显示声明为 undefined，要使用 void(0)

不同类型与布尔值之间转换规则：if 等流控制语句会自动执行其他类型值到布尔值的转换（经常用！！）

| 数据类型  |  转换为true的值  | 转换为false的值 |
| :-------: | :--------------: | :-------------: |
|  Boolean  |       true       |      false      |
|  String   |    非空字符串    | ""（空字符串）  |
|  Number   | 非零数值（无穷） |     0、NaN      |
|  Object   |     任意对象     |      null       |
| Undefined |  N/A（不存在）   |    undefined    |

Number最大：Number.MAX_VALUE

Number最小：Number.MIN_VALUE

超出范围：Infinity 无穷 【Number.NEGATIVE_INFINITY 和 Number.POSITIVE_INFINITY 也可以获取正、负 Infinity。】

确定一个值是不是无穷大：isFinite 函数

NaN （非数值）：console.log(0/0); // NaN 

判断是否为非数值：isNaN

> isNaN()可以用于测试对象。此时，首先会调用对象的 valueOf()方法，然后再确定返回的值是否可以转换为数值。如果不能，再调用 toString()方法，并测试其返回值

```javascript
console.log(isNaN(NaN)); // true 
console.log(isNaN(10)); // false，10 是数值
console.log(isNaN("10")); // false，可以转换为数值 10 
console.log(isNaN("blue")); // true，不可以转换为数值
console.log(isNaN(true)); // false，可以转换为数值 1
```

将非数值转换为数值：Number()、parseInt()和 parseFloat()

Number函数转换规则：

- 布尔值 true为1
- 数值，直接返回
- null 返回0
- undefined 返回NaN
- 字符串【isNaN 为 true】
- 对象，调用 valueOf 方法，如果结果为 NaN，调用 toString() 方法

```javascript
let num1 = Number("Hello world!"); // NaN 
let num2 = Number(""); // 0 
let num3 = Number("000011"); // 11 
let num4 = Number(true); // 1
```

字符串转数字有专门的函数处理：parseInt和parseFloat

String 类型

字符字面量：

| 字面量 | 含义               |
| ------ | ------------------ |
| \n     | 换行               |
| \t     | 制表               |
| \b     | 退格               |
| \r     | 回车               |
| \f     | 换页               |
| \\ \   | 反斜杠             |
| \\'    | 单引号             |
| \\"    | 双引号             |
| \\`    | 反引号             |
| \xnn   | \x41 等于 "A"      |
| \unnnn | \u03a3 等于字符"Σ" |

转换为字符串：toString()

模板字面量：由反引号括起来（`123`）,允许支持字符串插值（${}）

模板字面量会保持反引号内部的空格

模板字面量：标签函数

```javascript
function simpleTag(strings, aValExpression, bValExpression, sumExpression) {}
simpleTag`${ a } + ${ b } = ${ a + b }`;
```

获取原始字符：.raw

为什么要获取原始字符：不要转义后的 © ，要 `\u00A9`

示例代码：

```javascript
function printRaw(strings) { 
   console.log('Actual characters:'); 
   for (const string of strings) { 
   		console.log(string); 
   } 
   console.log('Escaped characters;'); 
   for (const rawString of strings.raw) { 
   		console.log(rawString); 
   } 
} 
printRaw`\u00A9${ 'and' }\n`; 
// Actual characters: 
// © 
//（换行符）
// Escaped characters: 
// \u00A9 
// \n
```

Symbol 类型【了解，该内容属于进阶知识，可跳过】

是确保对象属性使用唯一标识符，不会发生属性冲突的危险。

```javascript
let sym = Symbol(); 
console.log(typeof sym); // symbol
```

凡是可以使用字符串或数值作为属性的地方，都可以使用符号

**Symbol.asyncIterator**：由 for-await-of 使用，异步迭代器API

```javascript
class Emitter { 
   constructor(max) { 
     this.max = max; 
     this.asyncIdx = 0; 
   } 
   async *[Symbol.asyncIterator]() { 
     while(this.asyncIdx < this.max) {
       yield new Promise((resolve) => resolve(this.asyncIdx++)); 
     } 
   } 
} 
async function asyncCount() { 
   let emitter = new Emitter(5); 
   for await(const x of emitter) { 
    	console.log(x); 
   } 
} 
asyncCount();
```

**Symbol.hasInstance** 由 instanchof 使用。确定一个对象实例的原型链上是否有原型。

```javascript
function Foo() {} 
let f = new Foo(); 
console.log(f instanceof Foo); // true
```

重新定义原型：

```javascript
class Bar {} 
class Baz extends Bar { 
   static [Symbol.hasInstance]() { 
      return false; 
   } 
}
```

**Symbol.isConcatSpreadable** 了解即可

**Symbol.iterator** 使用 for-of 遍历

**Symbol.match** 正则表达式需要

**Symbol.replace** 替换字符。 String.prototype.replace()方法使用

**Symbol.search** 匹配正则表达式索引

**Symbol.species** 该函数作为创建派生对象的构造函数

**Symbol.split** 拆分字符串

**Symbol.toPrimitive** 将对象转换为相应的原始值

**Symbol.toStringTag** 默认字符串

**Symbol.unscopables** 了解，不深入探究

Object 类型

创建对象

```javascript
let o = new Object()
```

每个Object都有的方法：

- constructor
- hasOwnProperty(属性名)
- isPrototypeof(object)
- propertyIsEnumerable(*propertyName*)
- toLocaleString
- toString
- valueOf

Object 是所有对象的基类，所以任何对象都有这些属性和方法。

BOM 和 DOM 可能会出现例外情况

### 2.3 操作符

操作符通常会调用 valueOf()和/或 toString()方法来取得可以计算的值。

一元操作符：

- 递增/递减操作符 ++/--

- 一元加/减，如 s1 = +s1;

- 位操作符

  - 按位非 ~
  - 按位与 &
  - 按位或 |
  - 按位异或 ^
  - 左移 <<
  - 有符号右移 >>
  - 无符号右移 >>>

- 布尔操作符

  - 逻辑非 !【同时使用两个叹号（!!），相当于调用了转型函

    数 Boolean()】

    ```javascript
    console.log(!false); // true 
    console.log(!"blue"); // false 
    console.log(!0); // true 
    console.log(!NaN); // true 
    console.log(!""); // true 
    console.log(!12345); // false
    ```

  - 逻辑与 &&

  - 逻辑或 ||

- 乘性操作符

  - 乘法 *
  - 除法 /
  - 取模 %

- 指数操作符 ** Math.pow()

- 关系操作符（大于>，等等）

- 相等操作符

  - 等于（==）或不等于（!=）
  - 全等（===）或不全等（`!==`）

- 条件操作符 flag ? true : false

- 赋值操作符 =

- 逗号操作符

  ```javascript
  let num1 = 1,num2 = 0
  ```

### 2.4 语句

- if 语句

- do-while语句

- while 语句

- for 语句

- for-in 语句

- for-of 语句

- 标签语句 常用于内部循环跳出外部循环 break start;

  ```javascript
  start: for (let i = 0; i < count; i++) { 
   console.log(i); 
  }
  ```

- break 和 continue

- with 语句 【不建议使用，严格模式报错】

  ```javascript
  let qs = location.search.substring(1); 
  let hostName = location.hostname; 
  let url = location.href;
  // 使用 with 简化
  with(location) { 
   let qs = search.substring(1); 
   let hostName = hostname; 
   let url = href; 
  }
  ```

- switch 语句

### 2.5 函数（Function）

它属于引用类型

基本语法：

```javascript
function functionName(arg0, arg1,...,argN) { 
 statements 
}
```

## 3. 变量、作用域与内存

### 3.1 变量

变量可以包含两种不同类型的数据：原始值和引用值

原始值：简单数据类型。（typeof有效），保存在栈上

引用值：多个值构成的对象。（instanceof 判断类型），保存在堆上。（引用值对象实际是指向对象的指针）

### 3.2 作用域

作用域链：各级上下文中的代码在访问变量和函数时的顺序。（更多资料可百度）

上下文是函数，其活动对象用作变量对象加入作用域链中。

对于过滤链举个简单例子方便理解：

```javascript
let color = "blue"; 
function changeColor() { 
 if (color === "blue") { 
 	color = "red"; 
 } else { 
 	color = "blue"; 
 } 
} 
changeColor();
```

在该函数 changeColor 的作用域链中包含两个对象：

1. arguments 自身变量对象【具体可百度】
2. 全局上下文变量对象

作用域链增强： catch 语句 和 with 语句

作用域链中查找指定标识符，找到搜索结束，全局上下文仍然没有找到相应标识符，则其说明未定义。

![image-20230605123626540](../FILES/JavaScript基础.md/image-20230605123626540.png)

### 3.3 垃圾回收（进阶知识）

1. 标记清理【任何上下文都无法访问，将会打上标记】
2. 引用计数。声明变量时引用数为1，当被其他值覆盖，引用数减去1，当引用数为0，则可删除。（不建议，循环引用不适用）

3. 性能问题（合适的时机删除变量）
4. 内存管理，建议不用的变量，手动赋值 null，释放其引用

### 3.4 小结

1. 执行上下文分全局上下文、函数上下文和块级上下文。
2. 代码执行流每进入一个新上下文，都会创建一个作用域链，用于搜索变量和函数。
3. 全局上下文只能访问全局上下文中的变量和函数，不能直接访问局部上下文中的任何数据。
4. 离开作用域的值会被自动标记为可回收，然后在垃圾回收期间被删除。
5. 主流的垃圾回收算法是标记清理，即先给当前不使用的值加上标记，再回来回收它们的内存。

## 4. 基本引用类型

❤ 小提示：前面内容没有太多有用信息。

### 4.1 Date

#### 4.1.1 创建日期对象

1. 创建一个 Date 的实例对象

```javascript
let now = new Date(); // 2023-06-05T06:02:04.276Z
```

2. 通过 Date.parse 创建对象

```javascript
let someDate = new Date(Date.parse("6/5/2023")); // 2023-06-05T16:00:00.000Z
```

Date.parse 参数支持的格式：

- 月/日/年 如: 6/5/2023
- 月名 日, 年 如：June 5, 2023
- 周几 月名 日 年 时:分:秒 时区 如"Mon June 5 2032 00:00:00 GMT-0700"
- 【推荐】YYYY-MM-DDTHH:mm:ss.sssZ 如2019-05-23T00:00:00

3. 通过 Date.UTC 创建对象 （月份应该要减去1）

```javascript
// 参数内容从左到右: 年月日时分秒
let utcDate = new Date(Date.UTC(2023, 6, 5, 14, 14, 55));// 2023-07-05T14:14:55.000Z
```

4. 返回当前日期 Date.now()

```javascript
let start = Date.now(); 
doSomething();
let end = Date.now();
result = end - start; // 用时: 2014毫秒
```

#### 4.1.2 日期格式化

- toDateString 显示周几、年月日
- toTimeString 显示时区、时分秒
- toLocaleDateString 
- toLocaleTimeString
- toUTCString 显示完整的UTC日期

```javascript
let now = new Date()
console.log("toDateString", now.toDateString());
console.log("toTImeString", now.toTimeString());
console.log("toLocaleDateString", now.toLocaleDateString());
console.log("toLocaleTimeString", now.toLocaleTimeString());
console.log("toUTCString", now.toUTCString());

// 输出结果
toDateString Mon Jun 05 2023
toTImeString 14:32:00 GMT+0800 (中国标准时间)
toLocaleDateString 2023/6/5
toLocaleTimeString 14:32:00
toUTCString Mon, 05 Jun 2023 06:32:00 GMT
```

#### 4.1.3 Date 类型具体方法

getTime()  返回日期的毫秒表示；与 valueOf()相同

setTime(*milliseconds*) 设置日期的毫秒表示，从而修改整个日期

更多方法，访问 MDN

### 4.2 RegExp 正则

基本格式：

```js
let expression = /pattern/flags;
```

pattern 模式：包括字符类、限定符、分组、向前查找和反向引用

flags 标记：0 个或多个，一般有6种模式

- g 全局模式，查找字符串全部内容
- i 不区分大小写
- m 多行模式
- y 粘附模式，只查找从 lastIndex 开始以及之后字符串
- u Unicode 模式
- s dotAll 模式 表示元字符`.` 匹配任何字符（包括\n 和 \r）】

```js
let patter = /123/g
let result = patter.exec("a123bc")// [ '123', index: 1, input: 'a123bc', groups: undefined ]
let result = patter.exec("abc")// null
let result = patter.test("a123bc");// true
```

更多资料参考菜鸟教程，多使用正则。

### 4.3 原始值包含类型

基本使用：

```js
// 将字符串转成数字
let value = Number("123")
```

### 4.4 内置对象

不用显示实例化内置对象，开箱即用

1. Global 对象

   1. isNaN 函数

   2. isFinite 函数

   3. parseInt 函数

   4. parseFloat 函数

   5. encodeURI() 用于编码URI 【类似encodeURIComponent】

      ```js
      let url = encodeURI("https://www.baidu.com/s?wd=菜鸟")
      console.log(url); // https://www.baidu.com/s?wd=%E8%8F%9C%E9%B8%9F
      ```

   6. decodeURI()和 decodeURIComponent()

      ```js
      let d = decodeURI("https://www.baidu.com/s?wd=%E8%8F%9C%E9%B8%9F")
      console.log(d); // https://www.baidu.com/s?wd=菜鸟
      ```

   7. <span style="color: red"> **[强大]** </span> eval 函数，执行 JS 语句 [==容易被 XSS 利用，谨慎！！==]

      ```js
      const str = `
          let a = 1;
          let b = 2;
          console.log(a + b);
      `
      eval(str); // 3
      ```

   8. Global 对象属性，请翻阅MDN

   9. Window 属性

      所有全局作用域中声明的变量和函数都变成了 window 的属性

      当然： 仅限 var 声明变量 和 函数

   ```js
   var color = "red"; 
   function sayColor() { 
    console.log(window.color); 
   } 
   window.sayColor(); // "red"
   ```

2. Math 对象： 数学公式

   更多资料请翻阅 MDN

### 4.5 小结

当代码开始执行时，全局上下文中会存在两个内置对象：Global 和 Math。

## 5. 集合引用类型

内容：对象、数组、定型数组、Map、WeakMap、Set和WeekSet

### 5.1 Object

1. 对象创建：

① new 操作符

```js
let p = new Object() // 也可以 let p = {}
p.name = "张三"
```

② 对象字面量

```js
let person = { 
 name: "Nicholas", 
 age: 29 
};
```

2. 获取属性

```js
person["name"]
person.name
```

### 5.2 Array

1. 数组创建

```js
let colors = new Array(); // Array(20) Array("1","2")
// 字面量创建
let colors = ["red", "green"]
```

2. 数组拆分

```js
Array.from("Matt"); // [ 'M', 'a', 't', 't' ]
```

3. 将集合映射成新数组

```js
const m = new Map().set(1, 2) .set(3, 4); 
const s = new Set().add(1) .add(2) .add(3) .add(4); 
console.log(Array.from(m)); // [[1, 2], [3, 4]] 
console.log(Array.from(s)); // [1, 2, 3, 4]
```

4. 浅复制当前数组

```js
const a1 = [1, 2, 3, 4];
const a2 = Array.from(a1);
console.log(a1 === a2);// false
```

5. 可以使用任何可迭代对象

```js
const iter = { 
 *[Symbol.iterator]() { 
 yield 1; 
 yield 2; 
 yield 3; 
 yield 4; 
 } 
}; 
console.log(Array.from(iter)); // [1, 2, 3, 4]
```

6. arguments 转为数组

```js
function getArgsArray() { 
 return Array.from(arguments); 
}
```

7. 换带有必要属性的自定义对象

```js
const arrayLikeObject = { 
 0: 1, 
 1: 2, 
 2: 3, 
 3: 4, 
 length: 4 
}; 
console.log(Array.from(arrayLikeObject)); // [1, 2, 3, 4]
```

8. Array.of 函数

```js
Array.of(1,2,3,4); // [1,2,3,4]
```

9. 数组空位 let arr = [,,,]  { % label 不建议 orange%}
10. 数组索引从0开始，到 length - 1结束
11. 判断是否为数组 
    1. instanchof
    2. Array.isArray
12. 迭代器方法：keys() values() 和 entries()
13. 复制和填充方法  copyWithin 和 fill
14. 栈方法 push 和 pop
15. 队列方法 
    1. shift 方法： 删除第一项并返回它，数组长度减去1
    2. push
    3. unshift 方法：数组开头添加，数组长度加1，返回新的数组长度
    4. pop
16. 排序方法 reverse 和 sort，返回数组的引用
17. 操作方法
    1. concat 函数 拼接数组
    2. slice 函数 相当于切片
    3. splice 函数，实现删除、插入、替换【<span style="color: red">**常用**</span>】
18. 搜索 
    1. indexOf 、lastIndexOf 和 includes 【严格相等】
    2. find、findIndex 【断言函数】
19. 迭代方法
    1. every 每项函数必须返回 true
    2. filter 每项函数返回 true 组成新数组
    3. forEach 遍历每一项
    4. map 返回由每项函数调用的结果组成的数组
    5. some 如果有一项返回 true
20. 归并方法
    1. reduce 
    2. reduceRight

> 注意 如果数组中某一项是 null 或 undefined，则在 join()、toLocaleString()、
>
> toString()和 valueOf()返回的结果中会以空字符串表示。

### 5.3 定型数组

1. ArrayBuffer：可用于在内存中分配特定数量的字节空间【类似C++ 的 malloc】【定型数组及视图引用的基本单位】

```js
// 在内存中分配 16 字节
const buf = new ArrayBuffer(16);
console.log(buf.byteLength); // 16
```

slice 方法：复制全部或部分到新数组

注意：

- 分配内存失败，报错
- 分配内存不能超过 Number.MAX_SAFE_INTEGER
- 初始成功后，将所有二进制位初始化为0
- 可以被垃圾回收

> 要读取或写入 ArrayBuffer，就必须通过视图

2. DataView 允许读写 ArrayBuffer 的视图

