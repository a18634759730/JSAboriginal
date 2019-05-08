# DOM树 
>递归 深度优先 广度优先

                    DOM
             ________|________
            |        |        |
        ____D____    E        F
       |    |    |
       A    B    C
> 深度优先 DOM -> D -> A -> B -> C -> E -> F
> 广度优先 DOM -> D -> E -> F -> A -> B -> C

## JavaScript JS  网景公司 95年 发布

> ECMAScript  ES

                      JS
 	     ______________|_____________
        |              |             |
        ES             DOM           BOM**


> JS分三部分

    * 核心 ECMAScript标准 
    * 文档对象模型 Dom Object Model
    * 浏览器对象模型 Browser Object Model

> 事件机制 同步 永远在 异步 之前


                   事件
      ______________|_____________
     |              |             |
    事件源       事件类型       事件执行函数
 

    target
       触发事件的元素
    currentTarget
       绑定事件的元素

    moment 格式化对象

## 面向对象

    var a = new A()

             ___ a = {}
            |
            |
    new ------- a.proto  = A.prototype
            |
            |___ A.call(a)

> new一个对象的过程

　　首先了解new做了什么，使用new关键字调用函数（new ClassA(…)）的具体步骤：

    　　1、创建一个新对象：

    　　var obj = {};

    　　2、设置新对象的constructor属性为构造函数的名称，设置新对象的__proto__属性指向构造函数的prototype对象；

    　　obj.__proto__ = ClassA.prototype;

    　　3、使用新对象调用函数，函数中的this被指向新实例对象：

    　　ClassA.call(obj);　　//{}.构造函数()

    　　4、将初始化完毕的新对象地址，保存到等号左边的变量中 


## 原型 原型链
 
    var a = new A() 
    prototype = A.prototype
    a.__proto__ = A.prototype
    A.constructor = A
  
## 函数对象 
  
    1.所有引用类型（函数，数组，对象）都有__proto__的属性（隐式原型）
    2.所有的函数拥有prototype属性(显示原型)（仅限函数）  

## 继承
 
    new B()
    
    B.prototype = a 

    B的portotype 指向 a.prototype
    
    A.call(this) 
    
## 跨域

     ____ XMLHttpRequest
    |
    |
    |____ axios/flgio
    |
    |
    |____ fetch 
    |
    |
    |____ CORS 跨域资源共享

> abort 取消 AJAX

> 同源策略  

    同协议 同域名 同端口

    跨域只是存在 前端  浏览器资源拦截

  
## JSONP 
 
         ____ 1.发起请求 callback = cb => cb 3.JSONP 
        |
    前端 <
        |____ 2.埋的个方法 wendow.cb = function(res){4执行函数}

  

## CORS 跨域资源共享 

    C cross

    O origin  

    R resouvce

    S sharing 

    服务器只需要在响应头部中设置 Access-Control-Allow-Origin 即可让客户端访问

    Access-Control-Allow-methous

## Restfu

              |--- Get  查
              | 
              |--- Post  增	
              |
    Restful---|--- Put  改
              |  
              |--- Delete 删
              |
              |--- Options 探测请求
 

## Request Headers   

                      |--- Accept 请求的文件
                      |   
                      |--- Content-type 
    Request Headers---|
                      |--- Origin
                      |  
                      |--- Referer 防盗链 浏览器的保护 在非本域名下访问资源
                      |
                      |--- User-Agent 
  




* webpack 只用于本地，不可以在线上使用

* Proxy 只用于本地，不可以在线上使用

* axios 前后端通用



## ES6 Object.defineProperty

> Object.defineProperty 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

### 语法
    Object.defineProperty(obj, prop, descriptor)

### 参数
    1.obj 要在其上定义属性的对象。
    2.prop 要定义或修改的属性的名称。
    3.descriptor 将被定义或修改的属性描述符。
    4.返回值 被传递给函数的对象。

> 在ES6中，由于 Symbol类型的特殊性，用Symbol类型的值来做对象的key与常规的定义或修改不同，而Object.defineProperty 是定义key为Symbol的属性的方法之一

### 属性描述符

                            |--- 1.writable 该属性为true的时候 value才能被赋值运算符改变 默认为 false
                            |
                            |--- 2.configurable 该属性为true的 该属性描述function才能被改变同时该属性也能从对应的对象上被删除  默认为  false
                            |
    Object.defineProperty---|--- 3.enumerable 当该属性为true时 该属性才能够出现在对象的枚举属性中 默认为 false
                            |  
                            |--- 4.value 该属性对应的值可以是任何有效的JavaScript值(数值,对象,函数)默认为 undefined
                            |
                            |--- 5.setter/getter 


 ### getter 
    一个给属性提供 getter 的方法 如果没有 getter 则为 undefined 
    当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是
    会传入this对象由于继承关系，这里的this并不一定是定义该属性的
    对象

### setter
    一个给属性提供 setter 的方法，如果没有 setter 则为 undefined
    当属性值修改时，触发执行该方法。该方法将接受唯一参数,即该属性
    新的参数值


















