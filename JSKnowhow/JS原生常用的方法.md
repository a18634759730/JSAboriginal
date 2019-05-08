# JS原生常用的方法
> 1.输出语句：document.write("") console.log() alert();

> 2.JS中的注释为//

> 3.传统的HTML文档顺序是:document->html->(head,body) en,history,location,document)

> 5.得到表单中元素的名称和值:document.getElementById("表单中元素的ID号").name(或value)

> 6.一个小写转大写的JS: document.getElementById("output").value = document.getElementById("input").value.toUpperCase();

> 7.JS中的值类型:String,Number,Boolean,Null,Object,Function

> 8.JS中的字符型转换成数值型:parseInt(),parseFloat()

> 9.JS中的数字转换成字符型:(""+变量)

> 10.JS中的取字符串长度是:(length)

> 11.JS中的字符与字符相连接使用+号.

> 12.JS中的比较操作符有:==等于,!=不等于,>,>=,<.<=

> 13.JS中声明变量使用:var来进行声明

> 14.JS中的判断语句结构:if(condition){}else{}

> 15.JS中的循环结构:for([initial e-xPRession];[condition];[upadte e-xpression]) {inside loop}

> 16.循环中止的命令是:break

> 17.JS中的函数定义:function functionName([parameter],...){statement[s]}

> 18.当文件中出现多个form表单时.可以用document.forms[0],document.forms[1]来代替.

> 19.窗口:打开窗口window.open(), 关闭一个窗口:window.close(), 窗口本身:self

> 20.状态栏的设置:window.status="字符";

> 21.弹出提示信息:window.alert("字符");

> 22.弹出确认框:window.confirm();

> 23.弹出输入提示框:window.prompt();

> 24.指定当前显示链接的位置:window.location.href="URL"

> 25.取出窗体中的所有表单的数量:document.forms.length

> 26.关闭文档的输出流:document.close();

> 27.字符串追加连接符:+=

> 28.创建一个文档元素:document.createElement(),document.createTextNode()

> 29.得到元素的方法:document.getElementById()

> 30.设置表单中所有文本型的成员的值为空:


    var form = window.document.forms[0]
    for (var i = 0; i<form.elements.length;i++){
        if (form.elements[i].type == "text"){
            form.elements[i].value = "";
        }
    }

> 31.复选按钮在JS中判断是否选中:document.forms[0].checkThis.checked (checked属性代表为是否选中返回TRUE或FALSE)

> 32.单选按钮组(单选按钮的名称必须相同):取单选按钮组的长度document.forms[0].groupName.length

> 33.单选按钮组判断是否被选中也是用checked.

> 34.下拉列表框的值:document.forms[0].selectName.options[n].value (n有时用下拉列表框名称加上.selectedIndex来确定被选中的值)

> 35.字符串的定义:var myString = new String("This is lightsWord");

> 36.字符串转成大写:string.toUpperCase(); 字符串转成小写:string.toLowerCase();

> 37.返回字符串2在字符串1中出现的位置:String1.indexOf("String2")!=-1则说明没找到.

> 38.取字符串中指定位置的一个字符:StringA.charAt(9);

> 39.取出字符串中指定起点和终点的子字符串:stringA.substring(2,6);

> 40.数学函数:

    Math.PI(返回圆周率),
    Math.SQRT2(返回开方),
    Math.max(value1,value2)返回两个数中的最在值,
    Math.pow(value1,10)返回value1的十次方,
    Math.round(value1)四舍五入函数,
    Math.floor(Math.random()*(n+1))返回随机数

> 41.定义日期型变量:

    var today = new Date();

> 42.日期函数列表:

    dateObj.getTime()得到时间,
    dateObj.getYear()得到年份,
    dateObj.getFullYear()得到四位的年份,
    dateObj.getMonth()得到月份,
    dateObj.getDate()得到日,
    dateObj.getDay()得到日期几,
    dateObj.getHours()得到小时,
    dateObj.getMinutes()得到分,
    dateObj.getSeconds()得到秒,
    dateObj.setTime(value)设置时间,
    dateObj.setYear(val)设置年,
    dateObj.setMonth(val)设置月,
    dateObj.setDate(val)设置日,
    dateObj.setDay(val)设置星期几,
    dateObj.setHours设置小时,
    dateObj.setMinutes(val)设置分,
    dateObj.setSeconds(val)设置秒 [注意:此日期时间从0开始计]

> 43.FRAME的表示方式:

    [window.]frames[n].ObjFuncVarName,frames["frameName"].ObjFuncVarName,frameName.ObjFuncVarName

> 44.parent代表父亲对象,top代表最顶端对象

> 45.打开子窗口的父窗口为:opener

> 46.表示当前所属的位置:this

> 47.当在超链接中调用JS函数时用:(javascript:)来开头后面加函数名

> 48.在老的浏览器中不执行此JS:<!--      //-->

> 49.引用一个文件式的JS:


    <script type="text/Javascript" src="aaa.js"></script>

> 50.指定在不支持脚本的浏览器显示的HTML:

    <noscript></noscript>

> 51.当超链和ONCLICK事件都有时,则老版本的浏览器转向a.html,否则转向b.html.例:

    <a href="a.html" onclick="location.href='b.html';return false">dfsadf</a>

