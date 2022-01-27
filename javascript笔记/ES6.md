## 探索 var 和 let 关键字之间的差异

使用`var`关键字来声明变量，会出现重复声明导致变量被覆盖却不会报错的问题：

> var camper = 'James';
> var camper = 'David';
> console.log(camper);
> // 打印出 'David'

在上面的代码中，`camper`的初始值为`'James'`，然后又被覆盖成了`'David'`。

在小型的应用中，你可能不会遇到这样的问题，但是当你的代码规模变得更加庞大的时候，就可能会在不经意间覆盖了之前定义的变量。

这样的行为不会报错，导致了 debug 非常困难。

在 ES6 中引入了新的关键字`let`来解决`var`关键字带来的潜在问题。

如果你在上面的代码中，使用了`let`关键字来代替`var`关键字，结果会是一个报错。

> let camper = 'James';
> let camper = 'David'; // 报错

你可以在浏览器的控制台里看见这个错误。

与`var`不同的是，当使用`let`的时候，同一名字的变量只能被声明一次。

请注意`"use strict"`。这代表着开启了严格模式，用于检测常见的代码错误以及"不安全"的行为，例如：

> "use strict";
> x = 3.14; // x 没有声明导致了报错

## 比较 var 和 let 关键字的作用域

当你使用`var`关键字来声明一个变量的时候，这个变量会被声明成全局变量，或是函数内的局部变量。

`let`关键字的作用类似，但会有一些额外的特性。如果你在代码块、语句或表达式中使用关键字`let`声明变量，这个变量的作用域就被限制在当前的代码块，语句或表达式之中。

举个例子：

> var numArray = [];
> for (var i = 0; i < 3; i++) {
>  numArray.push(i);
> }
> console.log(numArray);
> // 返回 [0, 1, 2]
> console.log(i);
> // 返回 3

当使用`var`关键字的时候，`i`会被声明成全局变量。当`i++`执行的时候，它会改变全局变量的值。这段代码可以看做下面这样:

> var numArray = [];
> var i;
> for (i = 0; i < 3; i++) {
>  numArray.push(i);
> }
> console.log(numArray);
> // returns [0, 1, 2]
> console.log(i);
> // returns 3

如果你在`for`循环中创建了使用`i`变量的函数，那么在后续调用函数的时候，上面提到的这种行为就会导致问题。这是因为函数存储的值会因为全局变量`i`的变化而不断的改变。

> var printNumTwo;
> for (var i = 0; i < 3; i++) {
>  if(i === 2){
>   printNumTwo = function() {
>    return i;
>   };
>  }
> }
> console.log(printNumTwo());
> // 返回 3

可以看到，`printNumTwo()`打印了 3 而不是 2。这是因为`i`发生了改变，并且函数`printNumTwo()`返回的是全局变量`i`的值，而不是`for`循环中创建函数时`i`的值。`let`关键字就不会有这种现象：

> 'use strict';
> let printNumTwo;
> for (let i = 0; i < 3; i++) {
>  if (i === 2) {
>   printNumTwo = function() {
>    return i;
>   };
>  }
> }
> console.log(printNumTwo());
> // 返回 2
> console.log(i);
> // 返回 "没有定义 i 变量"

`i`在全局作用域中没有声明，所以它没有被定义，它的声明只会发生在`for`循环内。在循环执行的时候，`let`关键字创建了三个不同的`i`变量，他们的值分别为 0、1 和 2，所以`printNumTwo()`返回了正确的值。



------



修改这段代码，使得在`if`语句中声明的`i`变量与在函数的第一行声明的`i`变量是彼此独立的。请注意不要在你的代码的任何地方使用`var`关键字。

这个练习说明了使用`var`与`let`关键字声明变量时，作用域之间的不同。当编写类似这个练习中的函数的时候，通常来说最好还是使用不同的变量名来避免误会。

```js
function checkScope() {
"use strict";
  let i = "function scope";
  if (true) {
    let i = "block scope";
    console.log("Block scope i is: ", i);
  }
  console.log("Function scope i is: ", i);
  return i;
}
```

## 用 const 关键字声明只读变量

