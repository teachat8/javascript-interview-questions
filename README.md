# JavaScript 面试题 & 回答

> 本项目的面试题来源于 [sudheerj/javascript-interview-questions](https://github.com/sudheerj/javascript-interview-questions) 这个项目。一时兴起就动了翻译的念头，由于本人的JavaScript 功力尚浅，翻译的内容难免有误或不妥的地方，望请各位见谅。如果你喜欢这个项目， 请 Star， 更感谢你的 Pull Request。

### 目录
<!--TOC-->
| 序号. | 问题 |
| --- | ---------- |
|1 | [JavaScript中创建对象有哪些方法？](#JavaScript中创建-对象有哪些方法) |
|2 | [什么是原型链？](#什么是-原型链) |
|3 | [Call、Apply和Bind之间有什么区别？](#Call、Apply和Bind之间有什么区别) |
|4 | [什么是JSON及其常见操作？](#什么是JSON及其常见操作) |
|5 | [数组slice方法的作用是什么？](#数组-slice方法的作用是什么) |
|6 | [数组splice方法的作用是什么？](#数组-splice方法的作用是什么) |
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
<!--/TOC-->

1. ### JavaScript中创建对象有哪些方法？

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
























