# JavaScript 面试题 & 回答

> 本项目的面试题来源于 [sudheerj/javascript-interview-questions](https://github.com/sudheerj/javascript-interview-questions) 这个项目。一时兴起就动了翻译的念头，由于本人的JavaScript 功力尚浅，翻译的内容难免有误或不妥的地方，望请各位见谅。如果你喜欢这个项目， 请 Star， 更感谢你的 Pull Request。

### 目录

| 序号. | 问题 |
| --- | --------- | 
|1 | [JavaScript中创建对象有哪些方法？](#JavaScript中创建对象有哪些方法) |
|2 | [什么是原型链？](#什么是原型链) |
|3 | [call、apply和bind之间有什么区别？](#call、apply和bind之间有什么区别) |
|4 | [什么是JSON及其常见操作？](#什么是JSON及其常见操作) |
|5 | [数组slice方法的作用是什么？](#数组slice方法的作用是什么) |
|6 | [数组splice方法的作用是什么？](#数组splice方法的作用是什么) |
|7 | [slice和slice有什么区别？](#slice和slice有什么区别) |
|8 | [比较Object和Map？](#比较Object和Map) |
|9 | [==和===有什么区别？](#==和===有什么区别) |
|10 | [什么是lambda或箭头函数？](#什么是lambda或箭头函数) |
|11 | [什么是头等函数？](#什么是头等函数) |
|12 | [什么是一阶函数？](#什么是一阶函数) |
|13 | [什么是高阶函数？](#什么是高阶函数) |
|14 | [什么是一元函数？](#什么是一元函数) |
|15 | [什么是柯里化函数？](#什么是柯里化函数) |
|16 | [什么是纯函数？](#什么是纯函数) |
|17 | [let关键字的作用是什么？](#let关键字的作用是什么) |
|18 | [let和var有什么区别？](#let和var有什么区别) |
|19 | [以let作为关键字命名的原因是什么？](#以let作为关键字命名的原因是什么) |
|20 | [不报错的情况下如何在switch块中重新声明变量？](#不报错的情况下如何在switch块中重新声明变量) |
|21 | [什么是暂时性死区？](#什么是暂时性死区) |
|22 | [什么是立即执行函数？](#什么是立即执行函数) |
|23 | [使用模块化有什么好处？](#使用模块化有什么好处) |
|24 | [什么是memoization？](#什么是memoization) |
|25 | [什么是提升？](#什么是提升) |

1. #### JavaScript中创建对象有哪些方法？

    JavaScript中有以下几种创建对象的方法：

    1. **Object构造函数:**

    创建空对象的最简单方法是使用Object构造函数，目前不推荐这种方法。

    ```javascript
    var object = new Object();
    ```
     2. **Object的create方法:**

    Object的create方法通过将原型对象作为参数传递来创建新对象

    ```javascript
    var object = Object.create(null);
    ```

    3. **Object字面量语法:**

    对象字面量语法将null作为参数传递时等效于create方法

    ```javascript
       var object = {};
    ```

    4. **Function构造函数:**

    创建函数并用new运算符创建对象实例

    ```javascript
     function Person(name){
        var object = {};
        object.name=name;
        object.age=21;
        return object;
     }
     var object = new Person("Sudheer");
    ```

    5. **Function构造函数与原型:**

    这与Function构造函数类似，但它使用prototype作为其属性和方法，

    ```javascript
    function Person(){}
    Person.prototype.name = "Sudheer";
    var object = new Person();
    ```
    相当于使用带有函数原型的对象create方法创建的实例，然后使用实例和参数作为参数调用该函数。

    ```javascript
    function func {};

    new func(x, y, z);

    **或者**

    // Create a new instance using function prototype.
    var newInstance = Object.create(func.prototype)

    // Call the function
    var result = func.call(newInstance, x, y, z),

    // If the result is a non-null object then use it otherwise just use the new instance.
    console.log(result && typeof result === 'object' ? result : newInstance);
    ```

    6. **ES6 Class语法:**

    ES6引入了class特性来创建对象

    ```javascript
    class Person {
    constructor(name) {
        this.name = name;
    }
    }

    var object = new Person("Sudheer");
    ```

    7. **单例模式:**

    单例是一个只能实例化一次的对象。对其构造函数的重复调用返回相同的实例，这样就可以确保它们不会意外地创建多个实例。

    ```javascript
    var object = new function(){
    this.name = "Sudheer";
    }
    ```

**[⬆ 返回顶部](#目录)**

2. ### 什么是原型链？

**原型链**用于基于现有对象构建新类型的对象。它类似于基于class语言中的继承。对象实例上的原型可通过Object.getPrototypeOf（object）或__proto__属性获得，而构造函数上的原型可通过object.prototype获得。

**[⬆ 返回顶部](#目录)**

3. ### call、apply和bind之间有什么区别？

**Call:** call()方法调用指定this和依次传入参数的函数

```javascript
var employee1 = {firstName: 'John', lastName: 'Rodson'};
var employee2 = {firstName: 'Jimmy', lastName: 'Baily'};

function invite(greeting1, greeting2) {
    console.log(greeting1 + ' ' + this.firstName + ' ' + this.lastName+ ', '+ this.greeting2);
}

invite.call(employee1, 'Hello', 'How are you?'); // Hello John Rodson
invite.call(employee2, 'Hello', 'How are you?'); // Hello Jimmy Baily
```


**Apply:** 调用函数，允许你将参数作为数组传递。
```javascript
var employee1 = {firstName: 'John', lastName: 'Rodson'};
var employee2 = {firstName: 'Jimmy', lastName: 'Baily'};

function invite(greeting1, greeting2) {
    console.log(greeting1 + ' ' + this.firstName + ' ' + this.lastName+ ', '+ this.greeting2);
}

invite.apply(employee1, ['Hello', 'How are you?']); // Hello John Rodson, How are you?
invite.apply(employee2, ['Hello', 'How are you?']); // Hello Jimmy Baily, How are you?
```

**bind:** 返回一个新函数，允许你传入一个数组和多个参数
```javascript
var employee1 = {firstName: 'John', lastName: 'Rodson'};
var employee2 = {firstName: 'Jimmy', lastName: 'Baily'};

function invite(greeting1, greeting2) {
    console.log(greeting1 + ' ' + this.firstName + ' ' + this.lastName+ ', '+ this.greeting2);
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1('Hello', 'How are you?'); // Hello John Rodson, How are you?
inviteEmployee1('Hello', 'How are you?'); // Hello Jimmy Baily, How are you?
```
Call和apply可以相互转化。两者都立即执行当前函数。你需要决定传递数组还是以逗号分隔的参数列表传递哪个更容易。你可以记住：Call是以逗号分隔的参数列表传递，Apply是以数组作为参数传递。而Bind创建一个新函数，将其设置为传递给bind（）的第一个参数。

**[⬆ 返回顶部](#目录)**

4. ### 什么是JSON及其常见操作？

**JSON**是一种遵循JavaScript对象语法的基于文本的数据格式，由Douglas Crockford推广。当您想要通过网络传输数据时，它非常有用，它基本上只是一个扩展名为.json的文本文件，以及MIME类型为application / json的文本文件。

Parsing: 将字符串转换为原始对象

```javascript
JSON.parse(text)
```

Stringification: 将原始对象转换为字符串，以便可以通过网络传输

```javascript
JSON.stringify(object)
```

**[⬆ 返回顶部](#目录)**

5. ### 数组slice方法的作用是什么？

**slice()** 方法将数组中的选定元素作为新数组对象返回。它选择从给定的起始参数开始的元素，并在给定的可选结束参数处结束，而不包括最后一个元素。如果省略第二个参数，则选择直到结束。

这个方法的一些例子：

```javascript
let arrayIntegers = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegers.slice(2,2); // returns [1,2]
let arrayIntegers2 = arrayIntegers.slice(2,3); // returns [3]
let arrayIntegers3 = arrayIntegers.slice(4); //returns [4]
```

**Note:** Slice方法不会改变原始数组，但会将子集作为新数组返回。

**[⬆ 返回顶部](#目录)**

6. ### 数组splice方法的作用是什么？

**splice()** 方法用于添加/删除数组中元素，然后返回已删除的元素。第一个参数指定插入或删除的数组位置，而选项第二个参数指定要删除的元素个数。每个附加参数都会添加到数组中。

这个方法的一些例子：

```javascript
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0,2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c", 5]
```

**Note:** Splice方法修改原始数组并返回已删除的数组。

**[⬆ 返回顶部](#目录)**

7. ### slice和slice有什么区别？

以表格形式的展示一些主要区别

| Slice | Splice |
|---- | ---------
|不改变原始数组(immutable)  | 改变原始数组(mutable) |
| 返回原始数组的子集 | 将已删除的元素作为数组返回  |
| 用于从数组中选择元素 | 用于添加/删除数组中元素|

**[⬆ 返回顶部](#目录)**

8. ### 比较Object和Map？

**Objects** 和 **Maps** 类似，它们既可以设置键值，也可以检索这些值，删除键，并检测某些键是否存储在键中。由于这个原因，Objects历来被用作Maps。但是在某些情况下，更适合使用Map。

    1. Object的键是String和Symbol，而它们可以是Map的任何值，包括函数，对象和任何原始类型。

    2. Map中的键是按顺序添加，而object的键则不是。因此，当迭代时Map对象按插入顺序返回键。

    3. 你可以使用size属性很容易获取Map的大小，而Object的属性个数必须手动确定。

    4. Map是可迭代的，因此可以直接迭代，而迭代Object需要以某种方式获取其键并迭代它们。

    5. 一个对象有一个原型，所以如果你不小心， map中的默认键可能会与你的键发生冲突。从ES5开始，这可以通过使用map = Object.create（null）来避免，但很少这样做。

    6. 涉及到频繁添加和删除键值对的情况下，Map可能表现更好

**[⬆ 返回顶部](#目录)**

9. ### ==和===有什么区别？

JavaScript提供严格（===，!==）和类型转换（==，!=）相等比较。严格运算符考虑变量类型，而非严格运算符根据变量值进行类型校正/转换。对于不同类型，严格操作符遵循以下条件。

1. 当两个字符串具有相同的字符序列，相同的长度和在相应位置有相同的字符时,那么这两个字符严格相等。
2. 当两个数字在数值上相等，比如具有相同的数值,那么这两个数字严格相等。

    有以下两种特例

    1. NaN不等于任何值，包括NaN自己。
    2. 正负零彼此相等。
3. 如果两个布尔操作数都为真或两者都为假，则它们严格相等。
4. 如果两个对象引用相同的对象，则它们严格相等。
5. Null== Undefined，Null !== Undefined，null===undefined --> false但是null==undefined --> true

一些例子涵盖了上述案例

```javascript
0 == false   // true
0 === false  // false
1 == "1"     // true
1 === "1"    // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```

**[⬆ 返回顶部](#目录)**

10. ### 什么是lambda或箭头函数？

箭头函数是函数表达式的较短语法，并且没有自己的**this，arguments，super或new.target**。这些函数最适合非方法函数，不能用作构造函数。

**[⬆ 返回顶部](#目录)**

11. ### 什么是头等函数？

在Javascript中，函数是头等对象。头等函数意味着将该语言中的函数视为任何其他变量。例如，在这种语言中，函数可以作为参数传递给其他函数，可以由另一个函数返回，并可以作为值赋值给变量。例如，在下面的示例中，handle函数被赋值给一个listener
```javascript
const handler = () => console.log ('This is a click handler function');
document.addEventListener ('click', handler);
```

**[⬆ 返回顶部](#目录)**

12. ### 什么是一阶函数？

一阶函数是不接受其他函数作为参数，并且不返回函数作为其返回值的函数。

```javascript
const firstOrder = () => console.log ('Iam a first order functionn!');
```

**[⬆ 返回顶部](#目录)**

13. ### 什么是高阶函数？

高阶函数是一个接受其他函数作为参数或将函数作为返回值返回的函数。

```javascript
const increment = x => x+1;
const higherOrder = higherOrder(increment);
console.log(higherOrder(1));
```

**[⬆ 返回顶部](#目录)**

14. ### 什么是一元函数？

一元函数（列如monadic）是一个只接受一个参数的函数。让我们举一个函数的例子。它代表函数接受的单个参数

```javascript
const unaryFunction = a => console.log (a + 10); //Add 10 to the given argument and display the value
```

15. ### 什么是柯里化函数？

柯里化是一个带有多个参数的函数并将其转换为函数序列的过程，每个函数只有一个参数。 柯里化以数学家Haskell Curry命名。通过使用柯里化，n个参数的函数将其转换为一元函数。让我们举一个n-ary函数的例子以及它如何变成柯里化函数

```javascript
const multiArgFunction = (a, b, c) => a + b + c;
const curryUnaryFunction = a => b => c => a + b + c;
curryUnaryFunction (1); // returns a function: b => c =>  1 + b + c
curryUnaryFunction (1) (2); // returns a function: c => 2 + c
curryUnaryFunction (1) (2) (3); // returns the number 6
```
柯里化函数非常适合提升代码的可重用性和函数的组合。

**[⬆ 返回顶部](#目录)**

16. ### 什么是纯函数？
一个**纯函数**返回值仅由其参数决定而没有任何副作用的函数。例如，如果在应用程序中调用具有相同参数'n'次数和'n'位置数的函数，那么它将始终返回相同的值。让我们举一个例子来看看纯函数和非纯函数之间的区别。

```javascript
//Impure
let numberArray = [];
const impureAddNumber = number => numberArray.push (number);
//Pure
const pureAddNumber = number => argNumberArray =>
  argNumberArray.concat ([number]);

//Display the results
console.log (impureAddNumber (6)); // returns 6
console.log (numberArray); // returns [6]
console.log (pureAddNumber (7) (numberArray)); // returns [6, 7]
console.log (numberArray); // returns [6]
```

正如上面的代码片段所示，Push函数通过修改数组并返回一个与参数值无关的 Push 数索引而使自身变得不纯。 另一方面，Concat 接受数组并将其与另一个数组连接起来，生成一个没有副作用的全新数组。 此外，返回值是前一个数组的串联。

请记住，纯函数很重要，因为它们简化了单元测试，没有任何副作用，也不需要依赖注入。 它们还避免了紧密耦合，并且由于没有任何副作用，使得破坏应用程序更加困难。 这些原则与 ES6的**Immutability**概念一起使用，优先使用**const**而不是**let**。

**[⬆ 返回顶部](#目录)**

17. ### let关键字的作用是什么？

let语句声明**块作用域局部变量**。因此，使用 let 关键字定义的变量范围仅限于使用它的块、语句或表达式。 而使用var关键字声明的变量则用于全局定义变量，或者局部定义整个函数，而与块作用域无关

```javascript
let counter = 30;
if (counter === 30) {
  let counter = 31;
  console.log(counter); // 31
}
console.log(counter); // 30 (because if block variable won't exist here)
```

**[⬆ 返回顶部](#目录)**

18. ### let和var有什么区别？

| var | let |
|---- | ---------
| 它从JavaScript开始就可以使用  | 作为 ES6的一部分引入 |
| 它有函数作用域 | 它有块作用域  |
| 变量会被提升 | 变量不会被提升|

让我们举个例子来看看它们之间的区别

```javascript
function userDetails(username) {
   if(username) {
     console.log(salary); // undefined(due to hoisting)
     console.log(age); // error: age is not defined
     let age = 30;
     var salary = 10000;
   }
   console.log(salary); //10000 (accessible to due function scope)
   console.log(age); //error: age is not defined(due to block scope)
}
```

**[⬆ 返回顶部](#目录)**

19. ### 以let作为关键字命名的原因是什么？

    Let是早期编程语言（如Scheme和Basic）采用的数学语句。它是从许多其他语言中借用的，这些语言使用let作为传统关键字尽可能接近var。

**[⬆ 返回顶部](#目录)**

20. ### 不报错的情况下如何在switch块中重新声明变量？

    如果您尝试在`switch block`中重新声明变量，那么它将导致错误，因为只有一个块。例如，下面的代码块抛出了如下所示的语法错误。

    ```javascript
    let counter = 1;
    switch(x) {
    case 0:
        let name;
        break;

    case 1:
        let name; // SyntaxError for redeclaration.
        break;
    }
    ```

    为了避免此错误，可以在case子句中创建嵌套块，这将创建一个新的块作用域的词法环境。

    ```javascript
    let counter = 1;
        switch(x) {
          case 0: {
            let name;
            break;
          }
          case 1: {
            let name; // No SyntaxError for redeclaration.
            break;
          }
        }
    ```

**[⬆ 返回顶部](#目录)**

21. ### 什么是暂时性死区？

    暂时死区是JavaScript 中的一种行为，它发生在使用let 和 const 关键字声明变量时，而不是使用 var。 在 ECMAScript 6中，在变量声明(在其作用域内)之前访问 let 或 const 变量会导致 ReferenceError 错误。 发生这种情况的时间跨度，从创建变量的绑定到它的声明，称为时间死区。让我们用一个例子来看看这种行为。

     ```javascript
    function somemethod() {
      console.log(counter1); // undefined
      console.log(counter2); // ReferenceError
      var counter1 = 1;
      let counter2 = 2;
    }
    ```

**[⬆ 返回顶部](#目录)**

22. ### 什么是立即执行函数？

    IIFE（立即调用函数表达式）是一个JavaScript函数，它在定义后立即执行。

    ```javascript
    (function ()
        {
          // logic here
        }
     )
    ();
    ```

    使用 IIFE 的主要原因是为了获得数据私有性，因为 IIFE 中声明的任何变量都不能被外界访问。如果你试图通过 IIFE 访问变量，则会抛出如下错误。

     ```javascript
    (function ()
            {
              var message = "IIFE";
              console.log(message);
            }
     )
    ();
    console.log(message); //Error: message is not defined
    ```

**[⬆ 返回顶部](#目录)**

23. ### 使用模块化有什么好处？

    使用模块有利于扩展，有很多好处。其中一些好处是
    1. 可维护性
    2. 可重用性
    3. 命名空间

**[⬆ 返回顶部](#目录)**

24. ### 什么是memoization？

    Memoization是一种编程技术，它试图通过缓存先前计算的结果来提高函数的性能。每次调用memoized函数时，都会使用其参数对缓存进行索引。 如果数据存在，则可以返回数据，而无需执行整个函数。 否则将执行该函数，然后将结果添加到缓存中。让我们举一个用memoization添加函数的例子。

    ```javascript
    const memoizAddition = () => {
      let cache = {};
     return (value) => {
      if (value in cache) {
       console.log('Fetching from cache');
       return cache.value;
      }
      else {
       console.log('Calculating result');
       let result = value + 20;
       cache[value] = result;
       return result;
      }
     }
    }
    // returned function from memoizAddition
    const addition = memoizAddition();
    console.log(addition(20)); //output: 40 calculated
    console.log(addition(20)); //output: 40 cached
    ```

**[⬆ 返回顶部](#目录)**

25. ### 什么是提升？

    提升是一种JavaScript机制，其中变量和函数声明在代码执行之前被移动到其作用域的顶部。请记住，JavaScript只提升声明，而不是初始化。让我们举一个变量提升的简单例子。

    ```javascript
    console.log(message); //output : undefined
    var message = ’The variable Has been hoisted’;
    ```
    对于解释器来说，上面的代码如下所示。

    ```javascript
    var message;
    console.log(message);
    message = ’The variable Has been hoisted’;
    ```

**[⬆ 返回顶部](#目录)**



























































