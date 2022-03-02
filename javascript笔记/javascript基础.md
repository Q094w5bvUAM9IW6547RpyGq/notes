## 字符串中的转义序列

引号不是字符串中唯一可以被转义的字符。使用转义字符有两个原因：首先是可以让你使用无法输入的字符，例如退格。其次是可以让你在一个字符串中表示多个引号，而不会出错。我们在之前的挑战中学到了这个。

| 代码 | 输出   |
| :--- | :----- |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\\` | 反斜杠 |
| `\n` | 换行符 |
| `\r` | 回车符 |
| `\t` | 制表符 |
| `\b` | 退格   |
| `\f` | 换页符 |

*请注意，必须对反斜杠本身进行转义才能显示为反斜杠。*



------



使用转义字符将下面三行文本字符串赋给变量`myStr`。

> FirstLine
>   \SecondLine
> ThirdLine

你需要使用转义字符正确的插入特殊字符，确保间距与上面文本一致并且单词或转义字符之间没有空格。

像这样用转义字符写出来：

"FirstLine 换行符 制表符 反斜杠 SecondLine 换行符 ThirdLine"

## 用加号运算符连接字符串

在 JavaScript 中，当对一个`String`类型的值使用`+`操作符的时候，它被称作 concatenation 操作符。你可以通过和其他字符串concatenation来创建一个新的字符串。

**示例**

> 'My name is Alan,' + ' I concatenate.'

**提示**
注意空格。拼接操作不会在两个字符串之间添加空格，所以想加上空格的话，你需要自己在字符串里面添加。

## 用 += 运算符连接字符串

我们还可以使用`+=`运算符来concatenate（拼接）字符串到现有字符串的结尾。对于那些被分割成几段的长的字符串来说，这一操作是非常有用的。

**提示**
注意空格。连接操作不会添加两个字符串外面的空格，所以如果想要加上空格的话，你需要自己在字符串里面添加。



------



通过使用`+=`操作符来连接这两个字符串：
`"This is the first sentence. "`和`"This is the second sentence."`并赋给变量`myStr`。

```js
var ourStr = "I come first. ";
ourStr += "I come second.";
```

## 用变量构造字符串

有时候你需要创建一个类似[Mad Libs](https://en.wikipedia.org/wiki/Mad_Libs)(填词游戏）风格的字符串。通过使用连接运算符`+ `，你可以插入一个或多个变量来组成一个字符串。



------



把你的名字赋值给变量`myName`，然后把变量`myName`插入到字符串`"My name is "`和`" and I am well!"`之间，并把连接后的结果赋值给变量`myStr`

```js
// 示例
var ourName = "freeCodeCamp";
var ourStr = "Hello, our name is " + ourName + ", how are you?";

// 请把你的代码写在这条注释以下
var myName="fanfei";
var myStr="My name is"+myName+" and I am well!";

```

## 将变量附加到字符串

我们不仅可以创建出多行的字符串，还可以使用加等号(`+=`)运算符来追加变量到字符串上。



------



设置变量`someAdjective`的值，并使用`+=`运算符把它追加到变量`myStr`上。

```js
// 示例
var anAdjective = "awesome!";
var ourStr = "freeCodeCamp is ";
ourStr += anAdjective;

// 请把你的代码写在这条注释以下

var someAdjective="really cool!";
var myStr = "Learning to code is ";
myStr+=someAdjective;
```

## 查找字符串的长度

你可以通过在字符串变量或字符串后面写上`.length`来获得字符串变量`字符串`值的长度。

```js
"Alan Peter".length; // 10
```

例如，我们创建了一个变量`var firstName = "Charles"`，我们就可以通过使用`firstName.length`来获得`"Charles"`字符串的长度。



------



使用`.length`属性来获得变量`lastName`的长度，并把它赋值给变量`lastNameLength`。

```js
// 示例
var firstNameLength = 0;
var firstName = "Ada";

firstNameLength = firstName.length;

// 初始化
var lastNameLength = 0;
var lastName = "Lovelace";

// 请把你的代码写在这条注释以下

lastNameLength = lastName.length;
```

## 使用方括号查找字符串中的第一个字符

方括号表示法是一种在字符串中的特定`index`（索引）处获取字符的方法。

大多数现代编程语言，如JavaScript，不同于人类从 1 开始计数。它们是从 0 开始计数，这被称为 基于零 的索引。

例如, 在单词 "Charles" 中索引 0 上的字符为 "C"，所以在`var firstName = "Charles"`中，你可以使用`firstName[0]`来获得第一个位置上的字符。



------



使用方括号获取变量`lastName`中的第一个字符，并赋给变量`firstLetterOfLastName`。

**提示**
如果你遇到困难了，不妨看看变量`firstLetterOfFirstName`是如何赋值的。

```js
// 示例
var firstLetterOfFirstName = "";
var firstName = "Ada";

firstLetterOfFirstName = firstName[0];

// 初始化
var firstLetterOfLastName = "";
var lastName = "Lovelace";

// 请把你的代码写在这条注释以下
firstLetterOfLastName = lastName[0];

```

## 了解字符串的不变性

在 JavaScript 中，`字符串`的值是 不可变的，这意味着一旦字符串被创建就不能被改变。

例如，下面的代码：

> var myStr = "Bob";
> myStr[0] = "J";

是不会把变量`myStr`的值改变成 "Job" 的，因为变量`myStr`是不可变的。注意，这*并不*意味着`myStr`永远不能被改变，只是字符串字面量 string literal 的各个字符不能被改变。改变`myStr`中的唯一方法是重新给它赋一个值，例如：

> var myStr = "Bob";
> myStr = "Job";



------



把`myStr`的值改为`Hello World`。

```js
// 初始化变量
var myStr = "Jello World";

// 请把你的代码写在这条注释以下

myStr = "Hello World"; // Fix Me
```

## 使用方括号查找字符串中的第N个字符

你也可以使用方括号来获得一个字符串中的其他位置的字符。

请记住，程序是从`0`开始计数，所以获取第一个字符实际上是[0]。



------



让我们使用方括号，把`lastName`变量的第三个字符赋值给`thirdLetterOfLastName`。

```js
// 示例
var firstName = "Ada";
var secondLetterOfFirstName = firstName[1];

// 初始化变量
var lastName = "Lovelace";

// 请把你的代码写在这条注释以下
var thirdLetterOfLastName = lastName[2];
```

## 使用方括号查找字符串中的最后一个字符

要获取字符串的最后一个字符，可以用字符串的长度减 1 的索引值。

例如，在`var firstName = "Charles"`中，你可以这样操作`firstName[firstName.length - 1]`来得到字符串的最后的一个字符。



------



使用方括号lastName变量中的最后一个字符。

```js
// 示例
var firstName = "Ada";
var lastLetterOfFirstName = firstName[firstName.length - 1];

// 初始化变量
var lastName = "Lovelace";

// 请把你的代码写在这条注释以下
var lastLetterOfLastName = lastName[lastName.length-1];
```

## 使用方括号查找字符串中的第N个字符到最后一个字符

我们既可以获取字符串的最后一个字符，也可以用获取字符串的倒数第N个字符。

例如，你可以这样`firstName[firstName.length - 3]`操作来获得`var firstName = "Charles"`字符串中的倒数第三个字符。



------



使用方括号来获得`lastName`字符串中的倒数第二个字符。

```js
// 示例
var firstName = "Ada";
var thirdToLastLetterOfFirstName = firstName[firstName.length - 3];

// 初始化变量
var lastName = "Lovelace";

// 请把你的代码写在这条注释以下
var secondToLastLetterOfLastName = lastName[lastName.length-2];


