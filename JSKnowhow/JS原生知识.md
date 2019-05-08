## 数据类型

    1.基本类型值包括：undefined null Boolean Number String 这些类型分别在内容中
    "占有固定的大小空间",它的值保存在"栈空间" 可通过"值来访问"

    2.引用类型: 对象 数组 函数
    
    3.对于引用数据类型的值，则必须要 "堆内存" 中为这个值分配空间,由于引用类型值的"大小不固定"
    对象有很多属性和方法而且还可以动态添加属性和方法因此不能把他们保持到栈内存中，但是"内存地
    址大小是固定"，因此可以"将内存地址保存在栈内容中"

    4.总结：栈内存中存放的是基本数据类型值，堆内存中放的是引用类型值，引用类型值在内容中的地址
    存放在栈中，也就是常说的对象对象引用

## 变量复制

    var a = 5;

    var b = a;

    console.log(a+"---"+b);//5---5

    b = 6;//这里重新给b赋值，a值并没有改变

    console.log(a+"---"+b);//5---6

    var obj = {name:"lisi"};

    var obj2 = obj;//这里是引用赋值，obj和obj2指向同一个对象

    console.log(obj.name + "---" + obj2.name);//lisi---lisi 

    obj2.name = "wangwu";

    console.log(obj.name + "---" + obj2.name);//wangwu---wangwu
 
## 函数

### this的工作原理（五种情况）
    
    1.全局作用域
      当在全部作用域内使用this 它将会指向全局对象，即window对
    2.函数调用
      挡在全局作用域调用函数时，this也会指向全局对象
    3.方法调用
      this指向调用该方法的对象
    4.调用构造函数
      在构造函数内部，this指向新创建的对象
    5.显示是设置this指向
  
##  匿名函数

    在javascript里面任何匿名函数都是属于window对象在匿名函数中，因为匿名函数是一个对象，
    所以在匿名函数内的中的当前对象应该是其父对象，没有自定义的父对象只能是其根对象Window
     
    在定义匿名函数的时候它会返回自己的内存地址，如果在此时有个变量接收的了这个匿名函数(内存地址)
    那么匿名函数就能在程序里面使用了(也可以在这个变量后面加一个()来调用这匿名函数)因为匿名函数也是在全局执行环境构造时候定义和赋值所以匿名函数的this指向也是window对象  

## 当在浏览器输入比如 http://www.baidu.com 按回车键后会发生什么

    1.浏览器向DNS服务器请求解析该URL中的域名所对应的IP地址

    2.解析出IP地址后，根据IP地址和默认端口80和服务器建立TCP连接

    3.浏览器发出读取文件,(URL中域名后面部分对应的文件),的HTTP请求,该请求报文作为TCP三次握手的第三个
    
    4.服务器给出响应，把对应的html文本发送给浏览器

    5.释放TCP连接

    6.浏览器将该文本显示出来


##  三次握手的过程
    URG 紧急指针是否有效。为1，表示某一位需要被优先处理
    ACK 确认号是否有效，一般置为1。
    PSH 提示接收端应用程序立即从
    TCP 缓冲区把数据读走。
    RST 对方要求重新建立连接，复位。
    SYN 请求建立连接，并在其序列号的字段进行序列号的初始值设定。建立连接，设置为1
    FIN? 希望断开连接
    LISTEN 收到
    SYN-SENT 同步已发送
    SYN-RCVD 同步收到
    ESTAB-LISHED 已经建立连接

> 1.第一次握手 建立连接时，客户端发送syn宝 并进入SYN-SENT状态，等待服务器确认:
  
> 2.第二次握手 服务器收到Syn包 必须确认客户的SYN 同时自己也发送一个ACK包 即SYN+ACK包，此时服务器进入SYN_RECV 状态;
  
> 3.第三次握手 客户端收到服务器的SYN+ACK包向服务器送确认包ACK 此包发送完毕，客户端和服务器进入ESTAB-LISHED(TCP连接成功)状态完成第三次握手