`let`并不是唯一的新的声明变量的方式。在 ES6里面，你还可以使用`const`关键字来声明变量。

`const`拥有`let`的所有优点，所不同的是，通过`const`声明的变量是只读的。这意味着通过`const`声明的变量只能被赋值一次，而不能被再次赋值。

> "use strict"
> const FAV_PET = "Cats";
> FAV_PET = "Dogs"; // 报错

可以看见，尝试给通过`const`声明的变量再次赋值会报错。你应该使用`const`关键字来对所有不打算再次赋值的变量进行声明。这有助于你避免给一个常量进行额外的再次赋值。一个最佳实践是对所有常量的命名采用全大写字母，并在单词之间使用下划线进行分隔。



------



改变以下代码，使得所有的变量都使用`let`或`const`关键词来声明。当变量将会改变的时候使用`let`关键字，当变量要保持常量的时候使用`const`关键字。同时，对使用`const`声明的变量进行最佳实践的重命名，变量名中的字母应该都是大写的。

```js
function printManyTimes(str) {
  "use strict";

  // 在这行以下修改代码

  const SENTENCE = str + " is cool!";
  for(let i = 0; i < str.length; i+=2) {
    console.log(SENTENCE);
  }

  // 在这行以上修改代码

}
printManyTimes("freeCodeCamp");
```

## 改变一个用 const 声明的数组

在现代的 JavaScript 里，`const`声明有很多用法。

一些开发者倾向默认使用`const`来声明所有变量，但如果它们打算在后续的代码中修改某个值，那在声明的时候就会用`let`。

然而，你要注意，对象（包括数组和函数）在使用`const`声明的时候依然是可变的。使用`const`来声明只会保证它的标识不会被重新赋值。

> "use strict";
> const s = [5, 6, 7];
> s = [1, 2, 3]; // 试图给 const 变量赋值，报错
> s[2] = 45; // 与用 var 或 let 声明的数组一样，这个操作也会成功
> console.log(s); // 返回 [5, 6, 45]

从以上代码看出，你可以改变`[5, 6, 7]`自身，所以`s`变量指向了改变后的数组`[5, 6, 45]`。和所有数组一样，数组`s`中的数组元素是可以被改变的，但是因为使用了`const`关键字，你不能使用赋值操作符将变量标识`s`指向另外一个数组。



------



这里有一个使用`const s = [5, 7, 2]`声明的数组。使用对各元素赋值的方法将数组改成`[2, 5, 7]`。

```js
const s = [5, 7, 2];
function editInPlace() {
  "use strict";
  // 在这行以下修改代码
  s[0]=2;
  s[1]=5;
  s[2]=7;

  // s = [2, 5, 7]; <- this is invalid

  // 在这行以上修改代码
}
editInPlace();
```

## 防止对象改变

通过之前的挑战可以看出,`const`声明并不会真的保护你的数据不被改变。为了确保数据不被改变，JavaScript 提供了一个函数`Object.freeze`来防止数据改变。

当一个对象被冻结的时候，你不能再对它的属性再进行增、删、改的操作。任何试图改变对象的操作都会被阻止，却不会报错。

> let obj = {
>  name:"FreeCodeCamp",
>  review:"Awesome"
> };
> Object.freeze(obj);
> obj.review = "bad"; // obj 对象被冻结了，这个操作会被忽略
> obj.newProp = "Test"; // 也会被忽略，不允许数据改变
> console.log(obj);
> // { name: "FreeCodeCamp", review:"Awesome"}



------



在这个挑战中，你将使用`Object.freeze`来防止数学常量被改变。你需要冻结`MATH_CONSTANTS`对象，使得没有人可以改变`PI`的值，抑或增加或删除属性。

```js
function freezeObj() {
  "use strict";
  const MATH_CONSTANTS = {
    PI: 3.14
  };
  // 在这行以下修改代码
  Object.freeze(MATH_CONSTANTS);


  // 在这行以上修改代码
  try {
    MATH_CONSTANTS.PI = 99;
  } catch( ex ) {
    console.log(ex);
  }
  return MATH_CONSTANTS.PI;
}
const PI = freezeObj();
```

## 使用箭头函数编写简洁的匿名函数

