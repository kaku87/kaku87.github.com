---
layout: post
title: "安装auto-fu.zsh让命令输入自动补全"
date: 2015-02-01 14:44
comments: true
categories: 
---
![](https://github.com/hchbaw/auto-fu.zsh/raw/readme/auto-fu.gif "")

 - 下载auto-fu.zsh

```bash
cd ~/.oh-my-zsh/custom/plugins
git clone https://github.com/hchbaw/auto-fu.zsh.git auto-fu
```

 - 执行zcompile

```bash
A=~/.oh-my-zsh/custom/plugins/auto-fu/auto-fu.zsh; (zsh -c "source $A ; auto-fu-zcompile $A ~/.zsh")
```

 - 添加下面的设置到zshrc中

```bash
## auto-fu.zsh stuff.
# source ~/.oh-my-zsh/custom/plugins/auto-fu/auto-fu.zsh
{ . ~/.zsh/auto-fu; auto-fu-install; }
zstyle ':auto-fu:highlight' input bold
zstyle ':auto-fu:highlight' completion fg=black,bold
zstyle ':auto-fu:var' postdisplay $'\n-azfu-'
zle-line-init () {auto-fu-init;}; zle -N zle-line-init
```
 - 重新编译zshrc

```bash
source ~/.zshrc
```

