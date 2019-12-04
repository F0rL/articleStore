各种奇怪的this指向代码向来是出现在各种笔试题，弄懂这些题目只需明白js中this的绑定规则。建议看《你不知道的js（上）》

* 题目一：
```
var number = 5;
var obj = {
    number: 3,
    fn1: (function () {
        var number;
        this.number *= 2;
        number = number * 2;
        number = 3;
        return function () {
            var num =this.number;
            this.number *= 2;
            console.log(num);
            number *= 3;
            console.log(number);
        }
    })()
}
var fn1 = obj.fn1;
fn1.call(null);
obj.fn1();
console.log(window.number);
```
这里有几个变量，第一行的是window.number初始值为5，obj里面的obj.number初始值为3。fn1里面声明的number，存在于闭包中，暂时记为bb.number。返回的函数里面声明的变量num，其余的就是this.number，需要根据情况判断是哪一个number。

`var fn1 = obj.fn1`这里定义了一个变量，值为obj.fn1，由于obj.fn1是立即执行函数,则fn1值为返回的函数。

`fn1.call(null)`，这里进行了显式绑定，call的第一个参数为this的指向，如果为null，那么指向window。
```
var number
this.number *=2  ==> window.number = 10
number = number * 2 ==> bb.number只声明，未赋值
number = 3 ==> bb.number = 3
var num =this.number ==> num = window.number = 10
this.number *= 2 ==> window.number = 20
console.log(num) ==> 输出 10
number *=3 ==> bb.number *=3 ==> bb.number =27
console.log(number) ==> 输出 9
```
`obj.fn1()`这是进行隐式绑定，this的指向为obj
```
var num =this.number ==> num = obj.number = 3
this.number *= 2 ==> obj.number = 6
console.log(num) ==> 输出 3
number *=3 ==> bb.number *=3 ==> bb.number = 27
console.log(number) ==> 输出 27
```
`console.log(window.number) 输出window.number 即为20`
那么最后的结果为 10 9 3 27 20