```

## 填词造句

现在，我们来用字符串的相关知识实现一个 "[Mad Libs](https://en.wikipedia.org/wiki/Mad_Libs)" 类的文字游戏，称为 "Word Blanks"。 你将创建一个（可选幽默的）“填空”样式句子。

在 "Mad Libs" 游戏中，提供一个缺少一些单词的句子，缺少的单词包括名词，动词，形容词和副词等。然后，你选择一些单词填写句子缺失的地方，使句子完整并且有意义。

思考一下这句话 - "It was really **____**, and we **____** ourselves **____**"。这句话有三个缺失的部分 - 形容词，动词和副词，选择合适单词填入完成它。然后将完成的句子赋值给变量，如下所示：

> var sentence = "It was really" + "hot" + ", and we" + "laughed" + "ourselves" + "silly.";



------



在这个挑战中，我们为你提供名词，动词，形容词和副词。你需要使用合适单词以及我们提供的单词来形成完整的句子。

你需要使用字符串连接运算符`+`来拼接字符串变量：`myNoun`，`myAdjective`，`myVerb`，和`myAdverb`来构建一个新字符串。然后，将新字符串赋给`result`变量。

你还需要考虑字符串中的空格，确保句子的所有单词之间有空格。结果应该是一个完整的句子。

```js
function wordBlanks(myNoun, myAdjective, myVerb, myAdverb) {
  // 请把你的代码写在这条注释以下
  var result =  "My " + myNoun + " Molly is really " + myAdjective + " and it " + myVerb + " really " + myAdverb;

  // 请把你的代码写在这条注释以上
  return result;
}

// 修改单词来测试函数
wordBlanks("dog", "big", "ran", "quickly");
```

## 使用 JavaScript 数组将多个值存储在一个变量中

使用`数组`，我们可以在一个地方存储多个数据。

以左方括号`[`开始定义一个数组，以右方括号`]`结束，里面每个元素之间用逗号隔开，例如：

`var sandwich = ["peanut butter", "jelly", "bread"]`.



------



创建一个包含`字符串`和`数字`的数组`myArray`

```js
// 示例
var ourArray = ["John", 23];

// 请把你的代码写在这条注释以下
var myArray = ['lili',1,2,'nihao'];

```

## 将一个数组嵌套在另一个数组中

你也可以在数组中包含其他数组，例如：`[["Bulls", 23], ["White Sox", 45]]`。这被称为一个多维数组。



------



创建一个名为`myArray`的多维数组。

```js
// 示例
var ourArray = [["the universe", 42], ["everything", 101010]];

// 请把你的代码写在这条注释以下
var myArray = [1,'nihao',['lili',2,3]];

```

## 通过索引访问数组中的数据

我们可以像操作字符串一样通过数组索引`[index]`来访问数组中的数据。

数组索引的使用与字符串索引一样，不同的是，通过字符串的索引得到的是一个字符，通过数组索引得到的是一个元素。与字符串类似，数组也是基于零的索引，因此数组的第一个元素的索引是`0`。

**示例**

> var array = [50,60,70];
> array[0]; // 值为 50
> var data = array[1]; // 值为 60

**提示**
数组名称和方括号之间不应有任何空格，如`array [0]`尽管 JavaScript 能够正确处理，但可能会让看你代码的其他程序员感到困惑



------



创建一个名为`myData`的变量，并把`myArray`的第一个索引上的值赋给它。

```js
// 示例
var ourArray = [50,60,70];
var ourData = ourArray[0]; // 值为 50

// 初始化变量
var myArray = [50,60,70];

// 请把你的代码写在这条注释以下
var myData=myArray[0];
```

## 通过索引修改数组中的数据

与字符串的数据不可变不同，数组的数据是可变的，并且可以自由地改变。

**示例**

> var ourArray = [50,40,30];
> ourArray[0] = 15; // 等于 [15,40,30]

**提示**
数组名称和方括号之间不应有任何空格，如`array [0]`尽管 JavaScript 能够正确处理，但可能会让看你代码的其他程序员感到困惑。



------



修改数组`myArray`中索引0上的值为`45`

```js
// 示例
var ourArray = [18,64,99];
ourArray[1] = 45; // ourArray now equals [18,45,99].

// 初始化变量
var myArray = [18,64,99];

// 请把你的代码写在这条注释以下
myArray[0]=45;

```

## 使用索引访问多维数组

可以把 多维 数组看作成是一个 *数组中的数组*。当使用方括号去访问数组的时候，第一个`[index]`访问的是第 N 个子数组，第二个`[index]`访问的是第 N 个子数组的第N个元素。

**示例**

> var arr = [
>  [1,2,3],
>  [4,5,6],
>  [7,8,9],
>  [[10,11,12], 13, 14]
> ];
> arr[3]; // 等于 [[10,11,12], 13, 14]
> arr[3][0]; // 等于 [10,11,12]
> arr[3][0][1]; // 等于 11

**提示**
数组名称和方括号之间不应该有任何空格，如`array [0][0]`甚至是这样`array [0] [0]`尽管 JavaScript 能够正确处理，但可能会让看你代码的其他程序员感到困惑。



------



使用恰当的`[index]`访问`myArray`，使得`myData`的值为`8`

```js
// 初始化变量
var myArray = [[1,2,3], [4,5,6], [7,8,9], [[10,11,12], 13, 14]];

// 请把你的代码写在这条注释以下
var myData = myArray[0][0];
myData=myArray[2][1];
```

## 使用 push() 操作数组

一个简单的方法将数据添加到一个数组的末尾是通过`push()`函数。

`.push()`接受把一个或多个参数，并把它“推”入到数组的末尾。

> var arr = [1,2,3];
> arr.push(4);
> // 现在arr的值为 [1,2,3,4]



------



把`["dog", 3]`“推”入到`myArray`变量的末尾。

```js
// 示例
var ourArray = ["Stimpson", "J", "cat"];
ourArray.push(["happy", "joy"]); 
// 经过 push 操作后，ourArray 的值为 ["Stimpson", "J", "cat", ["happy", "joy"]]

// 初始化变量
var myArray = [["John", 23], ["cat", 2]];

// 请把你的代码写在这条注释以下
myArray.push(["dog",3]);

```

## 使用 pop() 操作数组

改变数组中数据的另一种方法是用`.pop()`函数。

`.pop()`函数用来“抛出”一个数组末尾的值。我们可以把这个“抛出”的值赋给一个变量存储起来。换句话说就是`.pop()`函数移除数组末尾的元素并返回这个元素。

数组中任何类型的元素（数值，字符串，甚至是数组）可以被“抛出来” 。

> ```
> var threeArr = [1, 4, 6];var oneDown = threeArr.pop();console.log(oneDown); // 输出 6console.log(threeArr); // 输出 [1, 4]
> ```



------



使用`.pop()`函数移除`myArray`中的最后一个元素，并且把“抛出”的值赋给`removedFromMyArray`。

```js
// 示例
var ourArray = [1,2,3];
var removedFromOurArray = ourArray.pop(); 
// 经过 pop 操作之后，removedFromOurArray 的值为 3，ourArray 的值为 [1,2]

// 初始化变量
var myArray = [["John", 23], ["cat", 2]];

// 请把你的代码写在这条注释以下
var removedFromMyArray=myArray.pop();


```

## 使用 shift() 操作数组

`pop()`函数用来移出数组中最后一个元素。如果想要移出第一个元素要怎么办呢？

这就是`.shift()`的用武之地。它的工作原理就像`.pop()`，但它移除的是第一个元素，而不是最后一个。



------



使用`.shift()`函数移出`myArray`中的第一项，并把“移出”的值赋给`removedFromMyArray`。

```js
// 示例
var ourArray = ["Stimpson", "J", ["cat"]];
var removedFromOurArray = ourArray.shift();
// removedFromOurArray now equals "Stimpson" and ourArray now equals ["J", ["cat"]].

