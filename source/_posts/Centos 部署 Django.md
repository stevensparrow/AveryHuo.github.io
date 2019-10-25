---
title: Centos 部署 Django
categories:
- Python Web
tags: 
- Python
- Note
- Django
---

### 1. 下载必要库

```
yum -y groupinstall "Development tools"
```

### 2. 下载最新SQLITE

到SQLite官网的下载页面：https://www.sqlite.org/download.html  这里是最新的版本，我们就安装它吧。

```
wget https://www.sqlite.org/2017/sqlite-autoconf-3160200.tar.gz
tar zxvf sqlite-autoconf-3160200.tar.gz
cd sqlite-autoconf-3160200

./configure
make
sudo make install
```

以默认方式安装后，会把编译好的二进制文件安装到 /usr/local/lib， 把头文件sqlite3.h sqlite3ext.h安装到/usr/local/include。

用这两条命令确认一下已成功安装到这里：

```
ls -l /usr/local/lib/*sqlite*
ls -l /usr/local/include/*sqlite*
```

### 3.Python 安装

```
wget https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tgz
tar -zxvf Python-3.6.6.tgz

#进入解压好的目录
sudo LD_RUN_PATH=/usr/local/lib ./configure --enable-optimizations
sudo LD_RUN_PATH=/usr/local/lib make altinstall
```

