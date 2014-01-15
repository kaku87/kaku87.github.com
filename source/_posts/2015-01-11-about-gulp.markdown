---
layout: post
title: "gulp入门"
date: 2015-01-11 01:05
comments: true
categories: gulp
---

##概要
前端任务自动化工具

##官方网站
[gulpjs.com](gulpjs.com)

##相关知识
GoogleのWenStarterKit是用gulp来做的。

##环境
vagrant centos

##安装

	1. sudo yum -y install epel-release

	2. sodu yum -y install nodejs npm

		`node -v`确认node的版本号
		
		`npm -v`确认npm的版本号
		
	3. sudo npm install gulp -g

	 	`gulp -v`确认gulp的版本号

##gulp和grunt的区别


gulp         | grunt 
------------ | ------------- 
 插件少 		 |	插件多
8,398sta	 |	8,439starM
2013/6/30	 |	2011/9/18
gulpfie.js   |	Gruntfile.js
类似Node		 |类似JavaScript
Node的插件	 |	Grunt的插件

##和Grunt相比较的优点


1.配置文件比Grunt要少

2.比Grunt要快

##和Grunt相比的缺点

1.写法和Node接近，所以相对比较复杂

2.文档较少

##创建package.json
```
mkdir mysite
cd mysite 
npm init
npm install --save-dev gulp
npm -i -D gulp
rm -rf node_modules
npm install
```
##初识gulp.task()
```
var gulp = require('gulp');
	gulp.task('hello', function(){
		console.log('hello world!')
})

gulp.task('default', ['hello']);
```

	
##文件拷贝

把当前目录里的package.json文件拷贝到当前目录中的dist文件夹中。
```
var gulp = require('gulp');

gulp.task('copy', function() {
    gulp.src('./package.json')
      .pipe(gulp.dest('./dist'));
});

gulp.task('default',['copy']);
```	

##gulp的常用5种API

1. 定义task
```	
gulp.task('name',['tasks'], function() {
    // content
});
```	
2. 输入路径指定
```	
gulp.src('files')
  .pipe(name(''))
```	
3. 执行task
```	
gulp.task('foo', function() {
    gulp.run('bar');
});
```	
4. 输出路径指定
```	
.pipe(gulp.dest('folder'));
```	
5. 监视文件
```		
gulp.watch('files', function (event) {
	console.log('js file changed!!');
});
```	
详细API信息请参照这里   [github API doc](https://github.com/gulpjs/gulp/blob/master/docs/API.md)

##gulp task执行顺序

gulp的task默认为并行触发，若要顺序执行，要做如下处理。

1. 前面的task要写return
2. 后面的task要加第二参数，值为前面的task
```	
var gulp = require('gulp');

gulp.task('first', function() {
    return gulp.src('./package.json')
      .pipe(gulp.dest('./dist'));
});

gulp.task('second',['first'], function() {
    console.log('first task done!!');
});

gulp.task('default',['second']);
```	

