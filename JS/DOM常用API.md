

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



