---
title: Big Data Systems Lab Session Running Hadoop on a Single Node
tags: Big Data
categories: Linux
abbrlink: e8018068
date: 2020-02-21 15:06:56
---
{% note info %}
针对第三周实验的一些简单个人理解，有错误请指出。
{% endnote %}
# 1- Initial system setup
1. `whoami`: 显示当前用户
虚拟机进入时默认为root。
2. `su hduser`: su命令用于切换为`hduser`用户(hadoop user为该hadoop实例下自带的用户)
3. `cd ~`: 进入当前用户的根目录，如果当前是root用户，则进入`/root/`，如果当前是hduser，则进入`/home/hduser`,其中`/`代表整个虚拟机的根路径
4. `ssh-keygen -t rsa -P ""`: `ssh-keygen`用来生成密钥对。`-t rsa`指密钥类型为rsa, `-P`提供旧密语（类似默认密码）
生成的密钥默认位于`~/.ssh/`目录下，有两个文件，`id_rsa`是私钥，`id_rsa.pub`是公钥（`.ssh`代表隐藏文件，基于安全目的）
私钥不要泄漏出去，公钥则可以随意对外发布。用公钥进行加密的数据，只能用私钥才能解密。
使用ssh是为了使当前虚拟机与`localhost`建立安全连接（类似两台不同主机，不同服务器之间），还能免去输入密码，提高登录速度。
5. `cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys`: 把公钥内容添加到需要免密登录的主机中，这里`$HOME`和`~`的效果是一样的
> 如果想同时配置多个ssh密钥对，例如还要同时连接gitlab, github，需要手动配置config文件指定使用哪个密钥，这里留个坑，以后再补充。
6. `ssh localhost`: 刚才建立密钥对，就是为了连接`localhost`
7. `echo $HADOOP_HOME`: 这里用来显示`$HADOOP_HOME`环境变量值，指定`Hadoop`运行环境的路径
`~/.bashrc`这里储存了当前用户下的所有环境变量，只会对当前用户有效，每次启动`shell`自动被读取
8. `source .bashrc`: 运行此命令，使新建立的环境变量在当前shell中起作用，否则只能下次启动shell时激活该环境变量。
# 2- Setting up Hadoop and HDFS
{% note info %}
这一部分主要是配置`Hadoop`存储数据文件的路径，监听端口。
`hdfsTMP`用来储存临时文件
{% endnote %}
1. `nano core-site.xml`: 同`vi/vim`作用类似，文本编辑器，编辑`core-site.xml`文件。
这里使用`nano -w core-site.xml`命令更好，防止自动换行，造成不必要的错误。
常用操作：`Ctrl+O`(保存), `Ctrl+X`(退出), `Ctrl+C`(取消操作), `Ctrl+W`，搜索, 想再次搜索相同的字符串，按`Alt+W`
`vi/vim core-site.xml`: 常用操作：`i`(进入编辑模式)，`ESC`(退出编辑模式)，`:wq`(保存并退出)，`:q`(退出不保存)，`:q!`(强制退出)
2. `mkdir -p ~/hdfsTMP/namenode`: `-p`递归创建多个目录
3. `unset HADOOP_OPTS`: 清除环境变量`$HADOOP_OPTS`
# 3- Formatting HDFS
{% note info %}
创建Hadoop file system
{% endnote %}
1. `start-all.sh`: 没有权限时需要使用`chmod u+x 文件名.sh`来给可执行权限，不过该实验不用。
bash脚本执行方法：当前目录下，`./start-all.sh` 或 `sh start-all.sh`
# 4- Uploading data to HDFS
# 5- Creating a MapReduce Java application
这里有个坑，
`hadoop jar OurMapReduceJob.jar org.myorg.WordCount hdfsbook.txt output`跑完之后会报找不到main方法的错，原因是环境变量中的引号可能是中文的，回去检查一下。
