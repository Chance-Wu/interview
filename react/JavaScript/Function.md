每个 JavaScript 函数实际上都是一个 `Function` 对象。运行 `(function(){}).constructor === Function // true` 便可以得到这个结论。



#### 1. 构造函数

---

>`Function` 构造函数创建一个新的Function对象。直接调用此构造函数可以动态创建函数，但是会遇到和eval类似的安全问题和性能问题。然而，与eval不同的是，**Function创建的函数只能在全局作用域中运行**。
>
>语法：`new Function ([arg1[, arg2[, ...argN]],] functionBody)`
>
>```javascript
>const sum = new Function('a', 'b', 'return a + b');
>
>console.log(sum(2, 6));
>// expected output: 8
>```



#### 2. 描述

---

>使用Function构造器生成的Function对象是**在函数创建时解析**的。这比使用<u>函数声明</u>或者<u>函数表达式</u>并在代码中调用更为低效。
>
>以调用函数的方式调用Function的构造函数（`(function(){}).constructor`）跟以构造函数来调用是一样的。



#### 3. 属性和方法

---

全局的Function对象没有自己的属性和方法，但是，因为他本身也是一个函数，所以它也会**通过原型链从自己的原型链`Function.prototype`上继承一些属性和方法**。



#### 4. 原型对象

---

>属性：
>
>- `Function.arguments`：以数组形式获取传入函数的所有参数。此属性已被arguments替代。
>- `Function.caller`：获取调用函数的具体对象。
>- `Function.length`：获取函数的接收参数个数。
>- `Function.name`：获取函数的名称。
>- `Function.displayName`：获取函数的display name。
>- `Function.prototype.constructor`：声明函数的原型构造方法。

>方法：
>
>- [`Function.prototype.apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)：在一个对象的上下文中应用另一个对象的方法；参数能够以数组形式传入。
>
>- [`Function.prototype.bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)：**bind()方法会创建一个新函数，称为绑定函数**。当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind()方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。
>
>- [`Function.prototype.call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)：在一个对象的上下文中应用另一个对象的方法；参数能够以列表形式传入。
>
>- `Function.prototype.isGenerator()`：`若函数对象为`[generator](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Iterators_and_Generators)，返回true，反之返回 `false`。
>
>- [`Function.prototype.toSource()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/toSource) ：获取函数的实现源码的字符串。 覆盖了 [`Object.prototype.toSource`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toSource) 方法。
>
>- [`Function.prototype.toString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/toString)：获取函数的实现源码的字符串。覆盖了 [`Object.prototype.toString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) 方法。
>
>- 
>
>  `若函数对象为`[generator](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Iterators_and_Generators)，返回true，反之返回 `false`。
>
>  [`Function.prototype.toSource()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/toSource) 
>
>  获取函数的实现源码的字符串。 覆盖了 [`Object.prototype.toSource`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toSource) 方法。
>
>  [`Function.prototype.toString()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/toString)
>
>  获取函数的实现源码的字符串。覆盖了 [`Object.prototype.toString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) 方法。



#### 5. 实例

---

Function实例从`Function.prototype`继承了一些属性和方法。同其他构造函数一样，你可以改变构造函数的原型从而使得所有的Function实例的属性和方法发生改变。



#### 6. 示例

---

>传入参数调用Function构造函数：
>
>```javascript
>// 创建了一个能返回两个参数和的函数
>const adder = new Function("a", "b", "return a + b");
>
>// 调用函数
>adder(2, 6);
>```

>Function构造器与函数声明之间的不同：
>
>由 `Function` 构造器创建的函数不会创建当前环境的闭包，它们总是被创建于全局环境，因此在运行时它们只能访问全局变量和自己的局部变量，不能访问它们被 `Function` 构造器创建时所在的作用域的变量。
>
>```javascript
>var x = 10;
>
>function createFunction1() {
>  var x = 20;
>  return new Function('return x;'); // 这里的 x 指向最上面全局作用域内的 x
>}
>
>function createFunction2() {
>  var x = 20;
>  function f() {
>    return x; // 这里的 x 指向上方本地作用域内的 x
>  }
>  return f;
>}
>
>var f1 = createFunction1();
>console.log(f1());          // 10
>var f2 = createFunction2();
>console.log(f2());          // 20
>```
>
>虽然这段代码可以在浏览器中正常运行，但在 Node.js 中 `f1()` 会产生一个“找不到变量 `x` ”的 `ReferenceError`。这是因为在 Node 中顶级作用域不是全局作用域，而 `x` 其实是在当前模块的作用域之中。

