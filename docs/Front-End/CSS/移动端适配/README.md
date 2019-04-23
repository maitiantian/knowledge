<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a href="javascript:void(0)" style="color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 移动端适配

* 物理像素： 设备屏幕上的一个发光单元；
* 逻辑像素、CSS像素： CSS里的尺寸单位，1px，抽象的概念，无固定长度，是为web开发者创造的度量单位。
	* 不同设备、不同环境中，CSS的1px对应的物理像素是不同的;
	* 桌面浏览器中CSS的1px往往对应着电脑屏幕的1个物理像素；
	* 用户的缩放也会引起CSS像素的变化，如：当用户把页面放大一倍，CSS中1px所代表的物理像素也会增加一倍；把页面缩小一倍，CSS中1px所代表的物理像素也会减少一倍。

3个viewport：

视口是html的父元素，所以我们称视口为初始包含块。这样你就明白了，html元素的百分比是基于视口的。

html元素的大小，document.documentElement.offsetWidth，document.documentElement.offsetHeight

document.documentElement.clientWidth
500 == html父元素宽度，即初始包含块宽度
document.documentElement.clientHeight
300???????????

body的大小
document.body.clientWidth
document.body.clientHeight

[window属性：innerHeight](https://www.w3cschool.cn/fetch_api/fetch_api-rf2u2nv2.html)

* layout viewport：html的父元素，初始包含块的大小，这个就是 `<meta name="viewport">` 中所指的viewport；
* visual viewport：浏览器可视区域的大小，window.innerWidth，window.innerHeight；
* ideal viewport：layout viewport的理想尺寸；
	* 不需要用户缩放和横向滚动条就能正常的查看网站的所有内容；
	* 显示的文字的大小是合适的，比如一段14px大小的文字，不会因为在一个高密度像素的屏幕里显示得太小而无法看清，理想情况是这段14px的文字无论是在何种密度屏幕，何种分辨率下，显示出来的大小都是差不多的；
	* 不只是文字，其他元素像图片什么的也是这个道理。
	* 如果我们想把html的宽度设置成浏览器可视区域的宽度该怎么做呢？ `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

* visual viewport = ideal viewport / 缩放值
* 缩放值 = ideal viewport / visual viewport


* 屏幕尺寸：屏幕对角线的长度，单位英寸（1英寸=2.54厘米）；
* 分辨率：屏幕宽度和高度上的发光单元个数；
* 点距：发光单元中心之间的距离，点距和屏幕尺寸决定了分辨率大小；
* PPI（Pixels Per Inch）：屏幕像素密度，每英寸聚集的物理像素个数，这里的一英寸还是对角线长度；
* DPI（Dots Per Inch）：每英寸像素点（物理像素），印刷业术语。对于屏幕而言和PPI是一个意思；
* DPR（Device Pixel Ratio）：设备像素比，缩放比例为1时，等于 设备物理像素个数/理想视口CSS像素个数(device-width)，逻辑像素大小/物理像素大小，告诉浏览器该用多少个物理像素来绘制一个CSS像素，`dpr = window.devicePixelRatio;`；
* 缩放：CSS像素的大小是可变得，缩放就是放大或缩小CSS像素的过程。

![](../../../images/fe_css_viewport.png)

meta标签

`<meta name="viewport">` 是为了让 layout viewport 和 ideal viewport 的宽度匹配。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<!--  -->
<!-- device-width 是 ideal viewport 的宽度 -->

<!-- 1. 这里的 viewport 指的是 layout viewport -->
<!-- 2. init-scale：设置页面的初始缩放比例 -->
<!-- 3. minimum-scale：设置页面的最小缩放比例 -->
<!-- 4. maximum-scale：设置页面的最大缩放比例 -->
<!-- 5. user-scalable：是否允许用户对页面进行缩放操作 -->
```

CSS3 媒体查询

媒体查询是响应式设计的基础，有以下三点作用：

1. 检测媒体的类型：screen，print等；
2. 检测 layout viewport 的特性，宽高分辨率等；
3. 特性相关查询，比如检测浏览器是否支持某某特性（这一点不讨论，因为它被目前浏览器支持的功能对于web开发来讲很无用）

```css
@media 媒体类型 and (视口特性阀值){
    /* 满足条件的 css 样式代码 */
}

@media mediatype and|not|only (media feature){
    /* CSS-Code; */
}
```

这个viewport叫做 ideal viewport——移动设备的理想viewport。

ideal viewport并没有固定尺寸，不同设备拥有有不同的ideal viewport。
所有的iphone的ideal viewport宽度都是320px，无论它的屏幕宽度是320还是640，也就是说在iphone中，CSS中的320px就代表iphone屏幕的宽度。


一个 CSS 像素的大小与一个物理像素的大小的比值。告诉浏览器应该使用多少个屏幕的实际像素来绘制单个 CSS 像素。





媒体类型：

* all: 用于所有设备；
* print: 用于打印机和打印预览；
* screen: 用于电脑屏幕，平板电脑，智能手机等；
* speech: 应用于屏幕阅读器等发声设备。


媒体查询 参数：

* width: layout viewport 的宽度；
* height: layout viewport 的高度；
* device-width: ideal viewport 的宽度；
* device-height: ideal viewport 的高度；
* orientation: 检测设备目前处于横向（landscape）还是纵向（portrait）状态；
* aspect-ratio: 检测浏览器可视宽度和高度的比例（例如：aspect-ratio:16/9）；
* device-aspect-ratio: 检测设备的宽度和高度的比例；
* color: 检测颜色的位数。（例如：min-color:32就会检测设备是否拥有32位颜色）；
* color-index: 检查设备颜色索引表中的颜色，他的值不能是负数；
* resolution: 检测屏幕或打印机的分辨率（例如：min-resolution:300dpi或min-resolution:118dpcm）；
* grid: 检测设备是网格的还是位图设备。


* orientation: 输出设备中的页面可见区域高度是否大于或等于宽度；
* scan: 电视类设备的扫描工序；
* grid: 用来查询输出设备是否使用栅格或点阵；
* width: 输出设备中的页面可见区域宽度；
	* min-width: 输出设备中的页面最小可见区域宽度；
	* max-width: 输出设备中的页面最大可见区域宽度；
* height: 输出设备中的页面可见区域高度；
	* min-height: 输出设备中的页面最小可见区域高度；
	* max-height: 输出设备中的页面最大可见区域高度；
* device-width: 输出设备的屏幕可见宽度；
	* min-device-width: 输出设备的屏幕最小可见宽度；
	* max-device-width: 输出设备的屏幕最大可见宽度；
* device-height: 输出设备的屏幕可见高度；
	* min-device-height: 输出设备的屏幕的最小可见高度；
	* max-device-height: 输出设备的屏幕可见的最大高度；
* aspect-ratio: visual viewport 宽度与高度的比率（iPhone 5: 320/568）；
	* min-aspect-ratio: 输出设备中的页面可见区域宽度与高度的最小比率；
	* max-aspect-ratio: 输出设备的屏幕可见宽度与高度的最大比率；
* device-aspect-ratio: 输出设备的屏幕可见宽度与高度的比率；
	* min-device-aspect-ratio: 输出设备的屏幕可见宽度与高度的最小比率；
	* max-device-aspect-ratio: 输出设备的屏幕可见宽度与高度的最大比率；
* resolution: 设备的分辨率，如：96dpi、300dpi、118dpcm；
	* min-resolution: 设备的最小分辨率；
	* max-resolution: 设备的最大分辨率；
* color: 输出设备每一组彩色原件的个数，如果不是彩色设备，则值等于0；
	* min-color: 输出设备每一组彩色原件的最小个数；
	* max-color: 输出设备每一组彩色原件的最大个数；
* color-index: 在输出设备的彩色查询表中的条目数，如果没有使用彩色查询表，则值等于0；
	* min-color-index: 在输出设备的彩色查询表中的最小条目数；
	* max-color-index: 在输出设备的彩色查询表中的最大条目数。



----------------------------------------------------------------------------------------------------------

[一篇真正教会你开发移动端页面的文章(一)](https://blog.csdn.net/VhWfR2u02Q/article/details/78737075)

[一篇真正教会你开发移动端页面的文章(二)](http://web.jobbole.com/93253/)

[移动端适配（一）实操篇，前端必掌握技能](http://baijiahao.baidu.com/s?id=1596376727654829921&wfr=spider&for=pc)

[移动端适配（二）实操篇，前端必掌握技能](http://www.lucklnk.com/godaddy/details/aid/385911124)

* [如何在Vue项目中使用vw实现移动端适配](https://www.w3cplus.com/mobile/vw-layout-in-vue.html)
	* [再聊移动端页面的适配](https://www.w3cplus.com/css/vw-for-layout.html)
	* [使用Flexible实现手淘H5页面的终端适配](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html)

[CSS3 的视口单位vw、vh实现自适应（带有px，em，rem的简单介绍）](https://blog.csdn.net/sjw1039115768/article/details/80460777)

[移动端布局适配](https://www.jianshu.com/p/dfa14e6eb19a?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

[flexible.js 移动端自适应方案](https://www.jianshu.com/p/04efb4a1d2f8)

[Js 实现页面缩放](https://www.cnblogs.com/lyr1213/p/8658002.html)

[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

[Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

[移动前端开发之viewport的深入理解](https://www.cnblogs.com/2050/p/3877280.html)

[document.documentElement.clientWidth在PC端和移动端值得含义一样吗？](https://segmentfault.com/q/1010000004610317)