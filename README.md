# interview

### 1.javascript是一门什么样的语言，它有哪些特点？

### 2.javascript的数据类型都有什么？<br  />
基本类型(undefined,null,number,string,boolean)；<br  />
引用类型(object:array,data,regex,function)。<br  />
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
```
考察对dom节点的操作

那么这里又让我们来探讨一下innerHTML吧,w3school上的定义是：innerHTML属性设置或返回表格行的开始和结束标签之间的html，而有一个document.write()经常拿来和它做比较，w3school说write方法可向文档写入html表达式和javascript代码。

其实这两者还是有很多不同之处的，让我们来缕一缕：

* document.write表示的是document文档有一个write()方法，用来在文档中写入内容；innerHTML是DOM元素的一个属性，指代的是这个元素包含的所有内容。简单说就是DOM的innerHTML是DOM元素对象的一个属性，而write是document对象的一个方法。
* 前者重绘整个页面，innerHTML可以重绘局部。
* document.write直接输出在浏览器，后面继续write，内容会一直在后面添加。innerHTML是获取或指定DOM元素的内容。
* 可以使用document.write()向输出流写HTML，如：
```
document.write("<h1>Hello World!</h1>")
```

### 6.当一个DOM节点被点击时候，我们希望能够执行一个函数，应该怎么做？<br  />

三种方式执行一个函数<br  />
dom里绑定<br  />
在js里绑定<br  />
通过事件添加,添加addEventListener<br  />

* 直接在DOM里绑定事件：<div onclick="test()"></div>
* 在JS里通过onclick绑定：xxx.onclick = test
* 通过事件添加进行绑定：addEventListener(xxx, ‘click’, test)

那么又有问题了，Javascript的事件流(事件发生顺序)模型都有什么？又都是由谁提出的呢?

“事件冒泡”：事件开始由最具体的元素接受，然后逐级向上传播;由微软提出<br  />
“事件捕捉”：事件由最不具体的节点先接收，然后逐级向下，一直到最具体的;由网景提出<br  />
“DOM事件流”有三个阶段：事件捕捉，目标阶段，事件冒泡

### 7.什么是Ajax和JSON，它们的优缺点。<br  />
Ajax是异步javascript和xml,用于在web页中实现异步数据交互<br  />
优点:<br  />
局部加载,降低数据传输量<br  />
避免不断跳转,提高用户体验<br  />
缺点:<br  />
对搜索引擎不友好<br  />
可能造成请求数增加<br  />
跨域问题:jsonp,<br  />

那么什么是跨域问题呢?jsonp与json有什么区别呢?

关于跨域的概念:只要协议,域名,端口有任何一个不同,都被当做是不同的域.
jsonp(json with padding)也叫填充式json,可以认为是被包含在函数调用中的json:

```
callback({"name","trigkit4"});
```

参考资料:

[详解js跨域问题](http://segmentfault.com/a/1190000000718840)<br  />
[如何解决ajax跨域问题](http://www.cnblogs.com/sunxucool/p/3433992.html)

### 8.看下列代码输出为何？解释原因。<br  />
```js
var a;
alert(typeof a); // undefined
alert(b); // 报错
```
在使用var声明变量但并未对其赋值进行初始化时，这个变量的值就是undefined。而b由于未声明将报错。注意未申明的变量和声明了未赋值的是不一样的。<br  />
typeof用来返回数据类型<br  />
instanceof用来检测某个对象是不是另一个对象的实例<br  />

### 9.看下列代码,输出什么？解释原因。<br  />
```js
var a = null;
alert(typeof a); //object
```
null是一个只有一个值的数据类型，这个值就是null。表示一个空指针对象，所以用typeof检测会返回”object”。<br  />
如:typeof(null);//object

### 10.看下列代码,输出什么？解释原因。<br  />
```js
var undefined;
undefined == null;//true undefined和null相等;
1 == true;//true
2 == true;//true错误应为false;==会把比较的二者进行类型转换
0 == false;//true
0 == '';//true
NaN == NaN;//false
[] == false;//true
[] == ![];//false;错误应为true  因为![]是个布尔值,为false,因此我们比较的是[] == 0;
```
null用来表示尚未存在的对象<br  />
undefined是声明的变量尚未初始化

关于比较可以看迷渡的这篇:

[详解javascript中的比较](http://segmentfault.com/q/1010000000305997)

比如还有:

```
0 == '0';//true
[] == [];//false
[] == !{};//true;因为!{}是个布尔值,为false,因此我们比较的是[] == 0;

