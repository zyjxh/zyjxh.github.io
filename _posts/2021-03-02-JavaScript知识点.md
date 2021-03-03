---
layout:     post   				    # 使用的布局（不需要改）
title:      JavaScript知识点总结 				# 标题 
subtitle:   一些零散的js知识点，持续更新中。。。 #副标题
date:       2021-03-02				# 时间
author:     JXH 						# 作者
header-img: img/post-bg-coffee.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - JavaScript
---



## 思维导图
![JavaScrip思维导图1](/img/javascript20210203.jpg)
知识点如下： 
## 1.js的数据类型，值的存储
JavaScript一共有8种数据类型，其中有7种基本数据类型：Undefined、Null、Boolean、Number、String、Symbol（es6新增，表示独一无二的值）和BigInt（es10新增）；
1种引用数据类型——Object（Object本质上是由一组无序的名值对组成的）。里面包含 function、Array、Date等。JavaScript不支持任何创建自定义类型的机制，而所有值最终都将是上述 8 种数据类型之一。
原始数据类型：直接存储在栈（stack）中，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储。
引用数据类型：同时存储在栈（stack）和堆（heap）中，占据空间大、大小不固定。引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。

## 2.数据类型判断（typeof, instanceof, constructor, Object.prototype.toString.call()）

### (1) typeof
typeof只能判断原始类型，对应Array, Function这些不能判断
```
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof []);              // object     []数组的数据类型在 typeof 中被解释为 object
console.log(typeof function(){});    // function
console.log(typeof {});              // object
console.log(typeof undefined);       // undefined
console.log(typeof null);            // object     null 的数据类型被 typeof 解释为 object
```
### (2) instanceof
instanceof 可以正确的判断对象的类型，因为内部机制是通过判断对象的原型链中是不是能找到类型的 prototype。
```
console.log(2 instanceof Number);                    // false
console.log(true instanceof Boolean);                // false 
console.log('str' instanceof String);                // false  
console.log([] instanceof Array);                    // true
console.log(function(){} instanceof Function);       // true
console.log({} instanceof Object);                   // true    
// console.log(undefined instanceof Undefined);
// console.log(null instanceof Null);
```
### (3) constructor
注意，如果改变对象的原型，construcor就失效。
```
console.log((2).constructor === Number); // true
console.log((true).constructor === Boolean); // true
console.log(('str').constructor === String); // true
console.log(([]).constructor === Array); // true
console.log((function() {}).constructor === Function); // true
console.log(({}).constructor === Object); // true
```
### (4) Object.prototype.toString.call()
借用Object的 toString 方法
```
var a = Object.prototype.toString;
 
console.log(a.call(2));
console.log(a.call(true));
console.log(a.call('str'));
console.log(a.call([]));
console.log(a.call(function(){}));
console.log(a.call({}));
console.log(a.call(undefined));
console.log(a.call(null));
```

## 3.js的内置对象
常用的内置对象。
```
（1）值属性，这些全局属性返回一个简单值，这些值没有自己的属性和方法。

例如 Infinity、NaN、undefined、null 字面量

（2）函数属性，全局函数可以直接调用，不需要在调用时指定所属对象，执行结束后会将结果直接返回给调用者。

例如 eval()、parseFloat()、parseInt() 等

（3）基本对象，基本对象是定义或使用其他对象的基础。基本对象包括一般对象、函数对象和错误对象。

例如 Object、Function、Boolean、Symbol、Error 等

（4）数字和日期对象，用来表示数字、日期和执行数学计算的对象。

例如 Number、Math、Date

（5）字符串，用来表示和操作字符串的对象。

例如 String、RegExp

（6）可索引的集合对象，这些对象表示按照索引值来排序的数据集合，包括数组和类型数组，以及类数组结构的对象。例如 Array

（7）使用键的集合对象，这些集合对象在存储数据时会使用到键，支持按照插入顺序来迭代元素。

例如 Map、Set、WeakMap、WeakSet

（8）矢量集合，SIMD 矢量集合中的数据会被组织为一个数据序列。

例如 SIMD 等

（9）结构化数据，这些对象用来表示和操作结构化的缓冲区数据，或使用 JSON 编码的数据。

例如 JSON 等

（10）控制抽象对象

例如 Promise、Generator 等

（11）反射

例如 Reflect、Proxy

（12）国际化，为了支持多语言处理而加入 ECMAScript 的对象。

例如 Intl、Intl.Collator 等

（13）WebAssembly

（14）其他

```

## 4.null 和 undefined的区别
首先 Undefined 和 Null 都是基本数据类型，这两个基本数据类型分别都只有一个值，就是 undefined 和 null。
undefined 代表的含义是未定义，
null 代表的含义是空对象（其实不是真的对象，请看下面的注意！）。一般变量声明了但还没有定义的时候会返回 undefined，null
主要用于赋值给一些可能会返回对象的变量，作为初始化。

## 5.JavaScript的作用域和作用域链
*作用域*： 作用域是定义变量的区域，它有一套访问变量的规则，这套规则来管理浏览器引擎如何在当前作用域以及嵌套的作用域中根据变量（标识符）进行变量查找。  
*作用域链*： 作用域链的作用是保证对执行环境有权访问的所有变量和函数的有序访问，通过作用域链，我们可以访问到外层环境的变量和
函数。

## 6.JavaScript创建对象的几种方式
```
1）第一种是工厂模式，工厂模式的主要工作原理是用函数来封装创建对象的细节，从而通过调用函数来达到复用的目的。但是它有一个很大的问题就是创建出来的对象无法和某个类型联系起来，它只是简单的封装了复用代码，而没有建立起对象和类型间的关系。

（2）第二种是构造函数模式。js 中每一个函数都可以作为构造函数，只要一个函数是通过 new 来调用的，那么我们就可以把它称为构造函数。执行构造函数首先会创建一个对象，然后将对象的原型指向构造函数的 prototype 属性，然后将执行上下文中的 this 指向这个对象，最后再执行整个函数，如果返回值不是对象，则返回新建的对象。因为 this 的值指向了新建的对象，因此我们可以使用 this 给对象赋值。构造函数模式相对于工厂模式的优点是，所创建的对象和构造函数建立起了联系，因此我们可以通过原型来识别对象的类型。但是构造函数存在一个缺点就是，造成了不必要的函数对象的创建，因为在 js 中函数也是一个对象，因此如果对象属性中如果包含函数的话，那么每次我们都会新建一个函数对象，浪费了不必要的内存空间，因为函数是所有的实例都可以通用的。

（3）第三种模式是原型模式，因为每一个函数都有一个 prototype 属性，这个属性是一个对象，它包含了通过构造函数创建的所有实例都能共享的属性和方法。因此我们可以使用原型对象来添加公用属性和方法，从而实现代码的复用。这种方式相对于构造函数模式来说，解决了函数对象的复用问题。但是这种模式也存在一些问题，一个是没有办法通过传入参数来初始化值，另一个是如果存在一个引用类型如 Array 这样的值，那么所有的实例将共享一个对象，一个实例对引用类型值的改变会影响所有的实例。

（4）第四种模式是组合使用构造函数模式和原型模式，这是创建自定义类型的最常见方式。因为构造函数模式和原型模式分开使用都存在一些问题，因此我们可以组合使用这两种模式，通过构造函数来初始化对象的属性，通过原型对象来实现函数方法的复用。这种方法很好的解决了两种模式单独使用时的缺点，但是有一点不足的就是，因为使用了两种不同的模式，所以对于代码的封装性不够好。

（5）第五种模式是动态原型模式，这一种模式将原型方法赋值的创建过程移动到了构造函数的内部，通过对属性是否存在的判断，可以实现仅在第一次调用函数时对原型对象赋值一次的效果。这一种方式很好地对上面的混合模式进行了封装。

（6）第六种模式是寄生构造函数模式，这一种模式和工厂模式的实现基本相同，我对这个模式的理解是，它主要是基于一个已有的类型，在实例化时对实例化的对象进行扩展。这样既不用修改原来的构造函数，也达到了扩展对象的目的。它的一个缺点和工厂模式一样，无法实现对象的识别。
```

## 7.JavaScript继承的几种方式
```
（1）第一种是以原型链的方式来实现继承，但是这种实现方式存在的缺点是，在包含有引用类型的数据时，会被所有的实例对象所共享，容易造成修改的混乱。还有就是在创建子类型的时候不能向超类型传递参数。

（2）第二种方式是使用借用构造函数的方式，这种方式是通过在子类型的函数中调用超类型的构造函数来实现的，这一种方法解决了不能向超类型传递参数的缺点，但是它存在的一个问题就是无法实现函数方法的复用，并且超类型原型定义的方法子类型也没有办法访问到。

（3）第三种方式是组合继承，组合继承是将原型链和借用构造函数组合起来使用的一种方式。通过借用构造函数的方式来实现类型的属性的继承，通过将子类型的原型设置为超类型的实例来实现方法的继承。这种方式解决了上面的两种模式单独使用时的问题，但是由于我们是以超类型的实例来作为子类型的原型，所以调用了两次超类的构造函数，造成了子类型的原型中多了很多不必要的属性。

（4）第四种方式是原型式继承，原型式继承的主要思路就是基于已有的对象来创建新的对象，实现的原理是，向函数中传入一个对象，然后返回一个以这个对象为原型的对象。这种继承的思路主要不是为了实现创造一种新的类型，只是对某个对象实现一种简单继承，ES5 中定义的 Object.create() 方法就是原型式继承的实现。缺点与原型链方式相同。

（5）第五种方式是寄生式继承，寄生式继承的思路是创建一个用于封装继承过程的函数，通过传入一个对象，然后复制一个对象的副本，然后对象进行扩展，最后返回这个对象。这个扩展的过程就可以理解是一种继承。这种继承的优点就是对一个简单对象实现继承，如果这个对象不是我们的自定义类型时。缺点是没有办法实现函数的复用。

（6）第六种方式是寄生式组合继承，组合继承的缺点就是使用超类型的实例做为子类型的原型，导致添加了不必要的原型属性。寄生式组合继承的方式是使用超类型的原型的副本来作为子类型的原型，这样就避免了创建不必要的属性。
```
## 8.对this、call、apply和bind的理解
```
1.在浏览器里，在全局范围内this 指向window对象；
2.在函数中，this永远指向最后调用他的那个对象；
3.构造函数中，this指向new出来的那个新的对象；
4.call、apply、bind中的this被强绑定在指定的那个对象上；
5.箭头函数中this比较特殊,箭头函数this为父作用域的this，不是调用时的this.要知道前四种方式,都是调用时确定,也就是动态的,而箭头函数的this指向是静态的,声明的时候就确定了下来；
6.apply、call、bind都是js给函数内置的一些API，调用他们可以为函数指定this的执行,同时也可以传参。
```
![this](/img/this20210302.jpg)

## 9.JavaScript原型与原型链
在 js 中我们是使用构造函数来新建一个对象的，每一个构造函数的内部都有一个 prototype 属性值，这个属性值是一个对
象，这个对象包含了可以由该构造函数的所有实例共享的属性和方法。当我们使用构造函数新建一个对象后，在这个对象的内部
将包含一个指针，这个指针指向构造函数的 prototype 属性对应的值，在 ES5 中这个指针被称为对象的原型。一般来说我们
是不应该能够获取到这个值的，但是现在浏览器中都实现了 proto 属性来让我们访问这个属性，但是我们最好不要使用这
个属性，因为它不是规范中规定的。ES5 中新增了一个 Object.getPrototypeOf() 方法，我们可以通过这个方法来获取对
象的原型。  
  
当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么它就会去它的原型对象里找这个属性，这个原型对象又
会有自己的原型，于是就这样一直找下去，也就是原型链的概念。原型链的尽头一般来说都是 Object.prototype 所以这就 是我们新建的对象为什么能够使用 toString() 等方法的原因。

## 10.JavaScript获取原型的方法
* p.proto
* p.constructor.prototypr
* Object.getPrototyprOf(p)

## 11.闭包
**闭包是指有权访问另一个函数作用域内变量的函数**，创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量。
  
闭包有两个常用的用途。

> 闭包的第一个用途是使我们在函数外部能够访问到函数内部的变量。通过使用闭包，我们可以通过在外部调用闭包函数，从而在外部访问到函数内部的变量，可以使用这种方法来创建私有变量。
> 函数的另一个用途是使已经运行结束的函数上下文中的变量对象继续留在内存中，因为闭包函数保留了这个变量对象的引用，所以这个变量对象不会被回收。

## 12.三种事件模型
1. **DOM0级模型**：这种模型不会传播，所以没有事件流的概念，但是现在有的浏览器支持以冒泡的方式实现，它可以在网页中直接定义监听函数，也可以通过 js属性来指定监听函数。这种方式是所有浏览器都兼容的。
2. **IE 事件模型**： 在该事件模型中，一次事件共有两个过程，事件处理阶段，和事件冒泡阶段。事件处理阶段会首先执行目标元素绑定的监听事件。然后是事件冒泡阶段，冒泡指的是事件从目标元素冒泡document，依次检查经过的节点是否绑定了事件监听函数，如果有则执行。这种模型通过 attachEvent 来添加监听函数，可以添加多个监听函数，会按顺序依次执行。
3. **DOM2 级事件模型**： 在该事件模型中，一次事件共有三个过程，第一个过程是事件捕获阶段。捕获指的是事件从 document 一直向下传播到目标元素，依次检查经过的节点是否绑定了事件监听函数，如果有则执行。后面两个阶段和 IE 事件模型的两个阶段相同。这种事件模型，事件绑定的函数是 addEventListener，其中第三个参数可以指定事件是否在捕获阶段执行。

## 13.事件委托
**事件委托** 本质上是利用了浏览器事件冒泡的机制。因为事件在冒泡过程中会上传到父节点，并且父节点可以通过事件对象获取到 目标节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件，这种方式称为事件代理。

## 14.DOM操作

