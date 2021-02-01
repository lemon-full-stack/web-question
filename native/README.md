# 原生H5、CSS、JavaScript面试题

### 0x0001
Q：什么是JavaScript的强制类型换换？

A：在JS中，两种不同的内置类型间的转换被称为强制类型转换。 强转有两种形式：隐式转换和显式转换。

隐式转换：指的是由JavaScript解释器自动帮我们转换

显式转换：指的是需要我们手动写代码转换。

举一个隐式类型转换的例子：


### 0x0002
Q：JS是事件驱动机制吗？什么是事件驱动机制？



### 0x0003
Q：JavaScript 与 ECMAScript 是什么关系？

A：1996年8月，微软模仿 JavaScript 开发了一种相近的语言，取名为JScript（JavaScript 是 Netscape 的注册商标，微软不能用），首先内置于IE 3.0。Netscape 公司面临丧失浏览器脚本语言的主导权的局面。

1996年11月，Netscape 公司决定将 JavaScript 提交给国际标准化组织 ECMA（European Computer Manufacturers Association），希望 JavaScript 能够成为国际标准，以此抵抗微软。ECMA 的39号技术委员会（Technical Committee 39）负责制定和审核这个标准，成员由业内的大公司派出的工程师组成，目前共25个人。该委员会定期开会，所有的邮件讨论和会议记录，都是公开的。

1997年7月，ECMA 组织发布262号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为 ECMAScript。这个版本就是 ECMAScript 1.0 版。之所以不叫 JavaScript，一方面是由于商标的关系，Java 是 Sun 公司的商标，根据一份授权协议，只有 Netscape 公司可以合法地使用 JavaScript 这个名字，且 JavaScript 已经被 Netscape 公司注册为商标，另一方面也是想体现这门语言的制定者是 ECMA，不是 Netscape，这样有利于保证这门语言的开放性和中立性。因此，ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。

ECMAScript 只用来标准化 JavaScript 这种语言的基本语法结构，与部署环境相关的标准都由其他标准规定，比如 DOM 的标准就是由 W3C组织（World Wide Web Consortium）制定的。

我们经常说的ES5、ES6就是ECMAScript 5.0、ECMAScript 6.0这种脚本语言的标准的简称。

2015年6月，ECMAScript 6 正式发布，并且更名为“ECMAScript 2015”。这是因为 TC39 委员会计划，以后每年发布一个 ECMAScript 的版本，下一个版本在2016年发布，称为“ECMAScript 2016”，2017年发布“ECMAScript 2017”，以此类推。

### 0x0004

Q：这段代码最后会输出什么值？
```javascript
var a = 1;
var a;
console.log(a);
```

A：使用`var`重新声明一个已经存在的变量（但是没有新赋值），解析器会判定这行代码是无效的。 所以输出结果：
```javascript
1
```

Q：那么这段代码最后会又输出什么值？
```javascript
var a = 1;
var a = 2;
console.log(a);
```

A：使用`var`重新声明一个已经存在的变量且赋了新值，解析器则会覆盖原有的值。 所以输出结果：
```javascript
2
```


### 0x0005

Q：分别执行这两段代码，他们都分别会报错吗？

代码1
```javascript
console.log(a);
```

代码2

```javascript
console.log(a);
var a = 1;
```

A：代码1会报错，代码2不会报错。代码1会报出错误：
```shell
Uncaught ReferenceError: a is not defined
```

因为JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。
这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这叫做变量提升（hoisting）。
上面代码2首先使用console.log方法，在控制台显示变量a的值。 这时变量a还没有声明和赋值，所以这是一种错误的做法，
但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码，所以代码2才不会报错。
```javascript
var a;
console.log(a);
a = 1;
```
代码2最后控制台输出的是：
```javascript
undefined
```


### 0x0006

Q：以下 哪些变量命名是不合法的？
```html
arg0
π
1a
_tmp
23
$elem
***
变量名称
a+b
-d
```