在 JavaScript 里，我们会经常遇到不需要给函数命名的情况，尤其是在需要将一个函数作为参数传给另外一个函数的时候。这时，我们会创建匿名函数。因为这些函数不会在其他地方复用，所以我们不需要给它们命名。

这种情况下，我们通常会使用以下语法：

> const myFunc = function() {
>  const myVar = "value";
>  return myVar;
> }

ES6 提供了其他写匿名函数的方式的语法糖。你可以使用箭头函数：

> const myFunc = () => {
>  const myVar = "value";
>  return myVar;
> }

当不需要函数体，只返回一个值的时候，箭头函数允许你省略`return`关键字和外面的大括号。这样就可以将一个简单的函数简化成一个单行语句。

> const myFunc= () => "value"

这段代码仍然会返回`value`。



------



使用箭头函数的语法重写`magic`函数，使其返回一个新的`Date()`。同时不要用`var`关键字来定义任何变量。

## 编写带参数的箭头函数

和一般的函数一样，你也可以给箭头函数传递参数。

> // 给传入的数值乘以 2 并返回结果
> const doubler = (item) => item * 2;

你同样可以给箭头函数传递多个参数。



------



使用箭头函数的语法重写`myConcat`函数，使其可以将`arr2`的内容填充在`arr1`里。

```js
// var myConcat = function(arr1, arr2) {
//   "use strict";
//   return arr1.concat(arr2);
// };
// 测试你的代码
const myConcat=(arr1,arr2)=>arr1.concat(arr2);
console.log(myConcat([1, 2], [3, 4, 5]));
```

## 编写高阶箭头函数

我们已经见识到了箭头函数在处理数据时候的强大之处。

箭头函数在类似`map()`，`filter()`，`reduce()`等需要其他函数作为参数来处理数据的高阶函数里会很好用。

阅读以下代码：

> FBPosts.filter(function(post) {
>  return post.thumbnail !== null && post.shares > 100 && post.likes > 500;
> })

我们写下了`filter`函数，并尽量保证可读性。现在让我们用箭头函数来写同样的代码看看：

> FBPosts.filter((post) => post.thumbnail !== null && post.shares > 100 && post.likes > 500)

这段代码完成了同样的任务，却变得更加简短易懂了。



------





## 设置函数的默认参数

为了帮助我们创建更灵活的功能，ES6引入了功能的默认参数。

查看以下代码：

```js
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John")); // Hello John
console.log(greeting()); // Hello Anonymous
```

如果未指定参数（未定义），则会启动默认参数。如您在上面的示例中看到的那样，当您不为参数提供`name`值`"Anonymous"`时，该参数将收到其默认值。您可以根据需要为任意多个参数添加默认值。

------

修改功能，`increment`通过添加默认参数，这样它会加1 `number`，如果`value`没有指定。

```js
// Only change code below this line
const increment = (number, value=1) => number + value;
// Only change code above this line
```

## 将Rest参数与Function参数一起使用

为了帮助我们创建更灵活的功能，ES6引入了rest参数作为功能参数。使用rest参数，您可以创建带有可变数量参数的函数。这些参数存储在一个数组中，以后可以从函数内部进行访问。

查看以下代码：

```js
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], { })); // You have passed 4 arguments.
```

其余的参数，无需检查`args`阵列，并允许我们申请`map()`，`filter()`并`reduce()`在参数阵列上。

------

`sum`使用rest参数修改函数，使函数`sum`可以接受任意数量的参数并返回其和

```js
const sum = (...args) => {
  return args.reduce((a, b) => a + b, 0);
}
console.log(sum(1,2,3));
console.log(sum(5));
console.log(sum());

```

## 使用Spread运算符就地评估数组

ES6引入了散布运算符，它使我们可以在需要多个参数或元素的地方扩展数组和其他表达式。

以下ES5代码`apply()`用于计算数组中的最大值：

```js
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr); // returns 89
```

我们不得不使用`Math.max.apply(null, arr)`因为`Math.max(arr)`退货`NaN`。`Math.max()`期望使用逗号分隔的参数，但不能使用数组。传播运算符使该语法更易于阅读和维护。

```js
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // returns 89
```

