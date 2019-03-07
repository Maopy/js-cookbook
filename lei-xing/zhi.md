# 值

数组\(array\)、字符串\(string\)和数字\(number\)是一个程序最基本的组成部分，但在 JavaScript 中，它们可谓让人喜忧掺半。

## 数组

和其他强类型语言不同，在 JavaScript 中，数组可以容纳任何类型的值，可以是字符串、 数字、对象\(object\)，甚至是其他数组\(多维数组就是通过这种方式来实现的\):

```javascript
var a = [ 1, "2", [3] ];
a.length;       // 3
a[0] === 1;     // true
a[2][0] === 3;  // true
```

对数组声明后即可向其中加入值，不需要预先设定大小:

```javascript
var a = [ ];
a.length;   // 0
a[0] = 1;
a[1] = "2";
a[2] = [ 3 ];
a.length;   // 3
```

{% hint style="info" %}
使用 delete 运算符可以将单元从数组中删除，但是请注意，单元删除后，数组的 length 属性并不会发生变化。
{% endhint %}

在创建“稀疏”数组\(sparse array，即含有空白或空缺单元的数组\)时要特别注意:

```javascript
var a = [ ];
a[0] = 1;
// 此处没有设置a[1]单元 
a[2] = [ 3 ];
a[1];       // undefined
a.length;   // 3
```

上面的代码可以正常运行，但其中的“空白单元”\(empty slot\)可能会导致出人意料的结 果。a\[1\]的值为undefined，但这与将其显式赋值为undefined\(a\[1\] = undefined\)还是有所区别。

数组通过数字进行索引，但有趣的是它们也是对象，所以也可以包含字符串键值和属性 \(但这些并不计算在数组长度内\):

```javascript
var a = [ ];
a[0] = 1;
a["foobar"] = 2;
a.length; // 1
a["foobar"]; // 2
a.foobar; // 2
```

这里有个问题需要特别注意，如果字符串键值能够被强制类型转换为十进制数字的话，它就会被当作数字索引来处理。

```javascript
var a = [ ];
a["13"] = 42;
a.length; // 14
```

在数组中加入字符串键值 / 属性并不是一个好主意。建议使用对象来存放键值 / 属性值， 用数组来存放数字索引值。

### 类数组

有时需要将类数组\(一组通过数字索引的值\)转换为真正的数组，这一般通过数组工具函数\(如 indexOf\(..\)、concat\(..\)、forEach\(..\) 等\)来实现。

例如，一些 DOM 查询操作会返回 DOM 元素列表，它们并非真正意义上的数组，但十分类似。另一个例子是通过 arguments 对象\(类数组\)将函数的参数当作列表来访问\(从 ES6 开始已废止\)。

工具函数 slice\(..\) 经常被用于这类转换:

```javascript
function foo() {
  var arr = Array.prototype.slice.call( arguments );
  arr.push( "bam" );
  console.log( arr );
}
foo( "bar", "baz" ); // ["bar","baz","bam"]
```

如上所示，slice\(\) 返回参数列表\(上例中是一个类数组\)的一个数组复本。

用 ES6 中的内置工具函数 Array.from\(..\) 也能实现同样的功能:

```javascript
...
var arr = Array.from( arguments );
...
```

## 字符串

字符串经常被当成字符数组。字符串的内部实现究竟有没有使用数组并不好说，但 JavaScript 中的字符串和字符数组并不是一回事，最多只是看上去相似而已。

例如下面两个值:

```javascript
var a = "foo";
var b = ["f","o","o"];
```

字符串和数组的确很相似，它们都是类数组，都有 length 属性以及 indexOf\(..\)\(从 ES5 开始数组支持此方法\)和 concat\(..\) 方法:

```javascript
a.length; // 3
b.length; // 3
a.indexOf( "o" ); // 1
b.indexOf( "o" ); // 1
var c = a.concat( "bar" ); // "foobar"
var d = b.concat( ["b","a","r"] );  // ["f","o","o","b","a","r"]
a === c; // false
b === d; // false
a; // "foo"
b; // ["f","o","o"]
```

但这并不意味着它们都是“字符数组”，比如:

```javascript
a[1] = "O";
b[1] = "O";
a; // "foo"
b; // ["f","O","o"]
```

JavaScript 中字符串是不可变的，而数组是可变的。并且 a\[1\] 在 JavaScript 中并非总是合法语法，在老版本的 IE 中就不被允许\(现在可以了\)。正确的方法应该是 a.charAt\(1\)。

字符串不可变是指字符串的成员函数不会改变其原始值，而是创建并返回一个新的字符串。而数组的成员函数都是在其原始值上进行操作。

```javascript
c = a.toUpperCase();
a === c; // false
a; // "foo"
c; // "FOO"

b.push( "!" );
b; // ["f","O","o","!"]
```

许多数组函数用来处理字符串很方便。虽然字符串没有这些函数，但可以通过“借用”数组的非变更方法来处理字符串:

```javascript
a.join;         // undefined
 a.map;          // undefined
 var c = Array.prototype.join.call( a, "-" );
 var d = Array.prototype.map.call( a, function(v){
   return v.toUpperCase() + ".";
 } ).join( "" );
 c;              // "f-o-o"
 d;              // "F.O.O."
```

另一个不同点在于字符串反转\(JavaScript 面试常见问题\)。数组有一个字符串没有的可变更成员函数 reverse\(\):

```javascript
a.reverse; // undefined
b.reverse(); // ["!","o","O","f"]
b; // ["f","O","o","!"]
```



