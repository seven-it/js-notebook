# js基础知识总结笔记
关于js 原型 原型链 作用域等知识的理解笔记
## 目录
#### 01 js变量
* [01-01](https://github.com/TYRMars/JSlearn#01-01) `什么是变量`
* [01-02](https://github.com/TYRMars/JSlearn#01-01) `js变量的声明`
* [01-03](https://github.com/TYRMars/JSlearn#01-01) `js变量特性`
* [01-04](https://github.com/TYRMars/JSlearn#01-01) `js变量类型`
* [01-04-01](https://github.com/TYRMars/JSlearn#01-01) `js变量类型之值类型`
* [01-04-02](https://github.com/TYRMars/JSlearn#01-01) `js变量类型之引用类型`
* [01-04-03](https://github.com/TYRMars/JSlearn#01-01) `js变量类型之基本包装类型`

# 笔记内容
---
## 01-01
#### 什么是变量
* 变量是一个值的符号名称，可以通过名称来获得对值得引用，每个变量仅仅是一个用来保存值得占位符而已；
## 01-02
#### js变量的声明
    分两种情况 1.使用var 关键字 2.不使用var 关键字
    1.使用 var  关键字来声明变量
        如果是在函数中 那么变量就是私有变量，函数执行完毕就销毁；
    2.不使用var 来声明变量，该变量就会成为全局变量，任何地方都可以访问到；
```javascript
//下面代码可以看出无论函数是否已经调用，在函数外部都无法访问到message变量
function test(){
    var message = 'hi';
}
console.log(message); //Uncaught ReferenceError: message is not defined;
test();
console.log(message); //Uncaught ReferenceError: message is not defined;
-----分隔符-------------------------------------------------------------
//没有var 关键字，变量属于全局
function test(){
     message = 'hi';
}
test();
console.log(message);// 'hi'
```
这里需要注意的是 ，变量必须要用var (es6 用let)来声明变量，避免出现全局变量！！！
## 01-03
#### javascript 变量的特性   
    1.js变量是松散类型的，或者叫做无类型的，可以被赋予任何类型的值；
```javascript
var vb;
  vb = 'str';
  vb = 123;
  vb = true;
  vb = {};
  vb = [];
  vb = function (){};
  vb = null;
  vb = undefined;
```
    2. 变量只声明未赋值 返回Undefined;
```javascript
var message;
    console.log(message)// undefined;
```
    3.变量未声明就调用会报错；
```javascript
//var message;
    console.log(message)//Uncaught ReferenceError: message is not defined
```
    4.一条语句可以声明多个变量
```javascript
function test(){
  //下面的声明方式是完全没问题的
    var  message = 'hi',
      found = false,
      age = 29;
}
test();
console.log(message);//报错
console.log(found);//报错
console.log(age);//报错

//这说明使用这种方式声明的变量与单个var来声明变量的作用是同样的;
```   
## 01-04
#### javascript 变量类型
*概览
    javascript 变量类型分为值类型（也叫基本类型）与引用类型，这两个是按照内存地址来划分的;
    值类型
      string,number,boolean,undefined,null
    引用类型
      Object
        细分的话包括 对象{} ，数组[] , 函数 function
*细说值类型
    值类型 ：也就是基本类型，不同的值类型 内存地址也不一样；
```javascript
var num1 = 5;
var num2 = num1;
num1 = 10;
console.log(num2)// 5

//从上面代码可以看出  a 与 b两个变量的内存地址是不一样的，修改a 的值不会改变b ;
//原因：这是因为当一个变量从另一个变量复制基本类型的值时，会在变量对象上创建一个新值，然后把该值分配到新变量的位置上
```
    参考下图
![image](https://github.com/seven-it/js-/raw/master/images/1.jpg)
*细说引用类型
    引用类型： 它表示的是由多个值所组成的对象，变量只是一个指向它内存地址的指针；
```javascript
var a = {age:29};
var b = a;
a.age = 30;
console.log(b.age)//30
console.log(a === b) //true

//面代码可以看出，a 与 b 的指针都指向了相同的对象；
//因为 我们将a变量赋值给了b，这等于是将a的指针赋值给了b; 所以 修改他们任何一个都会影响另一个；
```

