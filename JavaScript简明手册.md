# JavaScript简明手册

## 概述
JavaScript是一门客户端脚本语言，用于在用户浏览器中执行一些 **数据判断**、**事件响应** 等任务。
具体参考:[百度百科](https://baike.baidu.com/item/JavaScript/321142)

    JavaScript发展史：
    1. 1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为 ： C--，后来更名为：ScriptEase
    2. 1995年，Netscape(网景)公司，开发了一门客户端脚本语言：LiveScript。后来，请来SUN公司的专家，修改LiveScript，命名为JavaScript
    3. 1996年，微软抄袭JavaScript开发出JScript语言
    4. 1997年，ECMA(欧洲计算机制造商协会)，制定出客户端脚本语言的标准：ECMAScript，就是统一了所有客户端脚本语言的编码方式。
    JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)
    
    //此段引用自 传智播客/黑马程序员 网络视频教程 中。

## 使用方法
1.内部JavaScript

    <!--    内部使用，可以放在任意位置(<header>、<body>标签等)，按位置先后进行执行-->
        //<script type="text/javascript">
        <script>
            document.write("JavaScript代码");
        </script>

2.引用外部 **js** 文件

    <!--    外部js文件，可多次引用，重复执行-->
        <script src="../js/out_ref.js"></script>

## 基本语法
### 1.注释
    //单行注释
    
    /*
    多行注释
    */

### 2.数据类型
    //基本数据类型
    number  数值类型，相当与java的 int+double
            其中 NaN 为无意义数值
    string  字符串类型，JavaScript不存在字符类型
    boolean true/false
    null    typeof操作符得出的结果为 Object
    undefined   字面意思为 未定义，实际为 未初始化，未赋值
    
    //引用数据类型
    Object  对象

### 3.关于变量
    JavaScript是一种弱类型语言，变量的类型完全由赋予的值所确定
    //变量的定义
    var a = 1;    //由var关键字定义，作用域为局部
    b = true;     //不使用关键定义，作用域为全局
    
    //变量的类型可以根据所赋的值的改变而改变
    var c = 1;  //number
    c = false;  //boolean
    c = "string";    //string
    
    ** 在最新的 ES6 中，新添加了两个用于变量声明的关键字 let 和 const **
    
    在以前的 JavaScript 中有两个作用域：全局作用域 与 函数作用域
    
    //var 存在的 问题
    例如：
    function f{
        for(var i=0;;){
        
        }
        document.write(i);  //在这里还可以访问。
    }
    即 var 定义的变量 具有 函数作用域。    
    而不使用 var 定义，直接使用的 就具有 全局作用域。
    
    引入 let 就解决了 JavaScript 没有 块作用域的问题。
    
    const 作用域 与 let 作用域相同，区别在于 使用 const 定义 的 变量，
    不能 被 二次赋值，也就是 一旦 被赋值后 就 不能 再去 修改/改变


​    
### 4. typeof 关键字——获取变量数据类型
    document.write(typeof 1+"<br/>");   //打印出   number
    document.write(typeof true+"<br/>");    //打印出   boolean
    document.write(typeof "string"+"<br/>");    //打印出   string
    document.write(typeof null+"<br/>");    //打印出   object
    document.write(typeof undefined+"<br/>");   //打印出   undefined
### 5.运算符
#### 逻辑运算符
    && || ! //短路与或 非
    //由于JavaScript是弱类型语言，并且语法特性松散
    //所以在JavaScript中 逻辑运算 不仅可以对 boolean 类型操作，对于非 boolean 类型也支持
    //（不会报错，也能正常运行，我们可以认为 是这样的）
        
    //对于操作数不是 boolean 类型，JavaScript则会将 操作数 先转为 boolean，然后再进行 与或非 运算
    
    //具体转换规则如下
        //对于 string 类型
            “” 空字符串为 false，其他为 true
        //对于 number 类型 
            0 为 false，非 0 为 true
        //对于 null 及 undefined 都为 false
        
    //对与 非 操作，完全可以参照上面的规则
        //s 是一个字符串变量
        if(s!=null && s.length>0){}   <==二者等价==>   if(s){}
        
    //但是对于 与或 的话，还有其他特性（符合逻辑，但又出乎预料，需要记住）
    //下面会输出什么结果大家知道吗？
        document.write("" && "与");      //打印 ""（空字符串）
        // ""   解释为 false，对应 短路与，此时该语句就停止了，那么结果就是当前的 "" (空字符串)
        document.write("" || "或");      //打印 "或"
        // ""   解释为 false，对于 短路或，此时该语句继续执行，那么结果就是后一个 "或"    
#### 一元运算符
    ++（自增） --（自减） +（正号）-（负号）
    //与逻辑运算符类似，JavaScript的一元运算符（其他语言应该叫做 一元算术运算符）
    //操作数不仅可以时number类型，还可以是其他类型
    
    //具体规则如下
        boolean 类型，true 先转 1，false 先转 0，再运算
        string  类型，可以转 number 就转，不行就 NaN,其中 "" 空字符串为 0
        null    转 0
        undefined   转 NaN
        NaN 还是 NaN
