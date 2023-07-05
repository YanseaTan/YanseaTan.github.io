# 在虚拟机中建立 CentOS 服务器

*Summarized on 2023.07.04 by [YanseaTan](https://yansea.cc)*

- [在虚拟机中建立 CentOS 服务器](#在虚拟机中建立-centos-服务器)
  - [安装虚拟机](#安装虚拟机)
  - [查询 ip 地址](#查询-ip-地址)
  - [传输文件](#传输文件)
  - [安装软件包](#安装软件包)
    - [unzip](#unzip)
    - [cmake3](#cmake3)
    - [gcc 7.3.1](#gcc-731)
    - [netstat](#netstat)
  - [使用 vscode 进行 SSH 连接](#使用-vscode-进行-ssh-连接)
  - [编译过程](#编译过程)
  - [打开服务器网络端口](#打开服务器网络端口)

## 安装虚拟机

使用 VMware 16 安装 CentOS 7.9，注意在安装过程中需要进行网络连接。

## 查询 ip 地址

打开网卡配置文件，将 ONBOOT 修改为 yes，每次启动系统时同时启动网卡。

`vi /etc/sysconfig/network-scripts/ifcfg-ens33`

重启网络服务。

`sudo service network restart`

输入`ip addr`查看 ip 地址。

## 传输文件

使用 xftp7 进行连接和传输，需填写 ip 地址以及用户名和密码。

## 安装软件包

### unzip

`yum install -y unzip`

### cmake3

`yum install -y epel-release`

`yum install -y cmake3`

### gcc 7.3.1

`yum install centos-release-scl`

`yum install devtoolset-7-gcc*`

`yum install devtoolset-7-gdb`

`scl enable devtoolset-7 bash`

### netstat

`yum install net-tools`

## 使用 vscode 进行 SSH 连接

提前安装 C/C++、Remote-SSH、CMake Tools 等插件。

新建 SSH 连接，输入格式为 ssh root@ip地址，如：

`ssh root@192.168.19.129`

编辑配置文件 config，刷新，进行连接，输入密码，打开相应文件目录即可。

随后在服务器端安装 CMake Tools 等插件。

## 编译过程

点击 CMake Tools 插件，设置，选择远端服务器，编辑 settings.json 文件，根据服务器实际文件路径进行填写。

```json
{
    "cmake.cmakePath": "/usr/bin/cmake3",
    "cmake.configureArgs":[
        "-DUSE_SIP_MD=OFF",
        "-DUSE_TDF_MD=ON",
        "-DUSE_CTP_MD=OFF",
        "-DUSE_ATP_MD=OFF",
        "ENABLE_RISK_CTRL=ON"
    ],
    "cmake.configureEnvironment": {
        "RSA_PUBLIC_KEY_PATH":"/root/server/yunshan_server_v2/atp_api/plugins/rsa_public_key.pem",
        "ATP_ENCRYPT_PASSWORD":"/root/server/yunshan_server_v2/atp_api/lib/librsa_2048_encrypt.so"
        },
        "cmake.touchbar.advanced": {}
}
```

重新启动 vscode 进行连接，调出命令行，输入 CMake: Edit User-Local Cmake Kits，根据服务器实际文件路径填写 cmake-tools-kits 配置文件，保存后再进行 kit 选择。

```json
[
  {
    "name": "GCC 4.8.5 x86_64-redhat-linux",
    "compilers": {
      "C": "/usr/bin/gcc",
      "CXX": "/usr/bin/g++"
    }
  },
  {
    "name": "GCC 7.3.1 x86_64-redhat-linux",
    "compilers": {
      "C": "/opt/rh/devtoolset-7/root/usr/bin/gcc",
      "CXX": "/opt/rh/devtoolset-7/root/usr/bin/g++"
    }
  }
]
```

点击 build 进行编译，编译完成后将必要的配置文件（xml、json、cfg 文件夹等）以及运行库文件（so）拷贝至 build/policyserver/ 目录下，随后即可选择 target 并运行。

## 打开服务器网络端口

通过如下命令查看对应窗口是否打开。

`firewall-cmd --query-port=8089/tcp`

打开端口。

`firewall-cmd --zone=public --add-port=8089/tcp --permanent`

重启防火墙。

`firewall-cmd --reload`