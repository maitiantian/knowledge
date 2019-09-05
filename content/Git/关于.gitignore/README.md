<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# 关于.gitignore

常用的规则：

1. /mtk/：过滤整个文件夹
2. *.zip：过滤所有.zip文件
3. /mtk/do.c：过滤某个具体文件

被过滤掉的文件就不会出现在git仓库中（gitlab或github），本地库中还有，只是push的时候不会上传。

gitignore还可以指定要将哪些文件添加到版本管理中：

1. !*.zip
2. !/mtk/one.txt


假如只需要管理/mtk/目录中的one.txt文件，这个目录中的其它文件都不需要管理，可以使用：

1. /mtk/
2. !/mtk/one.txt

如果在创建.gitignore文件之前就push了项目，那么即使在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。

原因是Git已经开始管理这些文件了，所以无法再通过过滤规则过滤它们。因此一定要在项目开始时就创建.gitignore文件。



1）配置语法：

以斜杠“/”开头表示目录；
以星号“*”通配多个字符；
以问号“?”通配单个字符
以方括号“[]”包含单个字符的匹配列表；
以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；
此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

示例:

1. fd1/*：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；
2. /fd1/*：忽略根目录下的 /fd1/ 目录的全部内容；
3. /*, !.gitignore, !/fw/bin/, !/fw/sf/：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/ 和 /fw/sf/ 目录。


```bash
*.a     # 忽略所有 .a 结尾的文件
!lib.a  # 但 lib.a 除外
/TODO   # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/  # 忽略 build/ 目录下的所有文件
doc/*.txt   # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

.gitignore只能忽略那些没有被track的文件，如果某些文件已经被纳入了版本管理中，再将其添加.gitignore是无效的。解决方法是先把本地缓存删除（改变成未track状态），然后再提交：

```bash
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```