```
var foo = "11"+2-"1";
console.log(foo);
console.log(typeof foo);
```

值为111,类型为number

### 11.看代码给答案<br  />
```js
var a = new Object();
a.value = 1;
b = a;
b.value = 2;
console.log(a.value);//2
```

这里考察数据类型:对于基本类型和引用类型的区别,引用数据类型细节.

### 12.已知数组var stringArray = [“This”, “is”, “Baidu”, “Campus”]，Alert出”This is Baidu Campus”。<br  />

alert(stringArray.join(" "));

这里考察数组的一些方法了,w3school对join的定义和用法如下:<br  />
join方法用于把数组中的所有元素放入一个字符串<br  />
元素是通过指定的分隔符进行分隔的<br  />

那么问题来了，已知有字符串foo="get-element-by-id",写一个function将其转化成驼峰表示法"getElementById"。

```js
function combo(msg){
    var arr = msg.split("-");
    var len = arr.length;    //将arr.length存储在一个局部变量可以提高for循环效率
    for(var i=1;i<len;i++){
        arr[i]=arr[i].charAt(0).toUpperCase()+arr[i].substr(1,arr[i].length-1);
    }
    msg=arr.join("");
    return msg;
}
```
考察基础API

### 13.var numberArray = [3, 6, 2, 4, 1, 5];

1)实现对该数组的倒排,输出[5, 1, 4, 2, 6, 3]<br  />
2)实现对该数组的降序排列,输出[6, 5, 4, 3, 2, 1]

```js
var numberArray = [3, 6, 2, 4, 1, 5];
numberArray.reverse();//5, 1, 4, 2, 6, 3
numberArray.sort(function(a,b){//6, 5, 4, 3, 2, 1
	return b-a;
	})
```
reverse()方法用于颠倒数组中元素的顺序.该方法会改变原来的数组,而不会创建新的数组

sort()方法用于对数组的元素进行由小到大排序,提供比较函数后可以按照其他标准进行排序

考察数组的相关操作

### 14.输出今天的日期，以YYYY-MM-DD的方式，比如今天是2014年9月26日，则输出2014-09-26.

```js
var date = new Date();
var year = date.getFullYear();//获取年,返回四位
var month = date.getMonth() + 1;//获取月份,0是1月
month = month < 10 ? '0' + month : month;//让月份显示两位
var day = date.getDate();//获取日
day = day < 10 ? '0' + day : day;//让天数显示两位
console.log(year + '-' + month + '-' + day);
```
考察日期的相关操作

### 15.将字符串”<tr><td>{id}</td><td>{name}</td></tr>”中的{id}替换成10，{name}替换成Tony （使用正则表达式）

答案："<tr><td>{id}</td><td>{id}_{$name}</td></tr>".replace(/{\$id}/g, '10').replace(/{\$name}/g, ‘Tony’);

### 16.为了保证页面输出安全，我们经常需要对一些特殊的字符进行转义，请写一个函数escapeHtml，将<, >, &, “进行转义.

```js
function escapeHtml(str){
	return str.replace(/[<>"&]/g, function(match){
		switch(match){
			case "<";
				return "&lt;";
			case ">":
				return "&gt;";
			case “&”:
            	return “&amp;”;
            case “\””:
            	return “&quot;”;
		}
	}
}
```

### 17.foo = foo||bar ，这行代码是什么意思？为什么要这样写？

答案：if(!foo) foo = bar; //如果foo存在，值不变，否则把bar的值赋给foo。

短路表达式：作为"&&"和"||"操作符的操作数表达式，这些表达式在进行求值时，只要最终的结果已经可以确定是真或假，求值过程便告终止，这称之为短路求值。

### 18.看下列代码，将会输出什么?

```js
var foo = 1;
function a(){
	console.log(foo);
	var foo = 2;
	console.log(foo);
};
a();
```

输出undefined和2.这里的一个考察点在于变量声明提前.也就是```var foo = 2;```其实应该拆分为两部分,var foo;和foo = 2;前者是声明,会提前,
后者是赋值,不会提前

