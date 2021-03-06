<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# CSS

#### vertical-align


* 替换元素
* 非替换元素



#### font-family

font-family: Times New Roman, open-sans, 微软雅黑, sans-serif;

* 属性值为字符串，可以是中文，可以有空格，不需要用括号括起来，不区分大小写；
* 使用中文属性值时候应注意，文件编码不匹配时可能会因为乱码而无法生效，可以直接使用Unicode编码使浏览器可以正确解析（最好还是直接使用英文属性值）；

|中文名称|英文名称|Unicode编码|
|:---|:---|:---|
|宋体|SimSun|\5B8B\4F53|
|新宋体|NSimSun|\65B0\5B8B\4F53|
|黑体|SimHei|\9ED1\4F53|
|微软雅黑|Microsoft YaHei|\5FAE\8F6F\96C5\9ED1|
|楷体\_GB2312|KaiTi\_GB2312|\6977\4F53\_GB2312|
|隶书|LiSu|\96B6\4E66|
|幼园|YouYuan|\5E7C\5706|
|华文细黑|STXihei|\534E\6587\7EC6\9ED1|
|细明体|MingLiU|\7EC6\660E\4F53|
|新细明体|PMingLiU|\65B0\7EC6\660E\4F53|

* 可以用多个字体组成一个“回退”系统，如果浏览器不支持第一个字体，则会尝试下一个；
* serif：调用浏览器设置的 serif 字体；
* sans-serif：调用浏览器设置的 sans-serif 字体。


##### 衬线字体和无衬线字体

serif： 有衬线字体，在字的笔画开始、结束处有额外装饰，笔画粗细会有不同；
sans-serif： 无衬线字体，没有这些额外的装饰，笔画粗细差不多。

* sans-serif 容易造成字母辨认的困扰（例如：I 和 l）；
* 在小字体的场合，通常 sans-serif 比 serif 更清晰。


##### 在Chrome浏览器中设置字体：

设置->自定义字体

![Chrome浏览器中自定义字体](../../images/fe_css_font_family.jpg)



##### px / em / rem

* px：绝对的长度单位；
    * 缺点：固定值，不够灵活
* em：相对的长度单位，相对于父元素的 font-size 值，如果父元素没有设置，则向上层寻找；
    * 缺点：一层一层的具有叠加效应
* rem：相对的长度单位，相对于 html 的 font-size 值。
    * 默认情况下，1rem = 16px
    * 兼容性写法（IE8以下）：p {font-size:14px; font-size:.875rem;}

