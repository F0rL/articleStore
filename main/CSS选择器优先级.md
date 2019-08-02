优先级就是分配给指定的CSS声明的一个权重，它由 匹配的选择器中的 每一种选择器类型的 数值 决定。

而当优先级与多个CSS声明中任意一个声明的优先级相等的时候，CSS中最后的那个声明将会被应用到元素上。

当同一个元素有多个声明的时候，优先级才会有意义。因为每一个直接作用于元素的CSS规则总是会接管/覆盖（take over）该元素从祖先元素继承而来的规则。
## 优先级的计算
优先级的计算首先是**选择器权重**的优先级计算，然后是**声明先后顺序**的优先级计算。

### 选择器优先级的权重计算
选择器的权重并不是网上很多人说的

>选择器通过权重值 1(div等)、10(class)、100(id)

这样的方式进行的，这只是别人理解出来的东西，真正的计算原理可以翻阅[W3C文档选择器权重的计算](https://www.w3.org/TR/selectors/#specificity-rules)。

> count the number of ID selectors in the selector (= A)  
> count the number of class selectors, attributes selectors, and pseudo-classes in the selector (= B)  
> count the number of type selectors and pseudo-elements in the selector (= C)  
> ignore the universal selector

翻译过来：
先比较iD选择器的数量a，再比较类选择器、属性选择器和伪类的数量b，然后比较类型（标签）选择器和伪元素的数量c，最后忽略掉[通用选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Universal_selectors)

>通配选择符（universal selector）(*), 关系选择符（combinators） (+, >, ~, ' ')  和 否定伪类（negation pseudo-class）(:not()) 对优先级没有影响。（但是，在 :not() 内部声明的选择器是会影响优先级）。

### 声明先后顺序
当 A 、B 、C 所计算的权重都相等时（ABC三个值相等）相等时，后面声明的值将会是最终的计算值。

最终得到了CSS属性的值。

## CSS权重关系图
![](https://ws1.sinaimg.cn/large/90864b23gy1g1xg79txuyj20zf19u45b.jpg)