函数声明与变量声明会被JavaScript引擎隐式地提升到当前作用域的顶部，但是只提升名称不会提升赋值部分。

### 19.用js实现随机选取10--100之间的10个数字，存入一个数组，并排序。
```js
var array = [];
for (i = 0; i < 10; i++){
	var number = Math.random()*90 + 10;
	array.push(number);
}
array.sort();
```
或者

```js
var iArray = [];
function getRandom(start,end){   
	var Range = end - start;    
	return (start +(Math.random() * Range));   
}   
for(var i=0; i<10; i++){
    iArray.push(getRandom(10,100));
}
console.log(iArray);
```
这里原答案有几处粗心的错误,一个是function没有写c,一个是()没有写全,其中function那个错误还找了好久没有找到问题,因为自己没有写function的
方法就没有比对着看.

### 20.把两个数组合并,并删除第二个元素

```js
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];
var array3 = array1.concat(array2);
array3.splice(1, 1);
```
concat的连接让我想到mysql里也是这个连接符.这是和别的sql语句不同的地方

考察的还是数组的相关操作,那就把数组的相关操作总结一下:

### 21.怎样添加、移除、移动、复制、创建和查找节点（原生JS，实在基础，没细写每一步)

1)创建新节点
```js
createDocumentFragment()//创建一个DOM片段
createElement()//创建一个具体的元素
createTextNode()//创建一个文本节点
```

2)添加,移除,替换,插入
```js
appendChild()//添加
removeChild()//移除
replaceChild()//替换
insertBefore()//插入
```

3)查找
```js
getElementsByTagName()//通过标签名称
getElementsByName()//通过元素的Name属性的值
getElementById()//通过元素id,唯一性
```

### 22.有这样一个URL：http://item.taobao.com/item.htm?a=1&b=2&c=&d=xxx&e，请写一段JS程序提取URL中的各个GET参数(参数名
和参数个数不确定)，将其按key-value形式返回到一个json结构中，如{a:'1', b:'2', c:'', d:'xxx', e:undefined}。

```js
function serilizeUrl(url) {
    var result = {};
    url = url.split("?")[1];
    var map = url.split("&");
    for(var i = 0, len = map.length; i < len; i++) {
        result[map[i].split("=")[0]] = map[i].split("=")[1];
    }
    return result;
}
```

w3cshool:split()方法用于把一个字符串分割成字符串数组.主要还是考察数组相关方法,干脆总结下数组大概有哪些方法:splice等

### 23.正则表达式构造函数var reg=new RegExp("xxx")与正则表达字面量var reg=//有什么不同？匹配邮箱的正则表达式？

答案：当使用RegExp()构造函数的时候，不仅需要转义引号（即\"表示"），并且还需要双反斜杠（即\\表示一个\）。使用正则表达字面量的效率更高。

邮箱的正则匹配:
```js
var regMail = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((.[a-zA-Z0-9_-]{2,3}){1,2})$/;
```

