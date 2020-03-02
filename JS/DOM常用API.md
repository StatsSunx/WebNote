

### DOM常用API

++++

#### 一、DOM基础

1、节点层次

```javascript
//节点类型
/*
元素节点：Node.ELEMENT_NODE(1)（常用）
属性节点：Node.ATTRIBUTE_NODE(2)（常用）
文本节点：Node.TEXT_NODE(3)（常用）
CDATA节点：Node.CDATA_SECTION_NODE(4)
实体引用名称节点：Node.ENTRY_REFERENCE_NODE(5)
实体名称节点：Node.ENTITY_NODE(6)
处理指令节点：Node.PROCESSING_INSTRUCTION_NODE(7)
注释节点：Node.COMMENT_NODE(8)（常用）
文档节点：Node.DOCUMENT_NODE(9)（常用）
文档类型节点：Node.DOCUMENT_TYPE_NODE(10)
文档片段节点：Node.DOCUMENT_FRAGMENT_NODE(11)
DTD声明节点：Node.NOTATION_NODE(12)
 */
var someNode;
someNode.nodeType;
someNode.nodeName;
someNode.tagName;
someNode.nodeVa

//节点关系
someNode.childNodes;
someNode.parentNode;
someNode.firstChild;
someNode.childNodes[0];
someNode.childNodes.item(0);
someNode.lastChild;
someNode.childNodes[someNode.childNodes.length-1];
someNode.childNodes.item(someNode.childNodes.length-1);
someNode.nextSibling;
someNode.previousSibling;
hasChildNodes();
ownerDocum

//操作节点
//在结尾插入子元素
someNode.appendChild(newNode);
//在targetNode元素前面插入子元素
someNode.insertNode(newnode,targetNode);
//替换元素
someNode.replaceChild(newNode, oldNode);
//删除元素
someNode.removeChild(oldNode);
//浅复制
someNode.cloneNode(false);
//深复制
someNode.cloneNode(true);
```

2、Document类型

```javascript
//文档子节点
    document.documentElement;
    document.firstChild;
    document.lastChild;
    document.childNodes;
    document.doctype;
    document.body;

//文档信息
    document.title;
    //地址栏中URL
    document.URL;
    //域名
    document.domain;
    //来源页面地址
    document.referrer;

//查找元素
    document.getElementById('id');
    document.getElementsByTagName('tagName');
    //文档中所有带有属性name的元素
    document.getElementsByName('name');

//特殊集合
    //文档中所有带有name属性的a元素
    document.anchors;
    //文档中所有form元素
    document.forms;
    //文档中所有图片元素
    document.images;
    //文档中所有带有href的a元素
    document.links;
    //DOM一致性检测
    document.implementation.hasFeature();

//文档写入
    //如果文档在加载结束后调用write函数，页面会被重写
    document.write();
    document.writeln();
    document.open(method, url, async, user, password);
    document.close();
```

3、Element类型

```javascript
/*HTML*/
<div id="myDiv" class="box" title="element test" dir="ltr" my_special_attribute='hello'>
    <ul>
        <li>列表1</li>
        <li>列表2</li>
        <li>列表3</li>
    </ul>
</div>

/*JavaScript*/
//HTML元素
    //元素的特性可以直接用‘.’号获取
    var div = document.getElementById("myDiv");
    console.log(div.id);
    console.log(div.className);
    console.log(div.title);
    console.log(div.dir);
    //对于非公认特性，及一般为自定义特性无法通过该方法获取
    console.log(div.my_special_attribute);//undefined

//取得特性
    // getAttribute(name: DOMString);
    console.log(div.getAttribute('id'));
    console.log(div.getAttribute('class'));
    console.log(div.getAttribute('title'));
    console.log(div.getAttribute('dir'));
    //该方法可以获取自定义的属性
    console.log(div.getAttribute('my_special_attribute'));
    //hell0

//设置特性
    // setAttribute(name: DOMString, value: DOMString);
    div.setAttribute('class', 'myClass');
    console.log(div.className);
    div.setAttribute('my_attribute', 'world');

//删除属性,不常用
    removeAttribute(name: DOMString)

//attributes属性
    console.log(div.attributes.length);
    console.log(div.attributes['id'].nodeName);
    console.log(div.attributes['id'].nodeValue);
    //获取元素所以属性名称及值
    function outputAttributes() {
        var pairs = new Array(),
            attrName,
            attrValue,
            i,
            len;
        for (i=0, len=div.attributes.length; i < len ; i++){
            attrName = div.attributes[i].nodeName;
            attrValue = div.attributes[i].nodeValue;
            if (div.attributes[i].specified) {
                pairs.push(attrName + "= \"" + attrValue + "\"");
            }
        }
        return pairs.join(" ");
    }
    console.log(outputAttributes());

//创建元素
    var p = document.createElement('p');
    document.body.appendChild(p);
    p.id = 'ppt';
    p.title = '段落';
    div.appendChild(p);

//元素的子节点
    //只选取元素节点
    for (var i=0, len = div.childNodes.length; i < len; i++){
        if (div.childNodes[i].nodeType === 1) {
            //执行操作
        }
    }
```