// 初始化变量
var myArray = [["John", 23], ["dog", 3]];

// 请把你的代码写在这条注释以下
// var removedFromMyArray=;
var removedFromMyArray=myArray.shift();


```

## 使用 unshift() 操作数组

你不仅可以`shift`（移出）数组中的第一个元素，你也可以`unshift`（移入）一个元素到数组的头部。

`.unshift()`函数用起来就像`.push()`函数一样, 但不是在数组的末尾添加元素，而是在数组的头部添加元素。



------



使用`unshift()`函数把`["Paul",35]`加入到`myArray`的头部。

```js
// 示例
var ourArray = ["Stimpson", "J", "cat"];
ourArray.shift(); // 经过 shift 操作后，ourArray 的值为 ["J", "cat"]
ourArray.unshift("Happy"); 
// 经过 unshift 操作后，ourArray 的值为 ["Happy", "J", "cat"]

// 初始化变量
var myArray = [["John", 23], ["dog", 3]];
myArray.shift();

// 请把你的代码写在这条注释以下
myArray.unshift(["Paul",35]);

```

## 用函数编写可重用代码

在 JavaScript 中，我们可以把代码的重复部分抽取出来，放到一个函数中。

举个例子：

> function functionName() {
>  console.log("Hello World");
> }

你可以通过函数名`functionName`加上后面的小括号来调用这个函数，就像这样：

```
functionName();
```

每次调用函数时，它都会在控制台上打印消息`"Hello World"`。每次调用函数时，大括号之间的所有代码都将被执行。



------



1. 先创建一个名为`reusableFunction`的函数，这个函数可以打印`"Hi World"`到控制台上。
2. 然后调用这个函数。

```js
// 示例
function ourReusableFunction() {
  console.log("Heyya, World");
}

ourReusableFunction();

// 请把你的代码写在这条注释以下
function reusableFunction(){
    console.log('Hi World');
}
reusableFunction();
```

## 将值传递给带有参数的函数

函数的参数`parameters`在函数中充当占位符(也叫形参)的作用，参数可以为一个或多个。调用一个函数时所传入的参数为实参，实参决定着形参真正的值。简单理解：形参即形式、实参即内容。

这是带有两个参数的函数，`param1`和`param2`：

> function testFun(param1, param2) {
>  console.log(param1, param2);
> }

接着我们调用`testFun`：

```
testFun("Hello", "World");
```

我们传递了两个参数，`"Hello"`和`"World"`。在函数内部，`param1`等于“Hello”，`param2`等于“World”。请注意，`testFun`函数可以多次调用，每次调用时传递的参数会决定形参的实际值。



------



1. 创建一个名为`functionWithArgs`的函数，它可以接收两个参数，计算参数的和，将结果输出到控制台。
2. 调用这个函数。

```js
// 示例
function ourFunctionWithArgs(a, b) {
  console.log(a - b);
}
ourFunctionWithArgs(10, 5); // Outputs 5

// 请把你的代码写在这条注释以下
function functionWithArgs(a,b){
  console.log(a+b);
}
functionWithArgs(1,2);
```

## 全局作用域和函数

在 JavaScript 中，作用域涉及到变量的作用范围。在函数外定义的变量具有 全局 作用域。这意味着，具有全局作用域的变量可以在代码的任何地方被调用。

这些没有使用`var`关键字定义的变量，会被自动创建在全局作用域中，形成全局变量。当在代码其他地方无意间定义了一个变量，刚好变量名与全局变量相同，这时会产生意想不到的后果。因此你应该总是使用var关键字来声明你的变量。



------



在函数外声明一个`全局`变量`myGlobal`，并给它一个初始值`10`

在函数`fun1`的内部，**不**使用`var`关键字来声明`oopsGlobal`，并赋值为`5`。

```js
// 声明变量
var myGlobal=10;
function fun1() {
  oopsGlobal=5;
  // 把 5 赋给 oopsGlobal
}
// 请把你的代码写在这条注释以上
function fun2() {
  var output = "";
  if (typeof myGlobal != "undefined") {
    output += "myGlobal: " + myGlobal;
  }
  if (typeof oopsGlobal != "undefined") {
    output += " oopsGlobal: " + oopsGlobal;
  }
  console.log(output);
}
```

## 局部作用域和函数

在一个函数内声明的变量，以及该函数的参数都是局部变量，意味着它们只在该函数内可见。

这是在函数`myTest`内声明局部变量`loc`的例子：

> function myTest() {
> var loc = "foo";
> console.log(loc);
> }
> myTest(); // 打印出 "foo"
> console.log(loc); // loc 没有定义

在函数外，`loc`是未定义的。



------



在函数`myFunction`内部声明一个局部变量`myVar`，并删除外部的 console.log。

**提示：**

如果你遇到了问题，可以先尝试刷新页面。

## 函数中的全局作用域和局部作用域

一个程序中有可能具有相同名称的局部变量 和全局变量。在这种情况下，`局部`变量将会优先于`全局`变量。

下面为例：

> var someVar = "Hat";
> function myFun() {
> var someVar = "Head";
> return someVar;
> }

函数`myFun`将会返回`"Head"`，因为`局部变量`优先级更高。



------



给`myOutfit`添加一个局部变量来覆盖`outerWear`的值为`"sweater"`。

```js
// 初始化变量
var outerWear = "T-Shirt";

function myOutfit() {
  // 请把你的代码写在这条注释以下
  var outerWear='sweater';
  // 请把你的代码写在这条注释以上
  return outerWear;
}
myOutfit();
```

## 函数可以返回某个值

我们可以通过函数的参数把值传入函数，也可以使用`return`语句把数据从一个函数中传出来。

**示例**

> function plusThree(num) {
> return num + 3;
> }
> var answer = plusThree(5); // 8

`plusThree`带有一个`num`的参数并且返回（returns）一个等于`num + 3`的值。



------



创建一个函数`timesFive`接收一个参数, 把它乘以`5`之后返回，关于如何测试timesFive 函数，可以参考编辑器中最后一行的示例。

```js
// 示例
function minusSeven(num) {
  return num - 7;
}

// 请把你的代码写在这条注释以下
function timesFive(a){
  return a*5;
}


console.log(minusSeven(10));
```

## 函数也可以返回 undefined

函数一般用`return`语句来返回值，但这不是必须的。在函数没有`return`语句的情况下，当你调用它时，该函数会执行内部代码，返回的值是`undefined`。

**示例**

> var sum = 0;
> function addSum(num) {
>  sum = sum + num;
> }
> var returnedValue = addSum(3); // sum 会改变，但函数的返回值仍为 undefined

`addSum`是一个没有`return`语句的函数。该函数将更改全局变量`sum`，函数的返回值为`undefined`。



------



创建一个没有任何参数的函数`addFive`。此函数使`sum`变量加 5，但其返回值是`undefined`。

```js
// 示例
var sum = 0;
function addThree() {
  sum = sum + 3;
}

// 请把你的代码写在这条注释以下
function addFive(){
  sum+=5;
}


// 请把你的代码写在这条注释以上
var returnedValue = addFive();
```

## 用返回值来赋值

如果你还记得我们在这一节 [Storing Values with the Assignment Operator](https://learn.freecodecamp.one/javascript-algorithms-and-data-structures/basic-javascript/storing-values-with-the-assignment-operator),的讨论，赋值之前，先完成等号右边的操作。这意味着我们可把一个函数的返回值，赋值给一个变量。

假设我们预先定义的函数`sum`其功能就是将两个数字相加，那么：

```
ourSum = sum(5, 12);
```

将调用`sum`函数，返回`return`了一个数值`17`，然后把它赋值给了`ourSum`变量。



------



调用`processArg`函数并给参数一个值`7`，然后把返回的值赋值给变量`processed`。

运行测试重置代码[获取提示](https://guide.freecodecamp.org/certifications/javascript-algorithms-and-data-structures/basic-javascript/assignment-with-a-returned-value)请求帮助

```js
// 示例
var changed = 0;

