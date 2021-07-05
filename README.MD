# 初识nginx

### nginx源码安装

环境准备：

- centos版本大于2.6，因为nginx依赖Linux的一个epoll函数；查看Linux服务器的版本信息，命令：`uname -a`

```sh
uname -a
Linux iZwz9gptd6bqapsj3bih7iZ 4.18.0-193.14.2.el8_2.x86_64 #1 SMP Sun Jul 26 03:54:29 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

- Linux服务器有网络，可以通过`ping` 命令来看下有没有网络：

  ```sh
  ping www.baidu.com
  ```

- 关闭防火墙

  ```sh
  # 关闭防火墙，重启Linux服务器时，会重新启动防火墙
  systemctl stop firewalld
  # 永久关闭，即使重启Linux服务器，也不会重启防火墙
  systemctl disable firewalld
  
  ```

  

- 确认停用SELinux，命令`sestatus`

  ```sh
  sestatus
  SELinux status:                 disabled
  ```

  停用的方式：

  ```sh
  vim /etc/selinux/config
  
  # This file controls the state of SELinux on the system.
  # SELINUX= can take one of these three values:
  #     enforcing - SELinux security policy is enforced.
  #     permissive - SELinux prints warnings instead of enforcing.
  #     disabled - No SELinux policy is loaded.
  SELINUX=disabled
  # SELINUXTYPE= can take one of these three values:
  #     targeted - Targeted processes are protected,
  #     minimum - Modification of targeted policy. Only selected processes are protected. 
  #     mls - Multi Level Security protection.
  SELINUXTYPE=targeted
  ```

- 依赖一下工具：

  - GCC编译器

    ```sh
    # 安装
    yum install -y gcc
    # 查看安装是否成功
    gcc --version
    ```

    

  - PCRE 兼容正则表达式的库

    ```sh
    # 安装
    yum install -y pcre-devel
    # 查看安装是否成功
    rpm -qa pcre-devel
    ```

  - zlib 压缩算法

    ```sh
    # 安装
    yum install -y zlib-devel
    # 查看安装是否成功
    rpm -qa zlib-devel
    ```

  - OpenSSL 保密可靠性

    ```sh
    # 安装
    yum install -y openssl-devel
    # 查看安装是否成功
    rpm -qa openssl-devel
    ```

  - 同时安装以上依赖的工具：

    ```sh
    yum install -y gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel
    ```

  - 同时查看devel工具是否安装成功：

    ```sh
    rpm -qa pcre pcre-devel zlib zlib-devel openssl openssl-devel
    ```

    **注意：`rpm`是软件包管理工具，`yum`是基于`rpm`的包管理工具**

开始源码安装：

- 官网获取下载地址，通过`wget`命令进行安装

  ```sh
  wget https://nginx.org/download/nginx-1.20.1.tar.gz
  ```

- 下载的资源放在指定的目录下，方便资源管理，比如在：

  ```sh
  mkdir -p nginx/core
  # 资源tar.gz包放在下面目录
  /root/nginx/core
  ```

- 解压nginx安装包，获取nginx资源目录文件

  ```sh
  tar -zxf nginx-1.20.1.tar.gz
  ```

- 进入nginx资源目录下，执行configure进行安装配置nginx

  可以加参数进行配置，因为还不会nginx的安装配置，所以直接执行，是最简单的配置

  安装的同时检查Linux系统环境，nginx依赖的环境、工具、软件是否都存在

  ```sh
  ./configure
  ```

- 执行相关命令：

  - make命令编译

  - make install命令安装

    由于上一步在configure同级目录下生成了Makefile文件

    ```sh
    make && make install
    ```

- 查看nginx安装到哪个目录中（nginx默认配置安装到哪里了）

  ```sh
  whereis nginx
  nginx: /usr/local/nginx
  ```

- 启动nginx（其中sbin是二进制目录，里面的nginx是对应的二进制文件）

  ```sh
  # 来到nginx安装目录
  cd /usr/local/nginx
  # 查看nginx目录中有哪些文件
  ll
  drwxr-xr-x 2 root root 333 Jul  5 20:39 conf
  drwxr-xr-x 2 root root  40 Jul  5 20:39 html
  drwxr-xr-x 2 root root   6 Jul  5 20:39 logs
  drwxr-xr-x 2 root root  19 Jul  5 20:39 sbin
  # 启动nginx，默认是80端口
  ./sbin/nginx
  
  ```

  