#### 三元运算符
    ? :
    //同逻辑运算符，不是 boolean 先转 boolean
#### 比较运算符
    // >, <, <=, >=, !=, ==, ===
    1.类型相同直接比较
        支持所有JavaScript数据类型比较
    2.类型不同先转换
        不同数据类型比较，优先会将 其他数据类型转为 number 类型，转换规则查看 一元运算符。
     ** NaN 与 undefined 比较特殊，他们 和 其他数据类型，没有可比性，操作符除了 != 会返回 true，其他都为 false。**
     ** 其中 NaN == NaN 也会返回 false **
### 6.特殊语法
    //在JavaScript语法中，
    // 如果   一行只有一条语句，则 末尾 语句结束符 ;(分号)可以省略
### 7.流程控制语句
    switch      // 可以 接收 任意 数据类型
    //以下与java一样
    if else 
    for     
    while   
    do while
## ECMA标准对象
### 1. Function（函数）对象
#### 创建方式
    //1.字符串形式
        //格式：let fun=new Function("形式参数1",...,"函数体");
    let fun=new Function("a","b","document.write(a+b);");
    fun(3,8);
    
    //2.常用方式
    //格式：function fun1(形式参数1,...){
    //      函数体;
    // }
    function fun1(a, b) {
        document.write(a + b);
    }
    fun1(3, 2);
    
    //3.其他方式
    //格式：let fun2=function(a,b){
    //      函数体;
    //    }
    let fun2 = function (a, b) {
        return a + b;
    };
    document.write(fun2(3,6));
#### 特点
    //1.JavaScript中不存在方法重载
    // ·函数只和名字有关
    // ·和参数无关
    // ·调用的永远是最后一个同名函数
    function f1(a) {
        alert(a);
    }
    f1(5);  //调用的是下面这个，弹出NaN
    function f1(a,b) {
        alert(a+b);
    }
    // ·实参个数形参，多余的忽略
    // ·少于，则 undefined
    // ·其中 undefined 与 除 string类型 外 进行运算 结果总是为 NaN
    //                与 string 进行操作 则值 表现为 字符串 "undefined"
#### 返回值
    function f1(){
    }
    alert(f1());     // 弹出 undefined
    
    function f2(){
        return "====";
    }
    alert(f2());     // 弹出 ====
#### 内置对象
    //1.arguments
    function f(){
        for (let i = 0; i < arguments.length; i++) {
            document.write(arguments[i]+"<br/>");
        }
    }
    alert(f(1,2,3,4,5,6,7,8));
### 2. Array对象
#### 创建
    //1.let arr1=new Array();
    //2.let arr2=new Array(数组长度);
    //3.let arr3=new Array(元素1,元素2,...);    
    //当只写一个 number 元素时，其表示的是 数组长度
    let arr1=new Array();
#### 特点
    //1.可同时存放任意数据类型 元素
    //2.长短可变，自动调节
    arr1.push(1,true,"123");
    //arr1[n]=1; //对下标为 n 的元素进行赋值后，其数组长度自动增加 至 n+1，其他未赋值为 undefined
#### 属性
    // length
    alert(arr1.length); //3
#### 方法
    // join(指定分隔符); 指定分隔符连接,默认为 逗号 ,
    alert(arr1.join("@"));  //1@true@123
### Date对象
    //基本使用
    function show(msg){
        document.write(msg+"<br/>");
    }
    let date=new Date();
    show(date);
    show(date.toLocaleString());
    show(Date.now());
### Math对象
    //基本用法
    show(Math.sqrt(23));    //取 平方根     4.795831523312719
    show(Math.random()*100);    //返回0~1之间的随机数，含0不含1     96.98194506148803
    show(Math.round(3.14));     //3
    show(Math.round(3.74)); //四舍五入      4
    show(Math.ceil(3.14));      //4
    show(Math.ceil(3.74));  //进一        4
    show(Math.floor(3.14));     //3
    show(Math.floor(3.74)); //去尾        3
### RegExp对象——正则表达式
    //基本用法
    let reg1=new RegExp("\\w{6,12}");
    show(reg1.test("abcdefgh"));
    let reg2=/\w{6,12}/;
    show(reg2.test("abcdefgh"));
### Global全局对象
    函数	描述
    decodeURI()	解码某个编码的 URI。
    decodeURIComponent()	解码一个编码的 URI 组件。
    encodeURI()	把字符串编码为 URI。
    encodeURIComponent()	把字符串编码为 URI 组件。
    escape()	对字符串进行编码。
    eval()	计算 JavaScript 字符串，并把它作为脚本代码来执行。
    getClass()	返回一个 JavaObject 的 JavaClass。
    isFinite()	检查某个值是否为有穷大的数。
    isNaN()	检查某个值是否是数字。
    Number()	把对象的值转换为数字。
    parseFloat()	解析一个字符串并返回一个浮点数。
    parseInt()	解析一个字符串并返回一个整数。
    String()	把对象的值转换为字符串。
    unescape()	对由 escape() 编码的字符串进行解码。
    属性	描述
    Infinity	代表正的无穷大的数值。
    java	代表 java.* 包层级的一个 JavaPackage。
    NaN	指示某个值是不是数字值。
    Packages	根 JavaPackage 对象。
    undefined	指示未定义的值。
    
    //方法 parseInt
    show(parseInt("123"));  //123
    show(parseInt("123abc"));   //123
    show(parseInt("abc123"));   //NaN
    //方法 isNaN
    //方法 eval
