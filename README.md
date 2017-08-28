# js基础知识总结笔记
关于js 原型 原型链 作用域等知识的理解笔记
## 目录
#### 01 js变量
* [01-01](https://github.com/seven-it/js-notebook#01-01) `什么是变量`
* [01-02](https://github.com/seven-it/js-notebook#01-02) `js变量的声明`
* [01-03](https://github.com/seven-it/js-notebook#01-03) `js变量特性`
* [01-04](https://github.com/seven-it/js-notebook#01-04) `js变量类型`
* [01-05](https://github.com/seven-it/js-notebook#01-05) `js变量类型之基本包装类型`
#### 02 js对象
* [02-01](https://github.com/seven-it/js-notebook#02-01) `什么是对象`
* [02-02](https://github.com/seven-it/js-notebook#02-02) `typeof操作符`
* [02-03](https://github.com/seven-it/js-notebook#02-03) `js中真的一切皆对象么`
* [02-04](https://github.com/seven-it/js-notebook#02-04) `js特殊对象 null`

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
* 概览

    javascript 变量类型分为值类型（也叫基本类型）与引用类型，这两个是按照内存地址来划分的;
    
    值类型
    
      string,number,boolean,undefined,null
      
    引用类型
    
      Object
        细分的话包括 对象{} ，数组[] , 函数 function
        
* 细说值类型

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
    ![img](https://github.com/seven-it/js-/raw/master/images/1.jpg)
    
* 细说引用类型

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
    参考下图
    ![img](https://github.com/seven-it/js-/raw/master/images/2.jpg)
    
```javascript
//如果不将a赋值给b ;那么b也就没有了指向a的指针
var a = {age:29};
var b = {age:29};
a.age = 30;
console.log(b.age)//29
console.log(a === b) //false
//从上面代码可以看出来，修改了a所指向对象的属性值，并不会影响到b;
//这说明，即使两个对象长的一模一样，但是他们的内存地址是不一样的；
//他们的指针所指向的地址也是不一样的；
```
* 另一种写法

    大家都知道  var a = {};这种写法叫做对象字面量；
    
    还有一种是用new 来创建对象；这是利用构造函数来创建对象
```javascript
    function Foo(name){
        this.name = name
    }

    var f = new Foo(); //相当于 var f = {};
    var d = f; //相当于 var d = f;
    d.age = 29; 
    console.log('age' in f)//true
    console.log('age' in d)//true
    //上面代码指向同一个内存地址，两者之间相互影响
    function Foo(name){
      this.name = name
    }

    var f = new Foo(); //相当于 var f = {};
    var d = new Foo(); //相当于 var d = {};
    d.age = 29; 
    console.log('age' in f)//false
    console.log('age' in d)//true

    //上面代码 指针 指向 各自 对应的对象地址，两者之间互不影响
```
    问题 为什么 推荐使用对象字面量方法来创建对象，而不使用new方法；
## 01-05 
#### javascript 基本包装类型
    1.动态属性
    
    值类型无法添加动态属性；
```javascript
    var a = 'str';，
    a.age = 20;，
    console.log(a.age) //undefined;，
    //上面代码显示 ，我们无法动态的为值类型动态的添加属性；
```

    引用类型添加属性和方法，引用类型是可以读写的，所以可以写入方法与属性
```javascript
    var a = {};
    a.age = 20;
    console.log(a.age) //20
```
    2.基本包装类型
    
    上面我们说值类型无法添加动态属性,但是 String Number 和 Boolean 却拥有自己的方法和属性;
    
    例如
```javascript
    var a = 'str';
    var b = a.substring(2)
    console.log(b)//r
    console.log(a.length)//3
```
    这是因为 js为了让人们方便操作基本类型的值,并且为了让我们实现这种直观的操作！后台已经自动完成了一系列的处理。
    当第二行代码访问 a 时，访问过程处于一种读取模式，也就是从内存中读取这个字符串的值。
    而在读取模式中访问字符串时，后台都会自动完成下列处理。
    
        1.创建 String 类型的一个实例；

        2.在实例上调用指定的方法；

        3.销毁这个实例。

        代码表示为
        var s1=new String("some text");  
        var s2=s1.substring(2);  
        s1=null; 
* 基本包装类型 与 引用类型的区别
    
    基本包装类型与引用类型的区别在于 对象的生存期，基本包装类型自动生成的对象只存在于代码执行的一瞬间
```javascript
    var a = 'str';
    a.age = 20;
    console.log(a.age) //undefined;
    //上面代码之所以返回Undefined
    //因为对象在到达第三行之前就已经被销毁，第三行执行的是重新创建的包装对象，而这个对象没有age属性，返回Undefined
    //我们来进一步解析代码
    
    var a = 'str';
    a.age = 20;//执行到这一步的时候 ,发生了下面的情况
    {
        var a = new String('str');
        a.age = 20;
        a = null;
        //对象已销毁
    }
    console.log(a.age) //undefined;
    //当我执行console时,后台重新操作基本包装类型，但是这时候的对象是一个新对象，没有age属性，返回Undefined；
    console.log(
        {
           var a = new String('str');
            //新对象没有 age属性 返回Undefined   
        }
    )
```
    上面就是整个包装对象 运行的流程
    
* 注意
    
        我们也可以通过 Boolean、Number 和 String 来创建基本包装类型的对象，
        不过，应该在绝对必要的情况下再这样做，
        因为这种做法很容易让人分不清自己是在处理基本包装类型还是引用基本包装类型的值。
        对基本包装类型的实例调用 typeof 会返回 “object”，
        而且所有基本包装类型的对象都会被转换为布尔值 true。
        
```javascript
        var obj=new Object("some text");  
		alert(obj instanceof String);//true
```

* 把字符串传给 Object 构造函数，就会创建 String 的实例；
* 而传入数值参数会得到Number 的实例，
* 传入布尔值参数就会得到 Boolean 的实例。
        
        要注意的是，使用 new 调用基本包装类型的构造函数，与直接调用同名的转型函数是不一样的。例如：
```javascript
        var value="25";  
        var number=Number(value); //转型函数  
        alert(typeof number); //"number"  
        var obj=new Number(value); //构造函数  
        alert(typeof obj); //"object" 
        //在这个例子中，变量 number 中保存的是基本类型的值 25，而变量 obj 中保存的是Number 的实例。
```        

		通过显示的创建 包装类型 可以为其添加属性与方法；
```javascript
        var a = new String('sss');
        a.age = 50
        console.log(a.age)//50
        console.log(typeof a)//"object"  
```

* ECMAScript提供了三个基本包装类型；分别是String Number 和 Boolean；它们分别内置了自己的方法和属性；
* 尽管我们不建议显式的创建基本包装类型的对象，但它们操作基本类型值的能力还是相当重要的。
* 而每个基本包装类型都提供了操作相应值的便捷方法。
* 基本包装类型是只能读取而无法写入的；
---   
## 02-01
#### 什么是对象

	对象就是属性与方法的集合
## 02-02
#### typeof操作符
	typeof 操作符 用来检测 数据类型是基本类型还是引用类型
```javascript
	通过typeof可以就可以检测出；
	var str = 'aaa';
	var num = 123;
	var blo = true;
	var und = undefined;
	var nul = null;
	var obj = {};
	var arr = [];
	var fn = function(){};

	console.log(typeof str);//string
	console.log(typeof num);//number
	console.log(typeof blo);//boolean
	console.log(typeof und);//undefined
	console.log(typeof nul);//object
	console.log(typeof obj);//object
	console.log(typeof arr);//object
	console.log(typeof fn);//function
```

	通过typeof我们可以区分出基本类型与引用类型，但是我们想去细分引用类型时 typeof就不是很给力了
	这时我们就应该通过 instanceof 来去检测引用类型
```javascript
	var arr = [];
	var obj = {};
	var fn = function (){};

	console.log(arr instanceof Array)
	console.log(obj instanceof Object)
	console.log(fn instanceof Function)

	console.log(arr instanceof Object)
	console.log(obj instanceof Object)
	console.log(fn instanceof Object)
	
	//得到的结果都是 true
```

	在这里我们有一个问题，typeof 为什么会检测出 function ，而 instanceof 检测fn 返回 Object 为真
	揭秘：
	函数实际上也是对象，每个函数都是Function类型的实例，
	并且与其它引用类型一样具有属性和方法，而函数名实际也是一个指向函数对象的指针；
	JavaScript把函数当成一种数据类型，可以像其他类型的数据一样，进行赋值和传递，这为编程带来了很大的灵活性，
	体现了JavaScript作为“函数式语言”的本质
	例如：
```javascript
	function fn (){
		alert(1);
	}
	
	//我们为它添加一个name属性
	fn.name = 'fn';
	
	//访问它的属性
	console.log(fn.name)//'fn'

	//我们还可以为它添加一个方法
	fn.a = function (){
		alert(2)
	}
	fn.a()// 2

	//由于typeof只能检测基本类型，我们想要检测引用类型就要使用instanceof操作符
	console.log(fn instanceof Object)//true
	console.log(fn instanceof Function)//true

	//由此我们可以得出 函数也是对象的一种；
```	

	其实这里我们还可以引出一个问题
	为什么string,number,boolean是基本类型，但是他们拥有方法和属性；
	因为在js中存在一种特殊的对象，基本包装对象，它与对象的区别在与生存周期
	具体可以看一下上面关于包装类型的描述
* [点击查看01-05 基本包装类型](https://github.com/seven-it/js-notebook#01-05)

## 02-03
#### js中真的一切皆对象么？
	答案显然是否定的，这里的一切皆对象仅仅是泛指
	
	在我看来 真正的对象仅仅是引用类型而已 对象{} ， 数组[] ,函数 fn;
	至于基本包装对象，说它是对象它也是，说它不是也可以不是，存在时间那么短，谁在乎呢！
	null ,准确来说他是个值类型，并且真的有且仅有一个值 就是 null,姑且算它是特殊的对象吧（毕竟要给typeof一个面子的）
	那么 undefined 呢，人家就只有一个值 Undefined，而且是标准的值类型，和对象压根不搭嘎。
	只要Undefined一直存在，那么js中就不是真正的一切皆对象啊
## 02-04
#### js null
	通过typeof操作符我们可以看出 null的结果是Object，而在js中，null和Undefined都表示 没有，
	这两个的语法效果基本一致
```javascript
	if (!undefined) {
	  console.log('undefined is false');
	}
	// undefined is false

	if (!null) {
	  console.log('null is false');
	}
	// null is false

	undefined == null
	// true
	//在if语句中，它们都会被自动转为false，相等运算符（==）甚至直接报告两者相等。
```

	从上面代码可见，两者的行为是何等相似！谷歌公司开发的 JavaScript 语言的替代品 Dart 语言，就明确规定只有null，没有undefined！
	既然含义与用法都差不多，为什么要同时设置两个这样的值，这不是无端增加复杂度，令初学者困扰吗？这与历史原因有关。
	1995年 JavaScript 诞生时，最初像Java一样，只设置了null作为表示”无”的值。根据C语言的传统，null被设计成可以自动转为0。
	但是，JavaScript的设计者Brendan Eich，觉得这样做还不够，有两个原因。
	首先，null像在Java里一样，被当成一个对象。但是，JavaScript的值分成原始类型和合成类型两大类，Brendan Eich觉得表示”无”的值最好不是对象。
	其次，JavaScript的最初版本没有包括错误处理机制，发生数据类型不匹配时，往往是自动转换类型或者默默地失败。
	Brendan Eich觉得，如果null自动转为0，很不容易发现错误。
	因此，Brendan Eich又设计了一个undefined。他是这样区分的：
	* null是一个表示”无”的对象，转为数值时为0；
	* undefined是一个表示”无”的原始值，转为数值时为NaN。
	但是，这样的区分在实践中很快就被证明不可行。目前null和undefined基本是同义的，只有一些细微的差别。
	
	那么我们在使用null 和 Undefined是如何来区分的
	首先根据定义变量值得类型不同，在初始化一个没有值得变量时，
	如果该变量将来要用做对象赋值，那么我们就显示的 将null初始化给这个变量；也可以增加代码的可读性；
	

