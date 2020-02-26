

### BOM常用API

++++

#### 一、window对象

1、窗口位置

```javascript
var leftPos = (typeof window.screenLeft === "number") ? window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop === 'number') ? window.screenTop : window.screenY;
console.log('窗口相对于屏幕左边的位置：' + leftPos);
console.log('窗口相对于屏幕上边的位置：' + topPos);
```

2、窗口页面视图大小

```javascript
var pageWidth = window.innerWidth;
var pageHeight = window.innerHeight;
if (typeof pageWidth != 'number') {
	/*判断浏览器是否在标准模式下*/
	if (document.compatMode != 'CSS1Compat'){
		pageWidth = document.documentElement.clientWidth;
		pageHeight = document.documentElement.clientHeight;
	}else {
		pageWidth = document.body.clientWidth;
		pageHeight = document.body.clientHeight;
	}
}
console.log('页面视图宽度为：' + pageWidth);
console.log('页面视图高度为：' + pageHeight);
```

3、导航和打开窗口

测试弹出窗口是否被拦截

```javascript
var blocked = false;
try {
	var wroxWin = 				window.open('https://www.baidu.com','topframe','width=400,height=400,resizable=yes');
	console.log(wroxWin);
	if (wroxWin === null){
	blocked = true;
	}
}catch(ex) {
	blocked = true;
}
if(blocked) {
	console.log('The popup was blocked!');
}
```

4、间歇和超时调用

```javascript
var num = 0;
var max = 5;
var intervalId = null;
//间歇调用
function incrementNumber() {
    num++;
    console.log(num);
    if (num === max) {
        clearInterval(intervalId);
        console.log('Done')
    }
}
intervalId = setInterval(incrementNumber, 500);
//超时调用模仿间歇调用
function incrementNumber1() {
    num++;
    if (num < max) {
        setTimeout(incrementNumber1,500);
        console.log(num);
    }else {
        console.log('Done')
    }
}
setTimeout(incrementNumber1,500);
```



#### 二、location对象

1、查询字符串参数

提取每个查询字符串中的参数

```javascript
function getQueryStringArgs() {
    var qs = (location.search.length > 0 ? location.search.substring(1) : ''),
        args = {},
        items = qs.length ? qs.split('&') : [],
        item = null,
        name = null,
        value = null,
        i = 0,
        len = items.length;
    for (i=0; i < len; i++) {
        item = items[i].split('=');
        //间URL中转义序列转换成原字符
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);
        if (name.length) {
            args[name] = value;
        }
    }
    return args;
}
var args = getQueryStringArgs();
console.log(args);
```

2、位置操作

```javascript
//导航到新URL，并生成一条浏览记录
location.assign('https://www.baidu.com/');
//导航到指定URL，并生成一条浏览记录
location.href = 'https://www.baidu.com/';
//导航到指定URL，不生产浏览记录，无法通过后退键返回原页面
location.replace('https://www.baidu.com/');
//从浏览器缓存中重新加载当前页面
location.reload();
//从服务器中重新加载当前页面
location.reload(true);
```



#### 三、navigator对象

1、检查插件

```javascript
//检查插件,在IE中无效
function hasPlugin(name) {
    name = name.toLowerCase();
    for (var i = 0; i < navigator.plugins.length; i++) {
        if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){
            return true;
        }
    }
    return false;
}
console.log(hasPlugin('Chrome PDF Plugin'));

//检查IE插件
function hasIEPlugin(name) {
    try {
        new ActiveObject(name);
        return true;
    }catch(ex) {
        return false;
    }
}
console.log(hasIEPlugin('ShockwaveFlash.ShockwaveFlash'));
//检查单个具体插件
function hasFlash() {
    var result = hasPlugin('flash');
    if (!result) {
        result = hasIEPlugin('ShockwaveFlash.ShockwaveFlash');
    }
    return result;
}

console.log(hasFlash());
```



#### 四、screen对象

1、用来表示客户端的能力，例如显示器信息、像素宽高等

```javascript
//调整浏览器窗口大小，使其占据屏幕的可用空间
window.resizeTo(screen.availWidth, screen.availHeight);
```



#### 五、history对象

```javascript
//后退
history.go(-1);
//前进
history.go(1);
//跳到指定字符串最近的记录
history.go('baidu.com');
//后退
history.back();
//前进
history.forward();
```

