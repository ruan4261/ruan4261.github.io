---
title: Markdown syntax
date: 2020-10-22 00:00:00
categories: [Tutorials]
tags: [markdown, syntax, document]
---



# Markdown syntax

Markdown（下文中简称为md）是一种纯文本标记语言，你可以将其认为是html的超集。md是纯文本标记语言，相比于html，它更加简易，更加易于人类理解。md有非常多的拓展规范（方言），基本规范文档：RFC7763、RFC7764。  

因为md是html的超集，所以你可以使用任意html标签以补充想要的样式，例如使用`<div style="text-align: center"></div>`标签增添居中效果（部分方言/解析器可能会限制部分html标签及属性的使用）。  
原生md不支持数学表达式及UML图等，你可以通过三方插件实现这些功能，在显示时通过图片或脚本（部分平台支持在线编辑表达式并发布，通过平台依赖脚本进行渲染，坏处是无法转移至其他方言不兼容的平台）的方式插入，本文不作非md语法内容的描述。

***本文所述语法默认兼容GitHub及Cacher，与上述平台不兼容的部分，会给出提示。***

## 目录
* [反转义](#反转义)
* [注释](#注释)
* [标题](#标题)
* [分割线](#分割线)
* [换行方法](#换行方法)
* [字体效果](#字体效果)
* [引用块](#引用块)
* [列表](#列表)
* [选择框](#选择框)
* [超链接](#超链接)
* [图片](#图片)
* [表格](#表格)
* [行内代码及代码块](#行内代码及代码块)

## 反转义
> 反转义标签为`\`，将其置于可被反转义的标签前即可。

可被反转义的标签（即原生会转义的标签）有
```
\
`
*
_
{}
[]
()
#
+
-
.
!
```

## 注释
md中不存在原生注释（markdown是纯文本，居然有人想写注释？？？），但可以以其他方式来代替，代码块内无法进行注释。
1. 使用`<!-- -->`进行注释，因为md是html的超集，并且这种注释可以添加在任何地方，不受限于行头。
2. 使用`<ele style="display: none;"></ele>`进行注释，与第二种类似，不过该种注释会被渲染为DOM元素，而且比第一种麻烦，不推荐使用。

**示例**  
将以下代码块中的内容复制到md文件中，通过preview预览，你将不会看到任何内容。
```markdown
<!-- 第一种注释，可以在任何地方使用 -->
<div style="display: none;">第二种注释，不推荐使用</div>
```

**总结**  
使用`<!-- -->`进行注释。

## 标题
> 标题标签为`#`或`-`或`=`

使用`-`或`=`作为标题标签时，标题会使用上一行的内容，并且当前行不允许出现除空格以外的其他内容。  
作为标题的行不应该与自身的上一行产生关联，因为`-`和`=`只可以作用于自身的上一行，如果有多行内容即失效。
一级标题（h1标签）使用符号`=`，可以使用多个符号。  
二级标题（h2标签）使用符号`-`，可以使用多个符号。

**使用`#`作为标题的示例**
```markdown
# h1  
## h2  
### h3  
#### h4  
##### h5  
###### h6
```
显示如下
# h1
## h2
### h3
#### h4
##### h5
###### h6

**使用`-`或`=`作为标题的示例**
```markdown
一级标题
=
二级标题
-
```
显示如下

一级标题
=
二级标题
-

## 锚点
在md文档中，任何标题等同于锚点，大多解释器将md文档转换为html文档后，标题向元素的转换如下所示，标题自然地包含了一个同名的锚点。  
根据不同解释器的规则，对标题中出现的特殊标签（如字体效果）有不同的转换方法，所以不推荐在标题中使用特殊符号（本文不再赘述，请自行了解）。

```markdown
### 我是一个三级标题
i am h2 element.
--
```
它会变为如下元素
```html
<h3>
  <a id="我是一个三级标题" class="anchor" aria-hidden="true" href="#我是一个三级标题"></a>
  我是一个三级标题
</h3>
<h2>
  <a id="i-am-h2-element" class="anchor" aria-hidden="true" href="#i-am-h2-element"></a>
  i am h2 element.
</h2>
```

**添加自定义的锚点**  
你可以使用html标签在md文档的任何地方添加锚点，在将md文档转换为html时，这些标签不会发生变异。
```markdown
<input hidden id="我就**写一堆**特殊~~符号~~，XD"></input>
```

## 分割线
> 分割线标签为`---`或`***`，`-`或`*`符号数量需大于等于3，分割线两侧和中间允许出现空格。

**示例**
```markdown
***
---
<hr>
```
显示如下

***
---
<hr>

## 换行方法
对于大部分解析器来说，普通的回车换行是不起作用的。  
如下所示，回车仅仅只解析成了一个空格。  
>```markdown
>这是第一行
>这是第二行
>```
>这是第一行
>这是第二行

**如何换行呢？**
1. 在要空行的地方，增加两个空格，再回车进行换行。
2. 使用反斜杠`\`置于行尾。
3. 使用`<br>`标签，暴力换行。
4. 双回车，中间会留下一行空白。

**示例**
```markdown
I. 行尾增加两个空格  
第二行  
II. 使用反斜杠\
第二行  
III. 双回车

~~第二行~~（第三行）
```
I. 行尾增加两个空格  
第二行  
II. 使用反斜杠\
第二行  
III. 双回车

~~第二行~~（第三行）

## 字体效果
### 斜体
使用单个`*`或`_`包裹字体（注意两边不能有空格）。
```markdown
*斜体 字*  
_斜体 字_  
*斜体 字 *  
_斜体 字 _  
```
*斜体 字*  
_斜体 字_  
*斜体 字 *  
_斜体 字 _  

### 加粗
使用两个`*`或`_`包裹字体（注意两边不能有空格）。
```markdown
**加粗 字**  
__加粗 字__  
**加粗 字 **  
__加粗 字 __  
```
**加粗 字**  
__加粗 字__  
**加粗 字 **  
__加粗 字 __  

### 加粗斜体
使用仨个`*`或`_`包裹字体（注意两边不能有空格）。
```markdown
***加粗斜体 字***  
___加粗斜体 字___  
***加粗斜体 字 ***  
___加粗斜体 字 ___  
```
***加粗斜体 字***  
___加粗斜体 字___  
***加粗斜体 字 ***  
___加粗斜体 字 ___  

### 删除线
使用两个`~`包裹字体（注意两边不能有空格）。
```markdown
~~删除 线~~  
~~删除 线 ~~  
```
~~删除 线~~  
~~删除 线 ~~  

**注意: 删除线几乎所有平台支持，但是Cacher平台目前却暂不支持删除线，直接将双波浪号忽略。据其项目面板了解，未来将会支持这一feature。**  

### 下划线
md中不存在原生支持的下划线，你可以通过html标签实现。
```markdown
<u>markdown</u>
```
<u>markdown</u>

## 引用块
在行头使用一个或多个`>`符号来表示一级或多级引用。  
**注意**：在高层引用域返回低层引用域时，必须使用一行空引用，否则无法回到低层引用。

**正确的使用示例**
```markdown
> 1
>> 2
>>> 3
>>
>> 2
>
> 1
```
> 1
> > 2
> >
> > > 3
>
> > 2
>
> 1

## 列表
### 无序列表
Unordered List，也作Bulleted List。  
使用`-`或`+`或`*`表示无序列表，大多解释器会在不同层级列表使用不同样式的标头符号，与你使用的符号并无关联。
```markdown
- a
- b
- + c1
- + c2
- * d1
- * + third
* 两个不同的根列表之间应该会有显著的间隔
```
- a
- b
- + c1
- + c2
- * d1
- * + third
* 两个不同的根列表之间应该会有显著的间隔

### 有序列表
Ordered List，也作Numbered List。  
有序列表使用一个数值加小数点`.`表示，并且它与实际内容之间需要有空格占位。  
你无需对他进行严格的排序，你所标记的列序号对于大多解析器来说是没有意义的。
```markdown
0. 第一
0. 第二
999. 解析器会自行标记有序列表的序号，而不会根据你的序号进行标记。
```
0. 第一
0. 第二
999. 解析器会自行标记有序列表的序号，而不会根据你的序号进行标记。

### 列表通用操作
**列表嵌套** 及 **单列跨行**  
**列表嵌套**：列表可以进行层叠嵌套，与引用块类似。  
**单列跨行**：在第二行另起，并保持与前一行相同的缩进，即可以实现跨行。你需要注意，列表的行内部纯文本跨行需要遵循md的换行规则，一般情况下，单列跨行仅用于实现列表行内显示多行代码块等一些必要的跨行功能。
```markdown
0. 一
   \```
   此处有两个反斜杠转义用于防止代码块被截断，请不要在意。
   \```
0. * 第二层1
   * - 第三层1
     - 第三层2
   + 第二层2
0. 三
```
0. 一
   ```
   此处没有使用两个反斜杠，请不用在意这段话，你只需要知道这和上述代码块中一样就可以了。
   ```
0. * 第二层1
   * - 第三层1
     - 第三层2
   + 第二层2
0. 三

## 选择框
选择框一般用于与列表结合，作为Task List任务列表进行进度管理。  
选择框使用两个中括号加一个占位符表示，在未被选择和已被选择两种情况下，中括号的内部都需要有且仅有一个字符进行占位，占位符必须是空格或者英文字母`x`（一般不分大小写）。  
未被选择的选择框书写为`[ ]`，被选择的选择框书写为`[x]`。

**示例**
```markdown
- [x] 写代码
- [ ] 写文档
- [x] debug
```
- [x] 写代码
- [ ] 写文档
- [x] debug

## 超链接
### 普通模式
在md中，普通超链接使用`[]()`表示，中括号内表示超链接显示内容，小括号内表示超链接定位。  
小括号内的最后，可以使用引号（双引号和单引号都可以）标注超链接的Title，它是可以忽略的。

**示例**
```markdown
- [占位模式](#占位模式 '占位模式title')
- [脚注模式](#脚注模式 "脚注模式title")
```
- [占位模式](#占位模式 '占位模式title')
- [脚注模式](#脚注模式 "脚注模式title")

### 占位模式
> **显示内容**：超链接显示的内容。  
> **占位符**：自定义的内容，不会显示，用于文本替换。

占位模式的超链接使用一对或两对中括号`[]`表示。  
在一对中括号的情况下，括号内的内容是**显示内容**，同时也是**占位符**。  
在两对中括号的情况下，第一对括号内的内容是**显示内容**，第二对括号内的内容是**占位符**。

**占位符的使用方式**  
在md文档中的任意一处可声明占位符，它必须是独立行。  
语法如下。
```markdown
[占位符]: 超链接定位 'title'
```
**注意**：占位符不推荐使用除`-`,`_`以外的特殊字符，当前并不是不能使用，比如你使用了`^`作为占位符开头，他会在很多平台上被解释为脚注。

**示例**
```markdown
这是我的[GitHub][my_GitHub]，哦，还有我的[Gist]

[my_GitHub]: https://github.com/ruan4261 'GayHub'
[Gist]: https://gist.github.com/ruan4261 "my Gist"
```
这是我的[GitHub][my_GitHub]，哦，还有我的[Gist]

[my_GitHub]: https://github.com/ruan4261 "GayHub"
[Gist]: https://gist.github.com/ruan4261 "my Gist"

### 脚注模式
> 脚注模式是占位符模式的拓展  
> **GitHub不支持脚注模式（所以谨慎使用这种方式进行脚注）**  
> 但这个脚注超链接在写博客的时候非常方便，对其支持的平台有Cacher，国内的支持平台有知乎、简书等（其余大部分平台我都没试过，感兴趣可以自己试一试）。

脚注模式的超链接使用`[^占位符]`进行占位，他会显示为一个链接向脚注锚点的上标文本，所有的脚注都作为锚点显示在整个md文档的最下方。
对于脚注的占位符关键字，你可以取任意名称，不过在显示的时候，大多解释器会将其变化为序号。

**示例**（请到文档最下方查看脚注，前提是解析器支持，所以你在GitHub上是无法查看这一部分的实际效果的）
~~~markdown
Markdown[^1] is a lightweight markup language[^example] with plain-text-formatting syntax, created in 2004 by John Gruber[^john] and Aaron Swartz[^aaron]. Markdown is often used for formatting readme files, for writing messages in online discussion forums, and to create rich text using a plain text editor.

[^1]:[Markdown](https://wikipedia.org/wiki/Markdown)
[^example]:[Lightweight markup language](https://wikipedia.org/wiki/Lightweight_markup_language)
[^john]:[John Gruber](https://wikipedia.org/wiki/John_Gruber)
[^aaron]:[Aaron Swartz](https://wikipedia.org/wiki/Aaron_Swartz)
~~~

Markdown[^1] is a lightweight markup language[^example] with plain-text-formatting syntax, created in 2004 by John Gruber[^john] and Aaron Swartz[^aaron]. Markdown is often used for formatting readme files, for writing messages in online discussion forums, and to create rich text using a plain text editor.

***我的下方应该是下一个章节，如果此处显示了脚注信息，很遗憾当前解析器不支持脚注。***

[^1]:[Markdown](https://wikipedia.org/wiki/Markdown)
[^example]:[Lightweight markup language](https://wikipedia.org/wiki/Lightweight_markup_language)
[^john]:[John Gruber](https://wikipedia.org/wiki/John_Gruber)
[^aaron]:[Aaron Swartz](https://wikipedia.org/wiki/Aaron_Swartz)

## 图片
图片使用`!`加上图片的超链接表示，用法与超链接非常相似。  
Alt属性书写在超链接的显示内容中；Title书写在超链接的括号内的最后，用引号修饰（双引号和单引号都可以）。

**示例**
```markdown
![GitHub Logo](https://github.githubassets.com/favicons/favicon.svg 'Logo Title')
```
![GitHub Logo](https://github.githubassets.com/favicons/favicon.svg 'Logo Title')

如果你不需要Alt和Title属性，这样写`![](https://github.githubassets.com/favicons/favicon.svg)`  
图片也支持使用占位模式，使用方法和超链接完全一致，不再赘述。

### 图片超链接
你可以使用图片作为超链接，只要将图片作为超链接的显示内容即可，如下所示。
```markdown
[![Link](https://github.githubassets.com/favicons/favicon.svg)](https://github.githubassets.com/favicons/favicon.svg 'GitHub')
```
[![Link](https://github.githubassets.com/favicons/favicon.svg)](https://github.githubassets.com/favicons/favicon.svg 'GitHub')

## 表格
表格主要使用符号`|`构成。  
表格的第一行用于定义列，表格的两侧可以增加`|`，也可以省略。  

第二行用于分割表格的header和body，以及设置列的对齐方式。  
第二行的每一列都应该使用三个或以上的`-`符号进行占位，并且每个`-`符号之间不能含有空格，但是在两侧`-`和`|`之间可以含有空格。  
第二行中可以使用半角冒号`:`设置每一列的对其方式，冒号只可以加在连续的`-`符号的两侧，`:`和`-`符号之间不能含有空格，`:`和`|`符号之间可以含有空格。  
冒号加在左侧（`|:---|`）表示相左对齐，加在右侧（`|---:|`）表示向右对齐，两侧都加冒号（`|:---:|`）代表居中。

**示例**
```markdown
姓名|班级|成绩(Score)
---|---|:---:
李四|ClassA|25
张三|ClassC|59
```
姓名|班级|成绩(Score)
---|---|:---:
李四|ClassA|25
张三|ClassC|59

**注意**：少部分解析器不支持使用冒号进行对齐，如Cacher（GitHub及绝大部分平台是支持对齐的）。你可以放心使用这个功能，因为他不会影响表格的原样式。

## 行内代码块及跨行代码块
### 行内代码块
行内代码使用一对``` ` ```（重音符）号（`一`个或三个重音符都可以表示行内代码）表示。举个栗子，我们现在需要在行内使用行内代码块高亮显示 markdown 这个单词。
```markdown
行内代码块使用``` ` ```号表示（此处使用三个重音符，否则无法显示内部的单个重音符），如`markdown`
```
**显示如下**  
行内代码块使用``` ` ```号表示（此处使用三个重音符，否则无法显示内部的单个重音符），如`markdown`

### 跨行代码块
代码块使用一对3个连续的``` ` ```号或`~`号表示，代码块可以写在同一行代替行内代码（此时不能使用波浪号）。

**示例**  
~~~markdown
```
在这里书写你的代码
```
```写在一行也是可以的```
~~~
显示如下
```
在这里书写你的代码
```
```写在一行也是可以的```

**示例2**

```markdown
~~~
也可以在这里书写你的代码
~~~
```
显示如下
~~~
也可以在这里书写你的代码
~~~

你可以为代码块指定语言，它紧跟在前三个符号的后面，就像下面这样。

~~~markdown
```java
class Solution {
  void main(String[] args){}
}
```
~~~
```markdown
~~~html
<div>
  <a>鲁迅说过，这不是我说的</a>
</div>
~~~
```

## The End
以下是脚注（若解析器支持）