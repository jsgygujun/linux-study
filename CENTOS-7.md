# CentOS-7

## 常用运维命令

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

* 

* 