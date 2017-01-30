# 配置命令行快捷键

你在一遍又一遍地做着设置命令行快捷键的任务。如果你发现陷入无尽重复相同的工作当中，来看看这个，也许会解救你。

**长话短说**

* 设置快捷键：创建**别名**，好记又好输入。
* 创建一个Github dotfiles（如.vimrc，用以保存自定义设置的文件），可以分享和同步你的命令行快捷键。

## 如何设置

最简单的创建命令行快捷方式的方法就是给你的`bashrc`文件增加一个别名。Mac或Linux系统操作如下：

1.任意位置打开命令行终端，输入：
```
open -a 'Sublime Text' ~/.bashrc
```

2.增加一个新别名，例如:
```
alias master='git checkout master'
```
设置完成后，当在此文件夹下使用git仓库时，只需运行`master`命令，即可代替原来`git checkout master`检出master分支。

> 注: 查看设置别名详细说明 [setting up Windows aliases](https://msdn.microsoft.com/en-us/library/windows/desktop/ms682057(v=vs.85).aspx).

## 推荐快捷键

你会发现以下快捷键会很有用：

|Command | Alias |
|:-------|:------|
|Open your editor|	alias st='open -a "Sublime Text"'|
|Launch a server|	alias server="python -m SimpleHTTPServer"|
|Go to a directory you commonly work in|	alias p="cd ~/projects"|

## 保存、分享和同步快捷键

保存快捷键为`.xxx`文件到github上。并且可以通过设备分享、备份。

Github上甚至可以为dotfiles创建页面 [dedicated page for dotfiles](https://dotfiles.github.io/) Chrome小组： [Mathias Bynens' dotfiles](https://github.com/mathiasbynens/dotfiles).