`...arr`返回解压缩的数组。换句话说，它*扩展*了数组。但是，散布运算符只能在原位工作，就像在函数的自变量或数组文字中一样。以下代码不起作用：

```js
const spreaded = ...arr; // will throw a syntax error
```

------

使用传播运算符将的所有内容复制`arr1`到另一个数组中`arr2`。

```js
const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;

arr2 = [...arr1];  // Change this line

console.log(arr2);
```

## 使用解构分配从对象中提取值

销毁分配是ES6中引入的特殊语法，用于整齐地分配直接从对象获取的值。

考虑以下ES5代码：

```js
const user = { name: 'John Doe', age: 34 };

const name = user.name; // name = 'John Doe'
const age = user.age; // age = 34
```

这是使用ES6解构语法的等效赋值语句：

```js
const { name, age } = user;
// name = 'John Doe', age = 34
```

在这里，将创建`name`和`age`变量，并从`user`对象中为其分配各自值的值。您可以看到这有多清洁。

您可以根据需要从对象中提取任意多个值。

------

用等效的解构分配替换这两个分配。它还是应该分配变量`today`和`tomorrow`值`today`，并`tomorrow`从`HIGH_TEMPERATURES`对象。

```js
const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};

// Only change code below this line
const {today,tomorrow}=HIGH_TEMPERATURES;

// Only change code above this line
```

## 使用解构分配从对象分配变量

解构允许您在提取值时分配新的变量名称。您可以通过在分配值时将新名称放在冒号后面来实现。

使用上一个示例中的相同对象：

```js
const user = { name: 'John Doe', age: 34 };
```

在分配中给新变量名称的方法如下：

```js
const { name: userName, age: userAge } = user;
// userName = 'John Doe', userAge = 34
```

您可以将其读为“获取的值`user.name`并将其分配给名为的新变量`userName`，以此类推。

------

用等效的解构分配替换这两个分配。它还是应该分配变量`highToday`和`highTomorrow`值`today`，并`tomorrow`从`HIGH_TEMPERATURES`对象。

```js
const HIGH_TEMPERATURES = {
  yesterday: 75,
  today: 77,
  tomorrow: 80
};

// Only change code below this line
const {today:highToday,tomorrow:highTomorrow} = HIGH_TEMPERATURES;

// Only change code above this line
```

## 使用解构分配从嵌套对象分配变量

您可以使用前两课中的相同原理，从嵌套对象中解构值。

使用类似于先前示例的对象：

```js
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```

以下是提取对象属性的值并将其分配给具有相同名称的变量的方法：

```js
const { johnDoe: { age, email }} = user;
```

这是将对象属性的值分配给具有不同名称的变量的方法：

```js
const { johnDoe: { age: userAge, email: userEmail }} = user;
```

------

用等效的解构分配替换这两个分配。它还是应该分配变量`lowToday`和`highToday`值`today.low`，并`today.high`从`LOCAL_FORECAST`对象。

```js
const LOCAL_FORECAST = {
  yesterday: { low: 61, high: 75 },
  today: { low: 64, high: 77 },
  tomorrow: { low: 68, high: 80 }
};

// Only change code below this line
const {today:{low:lowToday,high:highToday}}= LOCAL_FORECAST; 


// Only change code above this line
```

## 使用解构分配从数组分配变量

ES6使解构数组像解构对象一样容易。

扩展运算符和数组解构之间的一个关键区别是，扩展运算符将数组的所有内容解压缩为逗号分隔的列表。因此，您不能选择要选择分配给变量的元素。

解构数组可以让我们完全做到这一点：

```js
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b); // 1, 2
```

该变量`a`被分配数组的第一个值，并被`b`分配数组的第二个值。我们还可以通过使用逗号到达所需索引的方式来解构数组中任何索引的值：

```js
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c); // 1, 2, 5
```

------

使用解构赋值来交换的价值`a`，并`b`让`a`接收存储在值`b`，并`b`接收存储在值`a`。

```js
let a = 8, b = 6;
// Only change code below this line
[a,b]=[b,a];
```

## 使用带有Rest参数的解构分配来重新分配数组元素

在某些涉及数组解构的情况下，我们可能希望将其余元素收集到一个单独的数组中。

