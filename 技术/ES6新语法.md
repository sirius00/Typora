# ES6语法

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