4、Text类型

```javascript
var div = document.getElementById('myDiv');
var textNode = div.childNodes[0];
console.log(textNode.nodeType === 3);
textNode.nodeValue = '我是div的第一个节点，属于文本节点';
console.log(textNode.data);

//创建文本节点
    var textNode1 = document.createTextNode('hello   world');
    var textNode2 =  document.createTextNode('你是最美的彩虹');
    div.appendChild(textNode1);
    div.appendChild(textNode2);

//规范化文本节点
    //将相邻的所有文本节点合并成一个文本节点；
    div.normalize();

//分割文本节点
    var newNode = div.firstChild.splitText(12);
    console.log(div.childNodes[0]);
    console.log(div.childNodes[1]);
```



#### 二、DOM扩展

以下案例的HTML结构

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>DOM常用API</title>
</head>
<body>
<!-- DOM扩展 -->
    <div class="myClass user" data-myname="dataset">
        <ul>
            <li></li>
            <li></li>
            <li></li>
        </ul>
        <div></div>
        <p></p>
        <a href="#"></a>
    </div>
    <div id="myId" class="myClass">
        <h1></h1>
        <h2></h2>
        <h3></h3>
        <p></p>
        <a href="#"></a>
    </div>
<body>
<head>
```

1、选择符API

```javascript
//一、选择符API		
		//querySelector()或querySelectorAll由document或element类型实例调用
    //querySelector()返回查找到的第一个匹配元素
    var div = document.querySelector('div');
    var div1 = document.querySelector('#myId');
    var div2 = document.querySelector('.myClass');
    console.log(div1 === div2);
    console.log(div === div2);

    //querySelectorAll()返回一个novelist，包含所有匹配到的元素
    var divAll = document.querySelectorAll('div');
    console.log(divAll.length);
    console.log(divAll);

    //matchesSelector()调用元素如果和选择符匹配，则返回true
    //chrome
    console.log(div1.webkitMatchesSelector('#myId'));
    //firefox
    console.log(div1.mozMatchesSelector('#myId'));
```

2、元素遍历

```javascript
//二、元素遍历
    //返回子元素个数（不包括文本节点和注释）
    childElementCount
    //指向第一个子元素
    firstElementChild
    //指向最后一个子元素
    lastElementChild
    //指向前一个同辈元素
    previousElementSibling
    //指向后一个同辈元素
    nextElementSibling

    元素遍历
    function traversalElement(element) {
        var element = document.querySelector(element);
        // console.log(element.childElementCount);
        var i,
            len,
            child = element.firstElementChild,
            nodeList = new Array();
            nodeList[0] = child;
        while (child != element.lastElementChild) {
            //已知其是元素
            // processChild(child);
            child = child.nextElementSibling;
            nodeList.push(child);
        }
        return console.log(nodeList);
    }
    traversalElement('div');
    traversalElement('#myId');