结果类似于`Array.prototype.slice()`，如下所示：

```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b); // 1, 2
console.log(arr); // [3, 4, 5, 7]
console.log(...arr);//3,4,5,7
```

变量`a`和`b`从数组中获取第一个和第二个值。之后，由于存在rest参数`arr`，因此以数组形式获取其余值。rest元素只能正确用作列表中的最后一个变量。与之类似，您不能使用rest参数来捕获一个子数组，该子数组会忽略原始数组的最后一个元素。

------

使用带有rest参数的解构赋值来执行有效操作，`Array.prototype.slice()`从而使`arr`原始数组的子数组`source`省略前两个元素。

```js
const source = [1,2,3,4,5,6,7,8,9,10];
function removeFirstTwo(list) {
  // Only change code below this line

  const [a,b,...arr] = list; // Change this line
  // Only change code above this line
  return arr;
}
const arr = removeFirstTwo(source);
```

## 使用解构分配将对象作为函数的参数传递

在某些情况下，您可以在函数参数本身中解构对象。

考虑下面的代码：

```js
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;
  // do something with these variables
}
```

这样可以有效地破坏发送到函数中的对象。这也可以就地完成：

```js
const profileUpdate = ({ name, age, nationality, location }) => {
  /* do something with these fields */
}
```

当`profileData`传递给上述函数时，这些值将从函数参数中解构出来，以供在函数内使用。

------

使用函数参数中解构赋值`half`只发送`max`和`min`在函数内部。

## 使用模板文字创建字符串`${}`

ES6的新功能是模板文字。这是一种特殊的字符串类型，可简化创建复杂字符串的过程。

模板文字使您可以创建多行字符串，并使用字符串插值功能来创建字符串。

考虑下面的代码

```js
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

// Template literal with multi-line and string interpolation
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting); // prints
// Hello, my name is Zodiac Hasbro!
// I am 56 years old.
```

使用带反引号的模板文字语法来创建列表元素（`li`）字符串数组。每个列表元素的文本应该是对象`failure`属性上的数组元素之一，`result`并具有一个`class`值为value的属性`text-warning`。该`makeList`函数应返回列表项字符串的数组。

使用迭代器方法（任何类型的循环）获得所需的输出（如下所示）。

```js
[
  '<li class="text-warning">no-var</li>',
  '<li class="text-warning">var-on-top</li>',
  '<li class="text-warning">linebreak</li>'
]
```

```js
const result = {
  success: ["max-length", "no-amd", "prefer-arrow-functions"],
  failure: ["no-var", "var-on-top", "linebreak"],
  skipped: ["no-extra-semi", "no-dup-keys"]
};
function makeList(arr) {
  "use strict";
  // change code below this line
  const failureItems = [];
  for (let i = 0; i < arr.length; i++) {
    failureItems.push(`<li class="text-warning">${arr[i]}</li>`);
  }
  // change code above this line
  return failureItems;
}

const failuresList = makeList(result.failure);
```



## 使用对象属性速记编写简洁的对象文字声明

ES6为轻松定义对象文字添加了一些不错的支持。

考虑以下代码：

```js
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
```

`getMousePosition`是一个简单的函数，它返回包含两个属性的对象。ES6提供了语法糖以消除必须写的冗余`x: x`。您只需编写`x`一次，即可在后台转换为`x: x`（或等效形式）。这是上面重写的相同函数，以使用此新语法：

```js
const getMousePosition = (x, y) => ({ x, y });
```

------

使用对象属性速记与对象文字创建并返回一个对象`name`，`age`和`gender`属性。

```js
const createPerson = (name, age, gender) => {
  // Only change code below this line
  return {
    name,
    age,
    gender,
  };
  // Only change code above this line
};
```

## 使用ES6编写简洁的声明性函数

在ES5中的对象中定义函数时，我们必须使用`function`如下关键字：

```js
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

使用ES6，可以`function`在对象中定义函数时完全删除关键字和冒号。这是此语法的示例：

```js
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

------

`setGear`在对象内部重构函数`bicycle`以使用上述速记语法。

