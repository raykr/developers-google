# 配置你的编辑器

你的代码编辑器是你的主要开发工具，你用它编写及保存一行行的代码。学会使用编辑器的快捷键，安装一些关键性插件可以帮助你更快更好的编写代码。

**长话短说**
* 有针对性的选择一款编辑器，譬如可自定义快捷键，拥有丰富的插件来帮助你写好代码。
* 使用包管理器，它可以让你更容易的查找、安装、升级插件。
* 安装插件，它可以帮你在开发过程中保持生产力。那么就从现在开始吧。

## 安装Sublime Text编辑器
[Sublime](http://www.sublimetext.com/)是一款优秀的编辑器，基础功能健全，给编码带来乐趣。并且你可以安装包管理器，可以更方便的安装插件，增加新功能。

Sublime提供两个版本可供下载，[Sublime Text 2](http://www.sublimetext.com/2)和[Sublime Text 3](http://www.sublimetext.com/3)。SublimeText3版本稳定，并且拥有一些SublimeText2没有的功能，然而有时候SublimeText2会更可靠。

## 为什么要使用包管理器？
使用包管理器，你可以更容易的查找、安装和更新插件。
![package_control](https://developers.google.com/web/tools/setup/imgs/package_control.png)

如何安装包管理器请参考：https://packagecontrol.io/installation

## 安装插件
插件可以提升你的生产力。想一想，有什么事是你必须要借助其他工具去做的？代码分析，有！版本控制，查看提交记录的插件？有！融合其他插件的，比如说Github？也有！

包管理器可以方便管理插件：
1. 在Sublime Text编辑器界面，打开包管理器(`Ctrl` + `Shift` + `P`)
2. 输入`Install Package`
3. 输入插件名称进行查找（或直接浏览所有插件）

点击查看[热门Sublime Text插件列表](https://packagecontrol.io/browse)，这儿有我们喜爱的插件，推荐你安装，因为这些插件会提升你的开发速度。

### 前缀自动补全（Autoprefixer）
如果你想在CSS中快速添加第三方前缀，你可以试试这个便捷的插件。

编写不带前缀的CSS，使用组合键`Ctrl` + `Shift` + `P`打开命令行，输入AutoprefixCSS即可补全第三方前缀。

[可以通过编译进程自动化完成以上操作]()，这样你就可以编写简单的CSS即可，而不必记住`Ctrl` + `Shift` + `P`这种命令。

![sublime-autoprefixer](https://developers.google.com/web/tools/setup/imgs/sublime-autoprefixer.gif)

### 颜色拾取器（ColorPicker）
在调色板中拾取任意颜色，使用`Ctrl` + `Shift` + `C`添加进CSS中。

![sublime-color-picker](https://developers.google.com/web/tools/setup/imgs/sublime-color-picker.png)

### 代码补全（Emmet）
为你的文本编辑器增加一些非常有用的键盘快捷键和代码段。查看此视频[Emmet.io](http://emmet.io)介绍了解详细。（个人最喜欢的命令是'Toggle Comment'）

![emmet-io-example](https://developers.google.com/web/tools/setup/imgs/emmet-io-example.gif)

### 前端代码美化（HTML-CSS-JS Prettify）
这个扩展程序可以美化你的HTML、CSS、JS代码格式。甚至可以在你保存文件的时候美化你的文件。

![sublime-prettify](https://developers.google.com/web/tools/setup/imgs/sublime-prettify.gif)

### 代码变动标识（Git Gutter）
在文本编辑器左侧的竖槽上增加文件改动标识。

![sublime-git-gutter](https://developers.google.com/web/tools/setup/imgs/sublime-git-gutter.png)

### 左侧竖槽颜色标识（Gutter Color）
> 注意：此插件只在Sublime Text 3中可用。

在左侧竖槽上显示CSS对应颜色的标识。

![sublime-gutter-color](https://developers.google.com/web/tools/setup/imgs/sublime-gutter-color.png)

此插件需要安装ImageMagick。如果你在Mac OS X系统上，我们建议你从[CactusLabs](http://cactuslab.com/imagemagick/)上安装。