```

3、HTML5

```javascript
//三、HTML5
    //类操作的API扩充
    var div = document.querySelector('#myId');
    var div1 = document.getElementsByClassName('myClass');

    div.classList.add('current');
    console.log(div.classList.contains('myClass'))
    div.classList.toggle('user');

    console.log(div.classList.length);
    console.log(div.classList);

    div.classList.remove('current');
    console.log(div.classList);


    //焦点管理
    var div = document.querySelector('#myId');
    var a = div.querySelector('a');
    a.focus();
    console.log(a === document.activeElement);
    console.log(document.hasFocus());


    //HTMLDocument的变化
    //readyState属性
    //指示文档是否已加载完成，有complete和loading两个值
    console.log(document.readyState);
    if (document.readyState === 'complete') {
        console.log('The document is completed!')
    }else {
        console.log('The document is loading!')
    };


    //兼容模式
    //compatMode有两个值：标准模式=CSS1Compat、混合模式=BackCompat
    if (document.compatMode === 'CSS1Compat') {
        console.log('standards mode');
    }else {
        console.log('Quirks mode');
    };


    //head属性
    var head = document.head || document.getElementsByTagName('head')[0];


    //字符集属性
    //当前问题实际使用的字符集
    console.log(document.charset);
    //浏览器及操作系统设置的文档默认字符集
    console.log(document.defaultCharset);


    //自定义数据属性
    //HTML5规定元素添加自定义属性必须加上data-前缀
    var div = document.querySelector('.user');
    console.log(div.dataset);
    console.log(div.dataset.myname);
    div.dataset.appid = '12345';
    console.log(div.dataset);


    //插入标记
    //innerHTML会替换掉div原所有的子节点
    //以下元素不支持innerHTML:frameset\head\html\style\table\tbody\thead\tfoot\tr
    var div = document.querySelector('.user');
    div.innerHTML = 'hello world';
    div.innerHTML = "hello & welcome, <b>'reader'!</b>";
    console.log(div.innerHTML);
    document.head.innerHTML = "<style type='text/css'>body {background-color: gray}</style>";

    //outerHTML会替换掉掉调用元素所有DOM子树包括自身
    console.log(div.outerHTML);
    div.outerHTML = "<p>this is a paragraph</p>";

    // //insertAdjacentHTML两个参数：插入位置和要插入的HTML文本
    // //在div前面添加兄弟元素
    div.insertAdjacentHTML("beforebegin", "<p>this is a paragraph</p>");
    // //在div里面作为第一个元素插入
    div.insertAdjacentHTML("afterbegin", "<p>this is a paragraph</p>");
    // // 在div里面作为最后一个元素插入
    div.insertAdjacentHTML("beforeend", "<p>this is a paragraph</p>");
    // // 在div后面添加兄弟元素
    div.insertAdjacentHTML("afterend", "<p>this is a paragraph</p>");


    //内存优化问题
    //为页面添加多个列表
    var ul = document.querySelector('ul'),
        values = ['列表1', '列表2', '列表3', '列表4', '列表5'],
        itemsHtml = "";
    for (var i = 0, len = values.length; i < len; i++) {
        itemsHtml += "<li>" + values[i]+ "</li>";
    };
    ul.innerHTML = itemsHtml;


    //滚动
    //使指定元素出现在视图窗口中
    scrollIntoView();
```

4、专有扩展

```javascript
//四、专有扩展
    //contains()方法
    console.log(document.documentElement.contains(document.body));
    							console.log(document.documentElement.compareDocumentPosition(document.querySelector('div')));
    console.log(document.documentElement.compareDocumentPosition(document.head));

    //插入文本
    var div = document.querySelector('.user');
    //插入的文本会替换元素中所有内容和子节点
    div.innerText = 'hello world';
    //innerText只插入文本，无法识别元素标签
    div.innerText = "hello & welcome, <b>'reader'!</b>";

    //滚动
    //当前页面不可见时滚动，在窗口内时不处理，作用与元素容器
    scrollIntoViewIfNeeded();
    //将元素内容滚动指定的页面高度，影响元素自身
    scrollByPages();
    //将元素内容滚动指定的行高，影响元素自身
    scrollByLines();
```



### 三、DOM2、DOM3

以下案例的HTML结构

```javascript
//HTML
<div id="div1" class="myClass" style="background-color: #eee; border: 1px solid red">
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <p>我是一个段落我是一个段落</p>
    <ul>
        <li>列表1</li>
        <li>列表2</li>
        <li>列表3</li>
    </ul>
</div>
//CSS
<style type="text/css">
    #div1 {
        background-color: lightblue;
        width: 200px;
        height: 100px;
        box-sizing: border-box;
        overflow: auto;
    }
    .myClass {
        margin: 30px;
    }
</style>
```



1、样式

```javascript
//访问元素样式
    var div1 = document.querySelector('#div1');
    console.log(div1.style);
    console.log(div1.style.length)
    console.log(div1.style.backgroundColor);
    //返回指定元素的属性值对
    function getElementStyleValues(element) {
        var element = document.querySelector(element),
            prop,
            value,
            i,
            len = element.style.length;
        for (i=0; i < len; i++) {
            prop = element.style[i];
            value = element.style.getPropertyValue(prop);
            console.log(prop + ':' + value);
        }
    }
    getElementStyleValues('#div1');


