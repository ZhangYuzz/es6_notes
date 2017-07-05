let const
***
	let提供了块级作用域的概念
    只在{}内起作用
    没有变量名提升，如果在定义前使用则会报错
    
    暂时性死区
    不允许重复申明
    
    do表达式 
    想要返回值，办法就是在块级作用域之前加上do，使它变为do表达式。

    let x = do {
      let t = f();
      t * t + 1;
    };
    
    const 申明一个常量
变量的结构赋值
***
	1.数组的解构赋值
	
        let [a, b, c] = [1, 2, 3];

        解构赋值允许指定默认值。
        let [foo = true] = [];
        foo // true
        let [x, y = 'b'] = ['a']; // x='a', y='b'
        let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
    
	2.对象的解构赋值
	
        解构不仅可以用于数组，还可以用于对象。
        let { foo, bar } = { foo: "aaa", bar: "bbb" };
        foo // "aaa"
        bar // "bbb"
    
    3.字符串的解构赋值
        const [a, b, c, d, e] = 'hello';
        a // "h"
        b // "e"
        c // "l"
        d // "l"
        e // "o"
    
    
    0.0 解构赋值的用途

    （1）交换变量的值[x, y] = [y, x];
    
    （2）从函数返回多个值
        function example() {
          return [1, 2, 3];
        }
        let [a, b, c] = example();
        
    


字符串扩展
***

		at()方法
        'abc'.charAt(0) // "a"
        
        includes()方法
        var s = 'Hello world!';
        s.includes('o') // true
        
        repeat方法
        
        padStart()自动补全
        
        字符串模板  变量写在${}里面
        $('#result').append(`
          There are <b>${basket.count}</b> items
           in your basket, <em>${basket.onSale}</em>
          are on sale!
        `);
正则扩展
***
	要的时候找资料吧
数值扩展
***
	要的时候找资料吧
    Math方法  去小数 判断正负 立方根 32位 返回所有参数平方和
    对数的方法.....
函数扩展
***
	1.设置默认值
	
        ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。

        function log(x, y = 'World') {
          console.log(x, y);
        }
      函数的length属性 返回的是参数的个数 默认值不算
      
    2.rest参数   rest参数后面不能有其他参数
    
        function add(...values) {
          let sum = 0;

          for (var val of values) {
            sum += val;
          }

          return sum;
        }
		add(2, 5, 3) // 10
        
    3.name属性
    
    	f.name 返回函数名
   		var f = function () {};

        // ES5
        f.name // ""

        // ES6
        f.name // "f"
        
   	4.箭头函数
   		
        箭头函数内的this指的就是定义时的对象不是使用时的
   		var f = v => v;  
        等于下面的函数
        var f = function(v) {
          return v;
        };
	
    5.通过::绑定this