function change(num) {
  return (num + 5) / 3;
}

changed = change(10);

// 初始化变量
var processed = 0;

function processArg(num) {
  return (num + 3) / 5;
}

// 请把你的代码写在这条注释以下
processed=processArg(7);

```

## 排队

在计算机科学中队列（queue）是一个抽象的数据结构，队列中的条目都是有秩序的。新的条目会被加到`队列`的末尾，旧的条目会从`队列`的头部被移出。

写一个函数`nextInLine`，用一个数组(`arr`)和一个数字(`item`)作为参数。

把数字添加到数组的结尾，然后移出数组的第一个元素。

最后`nextInLine`函数应该返回被删除的元素。

```js
function nextInLine(arr, item) {
  // 请把你的代码写在这里
  arr.push(item);
  var del=arr.shift();
  return del;  // 请修改这一行
}

// 初始化测试数据
var testArr = [1,2,3,4,5];

// 控制台输出
console.log("Before: " + JSON.stringify(testArr));
console.log(nextInLine(testArr, 6)); // Modify this line to test
console.log("After: " + JSON.stringify(testArr));
```

## 理解布尔值

另一种数据类型是布尔（Boolean）。`布尔`值要么是`true`要么是`false`。它非常像电路开关，`true`是“开”，`false`是“关”。这两种状态是互斥的。

**注意**
`布尔值`是不带引号的，`"true"`和`"false"`是`字符串`而不是`布尔值`，在 JavaScript 中也没有特殊含义。



------



修改`welcomeToBooleans`函数，让它返回`true`而不是`false`。

## 用 if 语句来表达条件逻辑

`If`语句用于在代码中做条件判断。关键字`if`告诉 JavaScript 在小括号中的条件为真的情况下去执行定义在大括号里面的代码。这种条件被称为`Boolean`条件，因为他们只可能是`true`（真）或`false`（假）。

当条件的计算结果为`true`，程序执行大括号内的语句。当布尔条件的计算结果为`false`，大括号内的代码将不会执行。

**伪代码**

> if(*条件为真*){
> *语句被执行*
> }

**示例**

> function test (myCondition) {
> if (myCondition) {
> return "It was true";
> }
> return "It was false";
> }
> test(true); // 返回 "It was true"
> test(false); // 返回 "It was false"

当`test`被调用，并且传递进来的参数值为`true`，`if`语句会计算`myCondition`的结果，看它是真还是假。如果条件为`true`，函数会返回`"It was true"`。当`test`被调用，并且传递进来的参数值为`false`，`myCondition`*不* 为`true`，并且不执行大括号后面的语句，函数返回`"It was false"`。



------



在函数内部创建一个`if`语句，如果该参数`wasThatTrue`值为`true`，返回`"Yes, that was true"`，否则，并返回`"No, that was false"`。

运行测试重置代码[获取提示](https://guide.freecodecamp.org/certifications/javascript-algorithms-and-data-structures/basic-javascript/use-conditional-logic-with-if-statements)请求帮助

```js
// 示例
function ourTrueOrFalse(isItTrue) {
  if (isItTrue) { 
    return "Yes, it's true";
  }
  return "No, it's false";
}

// 初始化变量
function trueOrFalse(wasThatTrue) {

  // 请把你的代码写在这条注释以下
  
  if(wasThatTrue){
      return "Yes, that was true";
  }else{
      return "No, that was false";
  }
  
  // 请把你的代码写在这条注释以上.

}

// 你可以修改这一行来测试你的代码
trueOrFalse(true);
```

## 相等运算符

在 JavaScript 中，有很多相互比较的操作。所有这些操作符都返回一个`true`或`false`值。

最基本的运算符是相等运算符：`==`。相等运算符比较两个值，如果它们是同等，返回`true`，如果它们不等，返回`false`。值得注意的是相等运算符不同于赋值运算符（`=`），赋值运算符是把等号右边的值赋给左边的变量。

> function equalityTest(myVal) {
> if (myVal == 10) {
> return "Equal";
> }
> return "Not Equal";
> }

如果`myVal`等于`10`，相等运算符会返回`true`，因此大括号里面的代码会被执行，函数将返回`"Equal"`。否则，函数返回`"Not Equal"`。

在 JavaScript 中，为了让两个不同的`数据类型`（例如`数字`和`字符串`）的值可以作比较，它必须把一种类型转换为另一种类型。然而一旦这样做，它可以像下面这样来比较：

> 1 == 1 // true
> 1 == 2 // false
> 1 == '1' // true
> "3" == 3 // true



------



把`相等运算符`添加到指定的行，这样当`val`的值为`12`的时候，函数会返回"Equal"。

```js
// 初始化变量
function testEqual(val) {
  if (val==12) { // 请修改这一行
    return "Equal";
  }
  return "Not Equal";
}

// 你可以修改这一行来测试你的代码
testEqual(12);
```

## 严格相等运算符

严格相等运算符（`===`）是相对相等操作符（`==`）的另一种比较操作符。与相等操作符不同的是，它会同时比较元素的值和`数据类型`。

**示例**

> 3 === 3 // true
> 3 === '3' // false

`3`是一个`数字`类型的，而`'3'`是一个`字符串`类型的，所以 3 不全等于 '3'。



------



在`if`语句值使用严格相等运算符，这样当`val`严格等于7的时候，函数会返回"Equal"。

```js
// 初始化变量
function testStrict(val) {
  if (val===7) { // 请修改这一行
    return "Equal";
  }
  return "Not Equal";
}