//计算的样式
    //style特性不能包含从其他样式表中层叠而来的元素样式信息
    //需要借助document.defaultView中的方法getComputedStyle，IE中是currenStyle
    var div1 = document.querySelector('#div1');
    var computedStyle = document.defaultView.getComputedStyle(div1, null);
    console.log(computedStyle);
    console.log(computedStyle.length);
    console.log(computedStyle.backgroundColor);
    //返回元素样式混合计算后的属性值对
    function getElementComputedStyle(element) {
        var element = document.querySelector(element),
            prop,
            value,
            i,
            len = computedStyle.length;

        if (element.currenStyle) {
            //IE
            computedStyle = element.currenStyle;
        }else {
            computedStyle = document.defaultView.getComputedStyle(element, null);
        }

        for (i=0; i < len; i++) {
            prop = computedStyle[i];
            value = computedStyle.getPropertyValue(prop);
            console.log(prop + ':' + value);
        }
    }
    getElementComputedStyle('#div1');


//操作样式表
    //检验浏览器是否支持styleSheets属性
    console.log(document.implementation.hasFeature('styleSheets', '2.0'));
    console.log(document.styleSheets);
    //获得元素的样式表
    function getStyleSheet(element) {
        var element = document.querySelector(element);
        //IE支持styleSheet
        return element.styleSheet || element.sheet;
    }
    // console.log(getStyleSheet('div'));

    //CSS规则
    var sheet = document.styleSheets[1];
    //IE支持rules属性
    var rules = sheet.cssRules || sheet.rules;
    var rule = rules[1];
    console.log(rule.cssText);
    console.log(rule.selectorText);
    console.log(rule.style);
    console.log(rule.type);
    console.log(rule.style.margin);
    rule.style.margin = '40px';

    //创建规则insertRule()
    //IE支持
    sheet.addRule("p","background-color: pink", 2);
    //除IE外浏览器支持
    sheet.insertRule("li {background-color: red}", 3);

    //样式规则插入函数（兼容版）
    function insertRules(sheet, selectorText, cssText, position) {
        if (sheet.insertRule) {
            sheet.insertRule(selectorText + "{" + cssText + "}", position)
        }else if(sheet.addRule){
            sheet.addRule(selectorText ,cssText, position);
        }
    }
    insertRules(document.styleSheets[1],
        "h4", "background-color: #ddd", 2);

    //删除规则,轻易不要用
    //IE支持
    sheet.removeRule(3);
    //除IE外浏览器支持
    sheet.deleteRule(2);
```

2、元素大小

```javascript
//偏移量
        //元素在屏幕上占用的所有可见空间，只读属性
        /*
        offsetHeight:   元素在垂直方向占据的空间、元素垂直可见高度+水平滚动条高度+上下边框高度
        offsetWidth:    元素在水平方向占据的空间、元素水平可见宽度+垂直滚动条宽度+左右边框宽度
        offsetTop: 元素上外边框距包含元素上内边框之间像素距离
        offsetLeft: 元素左外边框距包含元素左内边框直接像素距离
        */
        var div1 = document.querySelector('#div1');
        console.log(div1.offsetWidth);
        console.log(div1.offsetHeight);
        console.log(div1.offsetLeft);
        console.log(div1.offsetTop);

        //获得元素距离页面左边的偏移量
        function getElementLeft(element) {
            var element = document.querySelector(element);
            var actualLeft = element.offsetLeft;
            var currentContainer = element.offsetParent;
            while (currentContainer != null) {
                actualLeft += currentContainer.offsetLeft;
                currentContainer = currentContainer.offsetParent;
            }
            return actualLeft;
        }

        console.log(getElementLeft("ul"));
        console.log(getElementLeft("li"));

        //获得元素距离页面顶部的偏移量
        function getElementTop (element) {
            var element = document.querySelector(element),
                actualTop = element.offsetTop,
                currentContainer = element.offsetParent;

            while (currentContainer != null) {
                actualTop += currentContainer.offsetTop;
                currentContainer = currentContainer.offsetParent;
            }
            return actualTop;
        }
        console.log(getElementTop("h3"));

//客户区大小
        //元素内容及其内边距所占空间大小
        var ul = document.querySelector('ul');
        console.log(ul.clientWidth);
        console.log(ul.clientHeight);

        //获得浏览器窗口大小
        function getViewPort () {
            if (document.compatMode === 'BackCompat') {
                return {
                    width: document.body.clientWidth,
                    height: document.body.clientHeight
                };
            }else {
                return {
                    width: document.documentElement.clientWidth,
                    height: document.documentElement.clientHeight
                };
            }
        }
        console.log(getViewPort());