> 52.JS的内建对象有:

    Array,Boolean,Date,Error,EvalError,Function,Math,Number,Object,RangeError,
    ReferenceError,RegExp,String,SyntaxError,TypeError,URIError

> 53.JS中的换行:\n
> 54.窗口全屏大小:

    <script>
        function fullScreen(){ 
            this.moveTo(0,0);
            this.outerWidth=screen.availWidth;
            this.outerHeight=screen.availHeight;
        }
        window.maximize=fullScreen;
    </script>

> 55.JS中的all代表其下层的全部元素http://bizhi.knowsky.com/

> 56.JS中的焦点顺序:document.getElementByid("表单元素").tabIndex = 1

> 57.innerHTML的值是表单元素的值:如<p id="para">"how are <em>you</em>"</p>,则innerHTML的值就是:how are <em>you</em>

> 58.innerTEXT的值和上面的一样,只不过不会把<em>这种标记显示出来.

> 59.contentEditable可设置元素是否可被修改,isContentEditable返回是否可修改的状态.

> 60.isDisabled判断是否为禁止状态.disabled设置禁止状态

> 61.length取得长度,返回整型数值

> 62.addBehavior()是一种JS调用的外部函数文件其扩展名为.htc

> 63.window.focus()使当前的窗口在所有窗口之前.

> 64.blur()指失去焦点.与FOCUS()相反.

> 65.select()指元素为选中状态.

> 66.防止用户对文本框中输入文本:onfocus="this.blur()"

> 67.取出该元素在页面中出现的数量:document.all.tags("div(或其它HTML标记符)").length

> 68.JS中分为两种窗体输出:模态和非模态.window.showModaldialog(),window.showModeless()

> 69.状态栏文字的设置:window.status='文字',默认的状态栏文字设置:window.defaultStatus = '文字.';

> 70.添加到收藏夹:external.AddFavorite("http://www.xrss.cn","jaskdlf");

> 71.JS中遇到脚本错误时不做任何操作:window.onerror = doNothing; 指定错误句柄的语法为:window.onerror = handleError;

> 72.JS中指定当前打开窗口的父窗口:window.opener,支持opener.opener...的多重继续.

> 73.JS中的self指的是当前的窗口

> 74.JS中状态栏显示内容:window.status="内容"

> 75.JS中的top指的是框架集中最顶层的框架

> 76.JS中关闭当前的窗口:window.close();

> 77.JS中提出是否确认的框:

    if(confirm("Are you sure?")){
        alert("ok");
    }else{
        alert("Not Ok");
    }

> 78.JS中的窗口重定向:window.navigate("http://www.sina.com.cn");

> 79.JS中的打印:window.print()

> 80.JS中的提示输入框:window.prompt("message","defaultReply");

> 81.JS中的窗口滚动条:window.scroll(x,y)

> 82.JS中的窗口滚动到位置:window.scrollby

> 83.JS中设置时间间隔:

    setInterval("expr",msecDelay) 或 setInterval(funcRef,msecDelay) 或 setTimeout

> 84.JS中的模态显示在IE4+行,在NN中不行:showModalDialog("URL"[,arguments][,features]);

> 85.JS中的退出之前使用的句柄:

    function verifyClose(){
        event.returnValue="we really like you and hope you will stay longer.";
    }} 
    window.onbeforeunload=verifyClose;

> 86.当窗体第一次调用时使用的文件句柄:onload()

> 87.当窗体关闭时调用的文件句柄:onunload()

> 88.window.location的属性:

    protocol(http:),
    hostname(www.example.com),
    port(80),
    host(www.example.com:80),
    pathname("/a/a.html"),
    hash("#giantGizmo",指跳转到相应的锚记),href(全部的信息)

> 89.window.location.reload()刷新当前页面.

    1.parent.location.reload()刷新父亲对象（用于框架）
    2.opener.location.reload()刷新父窗口对象（用于单开窗口）
    3.top.location.reload()刷新最顶端对象（用于多开窗口）

> 90.

    window.history.back()返回上一页,
    window.history.forward()返回下一页,
    window.history.go(返回第几页,也可以使用访问过的URL)

> 91.

    document.write()不换行的输出,
    document.writeln()换行输出

> 92.document.body.noWrap=true;防止链接文字折行.

> 93.变量名.charAt(第几位),取该变量的第几位的字符.

> 94."abc".charCodeAt(第几个),返回第几个字符的ASCii码值.

> 95.字符串连接:string.concat(string2),或用+=进行连接

> 96.变量.indexOf("字符",起始位置),返回第一个出现的位置(从0开始计算)

> 97.string.lastIndexOf(searchString[,startIndex])最后一次出现的位置.

> 98.string.match(regExpression),判断字符是否匹配.

> 99.string.replace(regExpression,replaceString)替换现有字符串.

> 100.string.split(分隔符)返回一个数组存储值.

> 101.string.substr(start[,length])取从第几位到指定长度的字符串.

> 102.string.toLowerCase()使字符串全部变为小写.

> 103.string.toUpperCase()使全部字符变为大写.

> 104.parseInt(string[,radix(代表进制)])强制转换成整型.

> 105.parseFloat(string[,radix])强制转换成浮点型.

> 106.isNaN(变量):测试是否为数值型.

> 107.定义常量的关键字:const,定义变量的关键字:var