// 你可以修改这一行来测试你的代码
testStrict(7);
```

## 比较不同值

在上两个挑战中，我们学习了相等运算符 (`==`) 和严格相等运算符 (`===`)。现在让我们快速回顾并实践一下。

如果要比较的值不是同一类型，相等运算符会先执行数据类型转换，然后比较值。而严格相等运算符只比较值，不会进行数据类型转换。

由此可见，相等运算符和严格相等运算符的区别是：前者会执行隐式类型转换，后者不会。

**示例**

> 3 == '3' // 返回 true，因为 JavaScript 会执行类型转换把字符串 '3' 转化成数字
> 3 === '3' // 返回 false，因为类型不同，而这里不会进行类型转换

**提示**
在JavaScript中，你可以使用`typeof`运算符确定变量的类型或值，如下所示：

> typeof 3 // 返回 'number'
> typeof '3' // 返回 'string'



------



编辑器中的`compareEquality`函数使用相等运算符比较两个值。修改函数，使其仅在值严格相等时返回 "Equal" 。

运行测试重置代码[获取提示](https://guide.freecodecamp.org/certifications/javascript-algorithms-and-data-structures/basic-javascript/practice-comparing-different-values)请求帮助

## 严格不等运算符

严格不相等运算符（`!==`）与全等运算符是相反的。这意味着严格不相等并返回`false`的地方，用严格相等运算符会返回`true`，*反之亦然*。严格相等运算符不会转换值的数据类型。

**示例**

> 3 !== 3 // false
> 3 !== '3' // true
> 4 !== 3 // true



------



在`if`语句中，添加严格不相等运算符`!==`，这样如果`val`与`17`严格不相等的时候，函数会返回 "Not Equal"。

## 大于运算符

使用大于运算符（`>`）来比较两个数字。如果大于运算符左边的数字大于右边的数字，将会返回`true`。否则，它返回`false`。

与相等运算符一样，大于运算符在比较的时候，会转换值的数据类型。

**例如**

> 5 > 3 // true
> 7 > '3' // true
> 2 > 3 // false
> '1' > 9 // false



------



添加`大于`运算符到指定的行，使得返回的语句是有意义的。

## 大于或等于运算符

使用`大于等于`运算符（`>=`）来比较两个数字的大小。如果大于等于运算符左边的数字比右边的数字大或者相等，它会返回`true`。否则，它会返回`false`。

与相等运算符相似，`大于等于`运算符在比较的时候会转换值的数据类型。

**例如**

> 6 >= 6 // true
> 7 >= '3' // true
> 2 >= 3 // false
> '7' >= 9 // false



------



添加`大于等于`运算符到指定行，使得函数的返回语句有意义。

## 小于运算符

使用小于运算符（`<`）比较两个数字的大小。如果小于运算符左边的数字比右边的数字小，它会返回`true`。否则会返回`false`。与相等运算符类似，小于 运算符在做比较的时候会转换值的数据类型。

**例如**

> 2 < 5 // true
> '3' < 7 // true
> 5 < 5 // false
> 3 < 2 // false
> '8' < 4 // false



------



添加`小于`运算符到指定行，使得函数的返回语句有意义。

## 小于或等于运算符

使用`小于等于`运算符（`<=`）比较两个数字的大小。如果在小于等于运算符，左边的数字小于或者等于右边的数字，它会返回`true`。如果在小于等于运算符，左边的数字大于或者等于右边的数字，它会返回`false`。与相等运算符类似，`小于等于`运算符会转换数据类型。

**例如**

> 4 <= 5 // true
> '7' <= 7 // true
> 5 <= 5 // true
> 3 <= 2 // false
> '8' <= 4 // false



------



添加`小于等于`运算符到指定行，使得函数的返回语句有意义。

## 使用 Switch 语句从许多选项中进行选择

如果你有非常多的选项需要选择，可以使用 switch 语句。根据不同的参数值会匹配上不同的 case 分支，语句会从第一个匹配的 case 分支开始执行，直到碰到 break 就结束。

这是一个伪代码案例：

> switch(num) {
>  case value1:
>   statement1;
>   break;
>  case value2:
>  statement2;
>   break;
> ...
>  case valueN:
>   statementN;
>   break;
> }

测试`case`值使用严格相等运算符进行比较，break 关键字告诉 JavaScript 停止执行语句。如果没有 break 关键字，下一个语句会继续执行。



------



写一个测试`val`的 switch 语句，并且根据下面的条件来设置不同的`answer`：
`1`- "alpha"
`2`- "beta"
`3`- "gamma"
`4`- "delta"

```js
function caseInSwitch(val) {
  var answer = "";
  // Only change code below this line
  switch (val) {
    case 1:
      return "alpha";
      break;
    case 2:
      return "beta";
      break;
    case 3:
      return "gamma";
      break;
    case 4:
      return "delta";
      break;
  }

  // Only change code above this line
  return answer;
}

// Change this value to test
caseInSwitch(1);
```

## 在 Switch 语句中添加默认选项

在`switch`语句中你可能无法用 case 来指定所有情况，这时你可以添加 default 语句。当再也找不到 case 匹配的时候 default 语句会执行，非常类似于 if/else 组合中的 else 语句。

`default`语句应该是最后一个 case。

> switch (num) {
>  case value1:
>   statement1;
>   break;
>  case value2:
>   statement2;
>   break;
> ...
>  default:
>   defaultStatement;
>   break;
> }



------



写一个根据下面的条件来设置`answer`的switch语句：
`"a"`- "apple"
`"b"`- "bird"
`"c"`- "cat"
`default`- "stuff"

```js
function switchOfStuff(val) {
  var answer = "";
  // 请把你的代码写在这条注释以下
  switch(val){
    case "a":
    return "apple";
    break;
    case "b":
    return "bird";
    break;
    case "c":
    return "cat";
    break;
    default:
    return "stuff";
    break;
  }
  
  
  // 请把你的代码写在这条注释以上  
  return answer;  
}

// 你可以修改这一行来测试你的代码
switchOfStuff(1);

```

## 在 Switch 语句添加多个相同选项

如果你忘了给`switch`的每一条`case`添加`break`，那么直到遇见`break`为止，后续的`case`会一直执行。如果你想为多个不同的输入设置相同的结果，可以这样写：

> switch(val) {
>  case 1:
>  case 2:
>  case 3:
>   result = "1, 2, or 3";
>   break;
>  case 4:
>   result = "4 alone";
> }

这样，1、2、3 都会有相同的结果。



------



请写一个`switch`语句，根据输入的`val`的范围得出对应的`answer`：
`1-3`- "Low"
`4-6`- "Mid"
`7-9`- "High"

**提示：**
你的`case`应基于范围中的每一个数字编写。

```js
function sequentialSizes(val) {
  var answer = "";
  // 请把你的代码写在这条注释以下
  switch(val){
    case 1:
    case 2:
    case 3:
    return "Low";
    break;
    case 4:
    case 5:
    case 6:
    return "Mid";
    break;
    case 7:
    case 8:
    case 9:
    return "High";
    break;
  }
  
  
  // 请把你的代码写在这条注释以上  
  return answer;  
}

// 你可以修改这一行来测试你的代码
sequentialSizes(1);

```

## 用一个 Switch 语句来替代多个 if else 语句

如果你有多个选项需要选择，`switch`语句写起来会比多个串联的`if`/`if else`语句容易些，譬如:

> if (val === 1) {
>  answer = "a";
> } else if (val === 2) {
>  answer = "b";
> } else {
>  answer = "c";
> }

可以被下面替代：

> switch(val) {
>  case 1:
>   answer = "a";
>   break;
>  case 2:
>   answer = "b";
>   break;
>  default:
>   answer = "c";
> }



------



把串联的`if`/`if else`语句改成`switch`语句。

```js
function chainToSwitch(val) {
  var answer = "";
  // 请把你的代码写在这条注释以下
  
  // if (val === "bob") {
  //   answer = "Marley";
  // } else if (val === 42) {
  //   answer = "The Answer";
  // } else if (val === 1) {
  //   answer = "There is no #1";
  // } else if (val === 99) {
  //   answer = "Missed me by this much!";
  // } else if (val === 7) {
  //   answer = "Ate Nine";
  // }
  switch(val) {
    case "bob":
    return "Marley";
    break;
    case 42:
    return "The Answer";
    break;
    case 1:
    return "There is no #1";
    break;
    case 99:
    return "Missed me by this much!";
    break;
    case 7:
    return "Ate Nine";
    break;
  }
  
  // 请把你的代码写在这条注释以上  
  return answer;  
}

// 你可以修改这一行来测试你的代码
chainToSwitch(7);

```

## 从函数返回布尔值

你应该还记得[相等运算符](https://learn.freecodecamp.one/javascript-algorithms-and-data-structures/basic-javascript/comparison-with-the-equality-operator)这道挑战题。在那里我们提到，所有比较操作符都会返回 boolean：要么是`true`要么是`false`。

有时人们通过 if/else 语句来做比较然后返回`true`或`false`。

> function isEqual(a,b) {
>  if (a === b) {
>   return true;
>  } else {
>   return false;
>  }
> }

有一个更好的方法，因为`===`总是返回`true`或`false`，所以我们可以直接返回比较的结果：

> function isEqual(a,b) {
>  return a === b;
> }



------



移除`isLess`函数的`if/else`语句但不影响函数的功能。

```js
function isLess(a, b) {
  // 请修改这部分代码
  return a<=b;
}