//滚动大小
        //滚动大小指包含滚动内容的元素的大小
        var div1 = document.querySelector('#div1');
        //元素在没有滚动条的情况下，元素内容的总宽度，不包括边框和滚动条
        console.log(div1.scrollWidth);
        //元素在没有滚动条的情况下，元素内容的总高度，不包括边框
        console.log(div1.scrollHeight);
        //被隐藏在内容区域左侧元素的像素数
        console.log(div1.scrollLeft);
        //被隐藏在内容区域上方元素的像素数
        console.log(div1.scrollTop);

        //true
        console.log(div1.clientWidth === div1.scrollWidth);
        console.log(div1.clientHeight === div1.scrollHeight);
        //确定文档的总大小时要取客户区高度和滚动高度的最大值
        var docWidth = Math.max(document.documentElement.scrollWidth, document.documentElement.clientWidth);
        var docHeight = Math.max(document.documentElement.scrollHeight, document.documentElement.clientHeight);

        //使元素回滚到顶部
        function scrollToTop (element) {
            var element = document.querySelector(element);
            if (element.scrollTop != 0) {
                element.scrollTop = 0;
            }
        }

//确定元素大小
        function getBoundingClientRect1(element) {
            var element = document.querySelector(element);
            //将坐标归零
            if (typeof arguments.callee.offset != 'number') {
                var scrollTop = document.documentElement.scrollTop,
                    temp = document.createElement('div');
                temp.style.cssText = 'position: absolute;left: 0;top: 0;';
                document.body.appendChild(temp);
                arguments.callee.offset = -temp.getBoundingClientRect().top - scrollTop;
                document.body.removeChild(temp);
                temp = null;
            }

            var rect = element.getBoundingClientRect();
            var offset = arguments.callee.offset;

            return {
                left: rect.left + offset,
                right: rect.right + offset,
                top: rect.top + offset,
                bottom: rect.bottom + offset
            };
        }
        console.log(getBoundingClientRect1("div"));

        function getBoundingClientRect2(element) {
            var element = document.querySelector(element);
            var scrollTop = document.documentElement.scrollTop,
                scrollLeft = document.documentElement.scrollLeft;

            if (element.getBoundingClientRect) {
                if (typeof arguments.callee.offset != 'number') {
                    var temp = document.createElement('div');
                    temp.style.cssText = 'position: absolute; left:0; top:0';
                    document.body.appendChild(temp);
                    arguments.callee.offset = -temp.getBoundingClientRect().top - scrollTop;
                    document.body.removeChild(temp);
                    temp = null;
                }
                var rect = element.getBoundingClientRect();
                var offset = arguments.callee.offset;

                return {
                    left: rect.left + offset,
                    right: rect.right + offset,
                    top: rect.top + offset,
                    bottom: rect.bottom + offset
                };
            }else {
                var actualLeft = getElementLeft(element);
                var actualTop = getElementTop(element);

                return {
                    left: actualLeft - scrollLeft,
                    right: actualLeft - element.offsetWidth - scrollLeft,
                    top: actualTop - scrollTop,
                    bottom: actualTop + element.offsetHeight - scrollTop
                };
            }
        }

        console.log(getBoundingClientRect2('ul'));
```



3、遍历

```javascript
//NodeIterator遍历函数，有四个参数：遍历根节点、要访问节点类型、过滤器、是否扩展实体引用
        var div1 = document.querySelector('#div1');
        //定义过滤器
        var filter = function (node) {
            return node.tagName.toLowerCase() === "li" ? NodeFilter.FILTER_ACCEPT:NodeFilter.FILTER_SKIP;
        };
        //
        var iterator = document.createNodeIterator(div1, NodeFilter.SHOW_ELEMENT, filter, false);
        var node = iterator.nextNode();

        while (node !== null) {
            console.log(node.tagName.toLowerCase());
            node = iterator.nextNode();
        }
//TreeWalker比以上方法更灵活
        /*
        walker.parentNode():
        walker.firstChild():
        walker.lastChild():
        walker.nextSibling():
        walker.previousSibling():
         */
        var filter = function (node) {
            return node.tagName.toLowerCase() === "li" ? NodeFilter.FILTER_ACCEPT:NodeFilter.FILTER_SKIP;
        };
        //
        var walker = document.createTreeWalker(div1, NodeFilter.SHOW_ELEMENT, filter, false);
        var node = walker.nextNode();

        while (node !== null) {
            console.log(node.tagName.toLowerCase());
            node = walker.nextNode();
        }
        //currentNode表示遍历方法在上一次遍历中返回的节点
        console.log(walker.currentNode);
        walker.currentNode = document.body;
        console.log(walker.currentNode);
```



4、范围

```javascript
//待补充
```

