# interview

### 1.javascript是一门什么样的语言，它有哪些特点？

### 2.javascript的数据类型都有什么？<br  />
基本类型(undefined,null,number,string,boolean)；<br  />
引用类型(object:array,data,regex,function)，<br  />
引用类型里又有个引申问题就是说如何判断是否为数组数据类型，出处给出了三种方法：<br  />
方法一.判断其是否具有“数组性质”，如slice()方法。可自己给该变量定义slice方法，故有时会失效<br  />
方法二.obj instanceof Array 在某些IE版本中不正确<br  />
方法三.方法一二皆有漏洞，在ECMA Script5中定义了新方法Array.isArray(), 保证其兼容性<br  />

### 3.已知ID的input输入框，希望获取这个输入框的输入值，怎么做？(不使用第三方框架)<br  />
document.getElementById(“ID”).value

### 4.希望获取到页面中所有的checkbox怎么做?<br  />
```js
var checkList = document.getElementsByTagName('input');
var array = [];
var len = checkList.length;
while(len--){
    if(checkList[len].type == 'checkbox'){
        array.push(checkList[len]);
    }
}
console.log(array);
```

让我们再挖掘些别的涉及到的知识点<br  />
--i 和 i-- 有什么区别？i——是先使用i的值作为i——的值，然后，执行i=i-1操作<br  />
```js
var i=4,j,k;
j=i--;
k=--i;
console.log(i,j,k);//2,4,2
```

### 5.设置一个已知id的div的html内容为xxxx，字体颜色设置为黑色(不使用第三方框架)<br  />
```js
var div = document.getElementById('div1');
div.innerHTML = "xxxx";
div.style.color = "#000";
考察对dom节点的操作
```

### 6.当一个DOM节点被点击时候，我们希望能够执行一个函数，应该怎么做？<br  />
* 直接在DOM里绑定事件：<div onclick="test()"></div>
* 在JS里通过onclick绑定：xxx.onclick = test
* 通过事件添加进行绑定：addEventListener(xxx, ‘click’, test)
那么又有问题了，Javascript的事件流(事件发生顺序)模型都有什么？又都是由谁提出的呢?

“事件冒泡”：事件开始由最具体的元素接受，然后逐级向上传播;由微软提出
“事件捕捉”：事件由最不具体的节点先接收，然后逐级向下，一直到最具体的;由网景提出
“DOM事件流”有三个阶段：事件捕捉，目标阶段，事件冒泡

### 7.什么是Ajax和JSON，它们的优缺点。<br  />
Ajax是异步javascript和xml,用于在web页中实现异步数据交互<br  />
优点:
局部加载,降低数据传输量
避免不断跳转,提高用户体验
缺点:
对搜索引擎不友好
可能造成请求数增加
跨域问题:jsonp,jsonp与json区别,
详解js跨域问题:
http://segmentfault.com/a/1190000000718840
http://www.cnblogs.com/sunxucool/p/3433992.html

### 8.看下列代码输出为何？解释原因。<br  />
var a;
alert(typeof a); // undefined
alert(b); // 报错
在使用var声明变量但并未对其赋值进行初始化时，这个变量的值就是undefined。而b由于未声明将报错。注意未申明的变量和声明了未赋值的是不一样的。<br  />
typeof用来返回数据类型
instanceof用来检测某个对象是不是另一个对象的实例

### 9.看下列代码,输出什么？解释原因。<br  />
var a = null;
alert(typeof a); //object
null是一个只有一个值的数据类型，这个值就是null。表示一个空指针对象，所以用typeof检测会返回”object”。<br  />
如:typeof(null);//object

### 10.看下列代码,输出什么？解释原因。<br  />
var undefined;
undefined == null;//true undefined和null相等;关于undefined和null小结下
1 == true;//true
2 == true;//true错误应为false
0 == false;//true
0 == '';//true
NaN == NaN;//false
[] == false;//true
[] == ![];//false错误应为true  []是空数组字面量，转换成boolean值为true。
null用来表示尚未存在的对象
undefined是声明的变量尚未初始化

var foo = "11"+2-"1";
console.log(foo);
console.log(typeof foo);

### 11.看代码给答案<br  />

var a = new Object();
a.value = 1;
b = a;
b.value = 2;
console.log(a.value);//2

这里考察数据类型:对于基本类型和引用类型的区别

### 12.已知数组var stringArray = [“This”, “is”, “Baidu”, “Campus”]，Alert出”This is Baidu Campus”。<br  />

alert(stringArray.join(" "));

这里考察数组的一些方法了,w3school对join的定义和用法如下:<br  />
join方法用于把数组中的所有元素放入一个字符串<br  />
元素是通过指定的分隔符进行分隔的<br  />

那么问题来了，已知有字符串foo="get-element-by-id",写一个function将其转化成驼峰表示法"getElementById"。

function combo(msg){
    var arr = msg.split("-");
    var len = arr.length;    //将arr.length存储在一个局部变量可以提高for循环效率
    for(var i=1;i<len;i++){
        arr[i]=arr[i].charAt(0).toUpperCase()+arr[i].substr(1,arr[i].length-1);
    }
    msg=arr.join("");
    return msg;
}

//三种方式执行一个函数
//dom里绑定
//在js里绑定
//通过事件添加,添加addEventListener