### (1) 创建新节点
```
    createDocumentFragment()    //创建一个DOM片段
    createElement()   //创建一个具体的元素
    createTextNode()   //创建一个文本节点
```
### (2) 添加、移除、替换、插入
```
    appendChild(node)
    removeChild(node)
    replaceChild(new,old)
    insertBefore(new,old)
```
### (3) 查找
```
    getElementById();
    getElementsByName();
    getElementsByTagName();
    getElementsByClassName();
    querySelector();
    querySelectorAll();
```
### (4) 属性操作
```
    getAttribute(key);
    setAttribute(key, value);
    hasAttribute(key);
    removeAttribute(key);
```

## 15.数组和字符串方法
![数组方法](/img/array20210302.jpg)
![字符串方法](/img/string20210302.jpg)

## 16. AJAX
```javascript
//(1) 原生js
//1：创建Ajax对象
var xhr = window.XMLHttpRequest?new XMLHttpRequest():new ActiveXObject('Microsoft.XMLHTTP');// 兼容IE6及以下版本
//2：配置 Ajax请求地址
xhr.open('get','index.xml',true);
//3：发送请求
xhr.send(null); // 严谨写法
//4:监听请求，接受响应
xhr.onreadysatechange=function(){
     if(xhr.readySate==4&&xhr.status==200 || xhr.status==304 )
          console.log(xhr.responsetXML)
}

//(2) jquery
  $.ajax({
          type:'post',
          url:'',
          async:ture,//async 异步  sync  同步
          data:data,//针对post请求
          dataType:'jsonp',
          success:function (msg) {

          },
          error:function (error) {

          }
        })

//(3)promise疯转

function getJSON(url) {
  // 创建一个 promise 对象
  let promise = new Promise(function(resolve, reject) {
    let xhr = new XMLHttpRequest();

    // 新建一个 http 请求
    xhr.open("GET", url, true);

    // 设置状态的监听函数
    xhr.onreadystatechange = function() {
      if (this.readyState !== 4) return;

      // 当请求成功或失败时，改变 promise 的状态
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };

    // 设置错误监听函数
    xhr.onerror = function() {
      reject(new Error(this.statusText));
    };

    // 设置响应的数据类型
    xhr.responseType = "json";

    // 设置请求头信息
    xhr.setRequestHeader("Accept", "application/json");

    // 发送 http 请求
    xhr.send(null);
  });

  return promise;
}
```

## 17.js延迟加载的方式
js 的加载、解析和执行会阻塞页面的渲染过程，因此我们希望 js 脚本能够尽可能的延迟加载，提高页面的渲染速度。
我了解到的几种方式是：  

1. 将 js 脚本放在文档的底部，来使 js 脚本尽可能的在最后来加载执行。
2. 给 js 脚本添加 defer属性，这个属性会让脚本的加载与文档的解析同步解析，然后在文档解析完成后再执行这个脚本文件，这样的话就能使页面的渲染不被阻塞。多个设置了 defer 属性的脚本按规范来说最后是顺序执行的，但是在一些浏览器中可能不是这样。
3. 给 js 脚本添加 async属性，这个属性会使脚本异步加载，不会阻塞页面的解析过程，但是当脚本加载完成后立即执行 js脚本，这个时候如果文档没有解析完成的话同样会阻塞。多个 async 属性的脚本的执行顺序是不可预测的，一般不会按照代码的顺序依次执行。
4. 动态创建 DOM 标签的方式，我们可以对文档的加载事件进行监听，当文档加载完成后再动态的创建 script 标签来引入 js 脚本。

## 18.js的几种模块规范
* 第一种是 CommonJS 方案，它通过 require 来引入模块，通过 module.exports 定义模块的输出接口。这种模块加载方案是服务器端的解决方案，它是以同步的方式来引入模块的，因为在服务端文件都存储在本地磁盘，所以读取非常快，所以以同步的方式加载没有问题。但如果是在浏览器端，由于模块的加载是使用网络请求，因此使用异步加载的方式更加合适。
* 第二种是 AMD 方案，这种方案采用异步加载的方式来加载模块，模块的加载不影响后面语句的执行，所有依赖这个模块的语句都定义在一个回调函数里，等到加载完成后再执行回调函数。require.js 实现了 AMD 规范。
* 第三种是 CMD 方案，这种方案和 AMD 方案都是为了解决异步模块加载的问题，sea.js 实现了 CMD 规范。它和require.js的区别在于模块定义时对依赖的处理不同和对依赖模块的执行时机的处理不同。
* 第四种方案是 ES6 提出的方案，使用 import 和 export 的形式来导入导出模块。

## 19.ES6 模块与 CommonJS 模块、AMD、CMD 的差异。
1. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。CommonJS 模块输出的是值的，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。ES6 模块的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令 import，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。
2. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。CommonJS 模块就是对象，即在输入时是先加载整个模块，生成一个对象，然后再从这个对象上面读取方法，这种加载称为“运行时加载”。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。

## 20.requireJS的核心原理
```
require.js 的核心原理是通过动态创建 script 脚本来异步引入模块，然后对每个脚本的 load 事件进行监听，如果每个脚本都加载完成了，再调用回调函数。
```
 
## 21.谈谈JS的运行机制
### 1.js单线程
JavaScript语言的一大特点就是单线程，即同一时间只能做一件事情。
```
avaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？
所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。
``` 
### 2.js事件循环
js代码执行过程中会有很多任务，这些任务总的分成两类
```
* 同步任务
* 异步任务
``` 
![事件循环](/img/event20210302.jpg)
我们解释一下这张图：

* 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
* 当指定的事情完成时，Event Table会将这个函数移入Event Queue。
* 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
* 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

那主线程执行栈何时为空呢？js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数。  
  
以上就是js运行的整体流程  
  
需要注意的是除了同步任务和异步任务，任务还可以更加细分为macrotask(宏任务)和microtask(微任务)，js引擎会优先执行微任务
```
微任务包括了 promise 的回调、node 中的 process.nextTick 、对 Dom 变化监听的 MutationObserver。

宏任务包括了 script 脚本的执行、setTimeout ，setInterval ，setImmediate 一类的定时事件，还有如 I/O 操作、UI 渲
染等。
```
*总结*：

1. 首先js 是单线程运行的，在代码执行的时候，通过将不同函数的执行上下文压入执行栈中来保证代码的有序执行。
2. 在执行同步代码的时候，如果遇到了异步事件，js 引擎并不会一直等待其返回结果，而是会将这个事件挂起，继续执行执行栈中的其他任务
3. 当同步事件执行完毕后，再将异步事件对应的回调加入到与当前执行栈中不同的另一个任务队列中等待执行。
4. 任务队列可以分为宏任务对列和微任务对列，当当前执行栈中的事件执行完毕后，js 引擎首先会判断微任务对列中是否有任务可以执行，如果有就将微任务队首的事件压入栈中执行。
5. 当微任务对列中的任务都执行完成后再去判断宏任务对列中的任务。

最后可以用下面一道题检测一下收获：
```
setTimeout(function() {
  console.log(1)
}, 0);
new Promise(function(resolve, reject) {
  console.log(2);
  resolve()
}).then(function() {
  console.log(3)
});
process.nextTick(function () {
  console.log(4)
})
console.log(5)
```
第一轮：主线程开始执行，遇到setTimeout，将setTimeout的回调函数丢到宏任务队列中，在往下执行new Promise立即执行，输出2，then的回调函数丢到微任务队列中，再继续执行，遇到process.nextTick，同样将回调函数扔到为任务队列，再继续执行，输出5，当所有同步任务执行完成后看有没有可以执行的微任务，发现有then函数和nextTick两个微任务，先执行哪个呢？process.nextTick指定的异步任务总是发生在所有异步任务之前，因此先执行process.nextTick输出4然后执行then函数输出3，第一轮执行结束。
第二轮：从宏任务队列开始，发现setTimeout回调，输出1执行完毕，因此结果是25431

## 22. arguments 的对象是什么？
arguments对象是函数中传递的参数值的集合。它是一个类似数组的对象，因为它有一个length属性，我们可以使用数组索引表示法arguments[1]来访问单个值，但它没有数组中的内置方法，如：forEach、reduce、filter和map。  
我们可以使用Array.prototype.slice将arguments对象转换成一个数组。
```javascript
function one() {
  return Array.prototype.slice.call(arguments);
}
```
注意:箭头函数中没有arguments对象。

## 23. V8引擎的垃圾回收机制？
```
v8 的垃圾回收机制基于分代回收机制，这个机制又基于世代假说，这个假说有两个特点，一是新生的对象容易早死，另一个是不死的对象会活得更久。基于这个假说，v8 引擎将内存分为了新生代和老生代。

新创建的对象或者只经历过一次的垃圾回收的对象被称为新生代。经历过多次垃圾回收的对象被称为老生代。

新生代被分为 From 和 To 两个空间，To 一般是闲置的。当 From 空间满了的时候会执行 Scavenge 算法进行垃圾回收。当我们执行垃圾回收算法的时候应用逻辑将会停止，等垃圾回收结束后再继续执行。这个算法分为三步：

（1）首先检查 From 空间的存活对象，如果对象存活则判断对象是否满足晋升到老生代的条件，如果满足条件则晋升到老生代。如果不满足条件则移动 To 空间。

（2）如果对象不存活，则释放对象的空间。

（3）最后将 From 空间和 To 空间角色进行交换。

新生代对象晋升到老生代有两个条件：

（1）第一个是判断是对象否已经经过一次 Scavenge 回收。若经历过，则将对象从 From 空间复制到老生代中；若没有经历，则复制到 To 空间。

（2）第二个是 To 空间的内存使用占比是否超过限制。当对象从 From 空间复制到 To 空间时，若 To 空间使用超过 25%，则对象直接晋升到老生代中。设置 25% 的原因主要是因为算法结束后，两个空间结束后会交换位置，如果 To 空间的内存太小，会影响后续的内存分配。

老生代采用了标记清除法和标记压缩法。标记清除法首先会对内存中存活的对象进行标记，标记结束后清除掉那些没有标记的对象。由于标记清除后会造成很多的内存碎片，不便于后面的内存分配。所以了解决内存碎片的问题引入了标记压缩法。

由于在进行垃圾回收的时候会暂停应用的逻辑，对于新生代方法由于内存小，每次停顿的时间不会太长，但对于老生代来说每次垃圾回收的时间长，停顿会造成很大的影响。 为了解决这个问题 V8 引入了增量标记的方法，将一次停顿进行的过程分为了多步，每次执行完一小步就让运行逻辑执行一会，就这样交替运行。
```

## 24.那些操作会造成内存泄漏
* 1.意外的全局变量
* 2.被遗忘的计时器或回调函数
* 3.脱离 DOM 的引用
* 4.闭包


* 第一种情况是我们由于使用未声明的变量，而意外的创建了一个全局变量，而使这个变量一直留在内存中无法被回收。
* 第二种情况是我们设置了setInterval定时器，而忘记取消它，如果循环函数有对外部变量的引用的话，那么这个变量会被一直留在内存中，而无法被回收。
* 第三种情况是我们获取一个DOM元素的引用，而后面这个元素被删除，由于我们一直保留了对这个元素的引用，所以它也无法被回收。
* 第四种情况是不合理的使用闭包，从而导致某些变量一直被留在内存当中。

## 25.ECMAScript 2015（ES6）有哪些新特性？
```
块作用域
类
箭头函数
模板字符串
加强的对象字面
对象解构
Promise
模块
Symbol
代理（proxy）Set
函数默认参数
rest 和展开
```

## 25.var,let和const的区别是什么？
var声明的变量会挂载在window上，而let和const声明的变量不会：
```js
var a = 100;
console.log(a,window.a);    // 100 100

let b = 10;
console.log(b,window.b);    // 10 undefined

const c = 1;
console.log(c,window.c);    // 1 undefined
```
var声明变量存在变量提升，let和const不存在变量提升:
console.log(a); // undefined  ===>  a已声明还没赋值，默认得到undefined值
var a = 100;

console.log(b); // 报错：b is not defined  ===> 找不到b这个变量
let b = 10;

console.log(c); // 报错：c is not defined  ===> 找不到c这个变量
const c = 10;
```
let和const声明形成块作用域
```js
if(1){
  var a = 100;
  let b = 10;
}

console.log(a); // 100
console.log(b)  // 报错：b is not defined  ===> 找不到b这个变量

-------------------------------------------------------------

if(1){
  var a = 100;
  const c = 1;
}
console.log(a); // 100
console.log(c)  // 报错：c is not defined  ===> 找不到c这个变量
```
同一作用域下let和const不能声明同名变量，而var可以
```js
var a = 100;
console.log(a); // 100

var a = 10;
console.log(a); // 10
-------------------------------------
let a = 100;
let a = 10;

//  控制台报错：Identifier 'a' has already been declared  ===> 标识符a已经被声明了。
```
暂存死区
```js
var a = 100;

if(1){
    a = 10;
    //在当前块作用域中存在a使用let/const声明的情况下，给a赋值10时，只会在当前作用域找变量a，
    // 而这时，还未到声明时候，所以控制台Error:a is not defined
    let a = 1;
}
```
const
```js
/*
* 　　1、一旦声明必须赋值,不能使用null占位。
*
* 　　2、声明后不能再修改
*
* 　　3、如果声明的是复合类型数据，可以修改其属性
*
* */

const a = 100; 

const list = [];
list[0] = 10;
console.log(list);　　// [10]

const obj = {a:100};
obj.name = 'apple';
obj.a = 10000;
console.log(obj);　　// {a:10000,name:'apple'}
```
## 26. 什么是箭头函数？
箭头函数表达式的语法比函数表达式更简洁，并且没有自己的this，arguments，super或new.target。箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。
```js
//ES5 Version
var getCurrentDate = function (){
  return new Date();
}

