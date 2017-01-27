# 配置CSS和JS预处理器

正确使用CSS预编译器(例如Sass)和JS预编译器、转换编译器，可以更好的加快的你的开发进度。现在就学着开始配置它们吧。

**长话短说**

* 预编译器可以提供浏览器不支持的特性，比如说CSS变量。
* 如果使用预编译器，请确保你的源资源文件与使用Source Maps渲染转换后的文件已创建好映射关系。
* 确保你的浏览器支持Source Maps。
* 使用支持的预编译器去自动生成Source Maps。

> [Source maps](http://www.w3cplus.com/tools/source-maps-101.html)提供了一种语言无关的从产品代码到我们所写的原程序代码的映射方式。

> [Java Script Source Map 详解](http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html)

## 什么是预编译器？

预编译器可以获取任意一个资源文件并且转换为浏览器无法识别的信息。

如编译为CSS，预编译器常增加一些原生CSS并不支持（起码至今）的新特性：CSS变量、嵌套等等。最知名的有[Sass](http://sass-lang.com/)，[Less](http://lesscss.org/)和[Stylus](http://stylus-lang.com/)。

如编译为JavaScript，预编译器不仅可以转换（编译）一种完全不同的语言为JavaScript，还可以将一种超前或新语法语言将至当前语法标准。最知名的有[CoffeeScript](http://coffeescript.org/)和ES6（如[Babel](https://babeljs.io/)）。

## 调试和编辑预编译内容

当你每次在Chrome浏览器中使用DevTools编辑CSS或调试JS时，会有一个显而易见的问题：你所发现的问题并不能定位到源文件中，这真的无法帮助你解决问题。

绕其道而行之，绝大多数现代预编译程序都支持一个特性，叫做Source Maps（资源映射）。

### 什么是Source Maps？

Source Map就是一个JSON格式的信息文件，它记录着源文件和压缩版文件之间的关联信息。当你编译文件到生产环境时，一般都会压缩和重组JavaScript文件，此时便生成一个资源映射文件，用以记录源文件内容信息。

### Source Map如何工作？

在每次生成CSS文件时，CSS预编译器会在编译CSS的同时生成一个资源映射文件（.map）。该资源映射文件采用JSON格式，定义了CSS压缩文件和源CSS文件每一行对应关系的信息记录。

每个CSS文件都包含一个资源映射文件的URL路径，嵌在文件最后一行的的特殊注释中：

```
/*# sourceMappingURL=<url> */
```

例如，下例给出一个Sass的资源映射文件，`styles.scss`：

```
%$textSize: 26px;
$fontColor: red;
$bgColor: whitesmoke;
h2 {
    font-size: $textSize;
    color: $fontColor;
    background: $bgColor;
}
```

Sass生成一个包含`sourceMappingURL`注解的CSS文件`styles.css`：

```
h2 {
  font-size: 26px;
  color: red;
  background-color: whitesmoke;
}
/*# sourceMappingURL=styles.css.map */
```

资源映射文件里的内容：

```
{
  "version": "3",
  "mappings":"AAKA,EAAG;EACC,SAAS,EANF,IAAI;EAOX,KAAK"
  "sources": ["sass/styles.scss"],
  "file": "styles.css"
}
```

## 确保web服务器可以支持Source Maps

部分网路服务器，如Google App Engine，需要在服务器上对每个文件都显式配置。既然如此，需要使用`application/json`的内容格式（MIME）的映射文件，但是Chrome浏览器还支持[其他内容格式](https://stackoverflow.com/questions/19911929/what-mime-type-should-i-use-for-javascript-source-map-files)，比如说`application/octet-stream`。

### 扩展阅读: Source mapping 之 自定义头

如果不想在文件中添加扩展注释，你可以在压缩js文件中使用`HTTP头`字段，它会告诉DevTools资源映射文件的位置。这要求配置或自定义你的Web服务器，这不在本文的讨论范围。

```
X-SourceMap: /path/to/file.js.map
```

与注释一样，HTTP头的方式会告知DevTools和其他工具资源映射文件的位置信息。除此之外，该方式还可以获取资源映射文件反馈的问题信息，而单行注释并不支持。

## 支持的预编译器

几乎当下所有的JS编译器都有生成资源映射文件的选项，包括`Coffeescript`,`TypeScript`,`JSX`等等。另外，你可以在Node服务器中使用映射资源文件，在CSS中使用Sass,Less等预编译器，使用[browserify](http://blog.fens.me/nodejs-browserify/)（一款可以跑在浏览器上的Node程序）来实现前端js直接运行node服务器程序，还可以使用压缩工具（如`uglify-js`）生成整齐代码的多级别资源映射文件。

### JavaScript
| Compiler      |  Command      | Instructions          |
|:-------------:|:-----------:  |:-------------:        |
|[CoffeeScript](http://coffeescript.org/#source-maps)   | $ coffee -c square.coffee -m          |-m(--map)生成一个.map的资源映射文件|
|[TypeScript](http://www.typescriptlang.org/)     | $ tsc -sourcemap square.ts            | -sourcemap生成带注释的source map|
|[Traceur](https://github.com/google/traceur-compiler/wiki/SourceMaps)	    | $ traceur --source-maps=[file or inline] | `--source-maps=file`,生成的每个`.js`文件都有一个对应的`.map`文件; `source-maps='inline'`,生成的每个`.js`文件结尾处都会增加map文件的注释|
|[Babel](https://babeljs.io/docs/usage/cli/#compile-with-source-maps)	        | $ babel script.js --out-file script-compiled.js --source-maps|	使用`--source-maps`或`-s`生成Source Maps. 使用`--source-maps inline`生成行内Source Maps.|
|[UglifyJS](https://github.com/mishoo/UglifyJS2)	    | $ uglifyjs file.js -o file.min.js --source-map file.min.js.map	|一个为'file.js'生成映射文件的基础命令. 它也会自动加上注释|

### CSS

| Compiler      |  Command      | Instructions          |
|:-------------:|:-----------:  |:-------------:        |
|[Sass](http://sass-lang.com/)	|$ scss --sourcemap styles.scss styles.css	| Sass 3.3 版本以后支持 Source Maps|
|[Less](http://lesscss.org/)	|$ lessc styles.less > styles.css --source-map styles.css.map|	1.5.0版本之后可用. 查看[问题 #1050](https://github.com/less/less.js/issues/1050#issuecomment-25566463)详情.|
|[Stylus](https://learnboost.github.io/stylus/)	|$ stylus --sourcemaps styles.style styles.css	|This will embed the sourcemap as a base64 encoded string directly in the out file.|
|[Compass](http://compass-style.org/)	|$ sass --compass --sourcemap --watch scss:css	|Alternatively you can add `sourcemap: true` to your config.rb file.|
|[Autoprefixer](https://github.com/postcss/autoprefixer)|		|点击链接查看明细|

### Source Maps 和 DevTools

想必现在你已经知道资源映射文件如何配置，你也许会乐意了解DevTools，因为它内置支持基于映射文件的CSS和JS。

### 编辑CSS预处理器

点击此链接[Edit Sass, Less or Stylus](https://developers.google.com/web/tools/chrome-devtools/inspect-styles/edit-styles)查看如何正确使用DevTools去编辑、刷新CSS样式表。

### 编辑和调试JavaScript预处理文件

学习怎样在Sources面板中调试、编译、转换JavaScript[Map Preprocessed Code to Source Code](https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps).