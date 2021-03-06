---
title: 前端代码规范
date:
tags:
---
# 前端代码规范
## html规范
#### 1. 单标签不用写闭合

#### 2. img、link、input、hr、br

#### 3. 自定义属性要以data-开头  否则这将被认为是不规范的

#### 4. ul/ol的直接子元素只能是li
#### 5. section标签中要有标题标签
<!--more-->  
如果你用了section/aside/article/nav这种标签需要在里面写一个h1/h2/h3之类的标题标签，因为这四个标签可以划分章节，它们都是独立的章节，需要有标题，如果UI里面根本就没有标题呢？那你可以写一个隐藏的标题标签，如果出于SEO的目的，你不能直接display: none，而要用一些特殊的处理方式，如下套一个hidden-text的类
```
<style>.hidden-text{position: absolute; left: -9999px; right: -9999px}</style>
<section>
    <h1 class="hidden-text">Listing Detail</h1>
</section>
```
#### 6. 使用section可以划分章节 增强seo
#### 7. 样式要写在head标签里  
样式不能写在body里，写在body里会导致渲染两次，特别是写得越靠后，可能会出现闪屏的情况，例如上面的已经渲染好了，突然遇到一个style标签，导致它要重新渲染，这样就闪了一下，不管是从码农的追求还是用户的体验，在body里面写style终究是一种下策.
#### 8. 特殊符号使用html实体
     符号  | 实体编码
    ------ | :----:
     ©	   | \&copy;
     ¥	   | \&yen;
     ®	   | \&reg;
	 >	   | \&gt;
     <     | \&lt;
     &     | \&amp;
#### 9.  img空src的问题  
有时候可能你需要在写一个空的img标签，然后在JS里面动态地给它赋src，所以你可能会这么写:
```
<img src="" alt>
```
但是这样写会有问题，如果你写了一个空的src，会导致浏览器认为src就是当前页面链接，然后会再一次请求当前页面，就跟你写一个a标签的href为空类似。如果是background-image也会有类似的问题。这个时候怎么办呢？如果你随便写一个不存在的url，浏览器会报404的错误。   
我知道的有两种解决方法，第一种是把src写成about:blank，如下： 

```
<img src="about:blank" alt>
```

这样它会去加载一个空白页面，这个没有兼容问题，不会加载当前页面，也不会报错。    
第二种办法是写一个1px的透明像素的base64，如下代码所示：

```
<img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7">
```

第二种可能比较符合规范，但是第一种比较简单，并且没有兼容性问题。

#### 10. 类的命名使用小写字母加中划线连接 

```
<div class="hello-world"></div> 
```

#### 11. 不要在https的连接中写http的图片  

```
<img src="//static.chimeroi.com/hello-world.jpg">
```

这样写就行了

## css编码规范

#### 1. 文件名规范  
小写字母加中横线
#### 2. 属性书写规范
![](/images/1.jpg)
#### 3. 选择器一般不要超过3个,即使是用scss写
#### 4. 减少对对样式的覆盖  

```
.house{
    margin-top: 20px;
}
.house:first-child{
    margin-top: 0;
}
```
可以写成


```
.house + .house{
    margin-top: 20px;
}
```
只有前面有.house的.house才能选中
还有这种

```
.request-demo input{
    border: 1px solid #282828;
}
.request-demo input[type=submit]{
    border: none;
}
```

可以写成

```
.request-demo input:not([type=sbumit]){
    border: 1px solid #282828;
}
```

#### 5. 少使用!important
#### 6. 多写注释
有时候你看源码的时候你会看到一些TODO的注释：

```
/* TODO(littledan): Computed properties don't work yet in nosnap.
   Rephrase when they do.
*/
```

表示这些代码还有待完善，或者有些缺陷需要以后修复。而这种TODO的注释一般编辑器会把TODO高亮。  

#### 7. 排版规范  
缩进四个空格
多个选择器共用一个样式集，每个选择器要各占一行，如下：

```
.landing-pop,
.samll-pop-outer,
.signup-success{   
    display: none;
}
```

每个属性名冒号后要带一个空格  

#### 8. 属性值规范  
不要设置太大的z-index  