// Change these values to test
isLess(10, 15);
```

## 函数执行到 return 语句就结束

当代码执行到 return 语句时，函数返回一个结果就结束运行了，return 后面的语句不会执行。

**示例**

> function myFun() {
>  console.log("Hello");
>  return "World";
>  console.log("byebye")
> }
> myFun();

上面的代码输出"Hello"到控制台、返回 "World"，但没有输出`"byebye"`，因为函数遇到 return 语句就退出了。



------



修改函数`abTest`当`a`或`b`小于0时，函数立即返回一个`undefined`并退出。

**提示**
记住[`undefined`，是一个关键字，而不是一个字符串。](http://www.freecodecamp.one/challenges/understanding-uninitialized-variables)

```js
// 初始化变量
function abTest(a, b) {
  // 请把你的代码写在这条注释以下
  if(a<0 || b<0){
    return undefined;

  }
  
  
  // 请把你的代码写在这条注释以上

  return Math.round(Math.pow(Math.sqrt(a) + Math.sqrt(b), 2));
}

// 你可以修改这一行来测试你的代码
abTest(2,2);
```

## 21点游戏

在赌场 21 点游戏中，玩家可以通过计算牌桌上已经发放的卡牌的高低值来让自己在游戏中保持优势，这就叫[ 21 点算法](https://www.douban.com/note/273781969/)。

根据下面的表格，每张卡牌都分配了一个值。如果卡牌的值大于 0，那么玩家应该追加赌注。反之，追加少许赌注甚至不追加赌注。

| Count Change | Cards                  |
| :----------- | :--------------------- |
| +1           | 2, 3, 4, 5, 6          |
| 0            | 7, 8, 9                |
| -1           | 10, 'J', 'Q', 'K', 'A' |

你需要写一个函数实现 21 点算法，它根据参数`card`的值来递增或递减变量`count`，函数返回一个由当前`count`和`Bet`(`count>0`)或`Hold`(`count<=0`) 拼接的字符串。注意`count`和`"Bet"`或`Hold`应该用空格分开。

**例如：**
`-3 Hold5 Bet`

**提示**
既然 card 的值为 7、8、9 时，count 值不变，那我们就可以忽略这种情况。

```js
var count = 0;

function cc(card) {
  // 请把你的代码写在这条注释以下
 switch(card){
   case 1:
   case 2:
   case 3:
   case 4:
   case 5:
   case 6:
   count++;
   break
   case 10:
   case 'J':
   case 'Q':
   case 'K':
   case 'A':
   count--;
   break;
 }
 if(count>0){
     return count+" Bet";
   }else{
     return count+" Hold";
   }
  return "Change Me";
  // 请把你的代码写在这条注释以上
}

// 你可以在这里添加/删除 cc 方法的调用来测试结果
// 提示: 左边只会显示最后一次执行的返回值
cc(2); cc(3); cc(7); cc('K'); cc('A');
```

## 新建 JavaScript 对象

你之前可能听说过对象`object`。

对象和数组很相似，数组是通过索引来访问和修改数据，而对象是通过属性来访问和修改数据。

对象适合用来存储结构化数据，就和真实世界的对象一模一样，比如一只猫。

这是一个对象的示例：

> var cat = {
>  "name": "Whiskers",
>  "legs": 4,
>  "tails": 1,
>  "enemies": ["Water", "Dogs"]
> };

在这个示例中所有的属性以字符串的形式储存，例如 - `"name"`, `"legs"`，和`"tails"`。但是，你也可以使用数字作为属性，你甚至可以省略字符串属性的引号，如下所示：

> var anotherObject = {
>  make: "Ford",
>  5: "five",
>  "model": "focus"
> };

但是，如果你的对象具有任何非字符串属性，JavaScript 将自动将它们转换为字符串类型。



------



创建一个叫做`myDog`的对象，它里面有这些属性：`"name"`、`"legs"`,`"tails"`、`"friends"`。

你可以设置对象属性为任何值，只需要确保`"name"`是字符串、`"legs"`和`"tails"`是数字、`"friends"`是数组。

```js
// 示例
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};

// 请把你的代码写在这条注释以下

var myDog = {
  
  "name": "小白",
  "legs": 4,
  "tails":1,
  "friends":['everything!']
  
  
};
```



## 通过点符号访问对象属性

有两种方式访问对象属性，一个是点操作符(`.`)，一个是中括号操作符(`[]`)。

当你知道属性的名称的时候，使用点操作符。

这是一个使用点操作符读取对象属性的例子：

> var myObj = {
>  prop1: "val1",
>  prop2: "val2"
> };
> var prop1val = myObj.prop1; // val1
> var prop2val = myObj.prop2; // val2



------



通过点操作符读取对象`testObj`，把`hat`的属性值赋给变量`hatValue`，把`shirt`的属性值赋给`shirtValue`。

```js
// 初始化变量
var testObj = {
  "hat": "ballcap",
  "shirt": "jersey",
  "shoes": "cleats"
};

// 请把你的代码写在这条注释以下

// var hatValue = testObj;      // 请修改这一行
// var shirtValue = testObj;    // 请修改这一行
var hatValue = testObj.hat;
var shirtValue = testObj.shirt;
```

## 通过方括号访问对象属性

第二种访问对象的方式就是中括号操作符(`[]`)，如果你想访问的属性的名称有一个空格，这时你只能使用中括号操作符(`[]`)。

这是一个使用中括号操作符(`[]`)读取对象属性的例子：

> var myObj = {
>  "Space Name": "Kirk",
>  "More Space": "Spock",
>  "NoSpace": "USS Enterprise"
> };
> myObj["Space Name"]; // Kirk
> myObj['More Space']; // Spock
> myObj["NoSpace"]; // USS Enterprise

提示：属性名称中如果有空格，必须把属性名称用单引号或双引号包裹起来。



------



用中括号操作符读取对象`testObj`的属性`"an entree"`值和属性`"the drink"`值，并赋给`entreeValue`和`drinkValue`。

```js
// 初始化变量
var testObj = {
  "an entree": "hamburger",
  "my side": "veggies",
  "the drink": "water"
};

// 请把你的代码写在这条注释以下

// var entreeValue = testObj;   // 请修改这一行
// var drinkValue = testObj;    // 请修改这一行
var entreeValue = testObj["an entree"];
var drinkValue = testObj["the drink"];
```

## 通过变量访问对象属性

中括号操作符的另一个使用方式是用变量来访问一个属性。当你需要遍历对象的属性列表或查表时，这种方式极为有用。

这有一个使用变量来访问属性的例子：

> var dogs = {
>  Fido: "Mutt", Hunter: "Doberman", Snoopie: "Beagle"
> };
> var myDog = "Hunter";
> var myBreed = dogs[myDog];
> console.log(myBreed); // "Doberman"

还有更多：

> var someObj = {
>  propName: "John"
> };
> function propPrefix(str) {
>  var s = "prop";
>  return s + str;
> }
> var someProp = propPrefix("Name"); // someProp 现在的值为 'propName'
> console.log(someObj[someProp]); // 输出 "John"

提示：当我们通过变量名访问属性的时候，不需要给变量名包裹引号。因为实际上我们使用的是变量的值，而不是变量的名称。



------



使用变量`playerNumber`，通过中括号操作符找到`testObj`中`playerNumber`为`16`的值。然后把名字赋给变量`player`。

```js
// 初始化变量
var testObj = {
  12: "Namath",
  16: "Montana",
  19: "Unitas"
};

// 请把你的代码写在这条注释以下;