```js
// Only change code below this line
const bicycle = {
  gear: 2,
  setGear(newGear){
   this.gear=newGear;
  }
};
// Only change code above this line
bicycle.setGear(3);
console.log(bicycle.gear);
```

## 使用类语法定义构造函数

ES6提供了使用class关键字创建对象的新语法。

应该注意的是，`class`语法只是语法，而不是像Java，Python，Ruby等语言那样，不是完整的基于类的面向对象范例实现。

在ES5中，我们通常定义一个构造函数，并使用`new`关键字实例化一个对象。

```js
var SpaceShuttle = function(targetPlanet){
  this.targetPlanet = targetPlanet;
}
var zeus = new SpaceShuttle('Jupiter');
```

该`class`语法仅替换构造函数的创建：

```js
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
}
const zeus = new SpaceShuttle('Jupiter');
```

应该注意的是，`class`关键字声明了一个新函数，并向其添加了构造函数。在调用`new`创建新对象时会调用此构造函数。
**笔记：**

- 如上所用，UpperCamelCase应按惯例用于ES6类名称`SpaceShuttle`。
- 构造函数方法是一种用于创建和初始化使用类创建的对象的特殊方法。您将在JavaScript算法和数据结构认证的“面向对象的程序设计”部分中了解更多信息。

------

使用`class`关键字并编写一个构造函数来创建`Vegetable`类。

该`Vegetable`级允许你创建一个蔬菜对象与属性`name`获取传递给构造函数。

```js
// Only change code below this line
class Vegetable{
    constructor(name){
        this.name=name;
    }
}
// Only change code above this line

const carrot = new Vegetable('carrot');
console.log(carrot.name); // Should display 'carrot'
```

## 使用getter和setter来控制对对象的访问

您可以从对象获取值，并在对象内设置属性的值。

这些被称为经典的getter和setter方法。

Getter函数旨在简单地向用户返回（获取）对象的私有变量的值，而无需用户直接访问私有变量。

设置器函数用于根据传递到设置器函数中的值来修改（设置）对象私有变量的值。此更改可能涉及计算，甚至完全覆盖先前的值。

```js
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book('anonymous');
console.log(novel.writer);  // anonymous
novel.writer = 'newAuthor';
console.log(novel.writer);  // newAuthor
```

请注意用于调用getter和setter的语法。它们甚至看起来都不像函数。获取器和设置器很重要，因为它们隐藏了内部实现细节。**注意：**按照惯例，私有变量的名称前必须带有下划线（`_`）。但是，实践本身并未将变量设为私有。

------

使用`class`关键字创建恒温器类。构造函数接受华氏温度。

在该类中，创建一个`getter`以获取摄氏度的温度，并创建一个以摄氏`setter`温度设置的温度。

请记住，`C = 5/9 * (F - 32)`和`F = C * 9.0 / 5 + 32`，`F`是华氏温度的值，并且`C`是摄氏温度的同一温度的值。

**注意：**实施此方法时，您将以华氏度或摄氏度为单位对类内的温度进行跟踪。

这就是吸气剂和吸气剂的力量。您正在为另一个用户创建API，无论您跟踪哪个用户，该用户都可以获得正确的结果。

换句话说，您正在从用户中提取实现细节。

```js
// Only change code below this line
class Thermostat{
    constructor(fahrenheit){
        this.fahrenheit=fahrenheit;
    }
    get temperature(){
        return (5 / 9) * (this.fahrenheit - 32);
    }
    set temperature(celsius){
        this.fahrenheit=(celsius * 9.0) / 5 + 32;
    }
}
// Only change code above this line

const thermos = new Thermostat(76); // Setting in Fahrenheit scale
let temp = thermos.temperature; // 24.44 in Celsius
thermos.temperature = 26;
temp = thermos.temperature; // 26 in Celsius
```

## 创建模块脚本

JavaScript最初只是扮演很小的角色，而在其他通常是HTML的网络中发挥作用。如今，它非常庞大，有些网站几乎完全使用JavaScript构建。为了使JavaScript更加模块化，干净和可维护；ES6引入了一种在JavaScript文件之间轻松共享代码的方法。这涉及导出文件的一部分以供一个或多个其他文件使用，并在需要的地方导入所需的部分。为了利用此功能，您需要在HTML文档中创建类型为的脚本`module`。这是一个例子：

```html
<script type="module" src="filename.js"></script>
```

使用此`module`类型的脚本现在可以使用`import`和`export`功能，您将在即将到来的挑战中了解这些功能。

------

将脚本添加到类型的HTML文档中，`module`并为其提供源文件`index.js`

```js
<html>
  <body>
    <!-- Only change code below this line -->
<script type="module" src="index.js"></script>
    <!-- Only change code above this line -->
  </body>
</html>
```

## 使用导出共享代码块

想象一下一个名为的文件`math_functions.js`，其中包含一些与数学运算有关的函数。其中之一存储在变量中，该变量`add`接受两个数字并返回其总和。您想在多个不同的JavaScript文件中使用此功能。为了与其他文件共享，首先需要`export`它。

```js
export const add = (x, y) => {
  return x + y;
}
```

上面是导出单个函数的常用方法，但是您可以实现如下相同的操作：

```js
const add = (x, y) => {
  return x + y;
}

export { add };
```

导出变量或函数时，可以将其导入另一个文件中并使用它，而无需重写代码。您可以通过对每个要导出的对象重复第一个示例，或将它们全部放入第二个示例的export语句中，来导出多个对象，如下所示：

```js
export { add, subtract };
```

------

编辑器中有两个与字符串相关的函数。使用您选择的方法将它们都导出。

```js
export const uppercaseString = (string) => {
  return string.toUpperCase();
}

export const lowercaseString = (string) => {
  return string.toLowerCase()
}
```

## 使用导入重用JavaScript代码

`import`允许您选择要加载文件或模块的哪些部分。在上一课中，示例`add`从`math_functions.js`文件中导出。您可以通过以下方式将其导入以在另一个文件中使用：

```js
import { add } from './math_functions.js';
```

在这里，`import`将`add`在中找到`math_functions.js`，仅导入该函数供您使用，而忽略其余部分。该`./`通知进口来寻找`math_functions.js`在同一个文件夹中当前文件的文件。以这种方式使用导入时，需要相对文件路径（`./`）和文件扩展名（`.js`）。

您可以通过在`import`语句中添加以下项来从文件中导入多个项：

```js
import { add, subtract } from './math_functions.js';
```

------

添加适当的`import`语句，该语句将允许当前文件使用您在上一课中导出的`uppercaseString`和`lowercaseString`函数。这些功能位于一个名为的文件中`string_functions.js`，该文件与当前文件位于同一目录中。

```js
import {uppercaseString,lowercaseString} from './string_functions.js';
// Only change code above this line

uppercaseString("hello");
lowercaseString("WORLD!");
```

## 使用*从文件导入所有内容

假设您有一个文件，并且希望将其所有内容导入当前文件。这可以通过`import * as`语法来完成。这是一个示例，其中名为的文件的内容`math_functions.js`被导入到同一目录中的文件中：

```js
import * as myMathModule from "./math_functions.js";
```

上面的`import`语句将创建一个名为的对象`myMathModule`。这只是一个变量名，您可以为它命名。该对象将包含其中的所有导出`math_functions.js`内容，因此您可以像访问任何其他对象属性一样访问这些函数。以下是使用导入的`add`和`subtract`函数的方法：

```js
myMathModule.add(2,3);
myMathModule.subtract(5,3);
```

------

该文件中的代码需要文件：的内容`string_functions.js`，即与当前文件位于同一目录中。使用`import * as`语法将文件中的所有内容导入名为的对象`stringFunctions`。

```js
// Only change code above this line
import * as stringFunctions from "./string_functions.js";
stringFunctions.uppercaseString("hello");
stringFunctions.lowercaseString("WORLD!");
```

## 使用导出默认值创建导出回退

在本`export`课程中，您了解了称为named export的语法。这使您可以在其他文件中使用多个函数和变量。

`export`您还需要了解另一种语法，称为export default。通常，如果仅从文件导出一个值，则将使用此语法。它还用于为文件或模块创建后备值。

以下是使用示例`export default`：

```js
// named function
export default function add(x, y) {
  return x + y;
}

// anonymous function
export default function(x, y) {
  return x + y;
}
```

