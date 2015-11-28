---
layout: post
title: "如何重新搭建一个已经存在的Octopress博客"
date: 2015-11-27 22:46
comments: true
categories: blog
---

```bash
$ git clone git@github.com:username/username.github.com.git
$ cd username.github.com
username.github.com$ git checkout source
username.github.com$ mkdir _deploy
username.github.com$ cd _deploy
username.github.com/_deploy$ git init
username.github.com/_deploy$ git remote add origin git@github.com:username/username.github.com.git
username.github.com/_deploy$ git pull origin master
username.github.com/_deploy$ cd ..
username.github.com$
```