//ES6 Version
const getCurrentDate = () => new Date();
```
在本例中，ES5 版本中有function(){}声明和return关键字，这两个关键字分别是创建函数和返回值所需要的。在箭头函数版本中，我们只需要()括号，不需要 return 语句，因为如果我们只有一个表达式或值需要返回，箭头函数就会有一个隐式的返回。
```js
//ES5 Version
function greet(name) {
  return 'Hello ' + name + '!';
}

//ES6 Version
const greet = (name) => `Hello ${name}`;
const greet2 = name => `Hello ${name}`;
```
我们还可以在箭头函数中使用与函数表达式和函数声明相同的参数。如果我们在一个箭头函数中有一个参数，则可以省略括号。
```js
const getArgs = () => arguments

const getArgs2 = (...rest) => rest
```
箭头函数不能访问arguments对象。所以调用第一个getArgs函数会抛出一个错误。相反，我们可以使用rest参数来获得在箭头函数中传递的所有参数。
```js
const data = {
  result: 0,
  nums: [1, 2, 3, 4, 5],
  computeResult() {
    // 这里的“this”指的是“data”对象
    const addAll = () => {
      return this.nums.reduce((total, cur) => total + cur, 0)
    };
    this.result = addAll();
  }
};
```
箭头函数没有自己的this值。它捕获词法作用域函数的this值，在此示例中，addAll函数将复制computeResult 方法中的this值，如果我们在全局作用域声明箭头函数，则this值为 window 对象。

## 27. 什么是类？
类(class)是在 JS 中编写构造函数的新方法。它是使用构造函数的语法糖，在底层中使用仍然是原型和基于原型的继承。
```js
 //ES5 Version
   function Person(firstName, lastName, age, address){
      this.firstName = firstName;
      this.lastName = lastName;
      this.age = age;
      this.address = address;
   }

   Person.self = function(){
     return this;
   }

   Person.prototype.toString = function(){
     return "[object Person]";
   }

   Person.prototype.getFullName = function (){
     return this.firstName + " " + this.lastName;
   }  

   //ES6 Version
   class Person {
        constructor(firstName, lastName, age, address){
            this.lastName = lastName;
            this.firstName = firstName;
            this.age = age;
            this.address = address;
        }

        static self() {
           return this;
        }

        toString(){
           return "[object Person]";
        }

        getFullName(){
           return `${this.firstName} ${this.lastName}`;
        }
   }
```
重写方法并从另一个类继承。
```js
//ES5 Version
Employee.prototype = Object.create(Person.prototype);

function Employee(firstName, lastName, age, address, jobTitle, yearStarted) {
  Person.call(this, firstName, lastName, age, address);
  this.jobTitle = jobTitle;
  this.yearStarted = yearStarted;
}

Employee.prototype.describe = function () {
  return `I am ${this.getFullName()} and I have a position of ${this.jobTitle} and I started at ${this.yearStarted}`;
}

Employee.prototype.toString = function () {
  return "[object Employee]";
}

//ES6 Version
class Employee extends Person { //Inherits from "Person" class
  constructor(firstName, lastName, age, address, jobTitle, yearStarted) {
    super(firstName, lastName, age, address);
    this.jobTitle = jobTitle;
    this.yearStarted = yearStarted;
  }

  describe() {
    return `I am ${this.getFullName()} and I have a position of ${this.jobTitle} and I started at ${this.yearStarted}`;
  }

  toString() { // Overriding the "toString" method of "Person"
    return "[object Employee]";
  }
}
```
所以我们要怎么知道它在内部使用原型？
```js
class Something {

}

function AnotherSomething(){

}
const as = new AnotherSomething();
const s = new Something();

console.log(typeof Something); // "function"
console.log(typeof AnotherSomething); // "function"
console.log(as.toString()); // "[object Object]"
console.log(as.toString()); // "[object Object]"
console.log(as.toString === Object.prototype.toString); // true
console.log(s.toString === Object.prototype.toString); // true
```

28. 什么是模板字符串？
模板字符串是在 JS 中创建字符串的一种新方法。我们可以通过使用反引号使模板字符串化。
```js
//ES5 Version
var greet = 'Hi I\'m Mark';

//ES6 Version
let greet = `Hi I'm Mark`;
```
在 ES5 中我们需要使用一些转义字符来达到多行的效果，在模板字符串不需要这么麻烦：
//ES5 Version
var lastWords = '\n'
  + '   I  \n'
  + '   Am  \n'
  + 'Iron Man \n';


//ES6 Version
let lastWords = `
    I
    Am
  Iron Man   
`;
```
在ES5版本中，我们需要添加\n以在字符串中添加新行。在模板字符串中，我们不需要这样做。
```js
//ES5 Version
function greet(name) {
  return 'Hello ' + name + '!';
}


//ES6 Version
function greet(name) {
  return `Hello ${name} !`;
}
```
在 ES5 版本中，如果需要在字符串中添加表达式或值，则需要使用+运算符。在模板字符串s中，我们可以使用${expr}嵌入一个表达式，这使其比 ES5 版本更整洁。

29. 什么是对象解构？
对象析构是从对象或数组中获取或提取值的一种新的、更简洁的方法。假设有如下的对象：
```js
const employee = {
  firstName: "Marko",
  lastName: "Polo",
  position: "Software Developer",
  yearHired: 2017
};
```
从对象获取属性，早期方法是创建一个与对象属性同名的变量。这种方法很麻烦，因为我们要为每个属性创建一个新变量。假设我们有一个大对象，它有很多属性和方法，用这种方法提取属性会很麻烦。
```js
var firstName = employee.firstName;
var lastName = employee.lastName;
var position = employee.position;
var yearHired = employee.yearHired;
```
使用解构方式语法就变得简洁多了：
```js
{ firstName, lastName, position, yearHired } = employee;
```
我们还可以为属性取别名：
```js
let { firstName: fName, lastName: lName, position, yearHired } = employee;
```
当然如果属性值为 undefined 时，我们还可以指定默认值：
```js
let { firstName = "Mark", lastName: lName, position, yearHired } = employee;
```
## 30. 什么是Set对象，它是如何工作的？
Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。  
我们可以使用Set构造函数创建Set实例。
```js
const set1 = new Set();
const set2 = new Set(["a","b","c","d","d","e"]);
```
我们可以使用add方法向Set实例中添加一个新值，因为add方法返回Set对象，所以我们可以以链式的方式再次使用add。如果一个值已经存在于Set对象中，那么它将不再被添加。
```js
set2.add("f");
set2.add("g").add("h").add("i").add("j").add("k").add("k");
// 后一个“k”不会被添加到set对象中，因为它已经存在了
```
我们可以使用has方法检查Set实例中是否存在特定的值。
```js
set2.has("a") // true
set2.has("z") // true
```
我们可以使用size属性获得Set实例的长度。
```js
set2.size // returns 10
```
可以使用clear方法删除 Set 中的数据。
```js
set2.clear();
```
我们可以使用Set对象来删除数组中重复的元素。
```js
const numbers = [1, 2, 3, 4, 5, 6, 6, 7, 8, 8, 5];
const uniqueNums = [...new Set(numbers)]; // [1,2,3,4,5,6,7,8]
```  
另外还有WeakSet， 与 Set 类似，也是不重复的值的集合。但是 WeakSet 的成员只能是对象，而不能是其他类型的值。WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet对该对象的引用。   


Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。   


WeakMap 结构与 Map 结构类似，也是用于生成键值对的集合。但是 WeakMap 只接受对象作为键名（ null 除外），不接受其他类型的值作为键名。而且 WeakMap 的键名所指向的对象，不计入垃圾回收机制。   


## 30. 什么是Proxy？
Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”，即对编程语言进行编程。  
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。
高能预警⚡⚡⚡，


## 31. 写一个通用的事件侦听器函数
```js
const EventUtils = {
  // 视能力分别使用dom0||dom2||IE方式 来绑定事件
  // 添加事件
  addEvent: function(element, type, handler) {
    if (element.addEventListener) {
      element.addEventListener(type, handler, false);
    } else if (element.attachEvent) {
      element.attachEvent("on" + type, handler);
    } else {
      element["on" + type] = handler;
    }
  },

  // 移除事件
  removeEvent: function(element, type, handler) {
    if (element.removeEventListener) {
      element.removeEventListener(type, handler, false);
    } else if (element.detachEvent) {
      element.detachEvent("on" + type, handler);
    } else {
      element["on" + type] = null;
    }
  },

  // 获取事件目标
  getTarget: function(event) {
    return event.target || event.srcElement;
  },

  // 获取 event 对象的引用，取到事件的所有信息，确保随时能使用 event
  getEvent: function(event) {
    return event || window.event;
  },

  // 阻止事件（主要是事件冒泡，因为 IE 不支持事件捕获）
  stopPropagation: function(event) {
    if (event.stopPropagation) {
      event.stopPropagation();
    } else {
      event.cancelBubble = true;
    }
  },

  // 取消事件的默认行为
  preventDefault: function(event) {
    if (event.preventDefault) {
      event.preventDefault();
    } else {
      event.returnValue = false;
    }
  }
};
```
## 32.  什么是函数式编程? JavaScript的哪些特性使其成为函数式语言的候选语言？
函数式编程（通常缩写为FP）是通过编写纯函数，避免共享状态、可变数据、副作用 来构建软件的过程。数式编程是声明式 的而不是命令式 的，应用程序的状态是通过纯函数流动的。与面向对象编程形成对比，面向对象中应用程序的状态通常与对象中的方法共享和共处。
函数式编程是一种编程范式 ，这意味着它是一种基于一些基本的定义原则（如上所列）思考软件构建的方式。当然，编程范式的其他示例也包括面向对象编程和过程编程。
函数式的代码往往比命令式或面向对象的代码更简洁，更可预测，更容易测试 - 但如果不熟悉它以及与之相关的常见模式，函数式的代码也可能看起来更密集杂乱，并且 相关文献对新人来说是不好理解的。
## 33. 什么是高阶函数？
高阶函数只是将函数作为参数或返回值的函数。
```js
function higherOrderFunction(param,callback){
    return callback(param);
}
```
## 34. 为什么函数被称为一等公民？
在JavaScript中，函数不仅拥有一切传统函数的使用方式（声明和调用），而且可以做到像简单值一样:    
赋值（var func = function(){}）、 
传参(function func(x,callback){callback();})、   
返回(function(){return function(){}})，   

这样的函数也称之为第一级函数（First-class Function）。不仅如此，JavaScript中的函数还充当了类的构造函数的作用，同时又是一个Function类的实例(instance)。这样的多重身份让JavaScript的函数变得非常重要。
## 35. 手动实现 Array.prototype.map 方法
map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。
```js
function map(arr, mapCallback) {
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof mapCallback !== 'function') { 
    return [];
  } else {
    let result = [];
    // 每次调用此函数时，我们都会创建一个 result 数组
    // 因为我们不想改变原始数组。
    for (let i = 0, len = arr.length; i < len; i++) {
      result.push(mapCallback(arr[i], i, arr)); 
      // 将 mapCallback 返回的结果 push 到 result 数组中
    }
    return result;
  }
}
```
## 36. 手动实现Array.prototype.filter方法
filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
```js
function filter(arr, filterCallback) {
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof filterCallback !== 'function') 
  {
    return [];
  } else {
    let result = [];
     // 每次调用此函数时，我们都会创建一个 result 数组
     // 因为我们不想改变原始数组。
    for (let i = 0, len = arr.length; i < len; i++) {
      // 检查 filterCallback 的返回值是否是真值
      if (filterCallback(arr[i], i, arr)) { 
      // 如果条件为真，则将数组元素 push 到 result 中
        result.push(arr[i]);
      }
    }
    return result; // return the result array
  }
}
```
## 37.  手动实现Array.prototype.reduce方法
reduce() 方法对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值。
```js
function reduce(arr, reduceCallback, initialValue) {
  // 首先，检查传递的参数是否正确。
  if (!Array.isArray(arr) || !arr.length || typeof reduceCallback !== 'function') 
  {
    return [];
  } else {
    // 如果没有将initialValue传递给该函数，我们将使用第一个数组项作为initialValue
    let hasInitialValue = initialValue !== undefined;
    let value = hasInitialValue ? initialValue : arr[0];
   、

    // 如果有传递 initialValue，则索引从 1 开始，否则从 0 开始
    for (let i = hasInitialValue ? 1 : 0, len = arr.length; i < len; i++) {
      value = reduceCallback(value, arr[i], i, arr); 
    }
    return value;
  }
}
```
## 38. js的深浅拷贝
JavaScript的深浅拷贝一直是个难点，如果现在面试官让我写一个深拷贝，我可能也只是能写出个基础版的。所以在写这条之前我拜读了收藏夹里各路大佬写的博文。具体可以看下面我贴的链接，这里只做简单的总结。   

浅拷贝： 创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。  
深拷贝： 将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象。  

浅拷贝的实现方式：   

Object.assign() 方法： 用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。  
**Array.prototype.slice()：**slice() 方法返回一个新的数组对象，这一对象是一个由 begin和end（不包括end）决定的原数组的浅拷贝。原始数组不会被改变。  
拓展运算符...：  
```js
let a = {
    name: "Jake",
    flag: {
        title: "better day by day",
        time: "2020-05-31"
    }
}
let b = {...a};
```
深拷贝的实现方式：  

乞丐版： JSON.parse(JSON.stringify(object))，缺点诸多（会忽略undefined、symbol、函数；不能解决循环引用；不能处理正则、new Date()）  
基础版（面试够用）： 浅拷贝+递归 （只考虑了普通的 object和 array两种数据类型）  
```js
function cloneDeep(target,map = new WeakMap()) {
  if(typeOf taret ==='object'){
     let cloneTarget = Array.isArray(target) ? [] : {};
      
     if(map.get(target)) {
        return target;
    }
     map.set(target, cloneTarget);
     for(const key in target){
        cloneTarget[key] = cloneDeep(target[key], map);
     }
     return cloneTarget
  }else{
       return target
  }
 
}

```

