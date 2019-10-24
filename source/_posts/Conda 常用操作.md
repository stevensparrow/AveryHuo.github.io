---
title: Conda 常用操作
categories:
- Python Web
tags: 
- Python
- Note
- Django
- Conda
---


### Conda介绍

> Conda 是一个开源的软件包管理系统和环境管理系统，用于安装多个版本的软件包及其依赖关系，并在它们之间轻松切换。 Conda 是为 Python 程序创建的，适用于 Linux，OS X 和Windows，也可以打包和分发其他软件。

### 下载&安装
> conda官网：https://conda.io/miniconda.html

linux或mac ox版本：

```
wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

chmod 777 Miniconda3-latest-Linux-x86_64.sh #给执行权限
bash Miniconda3-latest-Linux-x86_64.sh #运行
```

> 当命令行前面出现(base)的时候说明现在已经在conda的环境中了。这时候输入conda list 命令就有反应了


###  添加频道

官方频道
 
```
conda config --add channels bioconda
conda config --add channels conda-forge
```

 清华镜像
  
``` 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
```

其他：

``` 
conda config --add channels genomedk
```

显示安装的频道

``` 
 conda config --set show_channel_urls yes 
 ``` 
 
查看已经添加的channels

``` 
conda config --get channels
``` 

已添加的channel在哪里查看

``` 
vim ~/.condarc
``` 