## DOM入门小示例——开关灯
    <body>
        <img id="light" src="../img/off.gif">
        <script>
            let light=document.getElementById("light");
            light.onclick=function () {
                if(light.src.endsWith("off.gif")){
                    light.src="../img/on.gif";
                }else {
                    light.src="../img/off.gif";
                }
            }
        </script>
    </body>
## BOM对象——浏览器对象模型
### 1. window
    //弹窗相关
        //1.alert(); 警告对话框
        //2.confirm();  确定对话框
        //3.prompt();   输入对话框
        
        let b = confirm("确定要退出吗");
        if(b){
            close();
        }
        let s = prompt("请输入身份证号：");
        alert(s);
    
    //打开关闭相关
        //open();
        //close();
        
        let open1;
        document.getElementById("btnopen").onclick = function () {
            open1 = open("https://baidu.com");
        };
        document.getElementById("btnclose").onclick = function () {
            open1.close();
        };
        
    //定时器相关
        //一次性定时器
        setTimeout("alert('时间到了')",2000);
        function t1(){
            document.write("Hello JS<br/>");
        }
        let timeout = setTimeout("t1()",2000);
        //取消一次性定时器
        clearTimeout(timeout);
        setTimeout(t1,1000);
        //循环计时器
        let interval = setInterval(t1,500);
        //取消循环定时器
        clearInterval(interval);
        
    //属性    可获得其他 BOM 对象
        //navigator     浏览器对象
        //screen        窗口对象
        //history       历史记录对象
        //location      地址栏对象
    //获取    DOM 对象
        //document      文档对象
### 2. navigator 浏览器对象
    //遍历属性
    show(navigator.appCodeName);    //Mozilla
    show(navigator.appName);    //Netscape
    show(navigator.appVersion); //5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.100 Safari/537.36
    show(navigator.clipboard);  //[object Clipboard]

### 3. screen    屏幕对象
    show(screen.availWidth);    //1536
    show(screen.availHeight);   //824

### 4. history   历史记录对象
    //与history对象关联的有三个重要方法
        //back()    返回
        //forward() 前进
        //go()      跳转指定页面
    //属性 length 页面个数
        show(history.length);
        document.getElementById("back").onclick=function () {
            history.back();
        };
        document.getElementById("forward").onclick=function () {
            history.forward();
        };
    
        document.getElementById("go").onclick=function () {
            history.go(2);
        };
### 5. location 地址栏对象
    document.getElementById("reload").onclick=function () {
        location.reload();
    };
    alert(location.href);
    document.getElementById("href").onclick=function () {
        location.href="https://baidu.com/";
    };
## DOM对象
    //简单示例
    //查看html/DOM_动态表格.html
### 事件绑定方式
    <!--
    事件绑定的两种方法:1.内部,2.外部
    -->
    <input type="button" value="内部事件绑定" onclick="f()">
    <input id="input1" type="button" value="外部事件绑定">
    
    <script>
        function f() {
            alert("点击事件");
        }
        document.getElementById("input1").onclick = f;
    </script>
### 常用事件
    1.点击事件
        onclick     单击/点击 事件
        ondbclick   双击事件
    2.焦点事件
        onblur      失去焦点时触发
        onfocus     获取焦点
    3.鼠标事件
        onmousedown     鼠标按下
        onmouseup       鼠标松开
        onmousemove     鼠标移动
        onmouseover     鼠标移开
        onmouseout      鼠标移入
    4.键盘事件
        onkeydown       某键按下
        onkeyup         某键松开
        onkeypress      某键按下并松开(即按了某键)
    5.加载事件
        onload          加载事件
    6.选择和改变事件
        onchange        内容改变
        onselect        被选中
    7.表单事件
        onsubmit        提交事件
        onreset         表单重置
### 表单事件
    <!--
    这里写 onclick/onsubmit 居然都可以,好奇怪
    -->
    <!--<form action="#" method="get" onclick="return f()">-->
    <form action="#" method="get" onsubmit="return f()">
        <input type="text" name="name">
        <input type="submit" value="表单提交事件1">
    </form>
    <form id="form2" action="#" method="get">
        <input type="text" name="name">
        <input type="submit" value="表单提交事件2">
    </form>
    <script>
        function f() {
            return false;
        }
        document.getElementById("form2").onsubmit = f;
    </script>
### 事件小示例
            学生信息表
    编号	姓名	性别	操作
    1	科尔森	男	删除
    2	梅	女	删除
    3	斯凯	女	删除


​    