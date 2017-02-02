# Set Up Your Build Tools

Build your multi-device site from the ground up. Learn how to speed up development and create a fast loading site with a set of build process tools. Every site should have a development version and a production version.

The development version has all the HTML, CSS, JS and image files that make up your site in a clean format that you are happy to work on.

A production version will take these files, minify them, concatenate / merge them and optimise files like images.
Web developers have to think about a million things at once and the build step is one of the most critical, yet most cumbersome to get started with. You have to work out all the tasks that you need to automate such as: Image compression, CSS minification, JavaScript concatenation, Responsive testing, Unit testing, the list goes on...

Follow this guide to learn the best way to structure your workflow so that the sites you create already follow all the best practices from the minute you start.

**TL;DR**

* Your build process tools must optimise for performance; they should automatically minify and concatenate JavaScript, CSS, HTML, and images.
* Use tools like LiveReload to make your development process smoother.

Before you start coding, you need to consider how to optimise and build the production version of your site. Setting up this workflow from the start prevents any nasty surprises at the end of the project and you can add tools into your workflow that speed up your development, doing the monotonous tasks for you.

## What is a build process?

A build process is a set of tasks which run over your projects files, compiling and testing code during development and used to create the deployment version of your site. Your build process shouldn't be a set of tasks you run at the end of your development workflow.

The most popular tools for implementing a build process are Gulp and Grunt, both of which are command line tools. If you have no experience of either, use Gulp, we use it for Web Starter Kit and recommend you do the same.

There are tools which have GUIs and may be a bit easier to get to grips with but will be less flexible.

|Supported Platforms & Tool Name||
|:---|:---|
|OS X / Windows| [Prepros](http://alphapixels.com/prepros/) |
|OS X|	[CodeKit](https://incident57.com/codekit/) |
|OS X|	[HammerForMac](http://hammerformac.com/) |

## What tasks should be in a build process?

In the following sections, we're going to look at the most common tasks you should have in your build process and recommend tasks for Grunt and Gulp.

This requires a lot of trial and error to get each piece set-up the way you want and can be daunting if you are new to build processes.

For a good example of a build process, check out the getting started guide for Web Starter Kit, which goes through how to use Web Starter Kit and explains what each of the commands in the Gulp file do. This can be used as a quick way to get set-up and then you can make changes if needed.

If you are looking to create your own build process and you're new to Gulp or Grunt, the quick start guides will be the best place to get into on installing and running your first build process:

* Grunt Getting Started
* Gulp Getting Started

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