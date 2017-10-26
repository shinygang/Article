> 编程语言的词法结构是一套基础性规则，用来描述如何使用这门语言来编写程序。作为语法的基础，它规定了诸如变量名是什么样的、怎么写注释，以及程序语言之间如何分隔等规则。

### 1、 字符集
JavaScript程序是使用[Unicode](https://baike.baidu.com/item/Unicode/750500?fr=aladdin)(计算机科学领域里的一项业界标准)符集编写的。Unicode是ASCII和Latin-1的超集，并支持地球上几乎所有在用的语言。有关[Unicode与JavaScript详解](http://www.ruanyifeng.com/blog/2014/12/unicode.html)，可以看看大神的文章。
#### 1.1、 区分大小写
JavaScript是区分大小写的语言。也就是说，关键字、变量、函数名和所有的标识符(identifier)都必须采取一致的大小写形式。比如：关键字"while"必须写成"while"，而不能写成"While" 或者 "WHILE"。
同时需要注意的是，HTML并不区分大小写。例如，在HTML中设置事件处理程序时，onclick属性可以写成onClick，但在JavaScript中，必须使用全部小写的onclick。
#### 1.2、空格、换行符和格式控制符
JavaScript会忽略程序中标识之间的空格，同样也会忽略换行符。为了提高代码可读性和可维护性。团队成员应该采用整齐、一致的缩进来行程统一的编码风格。比如采用EsLint代码风格来约束。
#### 1.3、Unicode 转义序列
JavaScript定义了一种特殊的序列：使用6个ASCII字符来代表任意16位Unicode内码。这些Unicode转义序列均以`\u`为前缀，其后跟随4个十六进制数（使用数字以及a-f的字母表示）。例如：
```
"café" === "caf\u00e9"    // => true
```
#### 1.4、标准化
Unicode标准为所有字符定义了一个首选的编码格式，并给出了一个标准化的处理方式将文本转换为一种适合比较的标准格式，JavaScript会认为它正在解析的程序代码已经是这种标准格式，不会再对其标识符、字符串或正则表达式作标准化处理。

### 2、注释
JavaScript支持两种格式的注释。在行尾 "//"之后的文本都会被JavaScript当做注释忽略掉。此外， `/*`和 `*/`之间的文本也会被当做注释，这种注释可以跨行书写，但不能有嵌套的注释。详情看下面：
```
	1、 // 这是单行注释
	2、 /* 这是一段注释 */    // 这里是另外一个注释
		/*
		* 这是一段注释
		* 这里可以多行注释描述
		*/
```
### 3、直接量
所谓直接量(literal),就是程序中直接使用的数据值。下面列出的都是直接量：

```
12              // 数字
1.2             // 小数
"hello tg"      // 字符串文本
true            // 布尔值
/javascript/g   // 正则表达式
null            // 空
{a:21, b:33}    // 对象
[1,2,3,4]       // 数组
``` 
### 4、标识符和保留字
#### 4.1、标识符
标识符就是一个名字。在JS中，标识符用来对变量和函数进行命名，或者用做JS代码中某些循环语句中的跳转位置标记。JS标识符必须以字母，下划线(_)或美元符号($)开头。后续的字符可以是字母，数字，下划线或美元符(数字是不允许作为首字符出现的，以便JS可以轻易区分开标识符和数字)。下面列举合法的标识符：

```
shinygang
my_shinygang
v12
_shinygang
$shinygang
```
出于可移植性考虑，通常我们采用ASCII字母或数字来书写标识符。然而，JS允许标识符中出现Unicode字符全集中的字母和数字。由此，程序员也可以使用非英语语言或数字符号来书写标识符：

```
let café = true;
let π = 3.14;
```
#### 4.2、保留字
JS把一些标识符拿出来用作自己的关键字。因此，就不能再在程序中把这些关键字用作标识符了：

```
break       delete     function     return     typeof     case     do     if     switch     var     catch     else     in     this     void     continue     false     instanceof     throw     while     debugger     finally     new     true     with     default     for     null     try
```
ES5中保留了这些关键字：

```
class     const     enum     export     extends     import     super
```
此外，下面这些关键字在普通JS代码中是合法的，但是在严格模式下是保留字：

```
implements     let     private     public     yield     interface     package     protected      static
```
严格模式同样对下面的标识符的使用做了严格限制，它们并不完全是保留字，但不能用作变量名、函数名或参数。

```
arguments      eval
```
ES3将Java的所有关键字都列为自己的保留字，尽管这些保留字在ES5中放宽了限制，但应当避免使用这些关键字作为标识符：

```
abstract     double     goto     native     static     boolean     enum     implements     package      super     byte     export     import     private     synchronized     char     extends     int     protected     throws     class     final     interface     public     transient     const     float     long     short     volatile
```
JS预定义了很多全局变量和函数，应当避免把它们的名字用作变量名活函数名：

```
arguments     encodeURI     Infinity     Number     RegExp     Array     encodeURIComponent     isFinite     Object     String     Boolean     Error     isNaN     parseFloat     SyntaxError     Date     eval     JSON     parseInt     TypeError     decodeURI     EvalError     Math     RangeError      undefined     decodeURIComponent    Fcuntion     Nan     referenceError     URIError
```
### 5、可选的分号
和其他许多编程语言一样，JS使用分号(;)将语句分隔开。这对增强代码的可读性和整洁性是非常重要的：缺少分隔符，一条语句的结束就成了下一条语句的开始，反之亦然。在JS中，如果语句各自独占一行，通常可以省略语句之间的分号(程序末尾或右花括号‘}’之前的分号也可以省略)。许多JS开发者使用分号来明确标记语句的结束，即使在并不完全需要分号的时候也是如此。另一种风格就是，在任何可以省略分号的地方都将其省略，只有在不得不用的时候才使用分号。不管采用哪种编程风格，关于JS中可选分号的问题有几个细节需要注意。

```
a = 3; // 这里的分号可以省略
b = 4;

c = 5; d = 6;   // 第一个分号不能省略
```
需要注意的是，JS并不是在所有换行处都填补分号：只有在缺少了分号就无法正确解析代码的时候，JS才会填补分号。也就是说，如果当前语句和随后的非空格字符不能当成一个整体来解析的话，JS就在当前语句行结束处填补分号。看一下如下代码：

```
var a
a
=
3
console.log(a)
JS将其解析为：
var a; a = 3; console.log(a);


// 错误的写法：
var y = x + z
(a + b).toString()
上面的代码会解析为：var y = x = z(a + b).toString()

//正确的写法
var y = x + z;
(a + b).toString();
```
如果当前语句和下一行语句无法合并解析，JS则在第一行后填补分号，这是通用规则，但有两个例外：

==（1）、在return、break和continue和随后的表达式之间不能有换行。==
```
return 
true;

JS会解析成：  return; true;
然而代码本意是这样:  return true;

```


==（2）涉及“++”和“--”运算符的时候，应当和表达式在同一行==

```
x
++
y

JS会解析为：x; ++y;
然而我们想要的是：x++;y
```

