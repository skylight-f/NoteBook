S中 [] == ![]结果为true，而 {} == !{}却为false， 追根刨底

magic_xiang 2018-11-03 14:06:09  10271  收藏 15
展开
console.log( [] == ![] )  // true
console.log( {} == !{} )  // false
在比较字符串、数值和布尔值的相等性时，问题还比较简单。但在涉及到对象的比较时，问题就变得复杂了。最早的ECMAScript中的相等和不相等操作符会在执行比较之前，先将对象转换成相似的类型。后来，有人提出了这种转换到底是否合理的质疑。最后，ECMAScript的解决方案就是提供两组操作符：

相等和不相等——先转换再比较      （==）

全等和不全等——仅比较而不转换  （===）

ECMAScript中相等操作符由两个等于号（==）表示，如果两个操作数相等，则返回true，这种操作符都会先转换操作数（通常称为强制转型），然后再比较它们的相等性

在转换不同的数据类型时，对于相等和不相等操作符：在JS高程中一书中给出如下的基本转换规则

①、如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值——false转换为0，而true转换为1；

②、如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值

③、如果一个操作数是对象，另一个操作数不是，则调用对象的valueOf()方法，用得到的基本类型值按照前面的规则进行比较

这两个操作符在进行比较时则要遵循下列规则。

①、null 和undefined 是相等的

②、要比较相等性之前，不能将null 和 undefined 转换成其他任何值

③、如果有一个操作数是NaN，则相等操作符返回 false ，而不相等操作符返回 true。重要提示：即使两个操作数都是NaN，相等操作符也返回 false了；因为按照规则， NaN 不等于 NaN

④、如果两个操作数都是对象，则比较它们是不是同一个对象，如果两个操作数都指向同一个对象，则相等操作符返回 true；否则， 返回false



这里说一下题外话：[] 和 {} 都是属于引用类型，引用类型是存放在堆内存中的，而在栈内存中会有一个或者多个地址来指向这个堆内存相对应的数据。所以在使用 == 操作符的时候，对于引用类型的数据，比较的是地址，而不是真实的值。

现在来探讨 [] == ! [] 的结果为什么会是true
①、根据运算符优先级 ，！ 的优先级是大于 == 的，所以先会执行 ![]

！可将变量转换成boolean类型，null、undefined、NaN以及空字符串('')取反都为true，其余都为false。

所以 ! [] 运算后的结果就是 false

也就是 [] == ! [] 相当于 [] == false

②、根据上面提到的规则（如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值——false转换为0，而true转换为1），则需要把 false 转成 0

也就是 [] == ! [] 相当于 [] == false 相当于 [] == 0

③、根据上面提到的规则（如果一个操作数是对象，另一个操作数不是，则调用对象的valueOf()方法，用得到的基本类型值按照前面的规则进行比较，如果对象没有valueOf()方法，则调用 toString()）

而对于空数组，[].toString() ->  '' (返回的是空字符串)

也就是  [] == 0 相当于 '' == 0

④、根据上面提到的规则（如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值）

Number('') -> 返回的是 0

相当于 0 == 0 自然就返回 true了

总结一下：

[] == ! []   ->   [] == false  ->  [] == 0  ->   '' == 0   ->  0 == 0   ->  true

 

那么对于 {} == !{} 也是同理的

关键在于  {}.toString() ->  NaN(返回的是NaN)

根据上面的规则（如果有一个操作数是NaN，则相等操作符返回 false）

总结一下：

{} == ! {}   ->   {} == false  ->  {} == 0  ->   NaN == 0    ->  false