#### 9.合并属性

#### 10. 清除浮动  
一般用clearfix

```
.clearfix:after{
    content: "";
    display: table;
    clear: both;
}
```

#### 11. 不要设置input的line-height  

#### 12. 行内元素 可以直接设置margin-left margin-right

## JS编码规范

#### 1. 在声明变量的时候进行赋值

#### 2. 函数的返回值类型要确定

#### 3. 排版规范  
一行太长就换行
#### 4. 减少魔数  对一些比较重要的常量起一个名字
#### 5. 不要让代码暴露在全局作用域下运行  
全局下变量的查找时间会更长, 污染全局作用域
#### 6. let / const / var 的使用  
避免变量重复定义 用let来定义变量, 用const适用于给常量起个名字  
for循环的变量作用域是独立的  
#### 7. 使用三目运算符替代 if-else
#### 8. 使用箭头函数来来取代简单的函数
```
setTimeout(function(){
    window.location.reload(true);
}, 2000);

setTimeout(()=>window.location.reload(true), 2000)
```
#### 9. 注意避免执行过长时间的JS代码  
#### 10. 多写注释  
文件顶部的注释 描述 作者 更新  
函数的注释
变量定义和代码的注释  
#### 11. 代码嵌套不要太深  
#### 12. jQuery编码规范  
 > 尽量不要使用parent去获取DOM元素，如下代码:

```
var $activeRows = $this.parent().parent().children(".active");
/*这样的代码扩展性不好，一旦DOM结构发生改变，这里的逻辑分分钟会挂，如某天你可能会套了个div用来清除浮动，但是没想到导致有个按钮点不了了就坑爹了。*/

//应该用closest，如：

var $activeRows = $this.closest(".order-list").find(".active");
/*直接定位和目标元素的最近共同祖先节点，然后find一下目标元素就好了，这样就不会出现上面的问题，只要容器的类没有变。如果你需要处理非自己的相邻元素，可以这么搞：*/

$this.closest("li").siblings("li.active").removeClass("active");
$this.addClass("active");
/*有时候你可以先把所有的li都置成某个类，然后再把自己改回去也是可取的，因为浏览器会进行优化，不会一见到DOM操作就立刻执行，会先排成一个队列，然后再一起处理，所以实际的DOM操作对自己先加一个类然后再去掉的正负相抵操作很可能是不会执行的。*/
```
> 选择器的性能问题  如下
```
$("page li").addClass("active");
$("page ul").text(number);
$("page .page-text").removeClass("active");
```
上面的代码做了三次全局查找,可进行如下优化:
```
var $page = $(".page");
$page.find("li").addClass("active");
$page.find("ul").text(number);
$page.find(".page-text").removeClass("active");
```
先做一个全局查找,然后后续的查找都缩小到$page范围,$page的范围就比全局要小的多了.
jQuery的查找也是使用的querySelectorAll, 这个函数除了用在doucment以外,也可用在其他DOM节点
> 对DOM节点较少的不要使用委托

> 有时候使用原生更简单  
如 获取input和他的value
```
let email = form.email.value.trim();
```
#### 13. 对常用的属性进行缓存

```
let webLink = window.location.protocol + window.location.hostname;
if(openType === "needtoTouch"){
    webLink += "/admin/lead/list/page" + 
             window.location.search.replace(/openType=needToTouch(&?)/, "") + 
             window.location.hash;
}
```
可以先把它缓存下(即用局部变量进行接收,然后再进行调用), 加快变量作用域查找
```
let location = window.location;
let webLink = location.protocol + location.hostname;
if(openType === "needtoTouch"){
    webLink += "/admin/lead/list/page" +
                location.search.replace(/openType=needToTouch(&?)/, "") +       
                location.hash;
}
```
#### 14. 尽量不要在JS中写CSS
如果要对样式进行处理，我们选择通过添加删除class的方式来进行控制
#### 15. 在必要的地方加上非空校验
#### 16. 不要使用for in来循环数组
用 foreach 或者map方法
#### 17. 不要直接使用localStorage


原文来自https://juejin.im/post/599ececb5188252423583c27, **侵删**  

这是一篇对这篇文章的摘录和笔记





