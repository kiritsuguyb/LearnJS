# Java Script 笔记
## 基本语法
1. 不需要使用；来结尾，但建议加上。
## 数据类型与变量
### 基本类型
1. 用`Number`类型替代`int`和`float`。
2. 存在`NaN`用于标识无法计算、`Infinity`标识无穷大。
3. 由于不存在`int`，也不会出现计算误差。
4. 使用`===`而非使用`==`。
5. 使用`isNaN()`来判断`NaN`。
### 数组
1. 数组如下直接初始化：
``` javascript
[1, 2, 3.14, 'Hello', null, true];
```
2. 未初始化的数组元素会被认为是`undefined`。
3. 可以通过索引存取，这一点与c#等语言并无不同。但是比较离谱的是**能够越界赋值**。但显然这是一个不太好的习惯，尽量保证**不要越界**。
4. 使用`indexOf()`查找元素位置。
5. 使用`slice()`对数组进行切片，对应`string`的`substring()`。第一个参数是起始位置，第二个参数是切片个数。没有参数的话返回副本，利用这点可以**用来复制数组**。
6. 使用`push`和`pop`，栈操作，前者返回栈高度，后者范围出栈元素。
7. `shift()`，队列操作，出队，反之使用`unshift()`则会在队头入队。
8. 调用`sort()`默认排序。
9. 调用`reverse()`翻转数组。
10. `splice()`可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：
``` javascript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```
11. `concat()`，A数组调用该函数并用B数组当作参数，返回数组AB。但这个函数**不改变原数组**，而是新建一个数组。
``` javascript
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```
12. `join()`，将数组元素用参数指定的字符串连接成新字符串后返回该字符串。
``` javascript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```
13. 允许使用多维数组。
14. 数组本身可以被理解为一个类型，每个数组是一个对象，存储着许多键值对，key就是索引，value就是数组元素。
### 对象
1. 对象是无序的键值对集合，感觉就比较离谱的样子，这样就似乎无法像C#一样进行类的嵌套。
大概是这样声明的：
```javascript
var myObject={//直接声明变量然后用块语句赋值
    name:"Jack",//直接使用变量名加冒号表示键值对，
    //逗号连接多个属性
    age:20,
    city:"Beijing"
}
```
C#的版本作为对比：
``` Csharp
public Class myObject{
    public string name="Jack";
    public int age=20;
    public string city="Beijing";
}
```
   
2. 对于非标准的属性名可以用`'keyname'`括起来声明并用`['keyname']`访问，但是不要给自己找麻烦，都用标准标识符就好了。
3. 淦，还可以访问不存在的属性，不会报错，只会返回`undefined`。
4. 但是没关系，不存在的属性赋值一下就变成存在的属性了，就尼玛离谱。
5. 可以使用`in`关键字来查看对象是否包含某属性，不区分是否是继承属性。
``` javascript
'keyname' in objectname
//return true of false，
//despite of whether the keyname belongs to its own
```
6. 使用`hasOwnProperty()`函数判断是否为自身属性。
7. JS中的类存储的是键值对，因而可以通过遍历key来访问值。
### 变量
1. 动态语言与静态语言不同，变量类型不需要显示声明。
2. 变量甚至可以不声明直接用。强类型语言写久了看到这个就觉得很夸张。
### 字符串
1. 用`''`或者`""`括起来都可以。
2. 可以用``来显示多行字符。但是感觉并不会用很多。
3. 除了使用`+`来连接字符串意外，还能够使用模板，注意这里使用的是**反引号`**:
``` javascript
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
``` 
4. 字符串字符数组常量，可以用下标来读取，超过索引范围返回`undefined`，不能更改，更改的话更改无效。
5. 有直接把字符串改为大小写的函数。
### 循环语句
1. **没有`foreach`**，只有`for ... in`，如下：
``` javascript
var myObject={
    name:"Jack",
    age:20,
    city:"Beijing"
}
for(var keyname in myObject){
    console.log(keyname);//输出'name' 'age' 'city'
}
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
}
//可以看出for in语句与C# foreach不同。
//后者取出的是值，前者取出的是键。
```
### Map和Set
1. `Map`类似C# dictionary。可以使用二维数组初始化：
```javascript
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95
```
2. `Set`与`Map`类似但不存储value。存储内容无法重复。
## Iterable
1. `for ... of`和`.foreach`循环。
2. `for ... of`即C#内foreach。
```javascript
   var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    console.log(x);
}
for (var x of s) { // 遍历Set
    console.log(x);
}
for (var x of m) { // 遍历Map
    console.log(x[0] + '=' + x[1]);
    //遍历Map时，将Map作为二维数组看待，索引0是key，索引1是value
}
```
3. 使用`.foreach`可以更加明确目的，这里使用匿名内部函数的方式作为回调函数。
```javascript
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
//Set 的参数只有element和它本身
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element+set);
});

