# 计算机组成原理

CPU执行一条指令的过程：

1. 取指令（Instruction Fetch，IF）
2. 指令译码（Instruction Decode，ID）
3. 执行指令（Execute，EX）
4. 访存取数（Memory，MEM）
5. 结果写回（Write Back，WB）

CPU主频：CPU内部晶振的频率；
CPI（Cycles Per Instruction）：执行一条指令所需要的时钟周期数；
MIPS（Million Instructions Per Second）：计算机每秒钟执行的百万指令数。

时钟周期：又称振荡周期，CPU主频的倒数，CPU仅执行一个基本动作，计算机中最基本、最小的时间单位；
机器周期：执行一个基本操作的时间，IF / ID / EX / MEM / WB；
指令周期：执行一条指令。

机器周期 = 若干个时钟周期
指令周期 = 若干个机器周期


简述时钟周期、机器周期、指令周期的概念及三者之间的关系：https://wenku.baidu.com/view/1a29d43543323968011c92e6.html
简述CPU执行一条指令的过程：https://zhidao.baidu.com/question/124425422.html
延迟图示：https://people.eecs.berkeley.edu/~rcs/research/interactive_latency.html / https://gist.github.com/hellerbarde/2843375
让 CPU 告诉你硬盘和网络到底有多慢：http://cizixs.com/2017/01/03/how-slow-is-disk-and-network/
牛人博客：http://cizixs.com/
CPU主频、倍频与外频：https://zhidao.baidu.com/question/29974153.html
Why do CPUs have multiple cache levels?：https://fgiesen.wordpress.com/2016/08/07/why-do-cpus-have-multiple-cache-levels/
Von Neumann bottleneck：https://en.wikipedia.org/wiki/Von_Neumann_architecture#Von_Neumann_bottleneck
Why is it faster to process a sorted array than an unsorted array?What is Branch Prediction?
：https://stackoverflow.com/questions/11227809/why-is-it-faster-to-process-a-sorted-array-than-an-unsorted-array