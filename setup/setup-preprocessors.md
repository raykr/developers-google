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

### Source Map是怎么工作的？

For each CSS file it produces, a CSS preprocessor generates a source map file (.map) in addition to the compiled CSS. The source map file is a JSON file that defines a mapping between each generated CSS declaration and the corresponding line of the source file.

Each CSS file contains an annotation that specifies the URL of its source map file, embedded in a special comment on the last line of the file:

```
/*# sourceMappingURL=<url> */
```

For instance, given an Sass source file named styles.scss:

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

Sass generates a CSS file, styles.css, with the sourceMappingURL annotation:

```
h2 {
  font-size: 26px;
  color: red;
  background-color: whitesmoke;
}
/*# sourceMappingURL=styles.css.map */
```

Below is an example source map file:

```
{
  "version": "3",
  "mappings":"AAKA,EAAG;EACC,SAAS,EANF,IAAI;EAOX,KAAK"
  "sources": ["sass/styles.scss"],
  "file": "styles.css"
}
```

## Verify web server can serve Source Maps

Some web servers, like Google App Engine for example, require explicit configuration for each file type served. In this case, your Source Maps should be served with a MIME type of application/json, but Chrome will actually accept any content-type, for example application/octet-stream.

### Bonus: Source mapping via custom header

If you don't want an extra comment in your file, use an HTTP header field on the minified JavaScript file to tell DevTools where to find the source map. This requires configuration or customization of your web server and is beyond the scope of this document.

```
X-SourceMap: /path/to/file.js.map
```

Like the comment, this tells DevTools and other tools where to look for the source map associated with a JavaScript file. This header also gets around the issue of referencing Source Maps in languages that don't support single-line comments.

## Supported preprocessors

Just about any compiled to JavaScript language has an option to generate Source Maps today – including Coffeescript, TypeScript, JSX and many more. You can additionally use Source Maps on the server side within Node, in our CSS with via Sass, Less and more, using browserify which gives you node-style require abilities, and through minification tools like uglify-js which also adds the neat ability to generate multi-level Source Maps.

### JavaScript

Compiler	Command	Instructions
CoffeeScript	$ coffee -c square.coffee -m	The -m (--map) flag is all it takes for the compiler to output a source map, it will also handle adding the sourceMapURL comment pragma for you to the outputted file.
TypeScript	$ tsc -sourcemap square.ts	The -sourcemap flag will generate the map and add the comment pragma.
Traceur	$ traceur --source-maps=[file|inline]	With --source-maps=file, every output file ending in .js will have a sourcemap file ending in .map; with source-maps='inline', every output file ending in .js will end with a comment containing the sourcemap encoded in a data: URL.
Babel	$ babel script.js --out-file script-compiled.js --source-maps	Use --source-maps or -s to generate Source Maps. Use --source-maps inline for inline Source Maps.
UglifyJS	$ uglifyjs file.js -o file.min.js --source-map file.min.js.map	That is the very basic command needed to generate a source map for 'file.js'. This will also add the comment pragma to output file.

### CSS

Compiler	Command	Instructions
Sass	$ scss --sourcemap styles.scss styles.css	Source Maps in Sass are supported since Sass 3.3.
Less	$ lessc styles.less > styles.css --source-map styles.css.map	Implemented in 1.5.0. See issue #1050 for details and usage patterns.
Stylus	$ stylus --sourcemaps styles.style styles.css	This will embed the sourcemap as a base64 encoded string directly in the out file.
Compass	$ sass --compass --sourcemap --watch scss:css	Alternatively you can add `sourcemap: true` to your config.rb file.
Autoprefixer		Follow the link to see how to use it and absorb an input sourcemap.

### Source Maps and DevTools

Now that you've got Source Maps properly set up, you might be happy to learn that DevTools has built-in support for both CSS and JS based Source Maps.

### Editing preprocessed CSS

Head over to Edit Sass, Less or Stylus to learn more about how to edit and refresh styles linked to a source map directly within DevTools.

### Editing and debugging preprocessed JavaScript

Learn more about how to debug manified, compiled or transpiled JavaScript in the Sources Panel in Map Preprocessed Code to Source Code.