关于正则的相关匹配,这里有篇对匹配URL比较详细的:
[更靠谱一些的正则表达式验证URL](http://www.soulteary.com/2014/12/05/better-url-regexp-in-js.html)

### 24.看下面代码，给出输出结果。

```js
for(var i=1;i<=3;i++){
  setTimeout(function(){
      console.log(i);
  },0);
};
```

结果是4,4,4

这是一个老生常谈的经典问题了,涉及异步和闭包的问题

http://www.bubuko.com/infodetail-1183545.html

### 25.写一个function，清除字符串前后的空格。（兼容所有浏览器）.使用自带接口trim()，考虑兼容性：

```js
if (!String.prototype.trim) { 
 String.prototype.trim = function() { 
 return this.replace(/^\s+/, "").replace(/\s+$/,"");
 } 
} 

// test the function 
var str = " \t\n test string ".trim(); 
alert(str == "test string"); // alerts "true"
```

### 26.Javascript中callee和caller的作用？

caller是返回一个对函数的引用，该函数调用了当前函数；

callee是返回正在被执行的function函数，也就是所指定的function对象的正文。

那么问题来了？如果一对兔子每月生一对兔子；一对新生兔，从第二个月起就开始生兔子；假定每对兔子都是一雌一雄，试问一对兔子，第n个月能繁殖成多少对兔子？（使用callee完成）

```js
var result=[];
function fn(n){  //典型的斐波那契数列
   if(n==1){
        return 1;
   }else if(n==2){
           return 1;
   }else{
        if(result[n]){
                return result[n];
        }else{
                //argument.callee()表示fn()
                result[n]=arguments.callee(n-1)+arguments.callee(n-2);
                return result[n];
        }
   }
}
```

### 27.实现一个函数clone，可以对JavaScript中的5种主要的数据类型（包括Number、String、Object、Array、Boolean）进行值复制
      
考察点1：对于基本数据类型和引用数据类型在内存中存放的是值还是指针这一区别是否清楚<br  />
考察点2：是否知道如何判断一个变量是什么类型的<br  />
考察点3：递归算法的设计<br  />

```js
// 方法一：
Object.prototype.clone = function(){
        var o = this.constructor === Array ? [] : {};
        for(var e in this){
                o[e] = typeof this[e] === "object" ? this[e].clone() : this[e];
        }
        return o;
}
```

```js
//方法二：
  /**
     * 克隆一个对象
     */ 
    function clone(Obj) {   
        var buf;   
        if (Obj instanceof Array) {   
            buf = [];                    //创建一个空的数组 
            var i = Obj.length;   
            while (i--) {   
                buf[i] = clone(Obj[i]);   
            }   
            return buf;    
        }else if (Obj instanceof Object){   
            buf = {};                   //创建一个空对象 
            for (var k in Obj) {           //为这个对象添加新的属性 
                buf[k] = clone(Obj[k]);   
            }   
            return buf;   
        }else{                         //普通变量直接赋值
            return Obj;   
        }   
    }
```

### 28.如何消除一个数组里面重复的元素？

```js
var arr=[1,2,3,3,4,4,5,5,6,1,9,3,25,4];
	function deRepeat(){
		var newArr=[];
		var obj={};
		var index=0;
		var l=arr.length;
		for(var i=0;i<l;i++){
			if(obj[arr[i]]==undefined)
			  {
				obj[arr[i]]=1;
				newArr[index++]=arr[i];
			  }
			else if(obj[arr[i]]==1)
			  continue;
		}
		return newArr;

	}
	var newArr2=deRepeat(arr);
	alert(newArr2); //输出1,2,3,4,5,6,9,25
```

### 29.小贤是一条可爱的小狗(Dog)，它的叫声很好听(wow)，每次看到主人的时候就会乖乖叫一声(yelp)。从这段描述可以得到以下对象：

```js
function Dog() {
       this.wow = function() {
               alert(’Wow’);
      }
       this.yelp = function() {
              this.wow();
      }
}
```

小芒和小贤一样，原来也是一条可爱的小狗，可是突然有一天疯了(MadDog)，一看到人就会每隔半秒叫一声(wow)地不停叫唤(yelp)。<br  />
请根据描述，按示例的形式用代码来实现。（继承，原型，setInterval）

```js
function MadDog() {
    this.yelp = function() {
          var self = this;          
          setInterval(function() {
                self.wow();      
          }, 500);
      }
}
MadDog.prototype = new Dog();

//for test
var dog = new Dog();
dog.yelp();
var madDog = new MadDog();
madDog.yelp();
```

### 30.下面这个ul，如何点击每一列的时候alert其index?

```js
<ul id=”test”>
	<li>这是第一条</li>
	<li>这是第二条</li>
	<li>这是第三条</li>
</ul>
```
答案:

```js
// 方法一：
var lis = document.getElementById('test').getElementsByTagName('li');
for(var i=0;i<3;i++){
    lis[i].index=i;
    lis[i].onclick=function(){
        alert(this.index);
    };
}

//方法二：
var lis = document.getElementById('test').getElementsByTagName('li');
for(var i=0;i<3;i++){
    lis[i].index=i;
    lis[i].onclick=(function(a){
        return function() {
            alert(a);
        }
    })(i);
}
```
两种方法,一种通过this来解决,一种通过闭包的形式

### 31.编写一个JavaScript函数，输入指定类型的选择器(仅需支持id，class，tagName三种简单CSS选择器，<br  />
无需兼容组合选择器)可以返回匹配的DOM节点，需考虑浏览器兼容性和性能