终极版：  
```js
const mapTag = '[object Map]';
const setTag = '[object Set]';
const arrayTag = '[object Array]';
const objectTag = '[object Object]';
const argsTag = '[object Arguments]';

const boolTag = '[object Boolean]';
const dateTag = '[object Date]';
const numberTag = '[object Number]';
const stringTag = '[object String]';
const symbolTag = '[object Symbol]';
const errorTag = '[object Error]';
const regexpTag = '[object RegExp]';
const funcTag = '[object Function]';

const deepTag = [mapTag, setTag, arrayTag, objectTag, argsTag];


function forEach(array, iteratee) {
    let index = -1;
    const length = array.length;
    while (++index < length) {
        iteratee(array[index], index);
    }
    return array;
}

function isObject(target) {
    const type = typeof target;
    return target !== null && (type === 'object' || type === 'function');
}

function getType(target) {
    return Object.prototype.toString.call(target);
}

function getInit(target) {
    const Ctor = target.constructor;
    return new Ctor();
}

function cloneSymbol(targe) {
    return Object(Symbol.prototype.valueOf.call(targe));
}

function cloneReg(targe) {
    const reFlags = /\w*$/;
    const result = new targe.constructor(targe.source, reFlags.exec(targe));
    result.lastIndex = targe.lastIndex;
    return result;
}

function cloneFunction(func) {
    const bodyReg = /(?<={)(.|\n)+(?=})/m;
    const paramReg = /(?<=\().+(?=\)\s+{)/;
    const funcString = func.toString();
    if (func.prototype) {
        const param = paramReg.exec(funcString);
        const body = bodyReg.exec(funcString);
        if (body) {
            if (param) {
                const paramArr = param[0].split(',');
                return new Function(...paramArr, body[0]);
            } else {
                return new Function(body[0]);
            }
        } else {
            return null;
        }
    } else {
        return eval(funcString);
    }
}

function cloneOtherType(targe, type) {
    const Ctor = targe.constructor;
    switch (type) {
        case boolTag:
        case numberTag:
        case stringTag:
        case errorTag:
        case dateTag:
            return new Ctor(targe);
        case regexpTag:
            return cloneReg(targe);
        case symbolTag:
            return cloneSymbol(targe);
        case funcTag:
            return cloneFunction(targe);
        default:
            return null;
    }
}

function clone(target, map = new WeakMap()) {

    // 克隆原始类型
    if (!isObject(target)) {
        return target;
    }

    // 初始化
    const type = getType(target);
    let cloneTarget;
    if (deepTag.includes(type)) {
        cloneTarget = getInit(target, type);
    } else {
        return cloneOtherType(target, type);
    }

    // 防止循环引用
    if (map.get(target)) {
        return map.get(target);
    }
    map.set(target, cloneTarget);

    // 克隆set
    if (type === setTag) {
        target.forEach(value => {
            cloneTarget.add(clone(value, map));
        });
        return cloneTarget;
    }

    // 克隆map
    if (type === mapTag) {
        target.forEach((value, key) => {
            cloneTarget.set(key, clone(value, map));
        });
        return cloneTarget;
    }

    // 克隆对象和数组
    const keys = type === arrayTag ? undefined : Object.keys(target);
    forEach(keys || target, (value, key) => {
        if (keys) {
            key = value;
        }
        cloneTarget[key] = clone(target[key], map);
    });

    return cloneTarget;
}

module.exports = {
    clone
};
```

## 39. 手写call、apply及bind函数
call 函数的实现步骤：  

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2. 判断传入上下文对象是否存在，如果不存在，则设置为 window 。
3. 处理传入的参数，截取第一个参数后的所有参数。
4. 将函数作为上下文对象的一个属性。
5. 使用上下文对象来调用这个方法，并保存返回结果。
6. 删除刚才新增的属性。
7. 返回结果。
```js
// call函数实现
Function.prototype.myCall = function(context) {
  // 判断调用对象
  if (typeof this !== "function") {
    console.error("type error");
  }

  // 获取参数
  let args = [...arguments].slice(1),
    result = null;

  // 判断 context 是否传入，如果未传入则设置为 window
  context = context || window;

  // 将调用函数设为对象的方法
  context.fn = this;

  // 调用函数
  result = context.fn(...args);

  // 将属性删除
  delete context.fn;

  return result;
};
```
apply 函数的实现步骤：

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。 
2. 判断传入上下文对象是否存在，如果不存在，则设置为 window 。 
3. 将函数作为上下文对象的一个属性。 
4. 判断参数值是否传入 
5. 使用上下文对象来调用这个方法，并保存返回结果。 
6. 删除刚才新增的属性 
7. 返回结果 

```js
// apply 函数实现

Function.prototype.myApply = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }

  let result = null;

  // 判断 context 是否存在，如果未传入则为 window
  context = context || window;

  // 将函数设为对象的方法
  context.fn = this;

  // 调用方法
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }

  // 将属性删除
  delete context.fn;

  return result;
};
```
bind 函数的实现步骤：  

1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2. 保存当前函数的引用，获取其余传入参数值。
3. 创建一个函数返回
4. 函数内部使用 apply 来绑定函数调用，需要判断函数作为构造函数的情况，这个时候需要传入当前函数的 this 给 apply 调用，其余情况都传入指定的上下文对象。

```js
// bind 函数实现
Function.prototype.myBind = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }

  // 获取参数
  var args = [...arguments].slice(1),
    fn = this;

  return function Fn() {
    // 根据调用方式，传入不同绑定值
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments)
    );
  };
};
```
## 40. 函数柯里化的实现
```js
// 函数柯里化指的是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。

function curry(fn, args) {
  // 获取函数需要的参数长度
  let length = fn.length;

  args = args || [];

  return function() {
    let subArgs = args.slice(0);

    // 拼接得到现有的所有参数
    for (let i = 0; i < arguments.length; i++) {
      subArgs.push(arguments[i]);
    }

    // 判断参数的长度是否已经满足函数所需参数的长度
    if (subArgs.length >= length) {
      // 如果满足，执行函数
      return fn.apply(this, subArgs);
    } else {
      // 如果不满足，递归返回科里化的函数，等待参数的传入
      return curry.call(this, fn, subArgs);
    }
  };
}

// es6 实现
function curry(fn, ...args) {
  return fn.length <= args.length ? fn(...args) : curry.bind(null, fn, ...args);
}
```

## 41. js模拟new操作符的实现
这个问题如果你在掘金上搜，你可能会搜索到类似下面的回答： 

说实话，看第一遍，我是不理解的，我需要去理一遍原型及原型链的知识才能理解。所以我觉得MDN对new的解释更容易理解：  
new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。new 关键字会进行如下的操作：   

1. 创建一个空的简单JavaScript对象（即{}）；  
2. 链接该对象（即设置该对象的构造函数）到另一个对象 ；  
3. 将步骤1新创建的对象作为this的上下文 ；  
4. 如果该函数没有返回对象，则返回this。  
```js
接下来我们看实现：
function Dog(name, color, age) {
  this.name = name;
  this.color = color;
  this.age = age;
}

Dog.prototype={
  getName: function() {
    return this.name
  }
}

var dog = new Dog('大黄', 'yellow', 3)

```
上面的代码相信不用解释，大家都懂。我们来看最后一行带new关键字的代码，按照上述的1,2,3,4步来解析new背后的操作。    
第一步：创建一个简单空对象
```js
var obj = {}
```
第二步：链接该对象到另一个对象（原型链）
```js
// 设置原型链
obj.__proto__ = Dog.prototype
```
第三步：将步骤1新创建的对象作为 this 的上下文
```js
// this指向obj对象
Dog.apply(obj, ['大黄', 'yellow', 3])
```
第四步：如果该函数没有返回对象，则返回this
```js
// 因为 Dog() 没有返回值，所以返回obj
var dog = obj
dog.getName() // '大黄'
```
需要注意的是如果 Dog() 有 return 则返回 return的值   
```js
var rtnObj = {}
function Dog(name, color, age) {
  // ...
  //返回一个对象
  return rtnObj
}

var dog = new Dog('大黄', 'yellow', 3)
console.log(dog === rtnObj) // true

```
接下来我们将以上步骤封装成一个对象实例化方法，即模拟new的操作：  
```js
function objectFactory(){
    var obj = {};
    //取得该方法的第一个参数(并删除第一个参数)，该参数是构造函数
    var Constructor = [].shift.apply(arguments);
    //将新对象的内部属性__proto__指向构造函数的原型，这样新对象就可以访问原型中的属性和方法
    obj.__proto__ = Constructor.prototype;
    //取得构造函数的返回值
    var ret = Constructor.apply(obj, arguments);
    //如果返回值是一个对象就返回该对象，否则返回构造函数的一个实例对象
    return typeof ret === "object" ? ret : obj;
}

```
## 42. 什么是回调函数？回调函数有什么缺点
回调函数是一段可执行的代码段，它作为一个参数传递给其他的代码，其作用是在需要的时候方便调用这段（回调函数）代码。 
在JavaScript中函数也是对象的一种，同样对象可以作为参数传递给函数，因此函数也可以作为参数传递给另外一个函数，这个作为参数的函数就是回调函数。 
```js
const btnAdd = document.getElementById('btnAdd');

btnAdd.addEventListener('click', function clickCallback(e) {
    // do something useless
});
```
在本例中，我们等待id为btnAdd的元素中的click事件，如果它被单击，则执行clickCallback函数。回调函数向某些数据或事件添加一些功能。 
回调函数有一个致命的弱点，就是容易写出回调地狱（Callback hell）。假设多个事件存在依赖性： 
```js
setTimeout(() => {
    console.log(1)
    setTimeout(() => {
        console.log(2)
        setTimeout(() => {
            console.log(3)
    
        },3000)
    
    },2000)
},1000)
```
这就是典型的回调地狱，以上代码看起来不利于阅读和维护，事件一旦多起来就更是乱糟糟，所以在es6中提出了Promise和async/await来解决回调地狱的问题。当然，回调函数还存在着别的几个缺点，比如不能使用 try catch 捕获错误，不能直接 return。接下来的两条就是来解决这些问题的，咱们往下看。

## 43. Promise是什么，可以手写实现一下吗？
Promise，翻译过来是承诺，承诺它过一段时间会给你一个结果。从编程讲Promise 是异步编程的一种解决方案。下面是Promise在MDN的相关说明：     
Promise 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象。  
一个 Promise有以下几种状态:  
  
* pending: 初始状态，既不是成功，也不是失败状态。
* fulfilled: 意味着操作成功完成。
* rejected: 意味着操作失败。

这个承诺一旦从等待状态变成为其他状态就永远不能更改状态了，也就是说一旦状态变为 fulfilled/rejected 后，就不能再次改变。
可能光看概念大家不理解Promise，我们举个简单的栗子；  

假如我有个女朋友，下周一是她生日，我答应她生日给她一个惊喜，那么从现在开始这个承诺就进入等待状态，等待下周一的到来，然后状态改变。如果下周一我如约给了女朋友惊喜，那么这个承诺的状态就会由pending切换为fulfilled，表示承诺成功兑现，一旦是这个结果了，就不会再有其他结果，即状态不会在发生改变；反之如果当天我因为工作太忙加班，把这事给忘了，说好的惊喜没有兑现，状态就会由pending切换为rejected，时间不可倒流，所以状态也不能再发生变化。  

上一条我们说过Promise可以解决回调地狱的问题，没错，pending 状态的 Promise 对象会触发 fulfilled/rejected 状态，一旦状态改变，Promise 对象的 then 方法就会被调用；否则就会触发 catch。我们将上一条回调地狱的代码改写一下：  
```js
new Promise((resolve，reject) => {
     setTimeout(() => {
            console.log(1)
            resolve()
        },1000)
        
}).then((res) => {
    setTimeout(() => {
            console.log(2)
        },2000)
}).then((res) => {
    setTimeout(() => {
            console.log(3)
        },3000)
}).catch((err) => {
console.log(err)
})
```
其实Promise也是存在一些缺点的，比如无法取消 Promise，错误需要通过回调函数捕获。  
promise手写实现，面试够用版：  
```js
function myPromise(constructor){
    let self=this;
    self.status="pending" //定义状态改变前的初始状态
    self.value=undefined;//定义状态为resolved的时候的状态
    self.reason=undefined;//定义状态为rejected的时候的状态
    function resolve(value){
        //两个==="pending"，保证了状态的改变是不可逆的
       if(self.status==="pending"){
          self.value=value;
          self.status="resolved";
       }
    }
    function reject(reason){
        //两个==="pending"，保证了状态的改变是不可逆的
       if(self.status==="pending"){
          self.reason=reason;
          self.status="rejected";
       }
    }
    //捕获构造异常
    try{
       constructor(resolve,reject);
    }catch(e){
       reject(e);
    }
}
// 定义链式调用的then方法
myPromise.prototype.then=function(onFullfilled,onRejected){
   let self=this;
   switch(self.status){
      case "resolved":
        onFullfilled(self.value);
        break;
      case "rejected":
        onRejected(self.reason);
        break;
      default:       
   }
}

```
关于Promise还有其他的知识，比如Promise.all()、Promise.race()等的运用，由于篇幅原因就不再做展开，想要深入了解的可看下面的文章。

## 44. Iterator是什么，有什么作用？  
Iterator是理解第61条的先决知识，也许是我IQ不够😭，Iterator和Generator看了很多遍还是一知半解，即使当时理解了，过一阵又忘得一干二净。。。  

Iterator（迭代器）是一种接口，也可以说是一种规范。为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。
  
Iterator语法：
```js
const obj = {
    [Symbol.iterator]:function(){}
}

```
[Symbol.iterator] 属性名是固定的写法，只要拥有了该属性的对象，就能够用迭代器的方式进行遍历。  

迭代器的遍历方法是首先获得一个迭代器的指针，初始时该指针指向第一条数据之前，接着通过调用 next 方法，改变指针的指向，让其指向下一条数据
每一次的 next 都会返回一个对象，该对象有两个属性 

>value 代表想要获取的数据
>done 布尔值，false表示当前指针指向的数据有值，true表示遍历已经结束