由于`export default`用于声明模块或文件的后备值，因此每个模块或文件中只能将一个值作为默认导出。此外，您不能使用`export default`与`var`，`let`或`const`

------

以下功能应为模块的后备值。请添加必要的代码。

```js
export default function subtract(x, y) {
  return x - y;
}
```

## 导入默认导出

在上一个挑战中，您了解了`export default`它的用途。要导入默认导出，您需要使用其他`import`语法。在以下示例中，`add`是`math_functions.js`文件的默认导出。导入方法如下：

```js
import add from "./math_functions.js";
```

语法在一个关键位置上有所不同。导入的值`add`不在大括号（`{}`）内。`add`无论`math_functions.js`文件的默认导出是什么，这里都只是一个变量名。导入默认值时，您可以在此处使用任何名称。

------

在以下代码中，从与`math_functions.js`此文件位于相同目录的文件中导入默认导出。为导入命名`subtract`。

```js
import subtract from "./`math_functions.js`";
subtract(7,5);
```



## 创建JavaScript承诺

JavaScript中的承诺实际上就是它的含义-您可以使用它来承诺做某事，通常是异步的。任务完成后，您要么兑现了诺言，要么失败了。`Promise`是构造函数，因此您需要使用`new`关键字来创建一个。它以带有两个参数-`resolve`和的函数作为参数`reject`。这些是用于确定承诺结果的方法。语法如下所示：

```js
const myPromise = new Promise((resolve, reject) => {

});
```

------

创建一个名为的新承诺`makeServerRequest`。将带有`resolve`和`reject`参数的函数传递给构造函数。

```js
const makeServerRequest = new Promise((resolve,reject)=>{

});
```

## 通过决心和拒绝完成承诺

一诺有三种状态：`pending`，`fulfilled`，和`rejected`。您在上一个挑战中创建的承诺永远都停留在`pending`状态中，因为您没有添加完成承诺的方法。给promise参数提供的`resolve`和`reject`参数用于执行此操作。`resolve`当您希望诺言成功时使用，当您希望诺言`reject`失败时使用。这些是带有参数的方法，如下所示。

```js
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```

上面的示例使用字符串作为这些函数的参数，但实际上可以是任何东西。通常，它可能是一个对象，您可以使用其中的数据将其放置到您的网站或其他地方。

------

让诺言处理成功和失败。如果`responseFromServer`为`true`，则调用该`resolve`方法以成功完成承诺。传递`resolve`一个带有值的字符串`We got the data`。如果`responseFromServer`是`false`，请改用`reject`方法，并将其传递给字符串：`Data not received`。

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer represents a response from a server

  let responseFromServer;
    
  if(responseFromServer) {
    resolve("We got the data");
    // Change this line
  } else {  
    reject("Data not received");
    // Change this line
  }
});
```

## 然后处理一个兑现的承诺

当您有一个过程花费了您代码中未知时间（即异步的时间）（通常是服务器请求）时，承诺最有用。发出服务器请求时，它会花费一些时间，并且在完成请求后，您通常希望对服务器的响应进行处理。这可以通过使用该`then`方法来实现。使用`then`履行您的诺言后，立即执行该方法`resolve`。这是一个例子：

```js
myPromise.then(result => {
  // do something with the result.
});
```

`result`来自给该`resolve`方法的参数。

------

将`then`方法添加到您的承诺中。使用`result`它的回调函数的参数，并登录`result`到控制台。

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to true to represent a successful response from a server
  let responseFromServer = true;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});
makeServerRequest.then(result=>{
  console.log(result);
}); 
```

## 处理被捕的被拒承诺

`catch`是您的诺言被拒绝时使用的方法。它会在`reject`调用promise方法后立即执行。语法如下：

```js
myPromise.catch(error => {
  // do something with the error.
});
```

`error`是传递给`reject`方法的参数。

------

将`catch`方法添加到您的承诺中。使用`error`它的回调函数的参数，并登录`error`到控制台。

```js
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer is set to false to represent an unsuccessful response from a server
  let responseFromServer = false;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {
  console.log(result);
});
makeServerRequest.catch(error=>{
  console.log(error);
});
```

