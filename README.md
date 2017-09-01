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
* [02-05](https://github.com/seven-it/js-notebook#02-05) `为什么推荐使用字面量的形式来创建对象`
* [02-06](https://github.com/seven-it/js-notebook#02-06) `new操作符原理`
#### 03 js原型
* [03-01](https://github.com/seven-it/js-notebook#03-01) `函数与对象的关系`
* [03-02](https://github.com/seven-it/js-notebook#03-02) `prototype对象`
* [03-03](https://github.com/seven-it/js-notebook#03-03) `__proto__ 隐式原型`
* [03-04](https://github.com/seven-it/js-notebook#03-04) `函数时被谁创建的？`
* [03-05](https://github.com/seven-it/js-notebook#03-05) `instanceof 操作符原理`
* [03-06](https://github.com/seven-it/js-notebook#03-06) `原型链与继承`
#### 04 js执行上下文环境
* [04-01](https://github.com/seven-it/js-notebook#04-01) `变量的执行上下文环境`
* [04-02](https://github.com/seven-it/js-notebook#04-02) `函数的执行上下文环境`
* [04-03](https://github.com/seven-it/js-notebook#04-03) `执行上下文的三种环境`
#### 05 js作用域
* [05-01](https://github.com/seven-it/js-notebook#05-01) `什么是作用域`
* [05-02](https://github.com/seven-it/js-notebook#05-02) `函数的执行上下文环境`
* [05-03](https://github.com/seven-it/js-notebook#05-03) `执行上下文的三种环境`
* [05-04](https://github.com/seven-it/js-notebook#05-04) `闭包`
#### 06 this
* [06-01](https://github.com/seven-it/js-notebook#06-01) `this调用的模式`
#### 07 异步与单线程
* [07-01](https://github.com/seven-it/js-notebook#07-01) `理解单线程模型`
* [07-02](https://github.com/seven-it/js-notebook#07-02) `js异步机制`
* [07-03](https://github.com/seven-it/js-notebook#07-03) `前端使用异步的场景`
#### 08 js时间对象
* [08-01](https://github.com/seven-it/js-notebook#08-01) `Date()`
* [08-02](https://github.com/seven-it/js-notebook#08-01) `get类方法`
* [08-03](https://github.com/seven-it/js-notebook#08-01) `set类方法`
#### [参考资料链接](https://github.com/seven-it/js-notebook#参考资料)
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
    
    可以跳转到 [02-05](https://github.com/seven-it/js-notebook#02-04)小结查看
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
## 02-05
#### 为什么推荐使用字面量的形式来创建对象

	对象字面量：这是一种优美的对象创建方式，它以包装在大括号中的逗号分割的键-值（key-value）对的方式创建对象。
	js内置构造函数几乎总是有一个更好且更短的字面量表示法
```javascript
	//使用字面量
	var car = {goes: 'far'};
	//使用内置构造函数（反模式）
	var car = new Object();
	car.goes = 'far';
```

	优先选择字面量模式创建对象的另一个原因在于它强调了该对象仅是一个可变哈希映射，而不是从对象中提取的属性或方法。 
	与使用 Object 构造函数相对，使用字面量的另一个原因在于它并没有作用域解析。
	因为可能以同样的名字创建了一个局部构造函数，解释器需要从调用 Object() 的位置开始一直向上查询作用域链，直到发现全局 Object 构造函数。

	Object() 构造函数仅接受一个参数，并且还依赖传递的值，该 Object() 可能会委派另一个内置构造函数来创建对象，并且返回了一个并非期望的不同对象。
	当传递给 Object() 构造函数的值是动态的，并且直到运行时才能确定其类型时， Object() 构造函数的这种行为可能会导致意料不到的结果。
	因此，不要使用 new Object() 构造函数，相反应该使用更为简单、可靠的对象字面量模式。
	
	个人总结 使用字面量来创建对象的优点，
	1.简洁易懂，
	2.操作简单，
	3.由于js内置的方法，性能好，速度快
	4.方便与json的转换
## 02-06
#### new操作符原理
![img3](https://github.com/seven-it/js-/raw/master/images/3.jpg)

![img4](https://github.com/seven-it/js-/raw/master/images/4.jpg)

	如果我们不通过new操作符来实例化构造函数，那么Foo和普通的函数没什么区别。this也是指向window的；
	那么new操作符都在这中间起了什么作用
	
	根据《js高程三》的描述
		通过new来调用构造函数会发生以下4步
			1.创建一个新对象
			2.将构造函数的作用域赋值给新对象
			3.执行构造函数中的代码（给新对象添加属性）
			4.返回新对象

		自己总结
			1.创建新对象
			2.新对象的__proto__ 指向 构造函数的原型对象
			3.将this指向新对象（也就是将自定义属性添加给新对象）
			4.返回新对象
			
	通过代码来演示
	
```javascript
	 var f = new Object();//创建新对象
	 f.__proto__ = Foo.prototype;//指向构造函数原型对象
	 Foo.call(f);//this指向新对象
	 return f;//返回新对象
```

![img6](https://github.com/seven-it/js-/raw/master/images/6.jpg)

	然而需要注意的是，在第三步之后 js会检测一下构造函数的返回值；
	如果发现是引用类型的值，那么直接返回该引用类型；如果是基本类型的值，那么返回的还是原对象；

  	当返回引用类型的值时，相当于是另一个对象了 ，该对象不会继承任何属性!
	
![img7](https://github.com/seven-it/js-/raw/master/images/7.jpg)

	当返回的是基本类型的值时，遵循的是正常的创建流程

![img8](https://github.com/seven-it/js-/raw/master/images/8.jpg)

	不加return返回的也是Undefined所以 如果是值类型就可以完全省略掉了；
	
* new 操作符原理参考资料  [JS中new到底发生了什么](https://warjiang.github.io/devcat/2016/05/12/JS%E4%B8%ADnew%E5%88%B0%E5%BA%95%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88/)


## 03-01
#### 函数与对象的关系
	1.对象是由函数来创建的
```javascript
	function Foo (){}
	var fn = new Foo();
	//上面代码是我们常用创建对象的方式；
	//更常用的方式比如
	var obj = {}
	var arr = []
	//而上面的方式其实是下面代码的语法糖
	var obj = new Object;
	var arr = new Array;
	检测一下 obj 和 arr
	console.log(typeof Object)//function
	console.log(typeof Array)//function
```

	2.函数也属于特殊的对象；
```javascript
	//函数时可以添加属性与方法的
	function fn(){}
	fn.age = 29;
	console.log(fn.age)//29
	console.log(fn instanceof Object)//true
	console.log(fn instanceof Function)//true
	//通过检测  fn 既是对象又是函数 
	
	console.log(Object instanceof Function)//true
	console.log(Function instanceof Object)//true
	//再次检测对象与函数的关系，都返回true！！！
```

	3.得出结论 ： 对象是由函数创建的，函数也是对象的一种
	（这个结论使人更加的迷惑，函数是对象，函数又创建了对象，他们的关系到底是怎样的，这里就要先理解一下prototype）
## 03-02
#### prototype原型
	1.在js中每个函数都会内置一个属性 即 prototype ，这个prototype的属性值是一个 对象 ，
	  而这个对象默认有一个属性constructor 指向这个函数本身
	
	参考图
![img9](https://github.com/seven-it/js-/raw/master/images/9.jpg)

	2.在js中会有很多内置的原型对象，这些对象天生带有各种各样的属性和方法，例如Object
	
	参考图
![img10](https://github.com/seven-it/js-/raw/master/images/10.jpg)

	通过上面 函数与原型对象的相互指针，我们可以向原型上添加自定义属性与方法
```javascript
	function Foo () {

	}
	Foo.prototype.name = 'zs';
	Foo.prototype.age  = 29;
	//上面代码为原型对象添加自定义属性
	var fn = new Foo;
	console.log(fn.name)//zs
	console.log(fn.age)//29
	//实例对象可以调用原型对象上的属性
```
## 03-03
#### __proto__ 隐式原型
	1.通过上面代码可以看出，实例对象可以调用原型对象上的属性；
	如果说 每个函数都有一个prototype原型对象，那么 每个对象都会有一个 __proto__ 隐式原型指向该函数的显示原型 prototype 对象；

	参考图
![img11](https://github.com/seven-it/js-/raw/master/images/11.jpg)
![img12](https://github.com/seven-it/js-/raw/master/images/12.jpg)

	通过上面两张图 可以看出  obj.__proto__ 与 Object.prototype 显示的结果是一样的!
	这是因为每个 自定义 函数的原型对象都是通过Object.prototype创建的，所以obj.__proto__ 指向Object.prototype
	也就是说明 每个对象的 __proto__ 隐式原型指向创建该对象的函数的显示原型 prototype 对象；
	
	参考图
![img13](https://github.com/seven-it/js-/raw/master/images/13.jpg)

	那么有一个问题，函数的原型是一个对象，而对象都有一个__proto__ ，那这个原型有么？
	答案是肯定的，只要是对象都会有一个__proto__，而自定义函数的原型对象，实际都是由Object.prototype创建出来的；
	所以 自定义函数的原型对象的 __proto__ 都指向 Object.prototype ！
	
	如果所有的原型对象的 __proto__ 都指向了Object.prototype 那它指向哪里呢 ？
	Object.prototype确实一个特例——它的__proto__指向的是null ！！！
	也就是说，Object.prototype 是所有原型对象的终点了！
	
	参考图
![img14](https://github.com/seven-it/js-/raw/master/images/14.jpg)

## 03-04
#### 函数时被谁创建的？
	前面有说到 ，函数创建了对象，那么函数又是怎么创建出来的？
```javascript
	function fn (x,y) {
	   return x+y
	}
	console.log(fn(1,2)) //3


	var fn1 = new Function('x','y','return x+y');
	console.log(fn1(2,3))//5
```

	以上代码中，第一种方式是比较传统的函数创建方式，第二种是用new Functoin创建。
	首先根本不推荐用第二种方式。
	这里只是演示，函数是被Function创建的。
	
	根据上面说的一句话——对象的__proto__指向的是创建它的函数的prototype，
	就会出现：Object.__proto__ === Function.prototype。用一个图来表示。
	
![img15](https://github.com/seven-it/js-/raw/master/images/15.png)

	上图中，很明显的标出了：
	自定义函数Foo.__proto__指向Function.prototype，
	Object.__proto__指向Function.prototype，
	唉，怎么还有一个……Function.__proto__指向Function.prototype？这不成了循环引用了？

	对！是一个环形结构。

	其实稍微想一下就明白了。
	Function也是一个函数，
	函数是一种对象，也有__proto__属性。
	既然是函数，那么它一定是被Function创建。
	所以——Function是被自身创建的。
	所以它的__proto__指向了自身的Prototype。
	
	最后一个问题：Function.prototype指向的对象，它的__proto__是不是也指向Object.prototype？
	答案是肯定的。因为Function.prototype指向的对象也是一个普通的被Object创建的对象，所以也遵循基本的规则。
	
![img16](https://github.com/seven-it/js-/raw/master/images/16.jpg)

## 03-05
#### instanceof 操作符原理
	typeof使用来检测基本类型与引用类型的操作符，而instanceof则是检测具体是何种引用类型（细化引用类型）
```javascript
	function fn (){
		alert(1);
	}
	//由于typeof只能检测基本类型，我们想要检测引用类型就要使用instanceof操作符
	console.log(fn instanceof Object)//true
	console.log(fn instanceof Function)//true
```

	上面代码 为什么检测Object返回true呢？
	假设Instanceof运算符的第一个变量是一个对象，暂时称为A；第二个变量一般是一个函数，暂时称为B。
	Instanceof的判断队则是：沿着A的__proto__这条线来找，同时沿着B的prototype这条线来找，
	如果两条线能找到同一个引用，即同一个对象，那么就返回true。如果找到终点还未重合，则返回false。
	
	参考图
	
![img17](https://github.com/seven-it/js-/raw/master/images/17.jpg)

	根据上图 fn 的原型链的终点就是到达了Object.prototype原型上 所以返回的true
	同理的，任何的对象最终的终点都会是Object.prototype原型 同样的返回true
	
	最终参考图
![img18](https://github.com/seven-it/js-/raw/master/images/18.jpg)
	
	通过连线可以看出整个对象原型之间的联系，红色的三个区域关系有些特殊，形成了一个环形的引用
## 03-06
#### 原型链与继承

	其实到这里就非常容易理解了，具体可以根据上面终极大图来分析
	
* 首先是原型链

	原型链就是 __proto__ 隐式原型所存在的一个链条
	访问一个对象的属性时，先在基本属性中查找，如果没有，再沿着__proto__这条链向上找，这就是原型链！
* 继承

	继承就是依托原型链，在该原型链上的所有属性与方法都可以被该对象继承

```javascript
	function Foo (name){
	  this.name = name
	}
	var fn = new Foo;
	
	console.log(fn.hasOwnProperty('name')) //true
```

	通过上面代码分析，fn是Foo构造函数 创建的实例对象，Foo只有一个name属性，那么fn是怎么得到hasOwnProperty方法的？
	这里首先就是原型链的概念，当fn调用hasOwnProperty方法时，
	先在它自身找 --> 没有找到 --> 再找Foo.prototype，还是没有 --> 继续找到Object.prototype --> 找到了就继承，没找到就报错
	
	参考图
![img19](https://github.com/seven-it/js-/raw/master/images/19.jpg)
![img20](https://github.com/seven-it/js-/raw/master/images/20.jpg)
	
## 04-01
#### 变量的执行上下文环境

```javascript
console.log(a)//a is not defined
console.log(a)//undefined
var a;

console.log(b)//undefined
var b = 10;
```

	上面三个console.log的结果，第一个是报错，第二，三个是Undefined;
	第一个很好理解 ，根本没有定义a变量当然报错了
	第二个也很好理解 ，a变量声明了但是未定义，所以返回是Undefined；
	第三个，我们声明变量也赋值了 返回的同样是Undefined；
	并且 ，第二个和第三个 我们console.log是在变量声明前进行的 ，为什么不是报错呢?
	
	这里就引出了一个执行上下文环境，我们来分解下第三个代码
	首先js代码执行之前 会将变量提升到执行环境的最顶部；但是不会赋值

```javascript
console.log(b)//undefined
var b = 10;
//上面代码可以解析为

var b; 
console.log(b) //undefined;
b=10;
console.log(b)//10
//js先将b变量提升，然后console.log的时候只是定义，但未赋值，所以返回Undefined，
//当console.log结束后 变量赋值，这时再访问b变量就是有值得；
```
## 04-01
#### 变量的执行上下文环境

	上面我们说的都是变量的执行上下文环境，下面来看下函数表达式与函数声明的情况，
	这两种情况是有区别的；
	首先函数声明：
	
```javascript
console.log(a)//函数体
function a(){
  alert(1)
}
//当我们console.log函数a的时候可以得到结果，就是a的函数体；
//这说明 对于函数声明来说；js会将整个函数都提升到 环境顶部，
//这也是为什么我们在函数体之前调用函数时，函数也可以顺利执行的原因；
```
```javascript
console.log(a)//函数体
a()//1

function a(){
  alert(1)
}
//上面代码  a函数 在头部执行，依然可以顺利弹出数字1；
//整个js运行情况就是:
//先将函数声明提升到顶部，a()调用其实是在函数体之后的；			
```
	
	但是，不建议像上面那种写法 ，先调用，后声明，的写法，尽量保持先函数声明，后调用函数的写法！！
	
	函数表达式：
```javascript
console.log(a)//undefined
var a = function (){
  alert(1)
}
//当使用函数表达式时，作用和普通声明变量是一样的，只会提前声明变量，不会将整个表达式都提升

var a；
console.log(a)//undefined
a = function (){
  alert(1)
}

//上面的情况一模一样；

```
## 04-03
#### 执行上下文的三种环境
	1.全局环境
	2.函数体环境
	3.eval环境
	
	全局环境：
	上面我们所展示的例子都是在全局环境下定义的，全局环境也就是script标签包裹的区域
	<script>
	.....代码段
	</script>
	
	函数体环境
	每一个函数声明内部都会生成执行上下文环境
```javascript
function (){
var a;//默认会提升到这里（最顶部），不会超出范围，也就是为什么在函数外部访问不到函数内的变量；
执行上下文在花括号里

var a = 10;//这时的a不会提升到全局作用域中，而是在当前函数作用域的最顶部
}
```

	eval()环境
	eval中包含的是一段代码字符串，不推荐使用eval
	
## 05-01
#### 什么是作用域

	作用域就是代码起作用的范围
	js包含全局作用域与函数作用域 
	全局作用域 大家都知道怎么回事
	函数作用域 就是当函数创建时所生成的{}括号内的范围；
```javascript
function a (){
  var b = 10;
}
console.log(b)//Undefined
b在a的作用域中，不在全局作用域 所以 取不到b变量；

var c = 20;
function a (){
  var b = 10;
  console.log(c)
  console.log(f)//f is not defined

  function x(){
    var f = 10;
  }
  x()
}
a()//20

//在a函数中可以取到 全局中 c变量的值；但是取不到函数x中的f变量的值；
```
	
	这里我们是不是可以得出一个结论
	子函数可以访问父函数的作用域，父函数不能访问子函数的作用域；
	
## 05-02
#### 作用域与执行上下文环境的区别

	作用域与执行上下文环境是两个不同的概念
	
	首先 两者的创建时间不一样
	作用域是在函数创建时就被创建出来的
	执行上下文环境则是在函数被调用时创建出来的

	其次，两者存在时间不一样
	执行上下文环境 在当次函数调用完成后就被销毁；
	作用域只要有函数活动，就不会被销毁；

	作用域只有一个，而执行上下文环境可以有多个，并且可同时存在；

	具体可以参考下面的图例 ，引用自 王福朋大牛博客《深入理解javascript原型和闭包》

	下面我们将按照程序执行的顺序，一步一步把各个上下文环境加上
	
	第一步，在加载程序时，已经确定了全局上下文环境，并随着程序的执行而对变量就行赋值。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250814158269779.png)

	第二步，程序执行到第27行，调用fn(10)，此时生成此次调用fn函数时的上下文环境，压栈，并将此上下文环境设置为活动状态。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250814386853995.png)

	第三步，执行到第23行时，调用bar(100)，生成此次调用的上下文环境，压栈，并设置为活动状态。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250815006238997.png)

	第四步，执行完第23行，bar(100)调用完成。则bar(100)上下文环境被销毁。
	接着执行第24行，调用bar(200)，则又生成bar(200)的上下文环境，压栈，设置为活动状态。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250815248579200.png)

	第五步，执行完第24行，则bar(200)调用结束，其上下文环境被销毁。此时会回到fn(10)上下文环境，变为活动状态。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250815435609914.png)

	第六步，执行完第27行代码，fn(10)执行完成之后，fn(10)上下文环境被销毁，全局上下文环境又回到活动状态。
	
![imgfasd](http://images.cnitblog.com/blog/138012/201409/250816112012394.png)

	最后我们可以把以上这几个图片连接起来看看。

![imgfasd](http://images.cnitblog.com/blog/138012/201409/250816269984619.png)

	作用域只是一个“地盘”，一个抽象的概念，其中没有变量。
	要通过作用域对应的执行上下文环境来获取变量的值。
	同一个作用域下，不同的调用会产生不同的执行上下文环境，继而产生不同的变量的值。
	所以，作用域中变量的值是在执行过程中产生的确定的，而作用域却是在函数创建时就确定了。

	所以，如果要查找一个作用域下某个变量的值，就需要找到这个作用域对应的执行上下文环境，再在其中寻找变量的值。
	
## 05-03
#### 作用域链
	
	作用域链与原型链差不多，现在自身查找，再向上查找 ,一直找到全局作用域；
	
	例如
```javascript
	var a = 1;
	function fn (){
	  var b = 2;
	  function fn1(){
	    var c = 3;
	    console.log(c,b);//3,2
	  }
	  fn1(); //调用fn1 现在它本作用域找 ，找到了 c 变量，没找到b ,向父级作用域找，找到并返回！
	}
	fn();
```
	
	作用域链只能向上查找 不能向下查找
	
```javascript
var c = 20;
function a (){
  var b = 10;
  console.log(c) //20
  console.log(f)//f is not defined
  
  function x(){
    var f = 10;
  }
  x()
}
a()
// 在a函数中可以取到 全局中 c变量的值；但是取不到函数x中的f变量的值；
```

	最重要的一点 ！
	
	作用域链查找的是 创建该函数时所形成的作用域链，也就是从函数本体所在位置向上查找，而不是在函数调用的位置查找；
	是创建 而不是调用 切记！！！

```javascript
var x=10;
function fn(){ //fn函数体被创建在这里  
	console.log(x)
}

function show(){
  var x = 20;
  (function (){
    fn() //fn 函数 在这里调用
    
   })();
}

show()//10
// 结果 是 10 而不是 20 ；
```

## 05-04
#### 闭包

个人理解 定义在一个函数内部的函数，作用就是存取私有变量

闭包的应用场景

	1.函数作为返回值
```javascript
function F1() {
  var a = 100;
  //返回一个函数（函数作为返回值）
  return function () {
    console.log(a);//自由变量，父作用域中查找
  }
}
//f1得到一个函数
var f1 = F1();
var a = 200;
f1();
```

	2.函数作为参数传递
```javascript
function F1() {
  var a = 100;
  return function () {
    console.log(a);  //自由变量，父作用域中查找
  }
}
var f1 = F1();
function F2(fn) {
  var a = 200;
  fn();
}
F2(f1);
```
## 06-01
#### 关于 this

	this的指向看调用模式
		方法调用模式
		函数调用模式
		构造函数调用模式
		apply模式

	1.方法调用
	
	当一个函数被保存为对象的属性时，称这个函数为方法，当一个方法被调用时，this被绑定到该对象
```javascript
var a = {
  name:1,
  fn:function(){
    console.log(this)
  }
}
a.fn()// {object} a对象

//特殊情况 1
当方法被赋值给变量来调用时，this指向window
var a = {
  name:1,
  fn:function(){
    console.log(this)
  }
}

var b = a.fn;
b();//window

//特殊情况 2
当方法里面包含有子函数时，子函数的this 指向window
var a = {
  name:1,
  fn:function(){
     (function(){
        console.log(this)
     })()
  }
}
a.fn();//window
```

	2.函数调用模式
	函数调用的this始终指向window
```javascript
function a(){
  console.log(this)
}
a()//window

//嵌套函数
function a(){
  function b(){
    console.log(this)
  }
  b()//window
}
a()//window

//对象中的函数
var a = {
  name:1,
  fn:function(){
     function d(){
       console.log(this)
     }
    d()//window
  }
}
a.fn();

//可以通过保存this 来再函数内部调用
var a = {
  name:1,
  fn:function(){
    var that = this
     function d(){
       console.log(that)//a对象
     }
    d()//window
  }
}
a.fn();
```

	3.构造函数调用
	this总是指向即将new出的实例对象上；
```javascript
function Foo(name){
  this.name=name;
}

var fn1 = new Foo('zs');
console.log(fn1.name)//zs

//如果直接调用构造函数，那么和调用普通函数没什么区别，this始终在window上；

function Foo(name){
  this.name=name;
  console.log(this)
}
Foo()//window
```
		
	4.使用apply，call
	this始终指向第一个参数所对用的对象；
```javascript
var obj = {}

function a(){
  console.log(this)
}
a.apply(obj);//obj
```
## 07-01
#### 理解单线程模型
	单线程模型指的是，JavaScript只在一个线程上运行。
	也就是说，JavaScript同时只能执行一个任务，其他任务都必须在后面排队等待。
	
	虽然 JavaScript 程序 只在一个线程上运行，
	但是javascript引擎（也就是浏览器）是有多线程的；
	单个脚本只能在一个线程上运行，其他线程都是在后台配合。
	
* JavaScript之所以采用单线程，
	* 是因为JavaScript从诞生起就是单线程，
	* 原因是不想让浏览器变得太复杂，因为多线程需要共享资源、且有可能修改彼此的运行结果，
	* 例如我在这个线程上添加了DOM ，在另一个线程上又删除了它，那么浏览器应该先执行哪个呢？
	* 所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。
	
## 07-02
#### js异步机制
	
* js程序用单线程来处理同步程序，为了不使程序发生阻塞，js会将等待的任务先独立出去，等待同步任务全部执行完成 ，再回过头来执行等待的任务；

![img21](https://github.com/seven-it/js-/raw/master/images/21.jpg)

* 例如上图（自己理解的画的）
	* js在运行时是一行代码一行代码运行的,如果是同步任务,就会依次推入同步任务栈中依次执行；
	* 当遇到等待任务时，js会先将需要等待执行的任务推入等待任务队列，并且继续执行后面的同步任务；
	* 当左侧的同步任务栈中的任务都执行完成之后，才会去看一下旁边是否有未执行的等待任务；
	* 在把等待任务推入同步栈中时，js会先检测一下，将可立即执行的任务推入同步栈中，如果任务没到执行时间，就先不去管它；
* 例如上图右侧的等待队列中有不同时间执行的任务，
	* 任务一再1秒后推入同步栈
	* 任务二 在10秒后推入
	* 任务三 在请求返回结果后推入（可以立即执行，也可能最后一个执行，看请求时间）
	* 任务四 在用户点击操作后执行 （如果不点击就一直不执行）
## 07-03
#### 前端使用异步的场景
* 定时器
```javascript
	 console.log(0);
	 setTimeout(function (){
		console.log(1)
	 })
	 //这里没有给定时器设定时间，默认0 但是结果依然是它最后一个输出
	 //因为js认为定时器是一个异步程序（等待程序） 所以会毫不犹豫的先将它拎出去，等待同步程序执行完
	 console.log(2)
	 //结果 0 , 2 , 1
```
* ajax请求，图片资源请求
```javascript
	console.log(0);
	$.get("test.json",function (data){
	console.log('name'+data.name+',age'+data.age);
	})
	console.log(2);
	//结果 0 ,2 ,ajax结果
	
	var img = document.createElement('img');
	img.onload=function (){
		console.log('加载img成功')
	}
	img.src='xxx.jpg'

	document.body.appendChild(img)
	console.log('end')

	结构 // end  ，加载img成功
```
* 事件绑定
```javascript
	document.onclick=function (){
		console.log(0)
	}

    console.log(1)
    // 1 , 0
	//如果不点击  那么永远不会执行
```
* 异步与同步的区别
	* 同步会阻塞代码执行，而异步不会
	* alert是同步，setTimeout是异步
* 何时需要异步
	* 在可能发生等待的情况
	* 等待过程中不能像alert一样阻塞程序运行
	* 因此，所有的所有的等待情况都需要异步
	
## 08-01
#### Date() 
* 作为普通函数使用 返回当日的日期和时间的字符串,传值或者不传值都是一样的结果
```javascript
	Date() 
	//"Fri Sep 01 2017 15:08:59 GMT+0800 (中国标准时间)"
	Date('2019')
	//"Fri Sep 01 2017 15:08:59 GMT+0800 (中国标准时间)"
```
* 作为构造函数通过new来实例化对象，返回当日的日期和时间的字符串；
	* 作为构造函数 ，Date接收多种形式的参数
	* 可以接收时间戳
```javascript
	var myDate = new Date(1504246210863);
    console.log(myDate)//Fri Sep 01 2017 14:10:10 GMT+0800 (中国标准时间)
```
	* 日期字符串作为参数
	
			日期字符串的完整格式是“month day, year hours:minutes:seconds”，
			比如“December 25, 1995  13:30:00”。
			如果省略了小时、分钟或秒数，这些值会被设为0。
```javascript
	new Date('2013-2-15')
	new Date('2013/2/15')
	new Date('02/15/2013')
	new Date('2013-FEB-15')
	new Date('FEB, 15, 2013')
	new Date('FEB 15, 2013')
	new Date('Feberuary, 15, 2013')
	new Date('Feberuary 15, 2013')
	new Date('15 Feb 2013')
	new Date('15, Feberuary, 2013')

	// Fri Feb 15 2013 00:00:00 GMT+0800 (CST)
```
	* 注意，在ES5之中，如果日期采用连词线（-）格式分隔，且具有前导0，JavaScript会认为这是一个ISO格式的日期字符串，导致返回的时间是以UTC时区计算的。
```javascript
	new Date('2014-01-01')
	// Wed Jan 01 2014 08:00:00 GMT+0800 (CST)

	new Date('2014-1-1')
	// Wed Jan 01 2014 00:00:00 GMT+0800 (CST)
```
* 参数范围
	* year：四位年份，如果写成两位数，则加上1900
	* month：表示月份，0表示一月，11表示12月
	* date：表示日期，1到31
	* hour：表示小时，0到23
	* minute：表示分钟，0到59
	* second：表示秒钟，0到59
	* ms：表示毫秒，0到999
	* 参数如果超出了正常范围，会被自动折算。比如，如果月设为15，就折算为下一年的4月。
```javascript
	new Date(2013, 15)
	// Tue Apr 01 2014 00:00:00 GMT+0800 (CST)

	new Date(2013, 0, 0)
	// Mon Dec 31 2012 00:00:00 GMT+0800 (CST)
```
* Date.now()
	* Date.now方法返回当前距离1970年1月1日00:00:00UTC的毫秒数。

## 08-02
#### get类方法

* 汇总
	* getTime()：返回距离1970年1月1日00:00:00的毫秒数，等同于valueOf方法。
	* getDate()：返回实例对象对应每个月的几号（从1开始）。
	* getDay()：返回星期几，星期日为0，星期一为1，以此类推。
	* getYear()：返回距离1900的年数。
	* getFullYear()：返回四位的年份。
	* getMonth()：返回月份（0表示1月，11表示12月）。
	* getHours()：返回小时（0-23）。
	* getMilliseconds()：返回毫秒（0-999）。
	* getMinutes()：返回分钟（0-59）。
	* getSeconds()：返回秒（0-59）。
	* getTimezoneOffset()：返回当前时间与UTC的时区差异，以分钟表示，返回结果考虑到了夏令时因素。
	* 所有这些get*方法返回的都是整数，不同方法返回值的范围不一样。
## 08-02
#### set类方法
* 汇总
	* setDate(date)：设置实例对象对应的每个月的几号（1-31），返回改变后毫秒时间戳。
	* setYear(year): 设置距离1900年的年数。
	* setFullYear(year [, month, date])：设置四位年份。
	* setHours(hour [, min, sec, ms])：设置小时（0-23）。
	* setMilliseconds()：设置毫秒（0-999）。
	* setMinutes(min [, sec, ms])：设置分钟（0-59）。
	* setMonth(month [, date])：设置月份（0-11）。
	* setSeconds(sec [, ms])：设置秒（0-59）。
	* setTime(milliseconds)：设置毫秒时间戳。
## 参考资料

* [深入理解javascript原型和闭包系列](http://www.cnblogs.com/wangfupeng1988/p/3977987.html)
* [JavaScript 标准参考教程（alpha)](http://javascript.ruanyifeng.com/#introduction)
* [JavaScript“并非”一切皆对象](http://www.cnblogs.com/myvin/p/4660138.html)
* [JS中new到底发生了什么](https://warjiang.github.io/devcat/2016/05/12/JS%E4%B8%ADnew%E5%88%B0%E5%BA%95%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88/)


	