Iterator 的作用有三个：   

1. 为各种数据结构，提供一个统一的、简便的访问接口；
2. 使得数据结构的成员能够按某种次序排列；
3. ES6 创造了一种新的遍历命令for…of循环，Iterator 接口主要供for…of消费。

**遍历过程：**     

1. 创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。
2. 第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。
3. 第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。
4. 不断调用指针对象的next方法，直到它指向数据结构的结束位置。

每一次调用next方法，都会返回数据结构的当前成员的信息。具体来说，就是返回一个包含value和done两个属性的对象。其中，value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束。  
```js
let arr = [{num:1},2,3]
let it = arr[Symbol.iterator]() // 获取数组中的迭代器
console.log(it.next()) 	// { value: Object { num: 1 }, done: false }
console.log(it.next()) 	// { value: 2, done: false }
console.log(it.next()) 	// { value: 3, done: false }
console.log(it.next()) 	// { value: undefined, done: true }

```
## 45. Generator函数是什么，有什么作用？
Generator函数可以说是Iterator接口的具体实现方式。Generator 最大的特点就是可以控制函数的执行。  

```js
function *foo(x) {
  let y = 2 * (yield (x + 1))
  let z = yield (y / 3)
  return (x + y + z)
}
let it = foo(5)
console.log(it.next())   // => {value: 6, done: false}
console.log(it.next(12)) // => {value: 8, done: false}
console.log(it.next(13)) // => {value: 42, done: true}

```
上面这个示例就是一个Generator函数，我们来分析其执行过程：   

* 首先 Generator 函数调用时它会返回一个迭代器
* 当执行第一次 next 时，传参会被忽略，并且函数暂停在 yield (x + 1) 处，所以返回 5 + 1 = 6
* 当执行第二次 next 时，传入的参数等于上一个 yield 的返回值，如果你不传参，yield 永远返回 undefined。此时 let y = 2 * 12，所以第二个 yield 等于 2 * 12 / 3 = 8
* 当执行第三次 next 时，传入的参数会传递给 z，所以 z = 13, x = 5, y = 24，相加等于 42

Generator 函数一般见到的不多，其实也于他有点绕有关系，并且一般会配合 co 库去使用。当然，我们可以通过 Generator 函数解决回调地狱的问题。

## 46. 什么是 async/await 及其如何工作,有什么优缺点？

**async/await**是一种建立在Promise之上的编写异步或非阻塞代码的新方法，被普遍认为是 JS异步操作的最终且最优雅的解决方案。相对于 Promise 和回调，它的可读性和简洁度都更高。毕竟一直then()也很烦。

>async 是异步的意思，而 await 是 async wait的简写，即异步等待。

所以从语义上就很好理解 async 用于声明一个 function 是异步的，而await 用于等待一个异步方法执行完成。   
一个函数如果加上 async ，那么该函数就会返回一个 Promise
```js
async function test() {
  return "1"
}
console.log(test()) // -> Promise {<resolved>: "1"}
```
可以看到输出的是一个Promise对象。所以，async 函数返回的是一个 Promise 对象，如果在 async 函数中直接 return 一个直接量，async 会把这个直接量通过 PromIse.resolve() 封装成Promise对象返回。
相比于 Promise，async/await能更好地处理 then 链
```js
function takeLongTime(n) {
    return new Promise(resolve => {
        setTimeout(() => resolve(n + 200), n);
    });
}

function step1(n) {
    console.log(`step1 with ${n}`);
    return takeLongTime(n);
}

function step2(n) {
    console.log(`step2 with ${n}`);
    return takeLongTime(n);
}

function step3(n) {
    console.log(`step3 with ${n}`);
    return takeLongTime(n);
}

```
现在分别用 Promise 和async/await来实现这三个步骤的处理。   
使用Promise
```js

function doIt() {
    console.time("doIt");
    const time1 = 300;
    step1(time1)
        .then(time2 => step2(time2))
        .then(time3 => step3(time3))
        .then(result => {
            console.log(`result is ${result}`);
        });
}
doIt();
// step1 with 300
// step2 with 500
// step3 with 700
// result is 900

```
使用async/await
```js
async function doIt() {
    console.time("doIt");
    const time1 = 300;
    const time2 = await step1(time1);
    const time3 = await step2(time2);
    const result = await step3(time3);
    console.log(`result is ${result}`);
}
doIt();
```
结果和之前的 Promise 实现是一样的，但是这个代码看起来是不是清晰得多，优雅整洁，几乎跟同步代码一样。
```js
await关键字只能在async function中使用。在任何非async function的函数中使用await关键字都会抛出错误。await关键字在执行下一行代码之前等待右侧表达式(可能是一个Promise)返回。
```
**优缺点**：
`async/await`的优势在于处理 then 的调用链，能够更清晰准确的写出代码，并且也能优雅地解决回调地狱问题。当然也存在一些缺点，因为 await 将异步代码改造成了同步代码，如果多个异步代码没有依赖性却使用了 await 会导致性能上的降低。

## 47. instanceof的原理是什么，如何实现
instanceof 可以正确的判断对象的类型，因为内部机制是通过判断对象的原型链中是不是能找到类型的 prototype。  
实现 instanceof：  

1. 首先获取类型的原型
2. 然后获得对象的原型
3. 然后一直循环判断对象的原型是否等于类型的原型，直到对象原型为 null，因为原型链最终为 null

```js
function myInstanceof(left, right) {
  let prototype = right.prototype
  left = left.__proto__
  while (true) {
    if (left === null || left === undefined)
      return false
    if (prototype === left)
      return true
    left = left.__proto__
  }
}
```
## 48. js 的节流与防抖
**函数防抖** 是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。
函数节流 是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。

```js
// 函数防抖的实现
function debounce(fn, wait) {
  var timer = null;

  return function() {
    var context = this,
      args = arguments;

    // 如果此时存在定时器的话，则取消之前的定时器重新记时
    if (timer) {
      clearTimeout(timer);
      timer = null;
    }

    // 设置定时器，使事件间隔指定事件后执行
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, wait);
  };
}

// 函数节流的实现;
function throttle(fn, delay) {
  var preTime = Date.now();

  return function() {
    var context = this,
      args = arguments,
      nowTime = Date.now();

    // 如果两次时间间隔超过了指定时间，则执行函数。
    if (nowTime - preTime >= delay) {
      preTime = Date.now();
      return fn.apply(context, args);
    }
  };
}
```
## 49.for of, for in 和 forEach, map 的区别
* for...of循环：具有 iterator 接口，就可以用for...of循环遍历它的成员(属性值)。for...of循环可以使用的范围包括数组、Set 和 Map 结构、某些类似数组的对象、Generator 对象，以及字符串。for...of循环调用遍历器接口，数组的遍历器接口只返回具有数字索引的属性。对于普通的对象，for...of结构不能直接使用，会报错，必须部署了 Iterator 接口后才能使用。可以中断循环。
* for...in循环：遍历对象自身的和继承的可枚举的属性, 不能直接获取属性值。可以中断循环。
* forEach: 只能遍历数组，不能中断，没有返回值(或认为返回值是undefined)。会改变原数组（引用类型）。
* map: 只能遍历数组，不能中断，返回值是修改后的数组。会改变原数组。
PS: Object.keys()：返回给定对象所有可枚举属性的字符串数组。

## 50.如何判断一个变量是不是数组？
* 使用 Array.isArray 判断，如果返回 true, 说明是数组
* 使用 instanceof Array 判断，如果返回true, 说明是数组
* 使用 Object.prototype.toString.call 判断，如果值是 [object Array], 说明是数组
* 通过 constructor 来判断，如果是数组，那么 arr.constructor === Array. (不准确，因为我们可以指定 obj.constructor = Array)

## 51.类数组和数组的区别是什么？
类数组：
* 1）拥有length属性，其它属性（索引）为非负整数（对象中的索引会被当做字符串来处理）;

* 2）不具有数组所具有的方法；

类数组是一个普通对象，而真实的数组是Array类型。  
类数组可以转换为数组:  
```js
//第一种方法
Array.prototype.slice.call(arrayLike, start);
//第二种方法
[...arrayLike];
//第三种方法:
Array.from(arrayLike);
```
PS: 任何定义了遍历器（Iterator）接口的对象，都可以用扩展运算符转为真正的数组。   
 
Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象。  

## 52.ES6中的class和ES5的类有什么区别？
1. ES6 class 内部所有定义的方法都是不可枚举的;
2. ES6 class 必须使用 new 调用;
3. ES6 class 不存在变量提升;
4. ES6 class 默认即是严格模式;
5. ES6 class 子类必须在构造函数中调用super()，这样才有this对象;ES5中类继承的关系是相反的，先有子类的this，然后用父类的方法应用在this上。

## 53.数组的哪些API会改变原数组？
修改原数组的API有:
```
splice/reverse/fill/copyWithin/sort/push/pop/unshift/shift
```
不修改原数组的API有:
```
slice/map/forEach/every/filter/reduce/entries/find
```
注: 数组的每一项是简单数据类型，且未直接操作数组的情况下(稍后会对此题重新作答)。

## 54. let、const 以及 var 的区别是什么？

>let 和 const 定义的变量不会出现变量提升，而 var 定义的变量会提升。
>let 和 const 是JS中的块级作用域
>let 和 const 不允许重复声明(会抛出错误)
>let 和 const 定义的变量在定义语句之前，如果使用会抛出错误(形成了暂时性死区)，而 var 不会。
>const 声明一个只读的常量。一旦声明，常量的值就不能改变(如果声明是一个对象，那么不能改变的是对象的引用地址)


## 55. 在JS中什么是变量提升？什么是暂时性死区？
变量提升就是变量在声明之前就可以使用，值为undefined。   
在代码块内，使用 let/const 命令声明变量之前，该变量都是不可用的(会抛出错误)。这在语法上，称为“暂时性死区”。暂时性死区也意味着 typeof 不再是一个百分百安全的操作。
```
typeof x; // ReferenceError(暂时性死区，抛错)
let x;
```
```
typeof y; // 值是undefined,不会报错
```
暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

## 56. 如何正确的判断this? 箭头函数的this是什么？
this的绑定规则有四种：默认绑定，隐式绑定，显式绑定，new绑定.

1. 函数是否在 new 中调用(new绑定)，如果是，那么 this 绑定的是new中新创建的对象。
2. 函数是否通过 call,apply 调用，或者使用了 bind (即硬绑定)，如果是，那么this绑定的就是指定的对象。
3. 函数是否在某个上下文对象中调用(隐式绑定)，如果是的话，this 绑定的是那个上下文对象。一般是 obj.foo()
4. 如果以上都不是，那么使用默认绑定。如果在严格模式下，则绑定到 undefined，否则绑定到全局对象。
5. 如果把 null 或者 undefined 作为 this 的绑定对象传入 call、apply 或者 bind, 这些值在调用时会被忽略，实际应用的是默认绑定规则。
6. 箭头函数没有自己的 this, 它的this继承于上一层代码块的this。

## 57. 词法作用域和this的区别。
* 词法作用域是由你在写代码时将变量和块作用域写在哪里来决定的
* this 是在调用时被绑定的，this 指向什么，完全取决于函数的调用位置(关于this的指向问题，本文已经有说明)

## 58. promise 有几种状态, Promise 有什么优缺点 ?
promise有三种状态: fulfilled, rejected, pending.  

Promise 的优点:  


1. 一旦状态改变，就不会再变，任何时候都可以得到这个结果
2. 可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数


Promise 的缺点:  


1. 无法取消 Promise
2. 当处于pending状态时，无法得知目前进展到哪一个阶段


## 59. Promise构造函数是同步还是异步执行，then中的方法呢 ?promise如何实现then处理 ?

>Promise的构造函数是同步执行的。then 中的方法是异步执行的。
>promise的then实现，详见: Promise源码实现

## 60. Promise和setTimeout的区别 ?
Promise 是微任务，setTimeout 是宏任务，同一个事件循环中，promise.then总是先于 setTimeout 执行。

## 61. 如何实现 Promise.all ?
要实现 Promise.all,首先我们需要知道 Promise.all 的功能：

1. 如果传入的参数是一个空的可迭代对象，那么此promise对象回调完成(resolve),只有此情况，是同步执行的，其它都是异步返回的。
2. 如果传入的参数不包含任何 promise，则返回一个异步完成.

promises 中所有的promise都“完成”时或参数中不包含 promise 时回调完成。
3. 如果参数中有一个promise失败，那么Promise.all返回的promise对象失败
4. 在任何情况下，Promise.all 返回的 promise 的完成状态的结果都是一个数组
```js
Promise.all = function (promises) {
    return new Promise((resolve, reject) => {
        let index = 0;
        let result = [];
        if (promises.length === 0) {
            resolve(result);
        } else {
            function processValue(i, data) {
                result[i] = data;
                if (++index === promises.length) {
                    resolve(result);
                }
            }
            for (let i = 0; i < promises.length; i++) {
                //promises[i] 可能是普通值
                Promise.resolve(promises[i]).then((data) => {
                    processValue(i, data);
                }, (err) => {
                    reject(err);
                    return;
                });
            }
        }
    });
}
```

## 62.如何实现 Promise.prototype.finally ?
不管成功还是失败，都会走到finally中,并且finally之后，还可以继续then。并且会将值原封不动的传递给后面的then.
```js
Promise.prototype.finally = function (callback) {
    return this.then((value) => {
        return Promise.resolve(callback()).then(() => {
            return value;
        });
    }, (err) => {
        return Promise.resolve(callback()).then(() => {
            throw err;
        });
    });
}
```
##  63.说一说JS异步发展史
异步最早的解决方案是回调函数，如事件的回调，setInterval/setTimeout中的回调。但是回调函数有一个很常见的问题，就是回调地狱的问题(稍后会举例说明);  
为了解决回调地狱的问题，社区提出了Promise解决方案，ES6将其写进了语言标准。Promise解决了回调地狱的问题，但是Promise也存在一些问题，如错误不能被try catch，而且使用Promise的链式调用，其实并没有从根本上解决回调地狱的问题，只是换了一种写法。  
ES6中引入 Generator 函数，Generator是一种异步编程解决方案，Generator 函数是协程在 ES6 的实现，最大特点就是可以交出函数的执行权，Generator 函数可以看出是异步任务的容器，需要暂停的地方，都用yield语句注明。但是 Generator 使用起来较为复杂。  
ES7又提出了新的异步解决方案:async/await，async是 Generator 函数的语法糖，async/await 使得异步代码看起来像同步代码，异步编程发展的目标就是让异步逻辑的代码看起来像同步一样。  