数组扩展
***
	1.扩展运算符 （...）
	把一个数组	转为用逗号分隔的参数  代替apply   函数参数传值    合并数组   函数返回值 
	console.log(...[1, 2, 3])
	// 1 2 3

	代替了apply方法
	// ES5 的写法
	Math.max.apply(null, [14, 3, 77])

	// ES6 的写法
	Math.max(...[14, 3, 77])

	// ES5的 写法
	var arr1 = [0, 1, 2];
	var arr2 = [3, 4, 5];
	Array.prototype.push.apply(arr1, arr2);

	// ES6 的写法
	var arr1 = [0, 1, 2];
	var arr2 = [3, 4, 5];
	arr1.push(...arr2);


	var arr1 = ['a', 'b'];
	var arr2 = ['c'];
	var arr3 = ['d', 'e'];

	[...arr1,...arr2,...arr3]

	

	2.Array.from()  
	将伪数组转化为数组  处理querySelectorAll
	let arrayLike = {
	    '0': 'a',
	    '1': 'b',
	    '2': 'c',
	    length: 3
	};

	// ES5的写法
	var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

	// ES6的写法
	let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']


	3.Array.of() 
	将一组值转化为数组
	Array.of(3, 11, 8) // [3,11,8]
	Array.of(3) // [3]
	Array.of(3).length // 1

	Array.of基本上可以用来替代Array()或new Array()，并且不存在由于参数不同而导致的重载。它的行为非常统一。
	Array.of() // []
	Array.of(undefined) // [undefined]
	Array.of(1) // [1]
	Array.of(1, 2) // [1, 2]
    
    
    4.数组实例cpyWithin()
    将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
    它接受三个参数。
    target（必需）：从该位置开始替换数据。
	start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
	end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
    // 将3号位复制到0号位
	[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
	// [4, 2, 3, 4, 5]

	// -2相当于3号位，-1相当于4号位
	[1, 2, 3, 4, 5].copyWithin(0, -2, -1)
	// [4, 2, 3, 4, 5]
    
    
 	5.数组实例的 find() 和 findIndex()
	
    find()
	参数是一个回调函数
    [1, 4, -5, 10].find((n) => n < 0)
    // -5
    上面代码找出数组中第一个小于0的成员。

    [1, 5, 10, 15].find(function(value, index, arr) {
      return value > 9;
    }) // 10
    
    findIndex()
    数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。

    [1, 5, 10, 15].findIndex(function(value, index, arr) {
      return value > 9;
    }) // 2
    
    6.fill() 
    fill方法使用给定值，填充一个数组
    ['a', 'b', 'c'].fill(7)
    // [7, 7, 7]
   	
   	7.数组实例的 entries()，keys() 和 values()
   	for (let index of ['a', 'b'].keys()) {
      console.log(index);
    }
    // 0
    // 1

    for (let elem of ['a', 'b'].values()) {
      console.log(elem);
    }
    // 'a'
    // 'b'

    for (let [index, elem] of ['a', 'b'].entries()) {
      console.log(index, elem);
    }
    // 0 "a"
    // 1 "b"

	8.数组实例的 includes() 
	[1, 2, 3].includes(2)     // true
    [1, 2, 3].includes(4)     // false
    [1, 2, NaN].includes(NaN) // true

	es6中不将数组空位转为undefined	
    
对象的扩展
***	
    1.方法简写
    
        var o = {
          method() {
            return "Hello!";
          }
        };

        // 等同于

        var o = {
          method: function() {
            return "Hello!";
          }
        };
    
    	模块化输出时
        module.exports = { getItem, setItem, clear };
        // 等同于
        module.exports = {
          getItem: getItem,
          setItem: setItem,
          clear: clear
        };
        
    2.属性名表达式
    
    	ES6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。

        let propKey = 'foo';

        let obj = {
          [propKey]: true,
          ['a' + 'bc']: 123
        };
        
    3.Object.is()
    
        ES5比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0。JavaScript缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

        ES6提出“Same-value equality”（同值相等）算法，用来解决这个问题。Object.is就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

		Object.is('foo', 'foo')
        // true
        Object.is({}, {})
        // false
    4.Object.saagin()
    
    	Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。如果有相同的属性名则会覆盖。
        var target = { a: 1 };
        var source1 = { b: 2 };
        var source2 = { c: 3 };

        Object.assign(target, source1, source2);
        target // {a:1, b:2, c:3}
        Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。
    
Symbol
***
		ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。
        
        let s = Symbol();
        typeof s
        // "symbol"
        
        Symbol后面的参数是起一个名字 参数名称相同Symbol值也不相同
        Symbol内置了11个值
        hasInstance
        isConcatSpreadable
        species
        match
        replace
        search
        split
        iterator
        toPrimitive
        toStringTag
        unscopables
        
Set和Map数据结构
***
	Set：
        
		set类似数组但是成员都是唯一的没有重复
        
        Set结构可以用来数组去重
        
        new Set(a[]);
        
        Set实例的方法分为 操作方法 和 遍历方法
        
        操作方法：
        
        1.add 2.delete 3.has 4.clear
        
        s.add(1).add(2).add(2);
        // 注意2被加入了两次

        s.size // 2

        s.has(1) // true
        s.has(2) // true
        s.has(3) // false

        s.delete(2);
        s.has(2) // false
       	
        Array.from可以将Set结构转为数组
        
        遍历方法：
        1.keys 2.values 3.entries 4.forEach
        

	Map：
        
        Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键也就是说，Object 结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。
        
        操作方法
        
        1.size属性
        2.set(key,value)
        3.get()
        4.has()
        5.delete
        6.clear
        
        遍历方法
        
        1.keys()
        2.values()
        3.entries()
        4.forEach()
        
	WeakMap
    
Promise对象
***
        Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6将其写进了语言标准，统一了用法，原生提供了Promise对象。
        
        Pending进行中，Resolved已完成，Rejected已失败
        
        下面代码创造了一个Promise实例。
        var promise = new Promise(function(resolve, reject) {
          // ... some code

          if (/* 异步操作成功 */){
            resolve(value);
          } else {
            reject(error);
          }
        });
        
	then方法：
    
        Promise实例生成以后，可以用then方法分别指定Resolved状态和Reject状态的回调函数。

        promise.then(function(value) {
          // success
        }, function(error) {
          // failure
        });
        
    catch方法：
    
    用于制定发生错误时的方法
    Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。

        getJSON('/posts.json').then(function(posts) {
          // ...
        }).catch(function(error) {
          // 处理 getJSON 和 前一个回调函数运行时发生的错误
          console.log('发生错误！', error);
        });


Iterator(遍历器)
***
    JavaScript 原有的表示“集合”的数据结构，主要是数组（Array）和对象（Object），ES6 又添加了Map和Set。这样就有了四种数据集合，用户还可以组合使用它们，定义自己的数据结构，比如数组的成员是Map，Map的成员是对象。这样就需要一种统一的接口机制，来处理所有不同的数据结构。		
    
    for...of循环
    
    代替了for...in循环
    
    for(let value in arr){
    	console.log(value)
    }
Generator函数
***
	形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）。

    function* helloWorldGenerator() {
      yield 'hello';
      yield 'world';
      return 'ending';
    }

    var hw = helloWorldGenerator();
    
    Generator方法调用后会生成一个在函数内部的指针，但是函数不会执行要通过next方法来执行
    
    hw.next()；
    //{value:"hello",done:false}
    yield语句是暂停标记需要下一个next来执行当碰到return语句时执行完毕
    
    使用for...of循环不需要使用next方法可以直接调用
    
        function *foo() {
          yield 1;
          yield 2;
          yield 3;
          yield 4;
          yield 5;
          return 6;
        }

        for (let v of foo()) {
          console.log(v);
        }
        // 1 2 3 4 5
        
 async（Generator函数的语法糖）
 ***	
        async函数返回一个 Promise 对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。
        
 		var gen = function* () {
          var f1 = yield readFile('/etc/fstab');
          var f2 = yield readFile('/etc/shells');
          console.log(f1.toString());
          console.log(f2.toString());
        };
        写成async函数，就是下面这样。

        var asyncReadFile = async function () {
          var f1 = await readFile('/etc/fstab');
          var f2 = await readFile('/etc/shells');
          console.log(f1.toString());
          console.log(f2.toString());
        };
 
 		一比较就会发现，async函数就是将 Generator 函数的星号（*）替换成async，将yield替换成await，仅此而已。
        
        
Class的使用
***
		因为js生成实例对象的方法是通过构造函数来实现和传统的面向对象编程的语言语法不同让新学习js的程序员头疼，所以在es6中引入了class的概念，通过class关键字可以定义类。
        
        //es5中定义构造函数生成实例对象
        function Point(x, y) {
          this.x = x;
          this.y = y;
        }

        Point.prototype.toString = function () {
          return '(' + this.x + ', ' + this.y + ')';
        };

        var p = new Point(1, 2);
        
        
        //es6中定义类  方法之间不要加逗号
        类中的方法实际上就是原型上的方法
        class Point {
          constructor(x, y) {
            this.x = x;
            this.y = y;
          }

          toString() {
            return '(' + this.x + ', ' + this.y + ')';
          }
        }
        //上述等同于
        Point.prototype={
        	constructor(){},
            toString(){}
        }
        
        Object.assign方法用来一次性向类添加多个方法
        
        Object.assign(Point.prototype, {
          toString(){},
          toValue(){}
        });
        
        
        每一个类都会默认自动添加一个constructor方法
        
        类必须使用new调用，普通构造函数不需要
        
	Class表达式
        
        const MyClass = class Me {
          getClassName() {
            return Me.name;
          }
        };
        上面代码使用表达式定义了一个类。需要注意的是，这个类的名字是MyClass而不是Me，Me只在 Class 的内部代码可用，指代当前类。
        
        类不存在变量名提升，所以class必须声明在使用前
        
        class加了私有属性方法是在属性名之前使用#标注
        
            class Point {
              #x;

              constructor(x = 0) {
                #x = +x; // 写成 this.#x 亦可
              }

              get x() { return #x }
              set x(value) { #x = +value }
            }
            上面代码中，#x就表示私有属性x，在Point类之外是读取不到这个属性的。还可以看到，私有属性与实例的属性是可以同名的（比如，#x与get x()）。
            
            class内的this默认指向类的实例，但是最后指向运行的环境
            
       
Module
***	
    	import输入
        
        // ES6模块
        import { stat, exists, readFile } from 'fs';

		export输出
        
        // profile.js
        export var firstName = 'Michael';
        export var lastName = 'Jackson';
        export var year = 1958;
        
        export {firstName, lastName, year};
        
        export输出时可以使用as关键字给变量重命名
        
        function v1() { ... }
        export {
          v1 as streamV1,
        };
        
        
        
        import命令
    
        import {firstName, lastName, year} from './profile';
       
        import后面的from指定模块文件的位置，可以是相对路径，也可以是绝对路径，.js路径可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置。

        import {myMethod} from 'util';
        
        import是静态加载因此不能有任何逻辑语句和变量

		

        // main.js

        import { area, circumference } from './circle';

        console.log('圆面积：' + area(4));
        console.log('圆周长：' + circumference(14));
        上面写法是逐一指定要加载的方法，整体加载的写法如下。

        import * as circle from './circle';

        console.log('圆面积：' + circle.area(4));
        console.log('圆周长：' + circle.circumference(14));


		因为import无法动态的加载，所以增加了一个import()函数，返回值是一个promise对象












    

	