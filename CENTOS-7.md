# CentOS-7

## 常用运维命令

* 配置阿里源，`yum`源配置目录为`/etc/yum.repos.d/`

  1. 安装`wget`命令

     ```shell
     yum install wget
     ```

  2. 进入`yum`源配置目录

     ```shell
     cd /etc/yum.repos.d/
     ```

  3. 备份官方源

     ```shell
     mv CentOS-Base.repo CentOS-Base.repo.bak
     ```

  4. 下载阿里源

     ```shell
     wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
     ```

  5. 清除旧`yum`源的缓存

     ```shell
     yum clean all
     ```

  6. 更新`yum`源缓存

     ```shell
     yum makecache
     ```

* 防火墙设置

  ```shell
  # 查看防火墙状态
  systemctl status firewalld
  # 停用防火墙
  systemctl stop firewalld
  # 关闭防火墙
  systemctl disable firewalld
  ```

* 网络设置

  编辑文件`/etc/sysconfig/network-scripts/ifcfg-ens0s3`

  ```shell
  BOOTPROTO=static # 静态 IP 类型
  IPADDR=10.10.10.100 # IP 地址
  GATEWAY=10.10.10.1 # 网关
  NETMASK=255.255.255.0 # 子网掩码
  DNS1=10.10.10.1 # DNS直接设置为网关
  ```

* Hostname 设置

  1. 修改`/etc/sysconfig/network`文件中的`HOSTNAME`值。

     ```shell
     sudo vim /etc/sysconfig/network
     # 修改HOSTNAME的值
     HOSTNAME=my.new-hostname.server
     ```

  2. 修改`/etc/hosts`文件。

     ```shell
     10.10.10.10 my.new-hostname.server hostname
     ```

  3. 执行`hostname`命令

     ```shell
     hostnamectl set-hostname my.new-hostname.server
     ```

  4. 重启网络

  ```shell
  /etc/init.d/network restart
  ```

* 将普通用户加入到 `sudoer`

  XXX is not in the sudoers file.  This incident will be reported.

  1. 切换到 root 用户下
  2. 编辑 `/etc/sudoers`，找到 `root ALL=(ALL) ALL`，在其下面添加 `xxx ALL=(ALL) ALL`, xxx 即为添加权限的用户。

* 查看网络接口的UUID

  ```shell
  nmcli connection show
  ```

* 重启网络服务

  ```shell
  service network restart
  ```

* 安装 `ipconfig`工具

  ```shell
  yum install -y net-tools
  ```

* 安装 `rsync` 工具

  ```shell
  yum install -y rsync
  ```

  

* .

* .

## VIM 设置

VIM 的全局配置文件在 `/etc/vim/vimrc`或者`/etc/vimrc`，对所有用户生效。用户个人的配置在 `~/.vimrc`

### 基本设置

```shell
set nocompatible
syntax on
set showmode
set showcmd
set encoding=utf-8
set t_Co=256
set autoindent
set tabstop=2
set softtabstop=2
set number
```



## 常用脚本

* 集群分发脚本 `xsync`

  ```shell
  #!/bin/bash
  
  pcount=$#
  if((pcount==0)); then
    echo no args;
    exit;
  fi
  
  p1=$1
  fname=`basename $p1`
  echo fname=$fname
  
  pdir=`cd -P $(dirname $p1); pwd`
  echo pdir=$pdir
  
  user=`whoami`
  
  for ((host=12;host<14;host++)); do
    echo --------------- hadoop-$host --------------
    rsync -rvl $pdir/$fname $user@hadoop-$host:$pdir
  done
  ```

* .

* .

* .

* .

## 常用软件安装

* 安装 MySQL

  1. 检查系统是否装有 MySQL

     ```shell
     rpm -qa | grep mysql
     ```

     返回空值，说明没有安装。

  2. 下载并安装 MySQL 的 repo 源

     ```shell
     wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
     sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
     ```

  3. 安装 MySQL

     ```shell
     sudo yum install mysql-server
     ```

  4. 启动 MySQL 服务

     ```shell
     sudo systemctl start mysql
     ```

* 1

* 1

* 1

* 