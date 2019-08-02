>质数（prime number）又称素数，有无限个。
质数定义为在大于1的自然数中，除了1和它本身以外不再有其他因数。

### 质数的判断
最简单的方法就是遍历小于目标数字的数，挨个与目标数字相除，例子：
```js
function isPrime(num) {
  if (num === 1) {
    return '1 不是质数，请输入大于1的数字'
  }else if (num === 2) {
    return true
  }else {
    for (let i = 2; i < num; i++) {
     if (num%i === 0) {
       return false
     }
    }
    return true
  }
}
isPrime(11) // true
isPrime(22) // false
```
这样简单但是当判断数字很大或者数目很多时计算量大，这里可以利用到一个方法

>在一般领域，对正整数n，如果用2到$\sqrt{n}$之间的所有整数去除，均无法整除，则n为质数。
质数大于等于2 不能被它本身和1以外的数整除

那么可以将`num%i === 0`改为`Math.sqrt(num)%i === 0`，减少循环的次数。对于1和2的判断，可以合并一下：
```js
function isPrime(num) {
  if (num <= 3) {
    return num > 1
  }else {
    let sq = Math.sqrt(num)
    for (let i = 2; i <= sq; i++) {
     if (num%i === 0) {
       return false
     }
    }
    return true
  }
}
```

### 筛选数组中的质素
这是一道常见面试题，在上面我们知道了如何判断质数，那么筛选数组中的质数就很好写了
```js
const oldArr = [11,23,44,12,13,56,71,97]

const newArr = oldArr.filter(isPrime)

console.log(newArr) // [11, 23, 13, 71, 97]
```
或者根据需求使用forEach、map等方法。