var playerNumber=16;       // 请修改这一行
var player = testObj[playerNumber];   // 请修改这一行
```

## 更新对象属性

当你创建了一个对象后，你可以用点操作符或中括号操作符来更新对象的属性。

举个例子，让我们看看`ourDog`:

> var ourDog = {
>  "name": "Camper",
>  "legs": 4,
>  "tails": 1,
>  "friends": ["everything!"]
> };

让我们更改它的名称为 "Happy Camper"，这有两种方式来更新对象的`name`属性：

`ourDog.name = "Happy Camper";`或

```
ourDog["name"] = "Happy Camper";
```

现在，`ourDog.name`的值就不再是 "Camper"，而是 "Happy Camper"。



------



更新`myDog`对象的`name`属性，让它的名字从 "Coder" 变成 "Happy Coder"。

## 给对象添加新属性

你也可以像更改属性一样给对象添加属性。

看看我们是如何给`ourDog`添加`"bark"`属性：

```
ourDog.bark = "bow-wow";
```

或者

```
ourDog["bark"] = "bow-wow";
```

现在当我们访问`ourDog.bark`时会得到 ourDog 的 bark 值 "bow-wow".



------



给`myDog`添加一个`"bark"`属性，设置它的值为狗的声音，例如："woof"。

```js
// 示例
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"]
};

ourDog.bark = "bow-wow";

// 初始化变量
var myDog = {
  "name": "Happy Coder",
  "legs": 4,
  "tails": 1,
  "friends": ["freeCodeCamp Campers"]
};

// 请把你的代码写在这条注释以下
myDog.bark="woof";
```

## 删除对象的属性

我们同样可以删除对象的属性，例如：

```
delete ourDog.bark;
```



------



删除`myDog`对象的`"tails"`属性。

```js
// 示例
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"],
  "bark": "bow-wow"
};

delete ourDog.bark;

// 初始化变量
var myDog = {
  "name": "Happy Coder",
  "legs": 4,
  "tails": 1,
  "friends": ["freeCodeCamp Campers"],
  "bark": "woof"
};

// 请把你的代码写在这条注释以下
delete myDog.tails;

```

## 使用对象进行查找

对象和字典一样，可以用来存储键/值对。如果你的数据跟对象一样，你可以用对象来查找你想要的值，而不是使用switch或if/else语句。当你知道你的输入数据在某个范围时，这种查找方式极为有效。

这是简单的反向字母表：

> var alpha = {
>  1:"Z",
>  2:"Y",
>  3:"X",
>  4:"W",
>  ...
>  24:"C",
>  25:"B",
>  26:"A"
> };
> alpha[2]; // "Y"
> alpha[24]; // "C"
>
> var value = 2;
> alpha[value]; // "Y"



------



把 switch 语句转化为`lookup`对象。使用它来查找`val`属性的值，并赋值给`result`变量。

```js
// 初始化变量
function phoneticLookup(val) {
  var result = "";
  // 请把你的代码写在这条注释以下
  // switch(val) {
  //   case "alpha": 
  //     result = "Adams";
  //     break;
  //   case "bravo": 
  //     result = "Boston";
  //     break;
  //   case "charlie": 
  //     result = "Chicago";
  //     break;
  //   case "delta": 
  //     result = "Denver";
  //     break;
  //   case "echo": 
  //     result = "Easy";
  //     break;
  //   case "foxtrot": 
  //     result = "Frank";
  // }
  var lookup= {
    "alpha":"Adams",
    "bravo":"Boston",
    "charlie":"Chicago",
    "delta":"Denver",
    "echo":"Easy",
    "foxtrot":"Frank"
  };
  var result=lookup[val];


  // 请把你的代码写在这条注释以上
  return result;
}

// 你可以修改这一行来测试你的代码
phoneticLookup("charlie");
```

## 测试对象的属性

有时检查一个对象属性是否存在是非常有用的，我们可以用`.hasOwnProperty(propname)`方法来检查对象是否有该属性。如果有返回`true`，反之返回`false`。

**示例**

> var myObj = {
>  top: "hat",
>  bottom: "pants"
> };
> myObj.hasOwnProperty("top"); // true
> myObj.hasOwnProperty("middle"); // false



------



修改函数`checkObj`检查`myObj`是否有`checkProp`属性，如果属性存在，返回属性对应的值，如果不存在，返回`"Not Found"`。

```js
// 初始化变量
var myObj = {
  gift: "pony",
  pet: "kitten",
  bed: "sleigh"
};

function checkObj(checkProp) {
  // 请把你的代码写在这条注释以下
  if(myObj.hasOwnProperty(checkProp)){
    return myObj[checkProp];
  }else{
    return "Not Found";
  }
 
}

// 你可以修改这一行来测试你的代码
checkObj("gift");
```

## 操作复杂对象

有时你可能希望将数据存储在灵活的数据结构中。JavaScript 对象是处理灵活数据的一种方法。它可以储存字符串，数字，布尔值，函数，和对象以及这些值的任意组合。

这是一个复杂数据结构的示例：

> var ourMusic = [
>  {
>   "artist": "Daft Punk",
>   "title": "Homework",
>   "release_year": 1997,
>   "formats": [
>    "CD",
>    "Cassette",
>    "LP"
>   ],
>   "gold": true
>  }
> ];

这是一个对象数组，并且对象有各种关于专辑的 详细信息。它也有一个嵌套的`formats`的数组。附加专辑记录可以被添加到数组的最上层。

对象将数据以一种键-值对的形式保存。在上面的示例中，`"artist": "Daft Punk"`是一个具有`"artist"`键和`"Daft Punk"`值的属性。

[JavaScript Object Notation](http://www.json.org/) 简称`JSON`是用于存储数据的相关数据交换格式。

> {
>  "artist": "Daft Punk",
>  "title": "Homework",
>  "release_year": 1997,
>  "formats": [
>   "CD",
>   "Cassette",
>   "LP"
>  ],
>  "gold": true
> }

**提示**
数组中有多个 JSON 对象的时候，对象与对象之间要用逗号隔开。

```js
var myMusic = [
  {
    "artist": "Billy Joel",
    "title": "Piano Man",
    "release_year": 1973,
    "formats": [ 
      "CD",
      "8T",
      "LP"
    ],
    "gold": true
  },
  // 请在这里添加专辑
  {
     "artist":"lala",
     "title":"nija",
     "release_year":2021,
     "formats":[
       "15",
       "12",
       "13"
     ]

  }
 


];

```

## 访问嵌套对象

通过串联起来的点操作符或中括号操作符来访问对象的嵌套属性。

下面是一个嵌套的对象：

> var ourStorage = {
>  "desk": {
>   "drawer": "stapler"
>  },
>  "cabinet": {
>   "top drawer": {
>    "folder1": "a file",
>    "folder2": "secrets"
>   },
>   "bottom drawer": "soda"
>  }
> };
> ourStorage.cabinet["top drawer"].folder2; // "secrets"
> ourStorage.desk.drawer; // "stapler"



------



检索对象`myStorage`中嵌套属性`glove box`的值。因为属性的名字带有空格，请使用中括号操作符来访问属性的值。

```js
// 初始化变量
var myStorage = {
  "car": {
    "inside": {
      "glove box": "maps",
      "passenger seat": "crumbs"
     },
    "outside": {
      "trunk": "jack"
    }
  }
};

var gloveBoxContents = myStorage.car.inside["glove box"]; // 请修改这一行

```

## 循环嵌套

如果你有一个二维数组，可以使用相同的逻辑，先遍历外面的数组，再遍历里面的子数组。下面是一个例子：

> var arr = [
>  [1,2], [3,4], [5,6]
> ];
> for (var i=0; i < arr.length; i++) {
>  for (var j=0; j < arr[i].length; j++) {
>   console.log(arr[i][j]);
>  }
> }

一次输出`arr`中的每个子元素。提示，对于内部循环，我们可以通过`arr[i]`的`.length`来获得子数组的长度，因为`arr[i]`的本身就是一个数组。



------



修改函数`multiplyAll`，获得`arr`内部数组的每个数字相乘的结果`product`。

```js
function multiplyAll(arr) {
  var product = 1;
  // 请把你的代码写在这条注释以下
  for(var i=0;i<arr.length;i++){
    for(var j=0;j<arr[i].length;j++){
      product*=arr[i][j];
    }
  }
  // 请把你的代码写在这条注释以上
  return product;
}