>1.回调函数: callback
```js
//node读取文件
fs.readFile(xxx, 'utf-8', function(err, data) {
    //code
});
```
复制代码回调函数的使用场景(包括但不限于):

1. 事件回调
2. Node API
3. setTimeout/setInterval中的回调函数

异步回调嵌套会导致代码难以维护，并且不方便统一处理错误，不能try catch 和 回调地狱(如先读取A文本内容，再根据A文本内容读取B再根据B的内容读取C...)。 
```js
fs.readFile(A, 'utf-8', function(err, data) {
    fs.readFile(B, 'utf-8', function(err, data) {
        fs.readFile(C, 'utf-8', function(err, data) {
            fs.readFile(D, 'utf-8', function(err, data) {
                //....
            });
        });
    });
});
```
>2.Promise

Promise 主要解决了回调地狱的问题，Promise 最早由社区提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象。  
那么我们看看Promise是如何解决回调地狱问题的，仍然以上文的readFile为例。  
```js
function read(url) {
    return new Promise((resolve, reject) => {
        fs.readFile(url, 'utf8', (err, data) => {
            if(err) reject(err);
            resolve(data);
        });
    });
}
read(A).then(data => {
    return read(B);
}).then(data => {
    return read(C);
}).then(data => {
    return read(D);
}).catch(reason => {
    console.log(reason);
});
```

>3.Generator

Generator 函数是 ES6 提供的一种异步编程解决方案，整个 Generator 函数就是一个封装的异步任务，或者说是异步任务的容器。异步操作需要暂停的地方，都用 yield 语句注明。   
Generator 函数一般配合 yield 或 Promise 使用。Generator函数返回的是迭代器。对生成器和迭代器不了解的同学，请自行补习下基础。下面我们看一下 Generator 的简单使用:
```js
function* gen() {
    let a = yield 111;
    console.log(a);
    let b = yield 222;
    console.log(b);
    let c = yield 333;
    console.log(c);
    let d = yield 444;
    console.log(d);
}
let t = gen();
//next方法可以带一个参数，该参数就会被当作上一个yield表达式的返回值
t.next(1); //第一次调用next函数时，传递的参数无效
t.next(2); //a输出2;
t.next(3); //b输出3; 
t.next(4); //c输出4;
t.next(5); //d输出5;
```

仍然以上文的readFile为例，使用 Generator + co库来实现:
```js
const fs = require('fs');
const co = require('co');
const bluebird = require('bluebird');
const readFile = bluebird.promisify(fs.readFile);

function* read() {
    yield readFile(A, 'utf-8');
    yield readFile(B, 'utf-8');
    yield readFile(C, 'utf-8');
    //....
}
co(read()).then(data => {
    //code
}).catch(err => {
    //code
});
```

>4.async/await

ES7中引入了 async/await 概念。async其实是一个语法糖，它的实现就是将Generator函数和自动执行器（co），包装在一个函数中。   
async/await 的优点是代码清晰，不用像 Promise 写很多 then 链，就可以处理回调地狱的问题。错误可以被try catch。   
```js
const fs = require('fs');
const bluebird = require('bluebird');
const readFile = bluebird.promisify(fs.readFile);

async function read() {
    await readFile(A, 'utf-8');
    await readFile(B, 'utf-8');
    await readFile(C, 'utf-8');
    //code
}

read().then((data) => {
    //code
}).catch(err => {
    //code
});
```

## 64.谈谈对 async/await 的理解，async/await 的实现原理是什么? 
async/await 就是 Generator 的语法糖，使得异步操作变得更加方便。  

async 函数就是将 Generator 函数的星号（*）替换成 async，将 yield 替换成await。  

> 我们说 async 是 Generator 的语法糖，那么这个糖究竟甜在哪呢？  

1）async函数内置执行器，函数调用之后，会自动执行，输出最后结果。而Generator需要调用next或者配合co模块使用。   
2）更好的语义，async和await，比起星号和yield，语义更清楚了。async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果。   
3）更广的适用性。co模块约定，yield命令后面只能是 Thunk 函数或 Promise 对象，而async 函数的 await 命令后面，可以是 Promise 对象和原始类型的值。  
4）返回值是Promise，async函数的返回值是 Promise 对象，Generator的返回值是 Iterator，Promise 对象使用起来更加方便。   

>async 函数的实现原理，就是将 Generator 函数和自动执行器，包装在一个函数里。

具体代码试下如下(和spawn的实现略有差异，个人觉得这样写更容易理解)
```js
function my_co(it) {
    return new Promise((resolve, reject) => {
        function next(data) {
            try {
                var { value, done } = it.next(data);
            }catch(e){
                return reject(e);
            }
            if (!done) { 
                //done为true,表示迭代完成
                //value 不一定是 Promise，可能是一个普通值。使用 Promise.resolve 进行包装。
                Promise.resolve(value).then(val => {
                    next(val);
                }, reject);
            } else {
                resolve(value);
            }
        }
        next(); //执行一次next
    });
}
function* test() {
    yield new Promise((resolve, reject) => {
        setTimeout(resolve, 100);
    });
    yield new Promise((resolve, reject) => {
        // throw Error(1);
        resolve(10)
    });
    yield 10;
    return 1000;
}

my_co(test()).then(data => {
    console.log(data); //输出1000
}).catch((err) => {
    console.log('err: ', err);
});
```

## 65.使用 async/await 需要注意什么？

1. await 命令后面的Promise对象，运行结果可能是 rejected，此时等同于 async 函数返回的 Promise 对象被reject。因此需要加上错误处理，可以给每个 await 后的 Promise 增加 catch 方法；也可以将 await 的代码放在 try...catch 中。
2. 多个await命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。
```js
//下面两种写法都可以同时触发
//法一
async function f1() {
    await Promise.all([
        new Promise((resolve) => {
            setTimeout(resolve, 600);
        }),
        new Promise((resolve) => {
            setTimeout(resolve, 600);
        })
    ])
}
//法二
async function f2() {
    let fn1 = new Promise((resolve) => {
            setTimeout(resolve, 800);
        });
    
    let fn2 = new Promise((resolve) => {
            setTimeout(resolve, 800);
        })
    await fn1;
    await fn2;
}
```
3. await命令只能用在async函数之中，如果用在普通函数，会报错。
4. async 函数可以保留运行堆栈。
```js
/**
* 函数a内部运行了一个异步任务b()。当b()运行的时候，函数a()不会中断，而是继续执行。
* 等到b()运行结束，可能a()早就* 运行结束了，b()所在的上下文环境已经消失了。
* 如果b()或c()报错，错误堆栈将不包括a()。
*/
function b() {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, 200)
    });
}
function c() {
    throw Error(10);
}
const a = () => {
    b().then(() => c());
};
a();
/**
* 改成async函数
*/
const m = async () => {
    await b();
    c();
};
m();

报错信息，可以看出 async 函数可以保留运行堆栈。
```


## 66.如何实现 Promise.race？
在代码实现前，我们需要先了解 Promise.race 的特点：  


1. Promise.race返回的仍然是一个Promise.
它的状态与第一个完成的Promise的状态相同。它可以是完成（ resolves），也可以是失败（rejects），这要取决于第一个Promise是哪一种状态。


2. 如果传入的参数是不可迭代的，那么将会抛出错误。


3. 如果传的参数数组是空，那么返回的 promise 将永远等待。


4. 如果迭代包含一个或多个非承诺值和/或已解决/拒绝的承诺，则 Promise.race 将解析为迭代中找到的第一个值。

```js
Promise.race = function (promises) {
    //promises 必须是一个可遍历的数据结构，否则抛错
    return new Promise((resolve, reject) => {
        if (typeof promises[Symbol.iterator] !== 'function') {
            //真实不是这个错误
            Promise.reject('args is not iteratable!');
        }
        if (promises.length === 0) {
            return;
        } else {
            for (let i = 0; i < promises.length; i++) {
                Promise.resolve(promises[i]).then((data) => {
                    resolve(data);
                    return;
                }, (err) => {
                    reject(err);
                    return;
                });
            }
        }
    });
}
```
测试代码：
```js
//一直在等待态
Promise.race([]).then((data) => {
    console.log('success ', data);
}, (err) => {
    console.log('err ', err);
});
//抛错
Promise.race().then((data) => {
    console.log('success ', data);
}, (err) => {
    console.log('err ', err);
});
Promise.race([
    new Promise((resolve, reject) => { setTimeout(() => { resolve(100) }, 1000) }),
    new Promise((resolve, reject) => { setTimeout(() => { resolve(200) }, 200) }),
    new Promise((resolve, reject) => { setTimeout(() => { reject(100) }, 100) })
]).then((data) => {
    console.log(data);
}, (err) => {
    console.log(err);
});
```


## 67.可遍历数据结构的有什么特点？
一个对象如果要具备可被 for...of 循环调用的 Iterator 接口，就必须在其 Symbol.iterator 的属性上部署遍历器生成方法(或者原型链上的对象具有该方法)  
**PS**: 遍历器对象根本特征就是具有next方法。每次调用next方法，都会返回一个代表当前成员的信息对象，具有value和done两个属性。
```js
//如为对象添加Iterator 接口;
let obj = {
    name: "Yvette",
    age: 18,
    job: 'engineer',
    [Symbol.iterator]() {
        const self = this;
        const keys = Object.keys(self);
        let index = 0;
        return {
            next() {
                if (index < keys.length) {
                    return {
                        value: self[keys[index++]],
                        done: false
                    };
                } else {
                    return { value: undefined, done: true };
                }
            }
        };
    }
};

for(let item of obj) {
    console.log(item); //Yvette  18  engineer
}
```
使用 Generator 函数(遍历器对象生成函数)简写 Symbol.iterator 方法，可以简写如下:
```js
let obj = {
    name: "Yvette",
    age: 18,
    job: 'engineer',
    * [Symbol.iterator] () {
        const self = this;
        const keys = Object.keys(self);
        for (let index = 0;index < keys.length; index++) {
            yield self[keys[index]];//yield表达式仅能使用在 Generator 函数中
        } 
    }
};
```
>原生具备 Iterator 接口的数据结构如下。
* Array
* Map
* Set
* String* 
* TypedArray
* 函数的 arguments 对象
* NodeList 对象
* ES6 的数组、Set、Map 都部署了以下三个方法: entries() / keys() / values()，调用后都返回遍历器对象。



## 68.requestAnimationFrame 和 setTimeout/setInterval 有什么区别？使用 requestAnimationFrame 有哪些好处？
在 requestAnimationFrame 之前，我们主要使用 setTimeout/setInterval 来编写JS动画。  
编写动画的关键是循环间隔的设置，一方面，循环间隔足够短，动画效果才能显得平滑流畅；另一方面，循环间隔还要足够长，才能确保浏览器有能力渲染产生的变化。  
大部分的电脑显示器的刷新频率是60HZ，也就是每秒钟重绘60次。大多数浏览器都会对重绘操作加以限制，不超过显示器的重绘频率，因为即使超过那个频率用户体验也不会提升。因此，最平滑动画的最佳循环间隔是 1000ms / 60 ，约为16.7ms。  
setTimeout/setInterval 有一个显著的缺陷在于时间是不精确的，setTimeout/setInterval 只能保证延时或间隔不小于设定的时间。因为它们实际上只是把任务添加到了任务队列中，但是如果前面的任务还没有执行完成，它们必须要等待。  
requestAnimationFrame 才有的是系统时间间隔，保持最佳绘制效率，不会因为间隔时间过短，造成过度绘制，增加开销；也不会因为间隔时间太长，使用动画卡顿不流畅，让各种网页动画效果能够有一个统一的刷新机制，从而节省系统资源，提高系统性能，改善视觉效果。  
综上所述，requestAnimationFrame 和 setTimeout/setInterval 在编写动画时相比，优点如下:  
1. requestAnimationFrame 不需要设置时间，采用系统时间间隔，能达到最佳的动画效果。
2. requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成。
3. 当 requestAnimationFrame() 运行在后台标签页或者隐藏的 `<iframe>` 里时，requestAnimationFrame() 会被暂停调用以提升性能和电池寿命（大多数浏览器中）。
requestAnimationFrame 使用(试试使用requestAnimationFrame写一个移动的小球，从A移动到B初):      
```js
function step(timestamp) {
    //code...
    window.requestAnimationFrame(step);
}
window.requestAnimationFrame(step);

```


## 69.JS 类型转换的规则是什么？
类型转换的规则三言两语说不清，真想哇得一声哭出来~  

JS中类型转换分为 强制类型转换 和 隐式类型转换 。  


* 通过 Number()、parseInt()、parseFloat()、toString()、String()、Boolean(),进行强制类型转换。


* 逻辑运算符(&&、 ||、 !)、运算符(+、-、*、/)、关系操作符(>、 <、 <= 、>=)、相等运算符(==)或者 if/while 的条件，可能会进行隐式类型转换。


**强制类型转换**   

>1.Number() 将任意类型的参数转换为数值类型

规则如下:  

* 如果是布尔值，true和false分别被转换为1和0
* 如果是数字，返回自身
* 如果是 null，返回 0
* 如果是 undefined，返回 NAN
* 如果是字符串，遵循以下规则:

