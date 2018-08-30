# markdown 语法 
<!-- (https://www.jianshu.com/p/b03a8d7b1719) -->

[TOC]


### 1.标题 
```
注意： #后面要空格 与上一行隔一行
# h1
## h2
### h3
#### h4
##### h5
###### h6
####### h7      // 错误代码
######## h8     // 错误代码
######### h9    // 错误代码
########## h10  // 错误代码
```
### 2.分级标题
```
注意: = - 最少可以只写一个，兼容性一般。
一级标题
======================
二级标题
---------------------
```
### 3.生成目录
```
[TOC]
```
### 4.引用
```
单行：
> hello

多行：
> hello Anita
hello Anita
hello Anita
或者
> hello Anita
> hello Anita
> hello Anita

多层嵌套
> aaaaaaaaa
>> bbbbbbbbb
>>> cccccccccc

```
### 5.行内标记
```
标记之外`hello world`标记之外
```
标记之外`hello world`标记之外

### 6.代码快
```
使用 ```包围一段文字即生成一个块
```
```javascript
注：根据不同的语言配置不同的代码着色
var num = 0;
for (var i = 0; i < 5; i++) {
    num+=i;
}
console.log(num);
```

### 7. 插入链接
```
注：{:target="_blank"}跳转方式兼容性一般 ，多数第三方平台不支持跳转
1.内联式
[百度1](http://www.baidu.com/" 百度一下"){:target="_blank"} 

2.引用时
[百度2][2]{:target="_blank"}
[2]: http://www.baidu.com/   "百度二下"
```

[百度1](https://www.baidu.com/" 百度一下"){:target="_blank"} 

[百度2][2]{:target="_blank"}
[2]: https://www.baidu.com/   "百度二下"

[baidu](https://www.baidu.com/)

### 8. 插如图片
```
1. 内联式
![](https://www.zybuluo.com/static/img/logo.png '描述')

2.引用式
![name][01]
[01]:https://www.zybuluo.com/static/img/logo.png '描述'

3.插入的图片带有链接
[![](https://www.zybuluo.com/static/img/logo.png '百度')](http://www.baidu.com){:target="_blank"}   

[![](https://www.zybuluo.com/static/img/logo.png '百度')][5]{:target="_blank"}                       
[5]: http://www.baidu.com
```
![](https://www.zybuluo.com/static/img/logo.png '描述')

### 9. 视频插入
```
注：Markdown 语法是不支持直接插入视频的
普遍的做法是 插入HTML的 iframe 框架，通过网站自带的分享功能获取，如果没有可以尝试第二种方法
第二是伪造播放界面，实质是插入视频图片，然后通过点击跳转到相关页面

多数第三方平台不支持插入<iframe>视频

<iframe height=498 width=510 src='http://player.youku.com/embed/XMjgzNzM0NTYxNg==' frameborder=0 'allowfullscreen'></iframe>
[![](https://www.zybuluo.com/static/img/logo.png)](http://v.youku.com/v_show/id_XMjgzNzM0NTYxNg==.html?spm=a2htv.20009910.contentHolderUnit2.A&from=y1.3-tv-grid-1007-9910.86804.1-2#paction){:target="_blank"}

```
图片跳转相关链接：
[![](https://www.zybuluo.com/static/img/logo.png)](http://v.youku.com/v_show/id_XMjgzNzM0NTYxNg==.html?spm=a2htv.20009910.contentHolderUnit2.A&from=y1.3-tv-grid-1007-9910.86804.1-2#paction){:target="_blank"}


### 10.序表
```
注：. 后加空格
有序：
1. one
2. two
3. three

无序：
* one
* two
* three
代码嵌套:
1. one
    1. one-1
    2. two-2
2. two 
    * two-1
    * two-2

嵌套代码块
注：换行+两个Tab
* one

    var a = 10;     // 与上行保持空行并 递进缩进
```
*演示*：
1. one
2. two
3. three

1. one
    1. one-1
    2. two-2
2. two 
    * two-1
    * two-2

* one

        var a = 10
### 11. 任务列表

```
注：要隔开一行
- [x] 选项一
- [ ] 选项二  
- [ ]  [选项3]
```

- [x] 选项一
- [ ] 选项二  
- [ ]  [选项3]

### 12.表情

表情地址：https://www.cnblogs.com/chenych/p/8623353.html

:bowtie:

:sunny:

### 13.表格
```
注： : 代表对齐方式 ,** : 与 | 之间不要有空格**，否则对齐会有些不兼容
|    a    |       b       |      c     |
|:-------:|:------------- | ----------:|
|   居中  |     左对齐    |   右对齐   |
|=========|===============|============|

简写：
a  | b | c  
:-:|:- |-:
    居中    |     左对齐      |   右对齐    
============|=================|=============

```
|    a    |       b       |      c     |
|:-------:|:------------- | ----------:|
|   居中  |     左对齐    |   右对齐   |
|=========|===============|============|

### 14.支持内嵌CSS样式
```
<p style="color: #AD5D0F;font-size: 30px; font-family: '宋体';">内联样式</p>
```

### 15.语义标记
```
*斜体*
_斜体_
**加粗**
***加粗+斜体***
**_加粗+斜体_**
~~删除线~~
```

### 16.语义标签
```
斜体	<i>斜体</i>	     <i>斜体</i>
加粗	<b>加粗</b>	     <b>加粗</b>
强调	<em>强调</em>	 <em>强调</em>
上标	Za	             Z<sup>a</sup>
下标	Za	             Z<sub>a</sub>
键盘文本	             <kbd>Ctrl</kbd>
```
### 17. <pre>

### 18.公式
```
注：1个$左对齐，2个居中
$$ x \href{why-equal.html}{=} y^2 + 1 $$
$ x = {-b \pm \sqrt{b^2-4ac} \over 2a}. $
```
$$ x \href{why-equal.html}{=} y^2 + 1 $$
$ x = {-b \pm \sqrt{b^2-4ac} \over 2a}. $

### 19.分隔符

```
注：最少三个 --- 或 ***或 * * *
***
---
* * *
```

### 20.脚注

```
Markdown[^1]
[^1]: Markdown是一种纯文本标记语言        // 在文章最后面显示脚注

```
### 21.锚点
```
注：只有标题支持锚点， 跳转目录方括号后 保持空格
[公式标题锚点](#1)

### [需要跳转的目录] {#1}    // 方括号后保持空格

```

### 22.自动邮箱链接
```
<xxx@outlook.com>
```
<1031381547@qq.com>

### 23.流程图
### 24.时序图
### 25.生成侧边栏扩展

```

```