##  四次挥手的过程
  
    1.客户端进程发出连接释放报文，并且停止发送数据。此时FIN-WAIT-1终止等待状态

    2.服务器收到连接释放报文，发出确认报文此时服务器进入了CLOSE-WAIT(关闭等待)状态

    3.客户端收到服务器的确认请求后，此时客户端进入FIN-WAIT-2(终止等待)状态

    4.服务器将最后数据发送完毕后，就向客户端发送连接释放报文，由于在半关闭状态，
    服务器很可能又发送了一些数据，此时服务器就进入了LAST-ACK（最后确认）状态，
    等待客户端的确认。

    5.客户端收到服务器的连接释放报文后，必须发出确认，此时客户端就进入了TIME-WAIT(时间等待)状态。

    6.服务器只要收到客户端发出的确认，立即进入CLOSED状态。同样TCB撤销后 就结束了TCP的连接。

>  服务器结束TCP连接的时间要比客户端早一些。
    
## MPA (Multi-page Application) 多页面应用多个完整页面构成

## SPA (Single-page Application) 顾名思义在 Web 设计上使用单一页面一个外壳页面和多个页面片段构成
    
## SPA

    SPA与MPA之间的区别
   
    刷新方式 多页面是整页刷新 页面片段局部刷新

    跳转方式 多页面之间的跳转是从一个页面跳转到另一个页面 单页面之间的跳转是把一个页面片段删除或者隐藏加载另一个页面片段并显示出来，这是片段之间的模拟
    跳转没有离开壳页面
         

## WBE APP
    WebApp是指基于Web的系统和应用，其作用是向广大的最终用户发布一组复杂的内容和能

## natve APP 原生APP
    Native App是一种基于智能手机本地操作系统如iOS、Android、WP并使用原生程式编写运行的第三方应用程序，也叫本地app。一般使用的开发语言为JAVA、C++、Objective-C

## M站
    移动端的APP和PC端的APP结合    
  
## hybird APP
    WBE  + natve  = hybird 两个结合（混合模式移动应用）是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势
  
## hybird的好处

    微信分享 人脸识别 调第三方APP  
    如果有进度条就是 WBE APP越接近原生性能越好webview 在小程序里打开WEB页面
  
    
## 怎么实现路由
    hash路由
        1.push
        2.replace
    history模式
        1.push
        2.replace
 

## 路由

                               |-->push: = 
                   |-->hash模式|
                   |           |-->replace:replace
    1.改变地址栏-->|
                   |              |-->push:pushState()                   
                   |-->history模式|
                                  |-->replace:replaceState()    
      


                 |-->hash模式:hashChange
                 |
    2.更新内容-->|
                 |               |->popState
                 |-->history模式:|
                                 |->updateView 提供一个方法
 
  
## hash模式
  
    hash模式背后的原理是onhashchange事件，可以在window对象上监听这个事件
    
    window.onhashchange = function(event){
        console.log(event.oldURL, event.newURL);
        let hash = location.hash.slice(1); 
        document.body.style.color = hash;
    }   

> hash发生变化的url都会被浏览器记录下来，从而你会发现浏览器的前进后退都可以用了，同时点击后退时，页面也会发生变化

> 尽管没有请求服务器，但是状态和url关联起来人们就叫他前端路由 ，成为了单页应用的标配

## history模式(放在服务器环境下测试)

    history的到来，前端的路由就开始进化了，onhashchange 只能改变，后面的url片段,而history则给了前端完全的自由

    history可以分为两大部分，切换和修好,参考MDN，切换历史状态包括back,forward,go三个方法 对应的是浏览器的 前进 后退 跳转

    history.go(-2);//后退两次
    history.go(2);//前进两次
    history.back(); //后退
    hsitory.forward(); //前进

    通过pushstate把页面的状态保存在state对象中，当页面的url再变回这个url时，可以通过event.state取到这个state对象，从而可以对页面状态进行还原

    通过history 丢掉了丑陋的#，但是它也有个问题：不怕前进，不怕后退，就怕刷新，f5，（如果后端没有准备的话）,因为刷新是实实在在地去请求服务器的,不玩虚的。 

    在hash模式下，前端路由修改的是#中的信息，而浏览器请求时是不带它玩的，所以没有问题.但是在history下，你可以自由的修改path，当刷新时，如果服务器中没有相应的响应或者资源，会分分钟刷出一个404