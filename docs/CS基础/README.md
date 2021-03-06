<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 目录




***动态语言（弱类型语言）：***
变量本身类型不固定的语言

***静态语言（强类型语言）：***
定义变量时必须指定变量类型，赋值时类型不匹配则报错

# 斜杠

斜杠分正斜杠（forward slash'/'）和反斜杠（back slash'\\'）。

* 在windows系统中，\\用来表示目录；
* 在unix系统中，/表示目录；
* web遵循unix命名，所以在网址（URL）中，/表示目录。


# 计算密集型 vs IO密集型

是否采用多任务的第二个考虑是任务的类型。我们可以把任务分为计算密集型和IO密集型。

计算密集型任务的特点是要进行大量的计算，消耗CPU资源，比如计算圆周率、对视频进行高清解码等等，全靠CPU的运算能力。这种计算密集型任务虽然也可以用多任务完成，但是任务越多，花在任务切换的时间就越多，CPU执行任务的效率就越低，所以，要最高效地利用CPU，计算密集型任务同时进行的数量应当等于CPU的核心数。

计算密集型任务由于主要消耗CPU资源，因此，代码运行效率至关重要。Python这样的脚本语言运行效率很低，完全不适合计算密集型任务。对于计算密集型任务，最好用C语言编写。

第二种任务的类型是IO密集型，涉及到网络、磁盘IO的任务都是IO密集型任务，这类任务的特点是CPU消耗很少，任务的大部分时间都在等待IO操作完成（因为IO的速度远远低于CPU和内存的速度）。对于IO密集型任务，任务越多，CPU效率越高，但也有一个限度。常见的大部分任务都是IO密集型任务，比如Web应用。

IO密集型任务执行期间，99%的时间都花在IO上，花在CPU上的时间很少，因此，用运行速度极快的C语言替换用Python这样运行速度极低的脚本语言，完全无法提升运行效率。对于IO密集型任务，最合适的语言就是开发效率最高（代码量最少）的语言，脚本语言是首选，C语言最差。


# 版本号

版本格式：X.Y.Z，Major.Minor.Patch，主版本号.次版本号.修订号

##### 项目立项

版本号：0.0.0

##### 开发阶段

此时系统尚不稳定，随时可能增减或者修改API：

1. 主版本号：0表示正在开发阶段；
2. 次版本号：增加新的功能时增加；
3. 修订号：只要有改动就增加。

##### 后续维护

1. 主版本号：全盘重构时增加；重大功能或方向改变时增加；大范围不兼容之前的接口时增加；
2. 次版本号：增加新的业务功能时增加；
3. 修订号：增加新的接口时增加；在接口不变的情况下，增加接口的非必填属性时增加；增强和扩展接口功能时增加。

关于新增接口：如果该新增的接口只是对现有的业务线进行扩展则增加修订号；如果是为了增加新的业务线则增加次版本号。

##### 先行版本号和开发版本号

先行版本号及版本编译信息可以加到“主版本号.次版本号.修订号”后面，作为延伸。

1. 先行版本号(Pre-release)：意味该版本不稳定，可能存在兼容性问题：
    X.Y.Z.[a-c][正整数]，如 1.0.0.a1，1.0.0.b99，1.0.0.c1000。
2. 开发版本号：常用于CI-CD（持续集成和持续交付）： 
    X.Y.Z-dev[正整数]，如 1.0.1-dev4。
3. 版本号排序规则为依次比较主版本号、次版本号和修订号的数值，当存在字母时，以ASCII的排序来比较：
    * 1.0.0 < 1.0.1 < 1.1.1 < 2.0.0；
    * 1.0.0.a100 < 1.0.0，2.1.0-dev3 < 2.1.0；
    * 1.0.0.a1 < 1.0.0.b1。

一些修饰的词：

    * alpha：内部版本
    * beta：测试版
    * demo：演示版
    * enhance：增强版
    * free：自由版
    * full version：完整版，即正式版
    * lts：长期维护版本
    * release：发行版
    * rc：即将作为正式版发布
    * standard：标准版
    * ultimate：旗舰版
    * upgrade：升级版


1. 版本一经发布，不得修改其内容，任何修改必须在新版本中发布；
2. 在接口还没有确定下来时，应该先使用开发版本号；
3. 业务功能 > 功能 > 接口。


