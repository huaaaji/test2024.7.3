[TOC]

# 学习Markdown

2024.6.30
是乃一注脚（注释）示例[^1]

## 基本语法

### 标题

标题可通过`#`进行标记，通过文本下方添加`=`或`-`同样可以分别创建1级、2级标题；
标题的HTML表示如：`<h1>Heading level 1</h1>`

***

### 段落

要创建段落，请使用空白行将一行或多行文本进行分隔。
>I really like using Markdown.

> <p> I think I'll use it to format all of my documents from now on.</p>
由于markdown中，不以空行间隔而单纯以enter回车而分开的两行不会被视为两个段落，即这种情况下似乎创建了一个软回车。且这种换行也可以通过`<p>`与`</p>`标记段落来实现。
不得以空格及制表键来缩进段落。

***

### 换行

几乎每个 Markdown 应用程序都支持两个或多个空格进行换行，称为 结尾空格（trailing whitespace) 的方式，但这是有争议的，因为很难在编辑器中直接看到空格，并且很多人在每个句子后面都会有意或无意地添加两个空格。
此外，markdown另有换行方式：HTML 的`<br>` 标签。

为了兼容性，请在行尾添加“结尾空格”或 HTML 的 `<br>` 标签来实现换行。

至少在VScode里，经测试，单纯使用回车实现的换行，可以正确显示，但在HTML中，换行位置未有任何标识，也非新段落。但使用结尾空格实现的换行，在HTML中会创建一个`</br>`。

***

### 强调语法

#### **粗体**

可通过在内容前后添加`**`或`__`来实现，HTML表示为`<strong>`与`</strong>`
并注意在单词或短语之中使用粗体合法the**bold**word。
Markdown 应用程序在如何处理单词或短语中间的下划线上并不一致。为兼容考虑，在单词或短语中间部分加粗的话，请使用星号（asterisks）。
若是有括号与`**`配合使用，则似乎可能有一些错误.

markdown处理`_`与`*`的逻辑似乎不同

#### *斜体*

要用斜体显示文本，请在单词或短语前后添加一个星号（asterisk）或下划线（underscore）。要斜体突出单词的中间部分，请在字母前后各添加一个星号，中间不要带空格。
斜体在HTML中表示为`<em>`与`</em>`

#### 同时使用

要同时用粗体和斜体突出显示文本，则在单词或短语的前后各添加三个星号或下划线。
要加粗并用斜体显示单词或短语的中间部分，则在要突出显示的部分前后各添加三个星号，中间不要带空格。

***

### 引用

于句首使用`>`可创建引用
块引用可以包含多个段落，而只需为段落之间的空白行添加一个 `>` 符号。
块引用可以嵌套。即嵌套使用多个`>`

块引用可以包含其他 Markdown 格式的元素。并非所有元素都可以使用

***

### 列表

要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。
且列表可以嵌套
其HTML表示：

    <ol>
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
    <li>Fourth item</li>
    </ol>

要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。
其HTML表示：

    <ul>
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
    <li>Fourth item</li>
    </ul>

要在保留列表连续性的同时在列表中添加另一种元素，请将该元素缩进四个空格或一个制表符，如下例所示：

    *   This is the first list item.
    *   Here's the second list item.

    I need to add another paragraph below the second list item.

    *   And here's the third list item.

代码块通常采用四个空格或一个制表符缩进。当它们被放在列表中时，请将它们缩进八个空格或两个制表符。

***

### 代码

将单词或短语表示为代码需要使用`` ` ``；
若是有需要，在行内内存或短语表示为代码需要使用``` `` ```，如`` `#include <iostream>` ``
若有需要，输入更多连续`` ` ``，需要保证最外层表示代码的`` ` ``数量要大于其中最长连续`` ` ``的数量，并注意空格分隔
HTML表示为`<code>`/`</code>`

欲创建代码块，则需将每一行加以缩进至少一个制表键（四个空格），并注意将第一行空出

    #include <iostream>
    using namespace std;

markdown同样有围栏代码块：
即需以```` ``` ````或`~~~`于代码块前一行和之后一行加以标记，像这样，可以在第一行的```` ``` ````之后标记代码块使用的语言，以使用对于代码的颜色标记，例以：

    ```json
    {
      "firstName": "John",
     "lastName": "Smith",
      "age": 25
    }
    ```
效果如：

``` json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

***

### 分割线

需要在一单独一行上输入三个及以上的`*`或`-`或`_`，表现效果一致
为了兼容性，需要在分割线前后添加空行