// 你可以修改这一行来测试你的代码
multiplyAll([[1,2],[3,4],[5,6,7]]);

```

## do...while 循环

这一节我们将要学习的是`do...while`循环，它会先执行`do`里面的代码，如果`while`表达式为真则重复执行，反之则停止执行。我们来看一个例子。

> var ourArray = [];
> var i = 0;
> do {
>  ourArray.push(i);
>  i++;
> } while (i < 5);

这看起来和其他循环语句差不多，返回的结果是`[0, 1, 2, 3, 4]`，`do...while`与其他循环不同点在于，初始条件为假时的表现，让我们通过实际的例子来看看。

这是一个普通的 while 循环，只要`i < 5`，它就会在循环中运行代码。

> var ourArray = [];
> var i = 5;
> while (i < 5) {
>  ourArray.push(i);
>  i++;
> }

注意，我们首先将`i`的值初始化为 5。执行下一行时，注意到`i`不小于 5，循环内的代码将不会执行。所以`ourArray`最终没有添加任何内容，因此示例中的所有代码执行完时，`ourArray`仍然是`[]`。

现在，看一下`do...while`循环。

> var ourArray = [];
> var i = 5;
> do {
>  ourArray.push(i);
>  i++;
> } while (i < 5);

在这里，和使用 while 循环时一样，我们将`i`的值初始化为 5。执行下一行时，没有检查`i`的值，直接执行花括号内的代码。数组会添加一个元素，并在进行条件检查之前递增`i`。然后，在条件检查时因为`i`等于 6 不符合条件`i < 5`，所以退出循环。最终`ourArray`的值是`[5]`。

本质上，`do...while`循环确保循环内的代码至少运行一次。

让我们通过`do...while`循环将值添加到数组中。



------



将代码中的`while`循环更改为`do...while`循环，实现数字 10 添加到`myArray`中，代码执行完时，`i`等于`11`。

```js
// 初始化变量
var myArray = [];
var i = 10;

// 请把你的代码写在这条注释以下

do{
  myArray.push(i);
  i++;
}while (i < 10)

```

## 使用 JavaScript 生成随机分数

随机数非常适合用来创建随机行为。

`Math.random()`用来生成一个在`0`（包括 0）到`1`不包括 1）之间的随机小数，因此`Math.random()`可能返回 0 但绝不会返回 1。

**提示**
这一节讲过[Storing Values with the Equal Operator](https://learn.freecodecamp.one/storing-values-with-the-assignment-operator)，所有函数调用将在`return`执行之前解析，因此我们可以返回`Math.random()`函数的值。



------



更改`randomFraction`使其返回一个随机数而不是`0`。

运行测试重置代码[获取提示](https://guide.freecodecamp.org/certifications/javascript-algorithms-and-data-structures/basic-javascript/generate-random-fractions-with-javascript)请求帮助

```js
function randomFraction() {

  // 请把你的代码写在这条注释以下
  

  return Math.random();

  // 请把你的代码写在这条注释以上.
}
```

## 使用 JavaScript 生成随机整数

生成随机小数很棒，但随机数更有用的地方在于生成随机整数。

1. 用`Math.random()`生成一个随机小数。
2. 把这个随机小数乘以`20`。
3. 用`Math.floor()`向下取整 获得它最近的整数。

记住`Math.random()`永远不会返回`1`。同时因为我们是在用`Math.floor()`向下取整，所以最终我们获得的结果不可能有`20`。这确保了我们获得了一个在0到19之间的整数。

把操作连缀起来，代码类似于下面：

```
Math.floor(Math.random() * 20);
```

我们先调用`Math.random()`，把它的结果乘以20，然后把上一步的结果传给`Math.floor()`，最终通过向下取整获得最近的整数。



------



生成一个`0`到`9`之间的随机整数。

```js
var randomNumberBetween0and19 = Math.floor(Math.random() * 20);

function randomWholeNum() {

  // 请把你的代码写在这条注释以下


  return Math.floor(Math.random()*10);
}
```

## 生成某个范围内的随机整数

我们之前生成的随机数是在0到某个数之间，现在我们要生成的随机数是在两个指定的数之间。

我们需要定义一个最小值和一个最大值。

下面是我们将要使用的方法，仔细看看并尝试理解这行代码到底在干嘛：

```
Math.floor(Math.random() * (max - min + 1)) + min
```



------



创建一个叫`randomRange`的函数，参数为 myMin 和 myMax，返回一个在`myMin`（包括 myMin）和`myMax`（包括 myMax）之间的随机数。

## 使用 parseInt 函数

`parseInt()`函数解析一个字符串返回一个整数下面是一个示例：

```
var a = parseInt("007");
```

上面的函数把字符串 "007" 转换成数字 7。 如果字符串参数的第一个字符是字符串类型的，结果将不会转换成数字，而是返回`NaN`.



------



在`convertToInteger`函数中使用`parseInt()`转换接受的的字符串`str`为正数并返回。

```js
function convertToInteger(str) {
  return parseInt(str);
}

convertToInteger("56");
```

## 使用 parseInt 函数并传入一个基数

`parseInt()`函数解析一个字符串并返回一个整数。它同时可接受第二个参数，一个介于2和36之间的整数，表示字符串的基数。

函数调用如下所示：

```
parseInt(string, radix);
```

示例：

```
var a = parseInt("11", 2);
```

参数 2 表示 "11" 使用二进制数值系统。此示例将字符串 "11" 转换为整数 3。



------



在`convertToIntegerparseInt()`函数把二进制数转换成十进制并返回。

```js
function convertToInteger(str) {
  return parseInt(str,2);
}

convertToInteger("10011");
```

## 使用三元运算符

条件运算符（也称为三元运算符）的用处就像写成一行的 if-else 表达式

语法如下所示：

```
condition ? statement-if-true : statement-if-false;
```

以下函数使用 if-else 语句来检查条件：

> function findGreater(a, b) {
>  if(a > b) {
>   return "a is greater";
>  }
>  else {
>   return "b is greater";
>  }
> }

上面的函数使用条件运算符写法如下：

> function findGreater(a, b) {
>  return a > b ? "a is greater" : "b is greater";
> }



------



在`checkEqual`函数中使用条件运算符检查两个数字是否相等，函数应该返回 true 或 false

```js
function checkEqual(a, b) {
  return a==b? true:false;
}

checkEqual(1, 2);
```

## 使用多个三元运算符

在之前的挑战中，你使用了一个条件运算符。你也可以将多个运算符串联在一起以检查多种条件。

下面的函数使用 if，else if 和 else 语句来检查多个条件：

> function findGreaterOrEqual(a, b) {
>  if(a === b) {
>   return "a and b are equal";
>  }
>  else if(a > b) {
>   return "a is greater";
>  }
>  else {
>   return "b is greater";
>  }
> }

上面的函数使用条件运算符写法如下：

> function findGreaterOrEqual(a, b) {
>  return (a === b) ? "a and b are equal" : (a > b) ? "a is greater" : "b is greater";
> }



------



在 checkSign 函数中使用多个条件运算符来检查数字是正数 ("positive")、负数 ("negative") 或零 ("zero")。

```js
function checkSign(num) {
  return num>0?"positive":num<0? "negative":"zero";
}

checkSign(10);
```

