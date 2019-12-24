# 前言
```
在工作中老会碰到某个地方会需要水平居中或者垂直居中；而且居中问题也一直是前端面试中经常会被问到的问题；又恰好再网上看到一篇关于居中的文章，就结合一下，到时候用的时候就能够信手拈来。
```
# 水平居中
+ 行内元素，在父元素上设置text-align:center，就可以实现行内元素水平居中，元素设置如下：
```
    span{
        text-align:center;
    }
```
+ 块级元素，宽度固定，给该元素设置margin:0 auto就可以，元素设置如下：
```
    div{
        width:300px;
        margin:0 auto;
    }
```
+ 宽度固定，使用绝对定位方式，以及负值的margin-left，子元素设置如下：
```
    .child{
        position: absolute;
        width:300px;
        left:50%;
        margin-left:-150px;
    }
```
+ 宽度固定，使用绝对定位方式，以及left:0;right:0;margin:0 auto;子元素设置如下：
```
    .child{
        position: absolute;
        width:300px;
        left:0;
        right:0;
        margin:0 auto;
    }
```
+ 使用flex可以轻松实现水平居中，只要给子元素设置如下：
```
    .child{
        display: flex;
        justify-content: center;
    }
```
+ 使用CSS3中新增的transform属性，子元素设置如下：(原谅我CSS3没有学好，这个居中方法没有用过)
```
    .child{
        position:absolute;
        left:50%;
        -webkit-transform: translate(-50%,0);  
        -ms-transform: translate(-50%,0);
        transform:translate(-50%,0);
    }
```
# 垂直居中
* 单行文本：若元素是单行文本，设置line-height等于元素高度，则元素可设置如下：
```
    .text{
        height:80px;
        line-height:80px;
    }
```
* 行内块级元素，基本思想是使用display:inline-block;vertical-align:middle和一个伪元素让内容块处于容器中央；元素可设置如下：(这是一种很流行的方法，也适应IE7)
```
    .parent::after,.child{
        display:inline-block;
        vertical-align:middle;
    }
    .parent:after{
        content:'';
        height:100%;
    }
```
* 元素高度不定，可以用vertical-align属性，而vertical-align只有在父层为td或th时才会生效，对于其他块级元素(比如：div,p等)默认情况是不支持的。为了使用vertical-align，我们需要设置父元素display:table，子元素display:table-cell;vertical-align:middle
```
    .parent{
        width: 300px;
   		height: 300px;
   		background: lightblue;
   		display:table;
    }
    .child{
        display:table-cell;
   		vertical-align: middle;
   		background: orange;
    }
```
### &emsp;&emsp; **优点：**
#### &emsp;&emsp;&emsp;&emsp;  元素高度可以动态改变, 不需再CSS中定义, 如果父元素没有足够空间时, 该元素内容也不会被截断。
### &emsp;&emsp; **缺点：**
#### &emsp;&emsp;&emsp;&emsp;  IE6~7, 甚至IE8中无效。
* 使用flex可以轻松实现垂直居中，这样设置父元素就可以保证子元素垂直居中：
```
    .parent{
        display:flex;
        align-items:center;
    }
```
### &emsp;&emsp; **优点：**
#### &emsp;&emsp;&emsp;&emsp;  内容块的宽度任意，优雅的溢出；同时可用于更复杂高级的布局技术中。
### &emsp;&emsp; **缺点：**
#### &emsp;&emsp;&emsp;&emsp;  IE8/IE9不支持，需要添加前缀(-webkit-),渲染上可能会有一些问题。
* 元素高度固定，设置父元素相对定位position:relative，子元素设置如下：
```
    .child{
        position:absolute;
        height:400px;
        top:50%;
        margin-top:-200px;
    }
```
### &emsp;&emsp; **优点：**
#### &emsp;&emsp;&emsp;&emsp;  适用于所有浏览器。
### &emsp;&emsp; **缺点：**
#### &emsp;&emsp;&emsp;&emsp;  父元素空间不够时, 子元素可能不可见(当浏览器窗口缩小时,滚动条不出现时).如果子元素设置了overflow:auto, 则高度不够时, 会出现滚动条。
* 元素高度固定，设置父元素相对定位position:relative，子元素设置如下：
```
    .child{
        position:absolute;
        height:400px;
        top:0;
        bottom:0;
        margin:auto 0;
    }
```
### &emsp;&emsp; **优点：**
#### &emsp;&emsp;&emsp;&emsp;  简单。
### &emsp;&emsp; **缺点：**
#### &emsp;&emsp;&emsp;&emsp;  没有足够空间时, 子元素会被截断, 但不会有滚动条。
* 使用CSS3的属性transform，设置父元素相对定位position:relative，子元素设置如下：(IE8不支持)
```
    .child{
        position:absolute;
        top:50%;
        -webkit-transform: translate(0,-50%);  
        -ms-transform: translate(0,-50%);
        transform: translate(0,-50%);
    }
```