***

### Markdown链接语法

#### 链接

超链接语法代码`[超链接显示名](超链接地址 "超链接title")`
HTML表示为`<a href="超链接地址" title="超链接title">超链接显示名</a>`，例以：

 [Markdown语法](https://markdown.com.cn)者，链接也。

链接title是当鼠标悬停在链接上时会出现的文字，其可选，于圆括号中链接地址后，跟链接地址之间以空格分隔。例以：

[Markdown语法](https://markdown.com.cn "最好的markdown教程")者，带链接title之链接也。

使用强调语法修饰一链接，可在链接前后添加星号，以实现强调效果：
*[Markdown语法](https://markdown.com.cn)*
**[Markdown语法](https://markdown.com.cn)**
若是将链接置于代码块之中，需要在`[]`内的超链接显示名左右加以`` ` ``

#### 引用类型链接

其有两部分，其一乃“与文本保持内联”之部分，其二乃“存储在文件中其他位置”之部分

*第一部分*：`[链接显示名][链接标签label]`，两个中括号之间可以有空格
*第二部分*：`[链接标签label]: <URL>"title"`其（指中括号）后至少紧跟一个冒号和至少一个空格。并注意，URL的尖括号可选；且注意，title即链接title，可置于双引号、单引号、括号之中。

#### 网址和email地址

使用尖括号可以很方便地把URL或者email地址变成可点击的链接
[URL者](https://blog.csdn.net/chen1415886044/article/details/103914255)

#### 注意

>不同的 Markdown 应用程序处理URL中间的空格方式不一样。为了兼容性，请尽量使用%20代替空格。

    [link](https://www.example.com/my%20great%20page)

***

### 图片

Markdown语法代码：`![图片alt](图片链接 "图片title")`
图片alt即图片替代文本；图片title可选
HTML表示：`<img src="图片链接" alt="图片alt" title="图片title">`

***

### 转义字符

#### 可转义字符

Character|Name
---|---
\\|backslash
\`|backtick (see also escaping backticks in code)
\*|asterisk
\_|underscore
\{ \}|curly braces
\[ \]|brackets
\( \)|parentheses
\#|pound sign
\+|plus sign
\-|minus sign (hyphen)
\.|dot
\!|exclamation mark
\||pipe (see also escaping pipe in tables)

#### 特殊字符自动转义

在HTML中，字符`<`和`&`需要特殊处理，在HTML中前者用于起始标签，后者用于标记HTML实体，若是表示这两个字符，需要使用实体的形式，即`&lt;`和`&amp;`。
网址中的如此字符同样需要如此表示才能放到链接标签的`href`属性里

然而，Markdown有自动转义功能
若是`&`作为HTML实体的一部分，则其不会被转换，但在其他情况下，其会被自动阀转化为`&amp;`

在 Markdown 的块级元素和内联元素中， `<` 和 `&` 两个符号都会被自动转换成 HTML 实体

***

### Markdown内嵌HTML标签

>如需使用 HTML，不需要额外标注这是 HTML 或是 Markdown，只需 HTML 标签添加到 Markdown 文本中即可

#### 行级内联标签

> HTML 的行级內联标签如 `<span>`、`<cite>`、`<del>` 不受限制，可以在 Markdown 的段落、列表或是标题里任意使用。依照个人习惯，甚至可以不用 Markdown 格式，而采用 HTML 标签来格式化。例如：如果比较喜欢 HTML 的 `<a>` 或 `<img>` 标签，可以直接使用这些标签，而不用 Markdown 提供的链接或是图片语法。当你需要更改元素的属性时（例如为文本指定颜色或更改图像的宽度），使用 HTML 标签更方便些。

>HTML 行级內联标签和区块标签不同，在內联标签的范围内， Markdown 的语法是可以解析的。

    This **word** is bold. This <em>word</em> is italic.
效果如：
This **word** is bold. This <em>word</em> is italic.

#### 区块标签

>区块元素──比如 `<div>`、`<table>`、`<pre>`、`<p>` 等标签，必须在前后加上空行，以便于内容区分。而且这些元素的开始与结尾标签，不可以用 tab 或是空白来缩进。Markdown 会自动识别这区块元素，避免在区块标签前后加上没有必要的 `<p>` 标签。

>例如，在 Markdown 文件里加上一段 HTML 表格：

    This is a regular paragraph.

    <table>
        <tr>
            <td>Foo</td>
        </tr>
    </table>

    This is another regular paragraph.
表示为：
This is a regular paragraph.

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

This is another regular paragraph.

>并注意，Markdown 语法在 HTML 区块标签（块级标签）中将不会被进行处理。例如，你无法在 HTML 区块内使用 Markdown 形式的`*强调*`。

>对于 HTML 的块级元素 `<div>`、`<table>`、`<pre>` 和 `<p>`，请在其前后使用空行（blank lines）与其它内容进行分隔。尽量不要使用制表符（tabs）或空格（spaces）对 HTML 标签做缩进，否则将影响格式。

***

以上部分内容主要整理于2024.6.30下午与2024.7.1晚

***

## 扩展语法

### Markdown扩展语法可用性

#### 轻量标记语言

***

### Markdown表格

>要添加表，请使用三个或多个连字符`---`创建每列的标题，并使用管道`|`分隔每列。您可以选择在表的任一端添加管道。

    | Syntax      | Description |
    | ----------- | ----------- |
    | Header      | Title       |
    | Paragraph   | Text        |

>Tip: 使用连字符和管道创建表可能很麻烦。为了加快该过程，请尝试使用**Markdown Tables Generator**。使用图形界面构建表，然后将生成的Markdown格式的文本复制到文件中。

>您可以通过在标题行中的连字符的左侧，右侧或两侧添加冒号`:`，将列中的文本对齐到左侧，右侧或中心。

    | Syntax      | Description | Test Text     |
    | :---        |    :----:   |          ---: |
    | Header      | Title       | Here's this   |
    | Paragraph   | Text        | And more      |

>您可以在表格中设置文本格式。例如，您可以添加链接，代码（仅反引号`` ` ``中的单词或短语，而不是代码块）和强调。您不能添加标题，块引用，列表，水平规则，图像或HTML标签。

您可以使用表格的HTML字符代码`&#124;`在表中显示竖线`|`字符。

***

### 注脚

在方括号`[^1]`内添加插入符号和标识符。标识符可以是数字或单词，但不能包含空格或制表符。标识符仅将脚注参考与脚注本身相关联-在输出中，脚注按顺序编号。
在括号内使用另一个插入符号和数字添加脚注，并用冒号和文本`[^1]: My footnote.`。您不必在文档末尾添加脚注。您可以将它们放在除列表，块引号和表之类的其他元素之外的任何位置。

是乃一注脚（注释）示例[^1]

[^1]： 测试

***

### Markdown标题编号

>许多Markdown处理器支持标题的自定义ID - 一些Markdown处理器会自动添加它们。添加自定义ID允许您直接链接到标题并使用CSS对其进行修改。要添加自定义标题ID，请在与标题相同的行上用大括号括起该自定义ID。

`### My Great Heading {#custom-id}`
html:
`<h3 id="custom-id">My Great Heading</h3>`

通过创建带有数字符号（#）和自定义标题ID的[标准链接]((/basic-syntax/links.html)，可以链接到文件中具有自定义ID的标题。

没看懂，暂略

***

### Markdown定义列表

>一些Markdown处理器允许您创建术语及其对应定义的定义列表。要创建定义列表，请在第一行上键入术语。在下一行，键入一个冒号，后跟一个空格和定义。

    First Term
    : This is the definition of the first term.

    Second Term
    : This is one definition of the second term.
    : This is another definition of the second term.
HTML如：

    <dl>
      <dt>First Term</dt>
      <dd>This is the definition of the first term.</dd>
      <dt>Second Term</dt>
      <dd>This is one definition of the second term. </dd>
      <dd>This is another definition of the second term.</dd>
    </dl>
显示效果如：
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.

***

### Markdown删除线

需要在单词前后添加`~~`

***

### Markdown任务列表

需要使用`- [ ]`于列表内容之行之首，并以空格于其后
使用`x`选择任务列表前的复选框，像`- [x]`
例以：
- [ ] test
- [x] test

***

### Markdown使用emoji

可以从有emoji的来源来复制到Markdown里，来源有如[emojipedia](https://emojipedia.org/)

可以使用表情符号简码，以冒号开头和结尾，并于中间输入表情符号名称
`:joy:`即：:joy:

***

### 自动网址链接

Markdown会自动将输入的网址（URL）转换为网址链接，即便没有使用方括号等。为避免自动链接，可以使用代码方式表示之，如`https://cn.bing.com/`

***
至此完成于2024.7.2晚