1. 如果字符串中只包含数字(或者是 0X / 0x 开头的十六进制数字字符串，允许包含正负号)，则将其转换为十进制
2. 如果字符串中包含有效的浮点格式，将其转换为浮点数值
3. 如果是空字符串，将其转换为0
4. 如不是以上格式的字符串，均返回 NaN


* 如果是Symbol，抛出错误
* 如果是对象，则调用对象的 valueOf() 方法，然后依据前面的规则转换返回的值。如果转换的结果是 NaN ，则调用对象的 toString() 方法，再次依照前面的规则转换返回的字符串值。

部分内置对象调用默认的 valueOf 的行为:     
| 对象       | 返回值                                                          |
| :---       | :---                                                           | 
| Array      | 数组本身（对象类型）                                             |
| Boolean    | 布尔值（原始类型）                                               | 
| Date       | 从 UTC 1970 年 1 月 1 日午夜开始计算，到所封装的日期所经过的毫秒数  | 
| Function   | 函数本身（对象类型）                                             | 
| Number     | 数字值（原始类型）                                               | 
| Object     | 对象本身（对象类型）                                             | 
| String     | 字符串值（原始类型）                                             | 
```js
Number('0111'); //111
Number('0X11') //17
Number(null); //0
Number(''); //0
Number('1a'); //NaN
Number(-0X11);//-17
```
>2.parseInt(param, radix)

如果第一个参数传入的是字符串类型: 

1. 忽略字符串前面的空格，直至找到第一个非空字符，如果是空字符串，返回NaN
2. 如果第一个字符不是数字符号或者正负号，返回NaN
3. 如果第一个字符是数字/正负号，则继续解析直至字符串解析完毕或者遇到一个非数字符号为止

如果第一个参数传入的Number类型:

1. 数字如果是0开头，则将其当作八进制来解析(如果是一个八进制数)；如果以0x开头，则将其当作十六进制来解析

如果第一个参数是 null 或者是 undefined，或者是一个对象类型：

1. 返回 NaN

如果第一个参数是数组：1. 去数组的第一个元素，按照上面的规则进行解析  
如果第一个参数是Symbol类型：1. 抛出错误   
如果指定radix参数，以radix为基数进行解析   
```js
parseInt('0111'); //111
parseInt(0111); //八进制数 73
parseInt('');//NaN
parseInt('0X11'); //17
parseInt('1a') //1
parseInt('a1'); //NaN
parseInt(['10aa','aaa']);//10

parseInt([]);//NaN; parseInt(undefined);
```
>parseFloat

规则和parseInt基本相同，接受一个Number类型或字符串，如果是字符串中，那么只有第一个小数点是有效的。

>toString()

规则如下:

* 如果是Number类型，输出数字字符串
* 如果是 null 或者是 undefined，抛错
* 如果是数组，那么将数组展开输出。空数组，返回''
* 如果是对象，返回 [object Object]
* 如果是Date, 返回日期的文字表示法
* 如果是函数，输出对应的字符串(如下demo)
* 如果是Symbol，输出Symbol字符串
```js
let arry = [];
let obj = {a:1};
let sym = Symbol(100);
let date = new Date();
let fn = function() {console.log('稳住，我们能赢！')}
let str = 'hello world';
console.log([].toString()); // ''
console.log([1, 2, 3, undefined, 5, 6].toString());//1,2,3,,5,6
console.log(arry.toString()); // 1,2,3
console.log(obj.toString()); // [object Object]
console.log(date.toString()); // Sun Apr 21 2019 16:11:39 GMT+0800 (CST)
console.log(fn.toString());// function () {console.log('稳住，我们能赢！')}
console.log(str.toString());// 'hello world'
console.log(sym.toString());// Symbol(100)
console.log(undefined.toString());// 抛错
console.log(null.toString());// 抛错
```
>String()

String() 的转换规则与 toString() 基本一致，最大的一点不同在于 null 和 undefined，使用 String 进行转换，null 和 undefined对应的是字符串 'null' 和 'undefined'

>Boolean

除了 undefined、 null、 false、 ''、 0(包括 +0，-0)、 NaN 转换出来是false，其它都是true.
**隐式类型转换**  

>&& 、|| 、 ! 、 if/while 的条件判断

需要将数据转换成 Boolean 类型，转换规则同 Boolean 强制类型转换

>运算符: + - * /

`+ `号操作符，不仅可以用作数字相加，还可以用作字符串拼接。  
仅当 `+` 号两边都是数字时，进行的是加法运算。如果两边都是字符串，直接拼接，无需进行隐式类型转换。   
除了上面的情况外，如果操作数是对象、数值或者布尔值，则调用toString()方法取得字符串值(toString转换规则)。对于 undefined 和 null，分别调用String()显式转换为字符串，然后再进行拼接。  
```js
console.log({}+10); //[object Object]10
console.log([1, 2, 3, undefined, 5, 6] + 10);//1,2,3,,5,610
```
`-、*、/` 操作符针对的是运算，如果操作值之一不是数值，则被隐式调用Number()函数进行转换。如果其中有一个转换除了为NaN，结果为NaN.

>关系操作符: ==、>、< 、<=、>=

`> , < ，<= ，>=`

1. 如果两个操作值都是数值，则进行数值比较
2. 如果两个操作值都是字符串，则比较字符串对应的字符编码值
3. 如果有一方是Symbol类型，抛出错误
4. 除了上述情况之外，都进行Number()进行类型转换，然后再进行比较。

**注**： NaN是非常特殊的值，它不和任何类型的值相等，包括它自己，同时它与任何类型的值比较大小时都返回false。
```js
console.log(10 > {});//返回false.
/**
 *{}.valueOf ---> {}
 *{}.toString() ---> '[object Object]' ---> NaN
 *NaN 和 任何类型比大小，都返回 false
 */
```
>相等操作符：==


1. 如果类型相同，无需进行类型转换。
2. 如果其中一个操作值是 null 或者是 undefined，那么另一个操作符必须为 null 或者 undefined 时，才返回 true，否则都返回 false.
3. 如果其中一个是 Symbol 类型，那么返回 false.
4. 两个操作值是否为 string 和 number，就会将字符串转换为 number
5. 如果一个操作值是 boolean，那么转换成 number
6. 如果一个操作值为 object 且另一方为 string、number 或者 symbol，是的话就会把 object 转为原始类型再进行判断(调用object的valueOf/toString方法进行转换)


>对象如何转换成原始数据类型

如果部署了 [Symbol.toPrimitive] 接口，那么调用此接口，若返回的不是基础数据类型，抛出错误。     
如果没有部署 [Symbol.toPrimitive] 接口，那么先返回 valueOf() 的值，若返回的不是基础类型的值，再返回 toString() 的值，若返回的不是基础类型的值， 则抛出异常。  
```js
//先调用 valueOf, 后调用 toString
let obj = {
    [Symbol.toPrimitive]() {
        return 200;
    },
    valueOf() {
        return 300;
    },
    toString() {
        return 'Hello';
    }
}
//如果 valueOf 返回的不是基本数据类型，则会调用 toString， 
//如果 toString 返回的也不是基本数据类型，会抛出错误
console.log(obj + 200); //400
```


## 70.简述下对 webWorker 的理解？
HTML5则提出了 Web Worker 标准，表示js允许多线程，但是子线程完全受主线程控制并且不能操作dom，只有主线程可以操作dom，所以js本质上依然是单线程语言。   
web worker就是在js单线程执行的基础上开启一个子线程，进行程序处理，而不影响主线程的执行，当子线程执行完之后再回到主线程上，在这个过程中不影响主线程的执行。子线程与主线程之间提供了数据交互的接口postMessage和onmessage，来进行数据发送和接收。  
```js
var worker = new Worker('./worker.js'); //创建一个子线程
worker.postMessage('Hello');
worker.onmessage = function (e) {
    console.log(e.data); //Hi
    worker.terminate(); //结束线程
};
```
```js
//worker.js
onmessage = function (e) {
    console.log(e.data); //Hello
    postMessage("Hi"); //向主进程发送消息
};
```

## 71.ES6模块和CommonJS模块的差异？


1. ES6模块在编译时，就能确定模块的依赖关系，以及输入和输出的变量。
CommonJS 模块，运行时加载。


2. ES6 模块自动采用严格模式，无论模块头部是否写了 "use strict";


3. require 可以做动态加载，import 语句做不到，import 语句必须位于顶层作用域中。


4. ES6 模块中顶层的 this 指向 undefined，CommonJS 模块的顶层 this 指向当前模块。


5. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。


CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。如：
```js
//name.js
var name = 'William';
setTimeout(() => name = 'Yvette', 200);
module.exports = {
    name
};
//index.js
const name = require('./name');
console.log(name); //William
setTimeout(() => console.log(name), 300); //William
```
对比 ES6 模块看一下:  
ES6 模块的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令 import ，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。
```js
//name.js
var name = 'William';
setTimeout(() => name = 'Yvette', 200);
export { name };
//index.js
import { name } from './name';
console.log(name); //William
setTimeout(() => console.log(name), 300); //Yvette
```

## 71.浏览器事件代理机制的原理是什么？
在说浏览器事件代理机制原理之前，我们首先了解一下事件流的概念，早期浏览器，IE采用的是事件冒泡事件流，而Netscape采用的则是事件捕获。"DOM2级事件"把事件流分为三个阶段，捕获阶段、目标阶段、冒泡阶段。现代浏览器也都遵循此规范。  


>那么事件代理是什么呢？

事件代理又称为事件委托，在祖先级DOM元素绑定一个事件，当触发子孙级DOM元素的事件时，利用事件冒泡的原理来触发绑定在祖先级DOM的事件。因为事件会从目标元素一层层冒泡至document对象。

>为什么要事件代理？



1. 添加到页面上的事件数量会影响页面的运行性能，如果添加的事件过多，会导致网页的性能下降。采用事件代理的方式，可以大大减少注册事件的个数。


2. 事件代理的当时，某个子孙元素是动态增加的，不需要再次对其进行事件绑定。


3. 不用担心某个注册了事件的DOM元素被移除后，可能无法回收其事件处理程序，我们只要把事件处理程序委托给更高层级的元素，就可以避免此问题。



>如将页面中的所有click事件都代理到document上:
```js
addEventListener 接受3个参数，分别是要处理的事件名、处理事件程序的函数和一个布尔值。布尔值默认为false。表示冒泡阶段调用事件处理程序，若设置为true，表示在捕获阶段调用事件处理程序。
document.addEventListener('click', function (e) {
    console.log(e.target);
    /**
    * 捕获阶段调用调用事件处理程序，eventPhase是 1; 
    * 处于目标，eventPhase是2 
    * 冒泡阶段调用事件处理程序，eventPhase是 1；
    */ 
    console.log(e.eventPhase);
    
});
```


## 72.js如何自定义事件？

>自定义 DOM 事件(不考虑IE9之前版本)

自定义事件有三种方法,一种是使用 new Event(), 另一种是 createEvent('CustomEvent') , 另一种是 new customEvent()

1. 使用 new Event()

获取不到 event.detail
```js
let btn = document.querySelector('#btn');
let ev = new Event('alert', {
    bubbles: true,    //事件是否冒泡;默认值false
    cancelable: true, //事件能否被取消;默认值false
    composed: false
});
btn.addEventListener('alert', function (event) {
    console.log(event.bubbles); //true
    console.log(event.cancelable); //true
    console.log(event.detail); //undefined
}, false);
btn.dispatchEvent(ev);
```
2. 使用 createEvent('CustomEvent') (DOM3)

要创建自定义事件，可以调用 createEvent('CustomEvent')，返回的对象有 initCustomEvent 方法，接受以下四个参数:

* type: 字符串，表示触发的事件类型，如此处的'alert'
* bubbles: 布尔值： 表示事件是否冒泡
* cancelable: 布尔值，表示事件是否可以取消
* detail: 任意值，保存在 event 对象的 detail 属性中
```js
let btn = document.querySelector('#btn');
let ev = btn.createEvent('CustomEvent');
ev.initCustomEvent('alert', true, true, 'button');
btn.addEventListener('alert', function (event) {
    console.log(event.bubbles); //true
    console.log(event.cancelable);//true
    console.log(event.detail); //button
}, false);
btn.dispatchEvent(ev);
```
3. 使用 new customEvent() (DOM4)

使用起来比 createEvent('CustomEvent')  更加方便 
```js
var btn = document.querySelector('#btn');
/*
 * 第一个参数是事件类型
 * 第二个参数是一个对象
 */
var ev = new CustomEvent('alert', {
    bubbles: 'true',
    cancelable: 'true',
    detail: 'button'
});
btn.addEventListener('alert', function (event) {
    console.log(event.bubbles); //true
    console.log(event.cancelable);//true
    console.log(event.detail); //button
}, false);
btn.dispatchEvent(ev);
```
>自定义非 DOM 事件(观察者模式)

EventTarget类型有一个单独的属性handlers，用于存储事件处理程序（观察者）。    
addHandler() 用于注册给定类型事件的事件处理程序；   
fire() 用于触发一个事件；    
removeHandler() 用于注销某个事件类型的事件处理程序。   
```js
function EventTarget(){
    this.handlers = {};
}

EventTarget.prototype = {
    constructor:EventTarget,
    addHandler:function(type,handler){
        if(typeof this.handlers[type] === "undefined"){
            this.handlers[type] = [];
        }
        this.handlers[type].push(handler);
    },
    fire:function(event){
        if(!event.target){
            event.target = this;
        }
        if(this.handlers[event.type] instanceof Array){
            const handlers = this.handlers[event.type];
            handlers.forEach((handler)=>{
                handler(event);
            });
        }
    },
    removeHandler:function(type,handler){
        if(this.handlers[type] instanceof Array){
            const handlers = this.handlers[type];
            for(var i = 0,len = handlers.length; i < len; i++){
                if(handlers[i] === handler){
                    break;
                }
            }
            handlers.splice(i,1);
        }
    }
}
//使用
function handleMessage(event){
    console.log(event.message);
}
//创建一个新对象
var target = new EventTarget();
//添加一个事件处理程序
target.addHandler("message", handleMessage);
//触发事件
target.fire({type:"message", message:"Hi"}); //Hi
//删除事件处理程序
target.removeHandler("message",handleMessage);
//再次触发事件，没有事件处理程序
target.fire({type:"message",message: "Hi"});
```

