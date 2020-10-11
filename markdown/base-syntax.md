# Markdown基本语法

## 起源

John Gruber 在2004年创建了Markdown，并与Aaron Swartz合作定义了语法。目标是为了创建一种易读且易写的纯文本格式，并可以转换成XHTML或HTML。


## 语法

此语法翻译自[官方文档][markdown-official-manual] ，英语比较好的可以直接跳转到此网站来学习。

    [markdown-official-manual]: https://daringfireball.net/projects/markdown/syntax "Markdown官方文档"

### 概览

#### 哲学

Markdown旨在尽可能地易于阅读和编写。

但是，首先要强调可读性。Markdown格式的文档应以纯文本形式原样发布，而不会看起来像被标签或格式说明所标记。虽然Markdown的语法受到了几种现有的文本到HTML过滤器的影响，包括Setext，atx，Textile，reStructuredText， Grutatext和EtText  ，但Markdown语法的最大灵感来源就是纯文本电子邮件的格式。

为此，Markdown的语法完全由标点符号组成，这些标点符号经过精心选择，以使其看起来像它们的含义。例如，单词周围的星号实际上看起来像*强调*。Markdown列表看起来很像列表。假设您曾经使用过电子邮件，即使是块引用也看起来像是引用的文本段落。

  [1]: http://docutils.sourceforge.net/mirror/setext.html
  [2]: http://www.aaronsw.com/2002/atx/
  [3]: http://textism.com/tools/textile/
  [4]: http://docutils.sourceforge.net/rst.html
  [5]: http://www.triptico.com/software/grutatxt.html
  [6]: http://ettext.taint.org/doc/

#### 内联HTML

Markdown的语法仅用于一个目的: 用作*编写*web页面的格式。

Markdown 不是HTML的替代品，也不会替掉HTML。它的语法非常精简, 对应于HTML标签非常小的子集。 这个想法不是要创建一种使插入HTML标签更容易的语法。HTML标签已经很容易插入了。Markdown的想法是使其易于阅读，编写和编辑文章。HTML*发布的* 格式; Markdown是*编写的*
格式. 因此, Markdown的格式语法仅解决以纯文本形式传达的问题。

对于Markdown语法未涵盖的标记，您只需使用HTML本身的就可以了。 无需在其前添加或定界以表明您已从Markdown切换为HTML；您只需要使用标签即可。

唯一的限制是块级HTML元素-例如`<div>`,
`<table>`, `<pre>`, `<p>`等-必须在前后用空行分离，并且该块的开始和结束标签不应用制表符或空格缩进。 Markdown非常聪明，不会在HTML块级标签周围添加额外的（不需要的）`<p>`标签。

例如，要将HTML表格添加到Markdown文章中：

    This is a regular paragraph.

    <table>
        <tr>
            <td>Foo</td>
        </tr>
    </table>

    This is another regular paragraph.

请注意，Markdown格式语法不会在块级HTML标签中被解析。例如，您不能在HTML块内使用Markdown样式*emphasis*。

HTML行内标签（例如`<span>`，`<cite>`或`<del>` ）可以在Markdown段落，列表项或标题中的任何位置使用。如果需要，甚至可以使用HTML标签替换Markdown格式。例如，如果您希望使用HTML`<a>`或`<img>`标签而不是Markdown的链接或图像语法。

#### 自动转义特殊字符

在HTML中，有两个字符需要特殊处理: `<`和 `&`. 左尖括号用于开始标签; “与”号表示HTML实体。如果要将它们用作文字字符，则必须将它们作为实体转义，例如`&lt;`和 `&amp;`。


＆符出现的频率比较高。 如果要写“ AT＆T”， 你需要写成 '`AT&amp;T`'. 您甚至需要转义URL中的“＆”号。因此，如果您想链接到:

    http://images.google.com/images?num=30&q=larry+bird

您需要将URL编码为：

    http://images.google.com/images?num=30&amp;q=larry+bird

Markdown允许您正常地使用这些字符，并为您进行所有必要的转义。如果将与号用作HTML实体的一部分，则它保持不变。否则将被翻译成`&amp;`。

因此，如果您想在文章中包含版权符号，可以编写：

    &copy;

Markdown将不理会它。但是，如果您写：

    AT&T

Markdown会将其转换为：

    AT&amp;T

