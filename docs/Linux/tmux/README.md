<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# <p align="center" style="border-bottom: 3px solid #e7e7e7;">tmux</p>

***终端复用命令行工具***

* __会话（Session）操作__
    * __tmux ls__ 列出所有会话
    * __tmux new -s foo__ 新建名为foo的会话
    * __tmux a -t foo__ 进入名为foo的会话
    * __tmux detach__ 退出当前会话
    * __tmux kill-session -t foo__ 删除名为foo的会话
    * __tmux kill-server__ 删除所有会话
    * __Ctrl+b $__ 重命名当前会话
    * __Ctrl+b s__ 选择会话列表
* __窗口（Window）操作__
    * __Ctrl+b c__ 新建窗口
    * __Ctrl+b w__ 窗口列表选择
    * __Ctrl+b &__ 关闭当前窗口
    * __Ctrl+b ,__ 重命名窗口
* __窗格（Pane）操作__
    * __Ctrl+b %__ 左右分屏
    * __Ctrl+b "__ 上下分屏
    * __Ctrl+b ↑↓←→__ 上下左右选择窗格
    * __Ctrl+b x__ 关闭当前窗格
    * __Ctrl+b Space__ 切换窗格布局
    * __Ctrl+b {__ 当前窗格前移
    * __Ctrl+b }__ 当前窗格后移
    * __Ctrl+b z__ 最大化当前窗格，再次执行恢复原来大小
    * __Ctrl+b q__ 显示窗格序号，序号出现期间按下对应的数字可跳转至对应的窗格