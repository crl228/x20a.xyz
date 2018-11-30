---
title: Ubuntu_Java环境配置
date: 2018-03-16 16:51:49
updated: 2018-03-16 16:51:49 
tags: [常用,笔记]
categories: 笔记
---

目前生产环境和测试环境机器使用都是JDK8，阿里云新增机器也统一使用Ubuntu16.04，记录下其中Java环境的安装。

### 安装Default JRE/JDK

Ubuntu上最快捷方便的方式是直接使用已经被打包进来的JDK，当前默认是OpenJDK 8，虽然因为各种原因我并没有使用。

```bash
sudo apt-get update
sudo apt-get install default-jre
sudo apt-get install default-jdk
```

### 安装Oracle JDK

如果想通过apt的方式来安装Oracle JDK，需要增加Oracle的PPA。

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

### 管理Java版本

假如我们机器上安装了多个Java版本，很有可能需要对他们进行一下管理或者切换。

```bash
sudo update-alternatives --config java
```
然后根据提示选择列表里我们需要的版本，切换它为默认的Java环境

### 配置环境变量

```bash
sudo vim /etc/environment
JAVA_HOME="/usr/lib/jvm/java-8-oracle"
source /etc/environment
echo $JAVA_HOME
```