A：简单的说，标识符命名规则如下：
1. 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（_）。
   
2. 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。

3. JavaScript 有一些保留字，不能用作标识符：
   
```html
arguments、break、case、catch、class、const、
continue、debugger、default、delete、do、else、
enum、eval、export、extends、false、finally、for、
function、if、implements、import、in、instanceof、
interface、let、new、null、package、private、
protected、public、return、static、super、switch、
this、throw、true、try、typeof、var、void、while、
with、yield。
```

注意：因为支持Unicode，所以变量名是可以使用中文的。
```html
arg0
π
1a // 不合法，第一个字符不能是数字
_tmp
23 // 不合法，第一个字符不能是数字
$elem
*** // 不合法，标识符不能包含星号
变量名称
a+b // 不合法，标识符不能包含加号
-d // 不合法，标识符不能包含减号或连词线
```

### 0x0007
Q：下面代码最终会输出什么结果：
```javascript
var x = 1;
x = 2; <!-- x = 3;
--> x = 4;
console.log(x);
```

A：由于 JavaScript 可以兼容 HTML 代码的注释，所以<!--和-->也被视为合法的单行注释。

即上面代码中`<!-- x = 3;`和`--> x = 4;`都不会背执行。所以，最后输出结果是：

```javascript
2
```

需要注意的是 -->只有在行首，才会被当成单行注释，否则会当作正常的运算 
```javascript
var x = 2;
if (x --> 0){
  console.log(x)
}
```
比如说上面的代码，x --> 0实际上会当作x-- > 0，即先把x本身减去了1，然后在做大于0的比较，所以最后输出：
```javascript
1
```

### 0x0008
Q：下面代码最终会输出什么结果？
```javascript
for (var a = 0; a < 10; a ++) {
    var x = a;
    let y = a;
}
console.log('a = ' + a);
console.log('x = ' + x);
console.log('y = ' + y);
```

A：JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

对于var命令来说，JavaScript 的区块不构成单独的作用域（scope），即全局都有效

ES6 新增了let命令，用来声明局部变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效，而且有暂时性死区的约束。

> ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

所以最后输出：
```javascript
a = 10
x = 9
y = undefined
```

### 0x0009 
Q：下面代码最终会输出什么结果？
```javascript
var m = 1;
var n = 2;

if (m !== 1)
if (n === 2) console.log('hello');
else console.log('world');
```

A：最终控制台什么都不会输出

因为`else`代码块总是与离自己最近的那个if语句配对，所以上面代码中的`else`跟着的是最近的那个if语句，相当于下面这样：
```javascript
if (m !== 1) {
  if (n === 2) {
    console.log('hello');
  } else {
    console.log('world');
  }
}
```

### 0x0010
Q：请问如下代码执行后控制台会输出什么结果？
```javascript
function two() {
    return 1 + 1
}

switch (two()){
  case '2':
    console.log('hello01')
    break
  case 3 - 1:
    console.log('hello02')
  default:
    console.log('hello03')
}
```

A：switch语句后面的表达式，与case语句后面的表示式比较运行结果时，采用的是严格相等运算符（===），
而不是相等运算符（==），这意味着比较时不会发生类型转换。而且case代码块之中没有break语句，
导致不会跳出switch结构，而会一直执行下去，所以最终的运行结果应该是：
```html
hello02
hello03
```

### 0x0011
Q：请问如下代码执行后控制台会输出哪些信息？
```javascript
hello:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue hello;
      console.log('i=' + i + ', j=' + j);
    }
  }
```

A：JavaScript语言允许语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，
continue语句可以与标签配合使用，用于直接跳转到指定标签的位置，所以当`i === 1 && j === 1`时直接跳转到了外层循环。

此时控制台显示内容是：
```html
i=0, j=0
i=0, j=1
i=0, j=2
i=1, j=0
i=2, j=0
i=2, j=1
i=2, j=2
```
