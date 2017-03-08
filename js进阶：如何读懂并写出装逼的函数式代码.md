#### 先看如下的代码：
```
function find(x, y) {
    for(let i = 0; i < x.length; i++) {
        if(x[i] == y) {
            return i;
        }
    }              
    return null;
}

let arr = [0,1,2,3,4,5];
console.log(find(arr, 2));
console.log(find(arr, 8));
```
#### 下面是函数式的写法
```
const find = ( f => f(f) ) ( f =>
  (next => (x, y, i = 0) =>
    ( i >= x.length) ?  null :
      ( x[i] == y ) ? i :
        next(x, y, i+1))((...args) =>
          (f(f))(...args)))
 
let arr = [0,1,2,3,4,5]
console.log(find(arr, 2))
console.log(find(arr, 8))
```

#### 为了说明相关内容，先补充一个知识点：箭头函数
ECMAScript2015 引入的箭头表达式。箭头函数其实都是匿名函数，其基本语法如下：
```
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
     // 等于 :  => { return expression; }
 
// 只有一个参数时,括号才可以不加:
(singleParam) => { statements }
singleParam => { statements }
 
//如果没有参数,就一定要加括号:
() => { statements }
```
#### 以下是一些示例
```
var simple = a => a > 15 ? 15 : a;
simple(16); // 15
simple(10); // 10
 
let max = (a, b) => a > b ? a : b;
 
// Easy array filtering, mapping, ...
 
var arr = [5, 6, 13, 0, 1, 18, 23];
var sum = arr.reduce((a, b) => a + b);  // 66
var even = arr.filter(v => v % 2 == 0); // [6, 0, 18]
var double = arr.map(v => v * 2);       // [10, 12, 26, 0, 2, 36, 46]
```
上面前两个 simple 和 max 的例子都把箭头函数赋值给了一个变量，于是它就有了一个名字。有时候，某些函数在声明的时候就是调用的时候，尤其是函数式编程中，一个函数还对外返回函数的时候。比如下在这个例子：

```
function MakePowerFn(power) {
  return function PowerFn(base) {
    return Math.pow(base, power);
  }
}
 
power3 = MakePowerFn(3); //制造一个X的3次方的函数
power2 = MakePowerFn(2); //制造一个X的2次方的函数
 
console.log(power3(10)); //10的3次方 = 1000
console.log(power2(10)); //10的2次方 = 100
```
以上的MakePowerFn函数返回了PowerFn函数，其实PowerFn函数不需要命名，因此可以写成：

```
function MakePowerFn(power) {
  return function(base) {
    return Math.pow(base, power);
  }
}

```

如果用箭头函数，可以写成：
```
MakePowerFn = power  => {
  return base => {
    return Math.pow(base, power);
  }
}
```
如果用表达式的话可以写得更加简洁，不需要{}和return语句：
```
MakePowerFn = power => base => Math.pow(base, power)
```
加上括号和换行可能会更加清楚：
```
MakePowerFn = (power) => (
  (base) => (Math.pow(base, power))
)
```
以上是对箭头函数的简单描述，一下可以进入更高级的话题：匿名函数的递归

#### 匿名函数的递归

函数式编程立志于用函数表达式消除有状态的函数，以及for/while循环，所以，在函数式编程的世界里是不应该用for/while循环的，而要改用递归（递归的性能很差，所以，一般是用尾递归来做优化，也就是把函数的计算的状态当成参数一层一层的往下传递，这样语言的编译器或解释器就不需要用函数栈来帮你保存函数的内部变量的状态了）。

以下是递归的代码，求阶乘：
```
function fact(n){
  return n==0 ? 1 :  n * fact(n-1);
};
result = fact(5);
```
对于匿名函数来说，可以把匿名函数当成一个参数传给另外一个函数，因为函数的参数有名字，所以就可以调用自己。 如下所示：
```
function combinator(func) {
  func(func);
}
```
把上面这个函数整成箭头函数式的匿名函数的样子:
```
（func) => (func(func))
```
把上面的求阶乘函数套入：
```
function fact(func, n) {
  return n==0 ? 1 :  n * func(func, n-1);
}
 
fact(fact, 5); //输出120
```
然后再变成箭头函数的匿名函数形式：
```
var fact = (func, n) => ( n==0 ? 1 :  n * func(func, n-1) )
fact(fact, 5)
```
接下来把
```
(func, n) => ( n==0 ? 1 :  n * func(func, n-1) )
```
作为参数传给下面的函数：
```
(func, x) => func(func, x)
```
最终得到以下代码：
```
( (func, x) => func(func, x) ) (  //函数体
  (func, n) => ( n==0 ? 1 :  n * func(func, n-1) ), //第一个调用参数
  5 //第二调用参数
);
```
#### 使用高阶函数的递归
```
HighOrderFact = function(func){
  return function(n){
    return n==0 ? 1 : n * func(func)(n-1);
  };
};
```
调用时：
```
fact = HighOrderFact(HighOrderFact);
fact(5);

连起来写就是：

HighOrderFact ( HighOrderFact ) ( 5 )
```
最后以一个函数把HighOrderFact ( HighOrderFact ) 代理一下：
```
fact = function ( hifunc ) {
  return hifunc ( hifunc );
} (
  //调用参数是一个函数
  function (func) {
    return function(n){
      return n==0 ? 1 : n * func(func)(n-1);
    };
  }
);
 
fact(5); //于是我们就可以直接使用了
```
用箭头函数重构即最终版的阶乘函数式代码：
```
fact = (highfunc => highfunc ( highfunc ) ) (
  func => n =>  n==0 ? 1 : n * func(func)(n-1)
);
```
#### 回顾之前的函数
查找数组的程序：
```
//正常的版本
function find (x, y) {
  for (let i = 0; i < x.length; i++ ) {
    if ( x[i] == y ) return i;
  }
  return null;
}
```
先把for消除掉，写成递归版本：
```
function find (x, y, i=0) {
  if ( i >= x.length ) return null;
  if ( x[i] == y ) return i;
  return find(x, y, i+1);
}
```
然后，写出带实参的匿名函数的版本（注：其中的if代码被重构成了 ？号表达式）：
```
((func, x, y, i) => func(func, x, y, i) ) (  //函数体
  (func, x, y, i=0) => (
      i >= x.length ?  null :
         x[i] == y  ?  i : func (func, x, y, i+1)
  ), //第一个调用参数
  arr, //第二调用参数
  2 //第三调用参数
)
```
最后，引入高阶函数，去除实参：
```
const find = ( highfunc => highfunc( highfunc ) ) (
   func => (x, y, i = 0) => (
     i >= x.length ?  null :
           x[i] == y  ?  i : func (func) (x, y, i+1)
   )
);
```
注：函数式编程装逼时一定要用const字符，这表示我写的函数里的状态是 immutable 的.










