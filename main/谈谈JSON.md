JSON是想必都不陌生，特别是前端要进行数据交互的时候。但是很多人容易把它合JS对象弄混，这里简单讲述下JSON的一些基本知识。
### 概念
>JSON（JavaScript Object Notation，JavaScript对象表示法，读作“Jason”）是一种由道格拉斯·克罗克福特构想和设计、轻量级的数据交换语言，该语言以易于让人阅读的文字为基础，用来传输由属性值或者序列性的值组成的数据对象。尽管JSON是JavaScript的一个子集，但JSON是独立于语言的文本格式，并且采用了类似于C语言家族的一些习惯。
JSON 数据格式与语言无关，脱胎自JavaScript，但当前很多编程语言都支持 JSON 格式数据的生成和解析。JSON 的官方 MIME 类型是 application/json，文件扩展名是 .json。

它是一种数据交换格式语言，用于取代繁重的XML。虽然它是基于 JavaScript 语法，但它独立于JavaScript。**JSON可以作为一个对象或者字符串存在**，前者用于解读 JSON 中的数据，后者用于通过网络传输 JSON 数据。

### 使用
可以说JSON是基于JS的对象，但是JSON作为数据格式，比JS的对象要求更为严格。

JSON有两种结构：
#### 对象（object）
一个对象包含一系列非排序的名称／值对(pair)，一个对象以{开始，并以}结束。每个名称／值对之间使用:
分割。举例：
```JSON
{
    "city": "HangZhou",
    "year": 2019,
    "active": true,
    "members": [{
        "name": "kuma",
        "age": 29,
        "hobby": [
          "basketball",
          "book"
        ]},
    	{
    	"name": "Alex",
    	"age": 39,
    	"hooby": [
    	  "football"
    	]}
    ]
}
```
#### 数组 (array)
一个数组是一个值(value)的集合，一个数组以[开始，并以]结束。数组成员之间使用,分割。
```JSON
[
    {
        "name": "kuma",
        "age": 29,
        "hobby": [
          "basketball",
          "book"
        ]
    },
    {
    	"name": "Alex",
    	"age": 39,
    	"hooby": [
    	  "football"
    	]
    }
]
```
#### 与JS对象的区别
JSON式比JS对象在格式上要求更为严格。

1. 一个名称必须是一个字符串,且必须在双引号里面；
2. 复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
3. 简单类型的值**只有四种**：字符串、数值（必须以十进制表示）、布尔值和null。
4. 所有字符串必须使用双引号表示，不能使用单引号。
5. 数组或对象最后一个成员的后面，不能加逗号。

只有符合以上条件，才是符合要求的JSON数据。

### JSON方法
在web环境中浏览器拥有一个内建的 JSON，包含以下两个方法。

parse(): 以文本字符串形式接受JSON对象作为参数，并返回相应的对象。

stringify(): 接收一个对象作为参数，返回一个对应的JSON字符串。

这两个方法可以帮你在传输/接收数据时进行处理。
```js
const obj = {
	"city": "HangZhou",
	"year": 2019,
	"number": {
    "a": "1",
    "b": "2"
  }
}
const str = JSON.stringify(obj)

console.log(typeof str) // string

const obj1 = JSON.parse(str)

console.log(typeof obj1) //object
```

### 深拷贝
你可能发现了，obj1与obj一模一样，事实上，通过这两个方法可以对JS对象进行简单类型的深拷贝。
```js
const obj = {
	"year": 2019,
	"number": {
    "a": 1,
    "b": 2
  }
}
const newObj = JSON.parse(JSON.stringify(obj))

newObj.number.a = 11

console.log(obj.number.a) // 1
console.log(newObj.number.a) // 11
```
#### 对象直接赋值
在JS中，对象是以堆的方式存储在内存，如果直接赋值`const newObj = obj`，只是将newObj指向了obj的位置，如果更改obj内的属性，newObj也会更改。
```js
const obj = {
	"year": 2019,
	"number": {
    "a": 1,
    "b": 2
  }
}

newObj.number.year = 2022
console.log(obj.number.year) // 2022
console.log(newObj.number.year) // 2022
```
#### 对象浅拷贝
如果使用Object.assign()进行复制，基础类型会复制，但对象里面有引用类型（数组、对象）时，只会复制其指针，新旧对象还是会相互影响。
```js
const obj = {
	"year": 2019,
	"number": {
    "a": 1,
    "b": 2
  }
}
const newObj = Object.assign({}, obj)
newObj.year = 2022
newObj.number.a = 11

console.log(obj.year) // 2019
console.log(newObj.year) // 2022
console.log(obj.number.a) // 11
console.log(newObj.number.a) // 11
```

#### 局限
使用JSON方法，新对象newObj中的对象属性的改变并不会影响就对象obj。如果复制对象中有函数、正则等等，那么这个方法就不能用了，因为JSON不支持。



