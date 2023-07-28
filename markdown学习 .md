
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

# RUNOOB Markdown Test
## Hello World!
我展示一级标题
========   

现在我展示二级标题
---- 

# 一级标题
## 二级标题  

这是第一段

这是第二段

*斜体文本*

**粗体文本**

----

~~双波浪表示删除文字的横线~~

<u>这个符号表示下划线</u>


创建脚注格式类似这样 [^1]。

我们需要创建第二个注脚[^2]。



[^1]: 菜鸟教程 -- 学的不仅是技术，更是梦想！！！   
[^2]: 这里应该展示第二个注脚


* 第一项
* 第二项
* 第三项：别忘了添加空格，前面的`*`其实可以换成+和-号

1. 这就直接可以表示有序了
2. 这就是有序了
3. 这里我们展示嵌套操作
    * 这里是第一个嵌套
        * 这里是第二个嵌套


> 这就是传说中的区块，别忘了所有的前面符号后要加入一个空格键
>> 这里展示嵌套操作

`print()`这里用的是反引号，可以表示某个函数或者代码片段

  
```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

```c++
#include  <stdio.h>`
int main(void)`
{
    printf("Hello world\n");
}

```
    

```python
#!/usr/bin/env python3
print("Hello, World!");
```

下面讲解链接地址
[链接名称](链接地址)
或者
<链接地址>
    
* 直接使用链接地址的例子：
这是一个链接 [菜鸟教程](https://www.runoob.com)

* 间接使用链接地址的例子
这个链接用 1 作为网址变量 [Google][3]
这个链接用 runoob 作为网址变量 **[Runoob][4]**
然后在文档的结尾为变量赋值（网址）

[3]: http://www.google.com/
[4]: http://www.runoob.com/


图片使用
![他说](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")

**下面的图片使用，这并非什么特别的深意，不需要过多深究**
当然，你也可以像网址那样对图片网址使用变量
这个链接用 6 作为网址变量 [RUNOOB][6].
然后在文档的结尾为变量赋值（网址）

[6]: http://static.runoob.com/images/runoob-logo.png



**对于表格的使用**
Markdown 制作表格使用 | 来分隔不同的单元格，使用 - 来分隔表头和其他行。

|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |

**对齐方式**

我们可以设置表格的对齐方式：

-: 设置内容和标题栏居右对齐。
:- 设置内容和标题栏居左对齐。
:-: 设置内容和标题栏居中对齐。
实例如下：

| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 居左 | 居右 | 居中 |

**接下来阐述一些高级技巧**

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：\<kbd> \<b> \<i> \<em> \<sup> \<sub> \<br>等 ，如：

使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

转义
Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字符，Markdown 使用反斜杠转义特殊字符：
**文本加粗** 
\*\* 正常显示星号 \*\*


**公式**
Markdown Preview Enhanced 使用 KaTeX 或者 MathJax 来渲染数学表达式。

KaTeX 拥有比 MathJax 更快的性能，但是它却少了很多 MathJax 拥有的特性。你可以查看 KaTeX supported functions/symbols 来了解 KaTeX 支持那些符号和函数。

默认下的分隔符：

\$...\$ 或者 \\(...\\) 中的数学表达式将会在行内显示。
\$\$...$$ 或者 \\[...\\] 或者 ```math 中的数学表达式将会在块内显示。

视频如下
![](https://www.runoob.com/wp-content/uploads/2019/03/0e408954-fda8-11e5-9eb4-562d7c0ca431.gif)