var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    console.log(value);
});
//实际上Array和Map的调用方式并无太大差别
//第一个参数都是值、属性，第二个参数是键，索引
```
## 函数
### 函数定义与调用
1. 这里的函数更类似delegate变量。
```javascript
function abs(x){
    return x>=0?x:-x;
}
//or
var abs=function(x){
    return 
}
```
可以看到函数声明与变量声明具有同等地位。后者就好像一个委托变量指向了一个匿名函数。而实际上后者就是一个Lambda表达式。经过试验之后发现如下写法也是成立的：
```javascript
         /*👇这是一个Lambda表达式*/
var abs =(x)=> x>=0?x:-x;
```
2. 调用函数时可以传入**任意数量参数**，比较离谱，但**多余的参数不会影响调用**，参数少于预定函数则该参数为`undefined`。
3. 使用`arguments`关键字可以获得输入的所有参数。
```javascript
function foo(x) {
    console.log('x = ' + x); // 10
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10, 20, 30);
/*output:
x = 10
arg 0 = 10
arg 1 = 20
arg 2 = 30
*/
```
`arguments`常用于判断参数个数
```javascript
// foo(a[, b], c)
// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
function foo(a, b, c) {
    if (arguments.length === 2) {
        // 实际拿到的参数是a和b，c为undefined
        c = b; // 把b赋给c
        b = null; // b变为默认值
    }
    // ...
}
```
4. 可以利用`rest`关键字来获取意料之外的参数，而非像`argument`一样一次性获取所有参数。如果参数不够，则`rest`参数为`undefined`。
5. 不要把`return`语句分行写，因为javascript会在行末添加分号，导致歧义。
### 变量作用域与解构赋值
1. javascript具有变量提升特性，会自动提前声明所有变量，但这很奇怪，因此最好在编写代码时将变量都生命在语句块的开头。
```javascript
function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}
//等价于👇
function foo() {
    var y; // 提升变量y的申明，此时y为undefined
    var x = 'Hello, ' + y;
    console.log(x);
    y = 'Bob';
}
```
2. Javascript将所有不在函数内的变量绑定到全局变量`window`上，成为`window`的一个属性。`window`是Js唯一的全局变量。
3. 实际上函数也是`window`的一个属性，函数名就是属性名。这与`var functionObject=function(){}`的函数定义方式是自洽的。类似`alert()`函数也是`window`的一个全局变量，因此`alert()`可以被重定向到一个另一个函数上。
4. 直接在函数外定义的变量都会变为`window`的属性，因此不同js文件容易造成命名冲突。可以**在每个文件中定义一个次级的全局变量**，用这个变量来存储所有的其他变量和函数。
5. 定义块级临时变量用`let`，用`var`定义的是函数级变量。
```javascript
function foo() {
    for (var i=0; i<100; i++) {
        //
    }
    i += 100; // 仍然可以引用变量i
}
//如果使用let
function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```
6. 常量使用`const`修饰，具有块级作用域。
7. 