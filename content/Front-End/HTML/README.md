<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 目录

* [HTML转译字符](#html转译字符)
* [HTML标签的语义](#html标签的语义)
* [HTML标签列表](#html标签列表)
    * [基础标签](#基础标签)
    * [元信息标签](#元信息标签)
    * [格式标签](#格式标签)
    * [表单标签](#表单标签)
    * [表格标签](#表格标签)
    * [框架标签](#框架标签)
    * [图像标签](#图像标签)
    * [音频/视频标签](#音频视频标签)
    * [链接标签](#链接标签)
    * [样式/节标签](#样式节标签)
    * [编程标签](#编程标签)


# <p align="center" style="border-bottom: 3px solid #e7e7e7;">HTML转译字符</p>

|字符|十进制|转义字符|
|:---|:---|:---|
|"|&amp;#34;|&amp;quot;|
|&|&amp;#38;|&amp;amp;|
|<|&amp;#60;|&amp;lt;|
|>|&amp;#62;|&amp;gt;|
|不断开空格(non-breaking space)|&amp;#160;|&amp;nbsp;|
[>>more](http://tool.oschina.net/commons?type=2)


# <p align="center" style="border-bottom: 3px solid #e7e7e7;">HTML标签的语义</p>

|html标签|英文全称|中文释义|
|:---|:---:|:---:|
|a|anchor|锚|
|abbr|abbreviation|缩写词|
|acronym|acronym|取首字母的缩写词|
|address|address|地址|
|dfn|defines a definition term|定义定义条目|
|kbd|keyboard|键盘（文本）|
|samp|sample|示例（文本）|
|var|variable|变量（文本）|
|tt|teletype|打印机（文本）|
|code|code|源代码（文本）|
|pre|preformatted|预定义格式（文本 ）|
|blockquote|block quotation|区块引用语|
|cite|citation|引用|
|q|quotation|引用语|
|strong|strong|加重（文本）|
|em|emphasized|加重（文本）|
|b|bold|粗体（文本）|
|i|italic|斜体（文本）|
|big|big|变大（文本）|
|small|small|变小（文本）|
|sup|superscripted|上标（文本）|
|sub|subscripted|下标（文本）|
|bdo|direction of text display|文本显示方向|
|br|break|换行|
|center|centered|居中（文本）|
|font|font|字体|
|u|underlined|下划线（文本）|
|s/strike|strikethrough|删除线|
|div|division|分隔|
|span|span|范围|
|ol|ordered list|排序列表|
|ul|unordered list|不排序列表|
|li|list item|列表项目|
|dl|definition list|定义列表|
|dt|definition term|定义术语|
|dd|definition description|定义描述|
|del|deleted|删除（的文本）|
|ins|inserted|插入（的文本）|
|h1~h6|header 1 to header 6|标题1到标题6|
|p|paragraph|段落|
|hr|horizontal rule|水平尺|
|href|hypertext reference|超文本引用|
|alt|alternative|替用（一般是图片显示不出的文本提示）|
|src|source|源文件链接|
|cell|cell|巢|
|cellpadding|cellpadding|巢补白|
|cellspacing|cellspacing|巢空间|
|nl|navigation lists|导航列表|
|tr|table row|表格中的一行|
|th|table header cell|表格中的表头|
|td|table data cell|表格中的一个单元格|
|iframe|inline frame|定义内联框架|
|optgroup|option group|定义选项组|

# <p align="center" style="border-bottom: 3px solid #e7e7e7;">HTML标签列表</p>

### 基础标签

|基础标签|描述|详细说明|
|:---|:---|:---|
|&lt;!DOCTYPE&gt;|定义文档（DOC）类型（TYPE）。DOC就是Document/文件|&lt;!DOCTYPE&gt;声明必须是HTML文档的第一行，位于&lt;html&gt;标签之前。&lt;!DOCTYPE&gt;声明不是HTML标签；它是指示web浏览器关于页面使用哪个HTML版本进行编写的指令。|
|&lt;html&gt;|定义HTML文档。HTML全称为Hyper Text Mark-up Language/超文本标记语言。|此元素可告知浏览器其自身是一个HTML文档。该标签限定了文档的开始点和结束点，在它们之间是文档的头部和主体。文档的头部由&lt;head&gt;标签定义，而主体由&lt;body&gt;标签定义。|
|&lt;title&gt;|定义文档的标题（title）。|浏览器会以特殊的方式来使用标题，并且通常把它放置在浏览器窗口的标题栏或状态栏上。同样，当把文档加入用户的链接列表戒者收藏夹或书签列表时，标题将成为该文档链接的默认名称。&lt;title&gt;标签是&lt;head&gt;标签中唯一要求包含的东西。|
|&lt;body&gt;|定义文档的主体（body）。|客户端能看到的东西属于&lt;body&gt;里面的内容。body元素包含文档的所有内容（比如文本、超链接、图像、表格和列表等等。）|
|&lt;h1&gt; to &lt;h6&gt;|定义HTML标题（head）。|h1表示一级标题，h2表示二级标题，依次类推。请您慎重地选择恰当的标签层级来构建文档的结构。&lt;h1&gt; to &lt;h6&gt;、&lt;head&gt;以及&lt;title&gt;有何区别？|
|&lt;p&gt;|定义段落（Paragraph）。|&lt;p&gt;元素会自动在其前后创建一些空白。浏览器会自动添加这些空间，您也可以在样式表中规定。|
|&lt;br&gt;|定义简单的折行（break）。|break表示间断、打破。只是简单地开始新的一行，当浏览器遇到&lt;p&gt;标签时，通常会在相邻的段落之间插入一些垂直的间距。与&lt;wbr&gt;区别？|
|&lt;hr&gt;|定义水平线（horizontal）。|可在页面中创建一条水平线。|
|&lt;!\-\-...\-\-&gt;|用于在源代码中插入注释（notes）。|注释不会显示在浏览器中。您可使用注释对您的代码进行解释，这样做有助于您在以后的时间对代码的编辑。当您编写了大量代码时尤其有用。使用注释标签来隐藏浏览器不支持的脚本也是一个好习惯（这样就不会把脚本显示为纯文本）。|

### 元信息标签

|元信息标签|描述|详细说明|
|:---|:---|:---|
|&lt;head&gt;|定义文档的头部（head），它是所有头部元素的容器。|&lt;head&gt;中的元素可以引用脚本、指示浏览器在哪里找到样式表、提供元信息等。文档的头部描述了文档的各种属性和信息，包括文档的标题、在Web 中的位置以及和其他文档的关系等。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。下面这些标签可用在head部分：&lt;base&gt;，&lt;link&gt;，&lt;meta&gt;，&lt;script&gt;，&lt;style&gt;以及&lt;title&gt;。&lt;title&gt;定义文档的标题，它是head部分中唯一必需的元素。应该把&lt;head&gt;标签放在文档的开始处，紧跟在&lt;html&gt;后面，并处于&lt;body&gt;标签或&lt;frameset&gt;标签之前。请记住始终为文档规定标题！|
|&lt;meta&gt;|定义关于HTML文档的元信息（meta-information）。|比如针对搜索引擎和更新频度的描述和关键词。&lt;meta&gt;位于文档的头部，不包含任何内容。&lt;meta&gt; 标签的属性定义了与文档相关联的名称/值对。&lt;meta&gt;标签永进位于head元素内部。元数据总是以名称/值的形式被成对传递的。|
|&lt;base&gt;|为页面上的所有链接规定默认地址或默认目标。理解了“相对URL”才能理解这个标签。|通常情况下，浏览器会从当前文档的URL中提取相应的元素来填写相对URL中的空白。使用&lt;base&gt;标签可以改变这一点。浏览器随后将不再使用当前文档的URL，而使用指定的基本URL来解析所有的相对URL。这其中包括&lt;a&gt;、&lt;img&gt;、&lt;link&gt;、&lt;form&gt;标签中的URL。&lt;base&gt;标签必须位于head元素内部。|
|&lt;basefont&gt;|不赞成使用。定义页面中文本的默认字体、颜色或尺寸。|该标签可以为文档中的所有文本定义默认字体颜色、字体大小和字体系列。|


### 格式标签

|格式标签|描述|详细说明|
|:---|:---|:---|
|&lt;acronym&gt;|定义只取首字母的缩写。Acronym['ækrənɪm]。|HTML5中不支持&lt;acronym&gt;。请用&lt;abbr&gt;标签代替。添加title属性可用于在鼠标指针移动到元素上时显示出缩写的完整版本。|
|&lt;abbr&gt;|定义缩写（abbreviation）。|&lt;abbr&gt;表示它所包含的文本是一个更长的单词或短语的缩写形式。通过对缩写进行标记，您能够为浏览器、拼写检查和搜索引擎提供有用的信息。|
|&lt;address&gt;|定义文档作者或拥有者的联系信息。|不应该用于描述通讯地址，除非它是联系信息的一部分。|
|&lt;u&gt;|不赞成使用。定义下划线（underline）文本。|请尽量避免为文本加下划线，用户会把它混淆为一个超链接。|
|&lt;b&gt;|定义粗体（bold）文本。|与&lt;strong&gt;的默认效果一样（&lt;strong&gt;还有其他效果）|
|&lt;strong&gt;|定义语气更为强烈的强调文本（其默认效果是&lt;b&gt;加粗）。|&lt;b&gt;标签是一个实体标签，它所包围的字符将被设为bold（粗体），而&lt;strong&gt;标签是一个逻辑标签，它的作用是加强字符的语气。一般来说，加强字符的语气是通过将字符变为bold（粗体）来实现的。&lt;b&gt;表示的是字体加粗，恰巧跟strong默认情况下强调的效果一致，其实这个strong完全可以定义成别的样式的强调效果（不限于加粗）。|
|&lt;bdi&gt;|定义文本的文本方向，使其脱离其周围文本的方向设置（bidi isolated，隔离）。|允许您设置一段文本，使其脱离其父元素的文本方向设置。在发布用户评论或其他您无法完全控制的内容时，该标签很有用。|
|&lt;bdo&gt;|定义文字方向（bi-directional override，覆盖）。|可覆盖默认的文本方向。|
|&lt;big&gt;|定义大号文本。|注意与&lt;strong&gt;和&lt;bold&gt;的区别。&lt;big&gt;定义的字体比周围的文字要大一号。但是，如果文字已经是最大号字体，这个&lt;big&gt;标签将不起任何作用。|
|&lt;small&gt;|定义小号文本。|和&lt;big&gt;同理，缩小字体。|
|&lt;center&gt;|不赞成使用。定义居中文本。|对其包围的文本进行水平居中处理。HTML5不支持&lt;center&gt;标签，请用CSS代替。在HTML 4.01中，&lt;center&gt;元素已废弃。|
|&lt;cite&gt;|定义引用（Cite）。|通常表示它所包含的文本对某个参考文献的引用，比如书籍或者杂志的标题。按照惯例，引用的文本将以斜体显示。|
|&lt;q&gt;|定义短的引用（quote）。|浏览器经常在引用的内容周围添加引号。&lt;q&gt; 标签在本质上与&lt;blockquote&gt;是一样的。不同之处在于它们的显示和应用。&lt;q&gt;标签用于简短的行内引用。如果需要从周围内容分离出来比较长的部分（通常显示为缩进的块block），请使用&lt;blockquote&gt;标签。|
|&lt;blockquote&gt;|定义长的引用（块引用/blockquote）。|&lt;blockquote&gt;与&lt;/blockquote&gt;之间的所有文本都会从常规文本中分离出来，经常会在左、右两边进行缩进（增加外边距），而且有时会使用斜体。也就是说，块引用拥有它们自己的空间。|
|&lt;code&gt;|定义计算机代码文本。|包含在该标签内的文本将用等宽、类似电传打字机样式的字体（Courier）显示出来。|
|&lt;del&gt;|定义文档中被删除（delete）文本。|请与&lt;ins&gt;标签配合使用，来描述文档中的更新和修正。电脑键盘上也有这个Delete键。|
|&lt;ins&gt;|定义文档中被插入（insert）文本。|请与&lt;del&gt;一同使用，来描述文档中的更新和修正。|
|&lt;dfn&gt;|定义定义（definition）项目。|标记对特殊术语或短语的定义。现在流行的浏览器通常用斜体来显示&lt;dfn&gt;中的文本。将来，&lt;dfn&gt;还可能有劣于创建文档的索引或术语表。|
|&lt;em&gt;|定义强调（emphasis）文本（其默认形式为斜体，与&lt;i&gt;相同）。|标签告诉浏览器把其中的文本表示为强调的内容。对于所有浏览器来说，这意味着要把这段文字用斜体来显示。如果你只想使用斜体字来显示文本的话，请使用 &lt;i&gt; 标签。|
|&lt;i&gt;|定义斜体（italic）文本。|&lt;b&gt;和&lt;i&gt;仅仅表示“这里应该用粗体显示”或者“这里应该用斜体显示”。而&lt;strong&gt;和&lt;em&gt;的默认形式是&lt;b&gt;和&lt;i&gt;，除此之外，还有其他强调形式。|
|&lt;font&gt;|不赞成使用。定义文本的字体（font）、尺寸和颜色。|请使用样式css（代替&lt;font&gt;）来定义文本的字体、字体颜色、字体尺寸。|
|&lt;kbd&gt;|定义键盘（keyboard）文本。|用来表示文本是从键盘上键入的。该标签经常用在于计算机相关的文档和手册中。如：键入&lt;kbd&gt;quit&lt;/kbd&gt; 退出程序，或者键入&lt;kbd&gt;menu&lt;/kbd&gt; 返回主菜单。|
|&lt;mark&gt;|定义有记号的（mark）文本。|&lt;mark&gt;标签是HTML5中的新标签。请在需要突出显示文本时（如高亮）使用。|
|&lt;meter&gt;|定义度量衡（meter）。|&lt;meter&gt;标签是HTML5中的新标签。Meter米，简称M；厘米Centimeter（CM）。必须定义度量的范围，既可以在元素的文本中，也可以在min/max属性中定义。|
|&lt;pre&gt;|定义预格式（preformat）文本。|被包围在&lt;pre&gt;元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。&lt;pre&gt;标签的一个常见应用就是用来表示计算机的源代码。|
|&lt;progress&gt;|定义任何类型的运行中的任务的进度或进程（progress）。|&lt;progress&gt;标签是HTML5中的新标签。请使用&lt;progress&gt;标签来显示下载的进度。可以使用&lt;progress&gt;标签来显示JavaScript中耗费时间的函数的进度。|
|&lt;rp&gt;|定义若浏览器不支持ruby元素显示的内容。|&lt;rp&gt;标签是HTML5的新标签。在ruby注释中使用，以定义不支持ruby元素的浏览器所显示的内容。ruby是一种脚本语言。|
|&lt;rt&gt;|定义ruby注释的解释。|&lt;rt&gt;标签定义字符（中文注音或字符）的解释或发音。ruby元素由一个或多个字符（需要一个解释/发音）和一个提供该信息的rt元素组成，还包括可选的rp元素，定义当浏览器不支持"ruby"元素时显示的内容。|
|&lt;ruby&gt;|定义ruby注释（中文注音或字符）。|&lt;ruby&gt; 标签是HTML5的新标签。支持"ruby"元素的浏览器不会显示"rp"元素的内容。|
|&lt;samp&gt;|定义计算机代码样本（sample）。|&lt;samp&gt; 标签并不经常使用。只有在要从正常的上下文中将某些短字符序列提取出来，对它们加以强调的极少情况下，才使用这个标签。|
|&lt;strike&gt;|不赞成使用。定义加删除线的（strikethrough）文本。|请使用&lt;del&gt;替代&lt;strike&gt;。|
|&lt;s&gt;|不赞成使用。定义加删除线的（strikethrough）文本。|请使用&lt;del&gt;替代&lt;s&gt;。&lt;s&gt;和&lt;strike&gt;没啥区别。|
|&lt;sup&gt;|定义上标（superior）文本。|包含在此标签中的内容将会以当前文本流中字符高度的一半来显示，但是与当前文本流中文字的字体和字号都是一样的。这个标签在向文档添加脚注以及表示方程式中的指数值时非常有用。如果和&lt;a&gt;标签结合起来使用，就可以创建出很好的超链接脚注。
|&lt;sub&gt;|定义下标（subscript）文本。|无论是&lt;sub&gt;标签还是和它对应的&lt;sup&gt;标签，在数学等式、科学符号和化学公式中都非常有用。|
|&lt;time&gt;|标签定义日期或时间，或者两者。|&lt;time&gt;标签是HTML5中的新标签。|
|&lt;tt&gt;|呈现类似打字机或者等宽的文本（Teletype text）效果。|&lt;tt&gt;标签与&lt;code&gt;和&lt;kbd&gt;标签一样，要把其中包含的文本显示为等宽字体。对于那些已经使用了等宽字体的浏览器来说，这个标签在文本的显示上就没有什么特殊效果了。|
|&lt;var&gt;|表示变量（variable）的名称，或者由用户提供的值。|这个标签经常与&lt;code&gt;和&lt;pre&gt;标签一起使用，用来显示计算机编程代码范例及类似方面的特定元素。用&lt;var&gt;标签标记的文本通常显示为斜体。
|&lt;wbr&gt;|定义可能的换行符（word break）。|用来指定软换行（或单词换行）。即使用&lt;nobr&gt;禁止了换行，使用&lt;wbr&gt;仍然可以换行，但是又不是强制换行，这点和&lt;br&gt;不一样。换不换行要看浏览器的横幅。例如：像“北京市海淀区黄浦区”这种表示地址的语句，允许在“北京市”和“海淀区”的中间换行，但不允许在“北京市海”和“淀区”的中间换行，那就要这样写：&lt;nobr&gt;北京市&lt;wbr&gt;海淀区&lt;/nobr&gt;。另外，像URL这种不含空格的全是半角英文数字的语句，通常在浏览器里显示的时候，会保持它的完整性。|


### 表单标签

|表单标签|描述|详细说明|
|:---|:---|:---|
|&lt;form&gt;|定义供用户输入的HTML表单（form）。|form元素是块级元素，其前后会产生折行。表单能够包含input元素，比如文本字段、复选框、单选框、提交按钮等。表单还可以包含menus、textarea、fieldset、legend和label元素。表单用于向服务器传输数据。注意表单不表格的区别。|
|&lt;input&gt;|定义输入（input）控件。注意与插入（insert）的区别。|&lt;input&gt;标签用于搜集用户信息。根据不同的type属性值，输入字段拥有很多种形式。输入字段可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等。|
|&lt;output&gt;|定义不同类型的输出（output），比如脚本的输出。|&lt;output&gt;标签是HTML5中的新标签。|
|&lt;textarea&gt;|定义多行的文本（textarea）输入控件。|文本区中可容纳无限数量的文本，文本的默认字体是等宽字体（通常是Courier）。可以通过cols和rows属性来规定textarea的尺寸，不过更好的办法是使用CSS的height和width属性。|
|&lt;button&gt;|定义按钮（button）。|如果在HTML表单中使用button元素，不同的浏览器会提交不同的按钮值。请使用input元素在HTML表单中创建按钮。|
|&lt;datalist&gt;|定义下拉列表（list）。|请与input元素配合使用该元素，来定义input可能的值。datalist及其选项不会被显示出来，它仅仅是合法的输入值列表。|
|&lt;select&gt;|定义选择（select）列表。|可创建单选或多选菜单。select元素是一种表单控件，可用于在表单中接受用户输入。|
|&lt;option&gt;|定义下拉列表中的一个选项/条目（option）。|option元素位于select元素内部。请不select元素配合使用此标签，否则这个标签是没有意义的。如果列表选项很多，可以使用&lt;optgroup&gt;标签对相关选项进行组合。|
|&lt;optgroup&gt;|定义选择列表中相关选项的组合（option group）。|当您使用一个长的选项列表时，对相关的选项进行组合会使处理更加容易。
|&lt;label&gt;|为input元素定义标注或标记（label）。|"for"属性可把label绑定到另外一个元素。请把"for"属性的值设置为相关元素的id属性的值。|
|&lt;fieldset&gt;|定义（围绕表单中元素的）边框（field）。|fieldset元素可将表单内的相关元素分组。|
|&lt;legend&gt;|为fieldset元素定义标题（caption）。|legend元素为fieldset元素定义标题（caption）。|
|&lt;isindex&gt;|定义与文档相关的可搜索索引（index）。|不赞成使用。|
|&lt;keygen&gt;|定义生成（generate）密钥（key）。|当提交表单时，私钥存储在本地，公钥发送到服务器。|

### 表格标签

|表格标签|描述|详细说明|
|:---|:---|:---|
|&lt;table&gt;|定义表格（table）。注意与表单（form）的区别。|表格table用于布局，表单form用于传输数据（用来提交到下一页，如登录、注册）。用表格来布局表单里面的数据。如果你有数据提供给后台程序，比如一个输入框，文本框等，这些元素通常要放到一个表单里，这样才可以完成数据的提交。|
|&lt;caption&gt;|定义表格标题（caption）。|caption标签必须紧随table标签之后。您只能对每个表格定义一个标题。通常这个标题会被居中于表格之上。|
|&lt;th&gt;|定义表格中的表头单元格（table head）。|HTML表单中有两种类型的单元格：表头单元格——包含表头信息（由th元素创建）和标准单元格——包含数据（由td元素创建）。th元素内部的文本通常会呈现为居中的粗体文本，而td元素内的文本通常是左对齐的普通文本。|
|&lt;td&gt;|定义HTML表格中的标准单元格（table data）。|请使用colspan和rowspan属性来实现内容横跨多个行或列。|
|&lt;tr&gt;|定义表格中的行（table row）。|tr 元素包含一个或多个th或td元素。|
|&lt;thead&gt;|定义表格中的表头（head）内容。|&lt;thead&gt; 标签定义表格的表头。该标签用于组合HTML表格的表头内容。thead元素应该与tbody和tfoot元素结合起来使用。tbody元素用于对HTML表格中的主体内容进行分组，而tfoot元素用于对HTML表格中的表注（页脚）内容进行分组。|
|&lt;tbody&gt;|定义表格中的主体（body）内容。|同上|
|&lt;tfoot&gt;|定义表格中的表注内容/脚注（foot）。|同上|
|&lt;col&gt;|定义表格中一个或多个列（column）的属性值。|请为&lt;col&gt;标签添加class属性。这样就可以使用CSS来负责对齐方式、宽度和颜色等等。
|&lt;colgroup&gt;|用于对表格中的列（column）进行组合（group），以便对其进行格式化。|请为&lt;colgroup&gt;标签添加class属性。这样就可以使用CSS来负责对齐方式、宽度和颜色等。|

### 框架标签

|框架标签|描述|详细说明|
|:---|:---|:---|
|&lt;frame&gt;|定义frameset中的一个特定的窗口/框架（frame）。|frameset中的每个frame都可以设置不同的属性，比如border、scrolling、noresize等。|
|&lt;frameset&gt;|定义框架（frame）集。|它被用来组织多个窗口（框架）。每个框架存有独立的文档。您必须使用cols或rows属性。|
|&lt;noframes&gt;|定义针对不支持框架的用户的替代内容。|如果您需要为不支持框架的浏览器添加一个&lt;noframes&gt;标签，请务必将此标签放置在&lt;body&gt;&lt;/body&gt; 标签中。|
|&lt;iframe&gt;|创建包含另外一个文档的内联（inline）框架（frame）。|Inline：内联的。插入的地图就是一个iframe。|

### 图像标签

|图像标签|描述|详细说明|
|:---|:---|:---|
|&lt;img&gt;|定义图像/图片（image）。|与&lt;figure&gt;有何不同？|
|&lt;map&gt;|定义图像映射（image-map）。|定义一个客户端图像映射。图像映射指带有可点击区域的一幅图像。|
|&lt;area&gt;|定义图像地图内部的区域（area）。|注意与&lt;textarea&gt;定义多行的文本输入控件的区别。|
|&lt;canvas&gt;|定义图形，比如图表和其他图像。|&lt;canvas&gt;标签只是图形容器，必须使用脚本来绘制图形。|
|&lt;figure&gt;|规定独立的流内容（图像、图表、照片、代码等）|&lt;figure&gt;标签是HTML5中的新标签。figure用于对元素进行组合，多用于图片不图片描述组合。而img只是一个图片元素而已，可以嵌套在figure中使用。&lt;img&gt;标签创建的是被引用图像的占位空间，不会在网页中插入图像，而是从网页上链接图像。|
|&lt;figcaption&gt;|定义figure元素的标题。|使用&lt;figcaption&gt;元素为figure添加标题（caption）。|

### 音频/视频标签

|音频/视频标签|描述|详细说明|
|:---|:---|:---|
|&lt;audio&gt;|定义声音（audio），比如音乐或其他音频流。|&lt;audio&gt; 标签是HTML5的新标签。|
|&lt;source&gt;|为媒介元素（比如&lt;video&gt;和&lt;audio&gt;）定义媒介资源。|&lt;source&gt;标签是HTML5中的新标签。|
|&lt;track&gt;|定义用在媒体播放器中的文本轨道（track）。|&lt;track&gt;标签是HTML5中的新标签。|
|&lt;video&gt;|定义视频（video），比如电影片段或其他视频流。|&lt;video&gt; 标签是HTML5的新标签。

### 链接标签

|链接标签|描述|详细说明|
|:---|:---|:---|
|&lt;a&gt;|定义超链接（anchor锚），用于从一张页面链接到另一张页面。|&lt;a&gt;元素最重要的属性是href属性，它指示链接的目标。如果未设置href属性，则只是超链接的占位符。|
|&lt;link&gt;|定义文档与外部资源的关系（link连接）。|&lt;link&gt; 标签最常见的用途是链接样式表（css）。link元素是空元素，它仅包含属性。此元素只能存在于head部分，不过它可出现任何次数。|
|&lt;nav&gt;|定义导航（navigator）链接。|&lt;nav&gt;标签是HTML5中的新标签。如果文档中有“前后”按钮，则应该把它放到&lt;nav&gt;元素中。|

### 列表标签

|列表标签|描述|详细说明|
|:---|:---|:---|
|&lt;ul&gt;|定义无序（unordered）列表（list）。|ul即unordered list。请使用CSS来定义列表的样式。|
|&lt;ol&gt;|定义有序（ordered）列表（list）。|ol即ordered list。请使用CSS来定义列表的样式。|
|&lt;li&gt;|定义列表的项目（list item）。|可用在有序列表（&lt;ol&gt;）和无序列表（&lt;ul&gt;）中。请使用CSS来定义列表和列表项目的样式。|
|&lt;dir&gt;|不赞成使用。定义目录列表（directory）。|一般用&lt;ul&gt;或&lt;ol&gt;，不用&lt;dir&gt;|
|&lt;dl&gt;|定义 定义列表（definition list）。|&lt;dl&gt;标签用于结合&lt;dt&gt;（定义列表中的项目）和&lt;dd&gt;（描述列表中的项目）。|
|&lt;dt&gt;|定义 定义列表中的项目（即术语term部分）。|dl即definition term。|
|&lt;dd&gt;|定义 定义列表中项目的描述（description）。|dd即definition description。|
|&lt;menu&gt;|定义菜单（menu）列表。当希望列出表单控件时使用。|请使用CSS来定义列表的样式。|
|&lt;menuitem&gt;|定义用户可以从弹出菜单（menu）调用的命令/菜单项目（item）。|&lt;menuitem&gt;标签是HTML5中的新标签。|
|&lt;command&gt;|定义命令（command）按钮。|&lt;command&gt; 标签是HTML5中的新标签。|

### 样式/节标签

|样式/节标签|描述|详细说明|
|:---|:---|:---|
|&lt;style&gt;|定义文档的样式（style）信息。|规定在浏览器中如何呈现HTML文档。type属性是必需的，定义style元素的内容。唯一可能的值是"text/css"。style 元素位于head部分中。如需链接外部样式表，请使用&lt;link&gt;标签。|
|&lt;div&gt;|定义文档中的分区或节（division/section）。div即division。|&lt;div&gt;标签可以把文档分割为独立的、不同的部分。&lt;div&gt;是一个块级元素。这意味着它的内容自动地开始一个新行。实际上，换行是&lt;div&gt;固有的唯一格式表现。可以通过&lt;div&gt;的class或id应用额外的样式。&lt;div&gt;是一个块级元素（而&lt;span&gt;则是内联元素），也就是说，浏览器通常会在div元素前后放置一个换行符。|
|&lt;section&gt;|定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。|&lt;section&gt;标签是HTML5中的新标签。|
|&lt;span&gt;|定义文档中的节（组合文档中的行内元素）。|&lt;span&gt;和&lt;div&gt;的区别：&lt;div&gt;是块级元素（block element）；&lt;span&gt;是内联元素，也叫内嵌元素（inline element）。&lt;span&gt;与&lt;p&gt;的区别：&lt;p&gt;指一个段落，默认是一个块级元素，而&lt;span&gt;是段落内的一部分文字，是一个行内元素。|
|&lt;header&gt;|定义section或page的页眉（介绍信息）。|&lt;header&gt;标签是HTML5中的新标签。|
|&lt;footer&gt;|定义文档或节的页脚（footer）。|页脚通常包含文档的作者、版权信息、使用条款链接、联系信息等等。您可以在一个文档中使用多个&lt;footer&gt;元素。|
|&lt;article&gt;|定义文章（规定独立的自包含内容）。|&lt;article&gt;标签是HTML5中的新标签。一篇文章应有其自身的意义，应该有可能独立于站点的其余部分对其进行分发。&lt;article&gt;元素的潜在来源：论坛帖子、报纸文章、博客条目、用户评论。|
|&lt;aside&gt;|定义页面内容之外的内容。|&lt;aside&gt;标签是HTML5的新标签。&lt;aside&gt;的内容可用作文章的侧栏。|
|&lt;details&gt;|用于描述文档或文档某个部分的细节。|&lt;details&gt;标签是HTML5中的新标签。与&lt;summary&gt;标签配合使用可以为details定义标题。标题是可见的，用户点击标题时，会显示出details。|
|&lt;summary&gt;|为&lt;details&gt;元素定义可见的标题。|&lt;summary&gt;标签是HTML5中的新标签。&lt;summary&gt;标签包含details元素的标题，"details"元素用于描述有关文档或文档片段的详细信息。请与&lt;details&gt;标签一起使用。标题是可见的，当用户点击标题时会显示出详细信息。"summary"元素应该是"details"元素的第一个子元素。|
|&lt;dialog&gt;|定义对话（dialog），比如交谈（conversation）。|&lt;dialog&gt;标签是HTML5中的新标签。对话中的每个句子都必须属于&lt;dt&gt;标签所定义的部分。|

### 编程标签

|编程标签|描述|详细说明|
|:---|:---|:---|
|&lt;script&gt;|定义客户端（client，user）脚本（script）。|比如JavaScript。script元素既可以包含脚本语句，也可以通过src属性指向外部脚本文件。必需的type属性规定脚本的MIME类型。JavaScript的常见应用是图像操作、表单验证以及动态内容更新。假如此元素内部的代码没有位于某个函数中，那么这些代码会在页面被加载时被立即执行。&lt;frameset&gt;之后的脚本会被忽略。|
|&lt;noscript&gt;|用来定义在脚本未被执行时的替代内容（文本）。|此标签可被用于可识别&lt;script&gt;标签但无法支持其中的脚本的浏览器。如果浏览器支持脚本，那么它不会显示出&lt;noscript&gt;标签中的文本。无法识别&lt;script&gt;标签的浏览器会把标签的内容显示到页面上。为了避免浏览器这样做，您应当在注释标签中隐藏脚本。老式的（无法识别&lt;script&gt;标签的）浏览器会忽略注释，这样就不会把标签的内容写到页面上，而新式的浏览器则懂得执行这些脚本，即使它们被包围在注释标签中。|
|&lt;embed&gt;|为外部应用程序（非HTML）定义容器。|&lt;embed&gt;标签是HTML5中的新标签。定义嵌入的内容，比如插件。&lt;embed&gt;标签必须有src属性。
|&lt;applet&gt;|不赞成使用。定义嵌入的applet。|HTML5中不支持&lt;applet&gt;标签。请使用object元素标签代替。Applet是采用Java编程语言编写的小应用程序，该程序可以包含在HTML页中，与在页中包含图像的方式大致相同。|
|&lt;object&gt;|定义一个嵌入的对象（object）。|&lt;object&gt;可以代替&lt;applet&gt;。用于包含对象，比如图像、音频、视频、Java applets、ActiveX、PDF以及Flash。object的初衷是取代img和applet元素。不过由于漏洞以及缺乏浏览器支持，这一点并未实现。不要对图像使用&lt;object&gt;标签，请使用&lt;img&gt;标签代替。|
|&lt;param&gt;|定义对象的参数。|此标签可为包含它的&lt;object&gt;或者&lt;applet&gt;标签提供参数。|

**备注：**
浏览器总是很宽大地试图去理解各种标签。因为浏览器为了提升用户体验，提高市场占有率，允许你犯错。提供给浏览器的语义信息越多，浏览器就可以越好地把这些信息展示给用户。我们在实际使用中最好根据W3C的标准，规范使用所有标签。