同样，由于Markdown支持 [内联HTML](#html), 如果您将尖括号用作HTML标签的定界符，则Markdown会将它们视为此类。但是，如果您写：

    4 < 5

Markdown会将其转换为：

    4 &lt; 5

但是，在Markdown代码内部，尖括号和与号始终自动进行编码。这使得使用Markdown编写HTML代码变得容易。

* * *

### 块元素

#### 段落和换行符

段落是一个或多个连续的文本行，由一个或多个空行分隔。（空行是看起来像空行的任何行，仅包含空格或制表符的行被视为空白。）普通段落不应以空格或制表符缩进。

当您确实想使用Markdown插入`<br />`标记时，请以两个或多个空格结束一行，然后键入return。

是的，这需要花费更多的精力来创建`<br />`，但是简单的“每条换行符是一个`<br />`”规则对Markdown不起作用。Markdown的电子邮件样式的[块引用][bq]和多段落[列表项][l] 在经过艰苦的格式化后，效果最佳，并且外观更好。

  [bq]: #blockquote
  [l]:  #list


#### 标题

Markdown 支持两种样式的标题, [Setext][1] 和 [atx][2].

Setext样式的标题使用等号（一级标题）和破折号（二级标题）“加下划线”。例如：

    This is an H1
    =============

    This is an H2
    -------------

任何数量的下划线 `=`或者`-`都可以。

Atx样式的标题在行的开头使用1-6个哈希字符，对应于标题级别1-6。例如：

    # This is an H1

    ## This is an H2

    ###### This is an H6

（可选）您可以“结束” atx样式的标题。这纯粹是装饰性的-如果您认为它看起来更好，则可以使用它。结束的哈希字符甚至数量上不需要跟打开的哈希字符一致。（打开的哈希字符数量的数量确定标题的级别。）：

    # This is an H1 #

    ## This is an H2 ##

    ### This is an H3 ######

#### 块引用

Markdown使用电子邮件样式的`>`字符进行块引用。如果您熟悉在电子邮件中引用文本段落的内容，那么您将知道如何在Markdown中创建块引用。如果将文本用硬包装并在每行行首写一个`>`，则看起来最好：

    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    > consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    > Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
    > 
    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    > id sem consectetuer libero luctus adipiscing.

Markdown可以让您变得懒惰，并且只在硬包装段落的第一行行首放置`>`：

    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    id sem consectetuer libero luctus adipiscing.

可以通过再添加`>`字符来嵌套块引用：

    > 这是第一层块引用。
    >
    > > 这是嵌套的块引用。
    >
    > 返回第一层块引用。

块引用可以包含其他Markdown元素，包括标题，列表和代码块：

	> ## 这是一个标题
	> 
	> 1.   This is the first list item.
	> 2.   This is the second list item.
	> 
	> Here's some example code:
	> 
	>     return shell_exec("echo $input | $markdown_script");

#### 列表

Markdown supports ordered (numbered) and unordered (bulleted) lists.

Unordered lists use asterisks, pluses, and hyphens -- interchangably
-- as list markers:

    *   Red
    *   Green
    *   Blue

is equivalent to:

    +   Red
    +   Green
    +   Blue

and:

    -   Red
    -   Green
    -   Blue

Ordered lists use numbers followed by periods:

    1.  Bird
    2.  McHale
    3.  Parish

It's important to note that the actual numbers you use to mark the
list have no effect on the HTML output Markdown produces. The HTML
Markdown produces from the above list is:

    <ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
    </ol>

If you instead wrote the list in Markdown like this:

    1.  Bird
    1.  McHale
    1.  Parish

or even:

    3. Bird
    1. McHale
    8. Parish

you'd get the exact same HTML output. The point is, if you want to,
you can use ordinal numbers in your ordered Markdown lists, so that
the numbers in your source match the numbers in your published HTML.
But if you want to be lazy, you don't have to.

If you do use lazy list numbering, however, you should still start the
list with the number 1. At some point in the future, Markdown may support
starting ordered lists at an arbitrary number.

List markers typically start at the left margin, but may be indented by
up to three spaces. List markers must be followed by one or more spaces
or a tab.

To make lists look nice, you can wrap items with hanging indents:

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
        Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
        viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.

But if you want to be lazy, you don't have to:

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

If list items are separated by blank lines, Markdown will wrap the
items in `<p>` tags in the HTML output. For example, this input:

    *   Bird
    *   Magic

will turn into:

    <ul>
    <li>Bird</li>
    <li>Magic</li>
    </ul>

But this:

    *   Bird

    *   Magic

will turn into:

    <ul>
    <li><p>Bird</p></li>
    <li><p>Magic</p></li>
    </ul>

List items may consist of multiple paragraphs. Each subsequent
paragraph in a list item must be indented by either 4 spaces
or one tab:

    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.

        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.

    2.  Suspendisse id sem consectetuer libero luctus adipiscing.

It looks nice if you indent every line of the subsequent
paragraphs, but here again, Markdown will allow you to be
lazy:

    *   This is a list item with two paragraphs.

        This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

    *   Another item in the same list.

To put a blockquote within a list item, the blockquote's `>`
delimiters need to be indented:

    *   A list item with a blockquote:

        > This is a blockquote
        > inside a list item.

To put a code block within a list item, the code block needs
to be indented *twice* -- 8 spaces or two tabs:

    *   A list item with a code block:

            <code goes here>


It's worth noting that it's possible to trigger an ordered list by
accident, by writing something like this:

    1986. What a great season.

In other words, a *number-period-space* sequence at the beginning of a
line. To avoid this, you can backslash-escape the period:

    1986\. What a great season.








