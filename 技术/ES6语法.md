# ES6语法

## 三元表达式

**语法**

- **boolean_expression ? true_value : false_value;**
- boolean_expression: 布尔表达式，表达式在参与三元运算中必须求得一个布尔类型的值，要么是 true，要么是 false，结果作为判断依据，判断到底去：前面的值还是后面的值
- true_value：布尔表达式的值为真时，三元表达式的结果
- false_value：布尔表达式的值为假时，三元表达式的结果
- 作用：根据布尔表达式的结果，如果为真，三元表达式结果就是真值，如果为假，三元表达式结果就是假值

```js
    var a = 3;
    var b = a >= 3 ? true : false
    console.log(b); // true
```



## Let、const和var

1. 作用域

   let作用于let命令所在的代码块;

   var在全局范围内有效

2. 变量提升

   var存在变量提升,

   let无法变量提升

   ~~~js
   // var 的情况
   console.log(foo); // 输出undefined
   var foo = 2;
   
   // let 的情况
   console.log(bar); // 报错ReferenceError
   let bar = 2;
   ~~~

3. 暂时性死区

   ~~~js
   var tmp = 123;
   
   if (true) {
     tmp = 'abc'; // ReferenceError
     let tmp;
   }
   ~~~



## 变量的解构赋值

### 解构赋值的含义:

解构:ES6按照一定的模式,从数组和对象中提取值,对变量进行赋值,被称为解构.本质上属于'模式匹配'



## 对象字面量的增强写法



~~~js
1.属性的增强写法
const name = 'why';
const age = 18;

//ES5写法
const obj = {
 name:name,
 age:age
}

//ES6写法
const obj = {
  name,
	age
}

2.函数增强写法
//ES5写法
const obj = {
	run:function(){

},
eat :function(){

}
}

//ES6写法
const obj = {
	run(){

},
	eat(){

}
}
~~~





## async 和 await 使用总结

1. ==async== 放在函数声明前面, 成为async function, 异步函数:

    

    ```js
    function hello() {return "hello" };
    hello();   //返回"hello"
    ```

    

    如果将该函数变为异步函数:

    ```js
    async function hello() {return "hello" };
    hello();
    
    // 异步函数表达式, 如下所示:
    let hello = async function() { return "hello" };
    hello();
    
    // 使用箭头函数
    let hello = async () => { return "hello" }
    ```

     现在调用该函数会返回一个promise. 这是异步函数的特征之一 ,他保证函数的返回值为 promise

    

    要实际使用promise完成返回的值,我们可以使用 .then()块, 因为他返回的是prmise:

    ```js
    hello().then((value) => console.log(value))
    
    // 简写
    hello().then(conosle.log)
    ```

    

 

1. ==await== 关键字只在异步函数中才起作用

    他可以放在任何异步的, 基于 promise 的函数之前。它会暂停代码在该行上，直到 promise 完成，然后返回结果值。在暂停的同时，其他正在等待执行的代码就有机会执行了。

    ```js
    async function hello() {
      return greeting = await Promise.resolve("Hello");
    };
     
    hello().then(alert);
    
    ```

    去除了到处是.then()代码块!

    

    不需要附加 .then() 代码块到每个promise-based方法的结尾，你只需要在方法调用前添加 await 关键字，然后把结果赋给变量。await 关键字使JavaScript运行时暂停于此行，允许其他代码在此期间执行，直到异步函数调用返回其结果。一旦完成，您的代码将继续从下一行开始执行。



# 方法

## 字符串

### replace

JavaScript中replace() 方法如果直接用str.replace("-","!") 只会替换第一个匹配的字符. 而str.replace(/\-/g,"!")则可以全部替换掉匹配的字符(g为全局标志)。 

所以可以用以下几种方式.：
				string.replace(/reallyDo/g, replaceWith);
				string.replace(new RegExp(reallyDo, 'g'), replaceWith);

string：字符串表达式包含要替代的子字符串。
			reallyDo：被搜索的子字符串。
			replaceWith：用于替换的子字符串。

str.replace("-","!") 替换str中第一次出现的"-"为"!";

str.replace(/\-/g,"!")替换str中所有的"为"!";