## 73.跨域的方法有哪些？原理是什么？
知其然知其所以然，在说跨域方法之前，我们先了解下什么叫跨域，浏览器有同源策略，只有当“协议”、“域名”、“端口号”都相同时，才能称之为是同源，其中有一个不同，即是跨域。  
那么同源策略的作用是什么呢？同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。  
那么我们又为什么需要跨域呢？一是前端和服务器分开部署，接口请求需要跨域，二是我们可能会加载其它网站的页面作为iframe内嵌。  

>跨域的方法有哪些？
 

>常用的跨域方法


1.jsonp    

尽管浏览器有同源策略，但是 `<script> `标签的 src 属性不会被同源策略所约束，可以获取任意服务器上的脚本并执行。jsonp 通过插入script标签的方式来实现跨域，参数只能通过url传入，仅能支持get请求。   
实现原理:   
* Step1: 创建 callback 方法  
* Step2: 插入 script 标签   
* Step3: 后台接受到请求，解析前端传过去的 callback 方法，返回该方法的调用，并且数据作为参数传入该方法
* Step4: 前端执行服务端返回的方法调用
下面代码仅为说明 jsonp 原理，项目中请使用成熟的库。分别看一下前端和服务端的简单实现：
```js
//前端代码
function jsonp({url, params, cb}) {
    return new Promise((resolve, reject) => {
        //创建script标签
        let script = document.createElement('script');
        //将回调函数挂在 window 上
        window[cb] = function(data) {
            resolve(data);
            //代码执行后，删除插入的script标签
            document.body.removeChild(script);
        }
        //回调函数加在请求地址上
        params = {...params, cb} //wb=b&cb=show
        let arrs = [];
        for(let key in params) {
            arrs.push(`${key}=${params[key]}`);
        }
        script.src = `${url}?${arrs.join('&')}`;
        document.body.appendChild(script);
    });
}
//使用
function sayHi(data) {
    console.log(data);
}
jsonp({
    url: 'http://localhost:3000/say',
    params: {
        //code
    },
    cb: 'sayHi'
}).then(data => {
    console.log(data);
});
```
```js
//express启动一个后台服务
let express = require('express');
let app = express();

app.get('/say', (req, res) => {
    let {cb} = req.query; //获取传来的callback函数名，cb是key
    res.send(`${cb}('Hello!')`);
});
app.listen(3000);
```


2.cors    

jsonp 只能支持 get 请求，cors 可以支持多种请求。cors 并不需要前端做什么工作。  

>简单跨域请求:

只要服务器设置的Access-Control-Allow-Origin Header和请求来源匹配，浏览器就允许跨域

1. 请求的方法是get，head或者post。
2. Content-Type是application/x-www-form-urlencoded, multipart/form-data 或 text/plain中的一个值，或者不设置也可以，一般默认就是application/x-www-form-urlencoded。
3. 请求中没有自定义的HTTP头部，如x-token。(应该是这几种头部 Accept，Accept-Language，Content-Language，Last-Event-ID，Content-Type）
```js
//简单跨域请求
app.use((req, res, next) => {
    res.setHeader('Access-Control-Allow-Origin', 'XXXX');
});
```
>带预检(Preflighted)的跨域请求

不满于简单跨域请求的，即是带预检的跨域请求。服务端需要设置 Access-Control-Allow-Origin (允许跨域资源请求的域) 、 Access-Control-Allow-Methods (允许的请求方法) 和 Access-Control-Allow-Headers (允许的请求头) 
```js
app.use((req, res, next) => {
    res.setHeader('Access-Control-Allow-Origin', 'XXX');
    res.setHeader('Access-Control-Allow-Headers', 'XXX'); //允许返回的头
    res.setHeader('Access-Control-Allow-Methods', 'XXX');//允许使用put方法请求接口
    res.setHeader('Access-Control-Max-Age', 6); //预检的存活时间
    if(req.method === "OPTIONS") {
        res.end(); //如果method是OPTIONS，不做处理
    }
});
```


3.nginx 反向代理

使用nginx反向代理实现跨域，只需要修改nginx的配置即可解决跨域问题。   
A网站向B网站请求某个接口时，向B网站发送一个请求，nginx根据配置文件接收这个请求，代替A网站向B网站来请求。  
nginx拿到这个资源后再返回给A网站，以此来解决了跨域问题。  
例如nginx的端口号为 8090，需要请求的服务器端口号为 3000。（localhost:8090 请求 localhost:3000/say）  
nginx配置如下:  
```js
server {
    listen       8090;

    server_name  localhost;

    location / {
        root   /Users/liuyan35/Test/Study/CORS/1-jsonp;
        index  index.html index.htm;
    }
    location /say {
        rewrite  ^/say/(.*)$ /$1 break;
        proxy_pass   http://localhost:3000;
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Credentials' 'true';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
    }
    # others
}
```
4.websocket   

Websocket 是 HTML5 的一个持久化的协议，它实现了浏览器与服务器的全双工通信，同时也是跨域的一种解决方案。   
Websocket 不受同源策略影响，只要服务器端支持，无需任何配置就支持跨域。   
前端页面在 8080 的端口。  
```js
let socket = new WebSocket('ws://localhost:3000'); //协议是ws
socket.onopen = function() {
    socket.send('Hi,你好');
}
socket.onmessage = function(e) {
    console.log(e.data)
}
```
服务端 3000端口。可以看出websocket无需做跨域配置。
```js
let WebSocket = require('ws');
let wss = new WebSocket.Server({port: 3000});
wss.on('connection', function(ws) {
    ws.on('message', function(data) {
        console.log(data); //接受到页面发来的消息'Hi,你好'
        ws.send('Hi'); //向页面发送消息
    });
});
```
5.postMessage

postMessage 通过用作前端页面之前的跨域，如父页面与iframe页面的跨域。window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源。   
话说工作中两个页面之前需要通信的情况并不多，我本人工作中，仅使用过两次，一次是H5页面中发送postMessage信息，ReactNative的webview中接收此此消息，并作出相应处理。另一次是可轮播的页面，某个轮播页使用的是iframe页面，为了解决滑动的事件冲突，iframe页面中去监听手势，发送消息告诉父页面是否左滑和右滑。  

>子页面向父页面发消息  

父页面
```js
window.addEventListener('message', (e) => {
    this.props.movePage(e.data);
}, false);
```
子页面(iframe):
```js
if(/*左滑*/) {
    window.parent && window.parent.postMessage(-1, '*')
}else if(/*右滑*/){
    window.parent && window.parent.postMessage(1, '*')
}
```
>父页面向子页面发消息

父页面:
```js
let iframe = document.querySelector('#iframe');
iframe.onload = function() {
    iframe.contentWindow.postMessage('hello', 'http://localhost:3002');
}
```
子页面:
```js
window.addEventListener('message', function(e) {
    console.log(e.data);
    e.source.postMessage('Hi', e.origin); //回消息
});
```
6.node 中间件

node 中间件的跨域原理和nginx代理跨域，同源策略是浏览器的限制，服务端没有同源策略。   
node中间件实现跨域的原理如下:   
1. 接受客户端请求
2. 将请求 转发给服务器。
3. 拿到服务器 响应 数据。
4. 将 响应 转发给客户端。

> 不常用跨域方法

以下三种跨域方式很少用，如有兴趣，可自行查阅相关资料。 


1. window.name + iframe


2. location.hash + iframe


3. document.domain (主域需相同)

## 74.下面这段代码的输出是什么？
```js
function Foo() {
    getName = function() {console.log(1)};
    return this;
}
Foo.getName = function() {console.log(2)};
Foo.prototype.getName = function() {console.log(3)};
var getName = function() {console.log(4)};
function getName() {console.log(5)};

Foo.getName();
getName();
Foo().getName();
getName();
new Foo.getName();
new Foo().getName();
new new Foo().getName();
```
**说明：**一道经典的面试题，仅是为了帮助大家回顾一下知识点，加深理解，真实工作中，是不可能这样写代码的，否则，肯定会被打死的。 
1. 首先预编译阶段，变量声明与函数声明提升至其对应作用域的最顶端。
因此上面的代码编译后如下(函数声明的优先级先于变量声明):  
```js
function Foo() {
    getName = function() {console.log(1)};
    return this;
}
function getName() {console.log(5)}; //函数优先(函数首先被提升)
var getName;//重复声明，被忽略
Foo.getName = function() {console.log(2)};
Foo.prototype.getName = function() {console.log(3)};
getName = function() {console.log(4)};
```
2.Foo.getName();直接调用Foo上getName方法，输出2  
3.getName();输出4，getName被重新赋值了   
4.Foo().getName();执行Foo()，window的getName被重新赋值，返回this;浏览器环境中，非严格模式，this 指向 window，this.getName();输出为1.  
如果是严格模式，this 指向 undefined，此处会抛出错误。  
如果是node环境中，this 指向 global，node的全局变量并不挂在global上，因为global.getName对应的是undefined，不是一个function，会抛出错误。  
5.getName();已经抛错的自然走不动这一步了；继续浏览器非严格模式；window.getName被重新赋过值，此时再调用，输出的是1   
6.new Foo.getName();考察运算符优先级的知识，new 无参数列表，对应的优先级是18；成员访问操作符 . , 对应的优先级是 19。因此相当于是 new (Foo.getName)();new操作符会执行构造函数中的方法，因此此处输出为 2.   
7.new Foo().getName()；new 带参数列表，对应的优先级是19，和成员访问操作符.优先级相同。同级运算符，按照从左到右的顺序依次计算。new Foo()先初始化 Foo 的实例化对象，实例上没有getName方法，因此需要原型上去找，即找到了 Foo.prototype.getName，输出3   
8.new new Foo().getName(); new 带参数列表，优先级19，因此相当于是 new (new Foo()).getName()；先初始化 Foo 的实例化对象，然后将其原型上的 getName 函数作为构造函数再次 new ，输出3   
因此最终结果如下:  
```js
Foo.getName(); //2
getName();//4
Foo().getName();//1
getName();//1
new Foo.getName();//2
new Foo().getName();//3
new new Foo().getName();//3
```
## 75.实现双向绑定 Proxy 与 Object.defineProperty 相比优劣如何?


1. Object.definedProperty 的作用是劫持一个对象的属性，劫持属性的getter和setter方法，在对象的属性发生变化时进行特定的操作。而 Proxy 劫持的是整个对象。


2. Proxy 会返回一个代理对象，我们只需要操作新对象即可，而 Object.defineProperty  只能遍历对象属性直接修改。


3. Object.definedProperty 不支持数组，更准确的说是不支持数组的各种API，因为如果仅仅考虑arry[i] = value 这种情况，是可以劫持的，但是这种劫持意义不大。而 Proxy 可以支持数组的各种API。


4. 尽管 Object.defineProperty 有诸多缺陷，但是其兼容性要好于 Proxy.


PS: Vue2.x 使用 Object.defineProperty 实现数据双向绑定，V3.0 则使用了 Proxy.
```js
//拦截器
let obj = {};
let temp = 'Yvette';
Object.defineProperty(obj, 'name', {
    get() {
        console.log("读取成功");
        return temp
    },
    set(value) {
        console.log("设置成功");
        temp = value;
    }
});

obj.name = 'Chris';
console.log(obj.name);
```
PS: Object.defineProperty 定义出来的属性，默认是不可枚举，不可更改，不可配置【无法delete】   
我们可以看到 Proxy 会劫持整个对象，读取对象中的属性或者是修改属性值，那么就会被劫持。但是有点需要注意，复杂数据类型，监控的是引用地址，而不是值，如果引用地址没有改变，那么不会触发set。
```js
let obj = {name: 'Yvette', hobbits: ['travel', 'reading'], info: {
    age: 20,
    job: 'engineer'
}};
let p = new Proxy(obj, {
    get(target, key) { //第三个参数是 proxy， 一般不使用
        console.log('读取成功');
        return Reflect.get(target, key);
    },
    set(target, key, value) {
        if(key === 'length') return true; //如果是数组长度的变化，返回。
        console.log('设置成功');
        return Reflect.set([target, key, value]);
    }
});
p.name = 20; //设置成功
p.age = 20; //设置成功; 不需要事先定义此属性
p.hobbits.push('photography'); //读取成功;注意不会触发设置成功
p.info.age = 18; //读取成功;不会触发设置成功
```
最后，我们再看下对于数组的劫持，Object.definedProperty 和 Proxy 的差别   
Object.definedProperty 可以将数组的索引作为属性进行劫持，但是仅支持直接对 arry[i] 进行操作，不支持数组的API，非常鸡肋。  
```js
let arry = []
Object.defineProperty(arry, '0', {
    get() {
        console.log("读取成功");
        return temp
    },
    set(value) {
        console.log("设置成功");
        temp = value;
    }
});

arry[0] = 10; //触发设置成功
arry.push(10); //不能被劫持
```
Proxy 可以监听到数组的变化，支持各种API。注意数组的变化触发get和set可能不止一次，如有需要，自行根据key值决定是否要进行处理。  
```js
let hobbits = ['travel', 'reading'];
let p = new Proxy(hobbits, {
    get(target, key) {
        // if(key === 'length') return true; //如果是数组长度的变化，返回。
        console.log('读取成功');
        return Reflect.get(target, key);
    },
    set(target, key, value) {
        // if(key === 'length') return true; //如果是数组长度的变化，返回。
        console.log('设置成功');
        return Reflect.set([target, key, value]);
    }
});
p.splice(0,1) //触发get和set，可以被劫持
p.push('photography');//触发get和set
p.slice(1); //触发get；因为 slice 是不会修改原数组的
```


-------------------------------
暂时就到这里了哦， 后续再更！
-------------------------------