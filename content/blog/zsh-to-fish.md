+++
date = "2016-03-16T14:45:35+08:00"
title = "zsh to fish"

+++

顺手的工具有不少，原来用`zsh`虽然很顺手，但总觉得有点慢，索性试了试`fish`


### zsh 和 fish 对比

#### zsh 

* 插件多，配置丰富 
* 插件多了慢

#### fish 

* 开箱即用 
* 不兼容bash语法

#### 我需求的功能

* autosuggestion
* autojump
* theme
* git

虽然fish的语法更加接近一名编程语言，奈何大多数工具脚本都是bash写的，而服务器上更不可能为了方便而安装fish,还是自己电脑上用好了

不过发现`python` 的virtualenvl 的activate的有fishshell 支持的！！

### 一些语法改动

PATH 写法

bash:

```bash
export PATH="/usr/local/bin:$PATH"
```

fish:

```fish
set PATH $PATH /usr/local/bin
```

### fish配置

使用`fish_config`，新开一个网页来配置主题，函数

<img src="/img/fish_config.png" alt="fish_config">

### fish插件管理工具 `omf`

#### 安装omf

`curl -L https://get.oh-my.fish | fish`

#### 使用新主题

`omf install robbyrussell` 

`omf theme robbyrussell` 

这个主题对git的支持很完善

<img src="/img/robbyrussell.png" alt="robbyrussell">

错误的也会有红色标记， 同时也会根据历史和命令给出建议

<img src="/img/cut_1.png" alt="cut_1">


#### 提供对`bash` 脚本支持

安装`bass`

`git clone https://github.com/edc/bass.git`
`make install`

bass使用

<img src="/img/bass.png" alt="bass">
