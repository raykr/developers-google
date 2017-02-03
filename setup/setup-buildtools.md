# 配置你的编译工具

从头开始编译你的多设备站点，学习如何提升开发效率，并使用编译工具集来创建一个加载迅速的站点。每个站点都应该部署一套开发版本和生产版本。

开发版本的文件，包括HTML，CSS，JS和图片等，都保持正确清晰的格式，如此可以让你乐于其中。

生产环境上的版本就需要把这些文件做相应处理，包括压缩、串联或合并、优化图片等操作。网页开发人员需要考虑成千上万的事情，而编译步骤是最关键的，然而很多步骤都是很繁杂的。你必须寻求一种自动化完成工作的方式，比如：图片压缩，CSS压缩，JavaScript关联，响应测试，关联测试等等...

跟着这篇导读去学习如何最好地规划你的工作流，如此一来你已经创建好站点就成为接下来开始改进的最好的练习。

**长话短说**

* 你的编译程序必须性能优异，这些工具应该实现自动化压缩或关联Javascript、CSS、HTML和图片。
* 使用工具（如LiveReload）让你的开发进程更加流畅。

开始编码之前，你需要考虑如何优化和编译站点的生产环境版本。从一开始就配置好工作流，从而避免在工程结束的时候出现一大堆令人讨厌的怪事，在工作流中增加工具来帮你完成一些单调的、重复性的工作，如此一来可以提升你的开发效率。

## 什么是编译进程？

编译进程是在开发期间替你编译、测试、运行程序的任务的总称，它常用来为站点创建开发版本。你的编译进程不应该是开发工作流末端的任务。

最流行编译进程工具无外乎[Gulp](http://gulpjs.com/)和[Grunt](http://gruntjs.com/)，二者都是命令行工具。如果你对此都没有过接触，我们推荐你使用`Gulp`，也是“网页开发入门套件”其一。

有许多带GUI界面的工具，可能在初涉入门时更简单易用一些，但是缺伐一定的灵活性。

|支持的平台|工具名|
|:---|:---|
|OS X / Windows| [Prepros](http://alphapixels.com/prepros/) |
|OS X|	[CodeKit](https://incident57.com/codekit/) |
|OS X|	[HammerForMac](http://hammerformac.com/) |

## 编译进程能做什么？

In the following sections, we're going to look at the most common tasks you should have in your build process and recommend tasks for Grunt and Gulp.

This requires a lot of trial and error to get each piece set-up the way you want and can be daunting if you are new to build processes.

For a good example of a build process, check out the getting started guide for Web Starter Kit, which goes through how to use Web Starter Kit and explains what each of the commands in the Gulp file do. This can be used as a quick way to get set-up and then you can make changes if needed.

If you are looking to create your own build process and you're new to Gulp or Grunt, the quick start guides will be the best place to get into on installing and running your first build process:

* [Grunt Getting Started](http://gruntjs.com/getting-started)
* [Gulp Getting Started](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md#getting-started)

### Use concatenation & minification for a faster site

For those unfamiliar with the terms concatenation and minification, concatenation means simply merging multiple files together, i.e. copying and pasting several files into one. The reason we do this is that it's more efficient for a browser to fetch one file, rather than lots of small files.

Minification is the process of taking a file and making the overall number of characters less, without changing how the code works. A good example of this is removing comments, or taking a long variable name and making it smaller. This makes the file size smaller, leading to faster downloads.

For minification, use the following:

|Type of File|	Gulp|	Grunt|
|:---|:---|:---|
|CSS|[gulp-csso](https://github.com/ben-eb/gulp-csso)|	[grunt-contrib-cssmin](https://github.com/gruntjs/grunt-contrib-cssmin)|
|JS|[gulp-uglify](https://github.com/terinjokes/gulp-uglify/)|	[grunt-contrib-uglify](https://github.com/gruntjs/grunt-contrib-uglify)|
|HTML|[gulp-minify-html](https://www.npmjs.com/package/gulp-minify-html)|[grunt-contrib-htmlmin](https://github.com/gruntjs/grunt-contrib-htmlmin)|

For concatentation, use the following:

|Type of File|	Gulp|	Grunt|
|:---|:---|:---|
|CSS (Sass)|[gulp-sass](https://github.com/dlmanning/gulp-sass) or [gulp-useref](https://github.com/jonkemp/gulp-useref)|	[grunt-contrib-sass](https://github.com/gruntjs/grunt-contrib-sass) or [grunt-usemin](https://github.com/yeoman/grunt-usemin)|
|JS|[gulp-useref](https://github.com/jonkemp/gulp-useref)|[grunt-usemin](https://github.com/yeoman/grunt-usemin) or [grunt-codekit](https://github.com/fatso83/grunt-codekit)|
**Note**: You can use Sass by taking advantage of the 'import' feature ([See Web Starter Kit for an example](https://github.com/google/web-starter-kit/blob/master/app/styles/main.scss)).

### Optimize your images

Image optimization is an important step to help speed up your site; you'd be surprised how much smaller you can make an image without losing quality. Meta data is removed from the image as it's not needed by the browser to display the image, for example, information about the camera used to take the photo.

For optimizing images, you can use these modules.

|Gulp & Grunt||
|:---|:---|
|[gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin)|[grunt-contrib-imagemin](https://github.com/gruntjs/grunt-contrib-imagemin)|

### Don't trip up with vendor prefixes

It can often become a bit tedious to include all the vendor prefixes for the CSS you use. Use an auto-prefixer to automatically add the prefixes you need to include:

|Gulp vs Grunt||
|:---|:---|
|[gulp-autoprefixer](https://github.com/sindresorhus/gulp-autoprefixer)|[grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer)|
**Note**
If you prefer, you can add a [Sublime package to do the auto-prefixing](https://developers.google.com/web/tools/setup/setup-editor#autoprefixer) for you.

### Never leave your text editor with live reloading

Live reloading updates your site in your browser each time your make a change. After using it once, you won't be able to live without it.

Web Starter Kit uses browser-sync for Live Reload support.

|Gulp vs Grunt||
|:---|:---|
|[browser-sync](http://www.browsersync.io/docs/gulp/)|[grunt-contrib-connect](https://github.com/gruntjs/grunt-contrib-connect) & [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch)|

> **Note**: If you like the idea of Live Reloading, but don't want to have a build process, Addy Osmani's write up on HTML5Rocks covers a range of alternatives (some free and some commercial).