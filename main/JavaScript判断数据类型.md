JavaScript中有6种数据类型：数字（number）、字符串（string）、布尔值（boolean）、undefined、null、对象（Object）、Symbol（ES6新增）。其中对象类型包括：数组（Array）、函数（Function）、还有两个特殊的对象：正则（RegExp）和日期（Date）。

JavaScript有多种方法确定一个值到底是什么类型。

### typeof运算符
typeof可以正确的返回部分类型数据，但是null、Object、正则、日期,均返回object。
```js
typeof {a:1} === 'object';
typeof /\s/g === 'object';
typeof new Date() === 'object';
typeof null === 'object';
```
备注： 
typeof(null)返回object的原因是一个历史遗留bug。在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是 0。由于 null 代表的是空指针（大多数平台下值为 0x00），因此，null的类型标签也成为了 0，typeof null就错误的返回了"object"。（reference）
ECMAScript提出了一个修复（通过opt-in），但被拒绝。这将导致typeof null === 'null'。

### instanceof运算符
instanceof操作符判断左操作数对象的原型链上是否有右边这个构造函数的prototype属性，也就是说指定对象是否是某个构造函数的实例，最后返回布尔值。
```js
[] instanceof Array; //true
[] instanceof Object; //true
new Date() instanceof Date;//true
new Date() instanceof Object;//true
function Person(){};
new Person() instanceof Person;//true
new Person() instanceof Object;//true
```
虽然 instanceof 能够判断出 [] 是Array的实例，但它认为 [] 也是Object的实例。

### constructor属性
constructor属性的作用是，可以得知某个实例对象，到底是哪一个构造函数产生的。但是 constructor 属性易变，不可信赖，这个主要体现在自定义对象上，当开发者重写prototype后，原有的constructor会丢失。
```js
let bool = true,
    num = 1,
    str = 'abc',
    und = undefined,
    nul = null,
    arr = [1,2,3],
    obj = {},
    fun = function(){}
bool.constructor === Boolean;// true
num.constructor === Number;// true
str.constructor === String;// true
arr.constructor === Array;// true
obj.constructor === Object;// true
fun.constructor === Function;// true
```
undefined和null没有contructor属性

### Object.prototype.toString
toString是Object原型对象上的一个方法，该方法默认返回其调用者的具体类型，更严格的讲，是 toString运行时this指向的对象类型, 返回的类型格式为[object,xxx],xxx是具体的数据类型，其中包括：String,Number,Boolean,Undefined,Null,Function,Date,Array,RegExp,Error,HTMLDocument,... 基本上所有对象的类型都可以通过这个方法获取到。
```js
function typeIs(basic){
  let type = Object.prototype.toString.call(basic).slice(8,-1)
  return type.toLowerCase()
}

let obj = {},
    arr = [],
    rex = /\s/g,
    fun = function (){},
    time = new Date(),
    str = 'kuma',
    num = 12,
    bol = false,
    und = undefined,
    nul = null,
    sym = Symbol('a');

console.log(typeIs(obj) === 'object')
console.log(typeIs(arr) === 'array')
console.log(typeIs(rex) === 'regexp')
console.log(typeIs(fun) === 'function')
console.log(typeIs(time) === 'date')
console.log(typeIs(str) === 'string')
console.log(typeIs(num) === 'number')
console.log(typeIs(bol) === 'boolean')
console.log(typeIs(und) === 'undefined')
console.log(typeIs(nul) === 'null')
console.log(typeIs(sym) === 'symbol')
```
这个方法最为推荐，可以写一个函数，返回对应的数据类型。