# 在虚拟机中建立 CentOS 服务器

*Summarized on 2023.07.04 by [YanseaTan](https://yansea.cc)*

- [在虚拟机中建立 CentOS 服务器](#在虚拟机中建立-centos-服务器)
  - [安装虚拟机](#安装虚拟机)
  - [查询 ip 地址](#查询-ip-地址)
  - [传输文件](#传输文件)
  - [替换国内镜像](#替换国内镜像)
    - [备份原有的 YUM 源文件](#备份原有的-yum-源文件)
    - [下载国内源的 YUM 配置文件](#下载国内源的-yum-配置文件)
    - [清理 YUM 缓存](#清理-yum-缓存)
    - [验证新源是否可用](#验证新源是否可用)
    - [安装 SCL 源相关软件包](#安装-scl-源相关软件包)
    - [检查并备份现有的 .repo 文件](#检查并备份现有的-repo-文件)
    - [配置国内源](#配置国内源)
    - [刷新 YUM 缓存](#刷新-yum-缓存)
  - [安装软件包](#安装软件包)
    - [unzip](#unzip)
    - [cmake3](#cmake3)
    - [gcc 7.3.1](#gcc-731)
    - [netstat](#netstat)
    - [git](#git)
    - [wget](#wget)
    - [htop](#htop)
  - [使用 vscode 进行 SSH 连接](#使用-vscode-进行-ssh-连接)
  - [编译过程](#编译过程)
  - [打开服务器网络端口](#打开服务器网络端口)
  - [解决 Downloading VS Code Server 问题](#解决-downloading-vs-code-server-问题)

## 安装虚拟机

使用 VMware 16 安装 CentOS 7.9，虚拟机最低配置建议为 4G 内存以及 4 核心处理器，注意在安装过程中需要进行网络连接。

## 查询 ip 地址

打开网卡配置文件，将 ONBOOT 修改为 yes，每次启动系统时同时启动网卡。

`vi /etc/sysconfig/network-scripts/ifcfg-ens33`

重启网络服务。

`service network restart`

输入`ip addr`查看 ip 地址。

若重启网络服务失败，首先查看 VM 网络相关服务（VMware DHCP Service，VMware NAT Service）是否在运行，如果在运行则尝试先关闭 NetworkManager 服务。

`systemctl stop NetworkManager`

`systemctl restart network.service`

`service network restart`

## 传输文件

使用 xftp7 进行连接和传输，需填写 ip 地址以及用户名和密码。

也可以直接使用 vscode SSH 连接后进行文件的上传和下载。

## 替换国内镜像

### 备份原有的 YUM 源文件

`sudo cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak`

### 下载国内源的 YUM 配置文件

`sudo wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo`

### 清理 YUM 缓存

`sudo yum clean all`

`sudo yum makecache`

### 验证新源是否可用

`sudo yum repolist`

### 安装 SCL 源相关软件包

`yum install -y centos-release-scl centos-release-scl-rh`

### 检查并备份现有的 .repo 文件

`cp /etc/yum.repos.d/CentOS-SCLo-scl.repo /etc/yum.repos.d/CentOS-SCLo-scl.repo.bak`

`cp /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo.bak`

### 配置国内源

`vim /etc/yum.repos.d/CentOS-SCLo-scl.repo`

```ini
[centos-sclo-sclo]
name=CentOS-7 - SCLo sclo
baseurl=https://mirrors.aliyun.com/centos/7/sclo/x86_64/sclo/
gpgcheck=0
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SCLo
```

`vim /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo`

```ini
[centos-sclo-rh]
name=CentOS-7 - SCLo rh
baseurl=https://mirrors.aliyun.com/centos/7/sclo/x86_64/rh/
gpgcheck=0
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SCLo
```

### 刷新 YUM 缓存

`yum clean all && yum makecache && yum repolist`

## 安装软件包

### unzip

`yum install -y unzip`

### cmake3

`yum install -y epel-release`

`yum install -y cmake3`

### gcc 7.3.1

`yum install -y devtoolset-11-gcc*`

`yum install -y devtoolset-11-gdb`

`scl enable devtoolset-11 bash`

### netstat

`yum install -y net-tools`

### git

`yum install -y git`

### wget

`yum install -y wget`

### htop

`yum install -y htop`

## 使用 vscode 进行 SSH 连接

提前安装 C/C++、Remote-SSH、CMake Tools 等插件。

新建 SSH 连接，输入格式为 ssh root@ip地址，如：

`ssh root@192.168.19.129`

编辑配置文件 config，刷新，进行连接，输入密码，打开相应文件目录即可。

随后从 gitee 平台克隆 yunshan-server-v2 仓库，并在服务器端安装 CMake Tools 等插件。

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
        "RSA_PUBLIC_KEY_PATH":"/root/repo/yunshan-server-v2/atp_api/plugins/rsa_public_key.pem",
        "ATP_ENCRYPT_PASSWORD":"/root/repo/yunshan-server-v2/atp_api/lib/librsa_2048_encrypt.so"
        },
        "cmake.touchbar.advanced": {},
        "cmake.cacheInit": null
}
```

重新启动 vscode 进行连接，调出命令行，输入 CMake: Edit User-Local Cmake Kits，根据服务器实际文件路径填写 cmake-tools-kits 配置文件，保存后再进行 kit 选择。

```json
[
    {
      "name": "GCC 11 x86_64-redhat-linux",
      "compilers": {
        "C": "/opt/rh/devtoolset-11/root/usr/bin/gcc",
        "CXX": "/opt/rh/devtoolset-11/root/usr/bin/g++"
      },
      "isTrusted": true
    }
]
```

选择编译对象为 all，然后点击 build 进行编译。

编译完成后将 ctp 官方 lib 文件复制到 `./build/policyserver/` 下，再将如图所示的部分库文件复制到 `./build/mdserver/` 路径下。

将对应的配置文件（config 文件夹以及 config.json 文件）拷贝至 `./build/policyserver/` 以及 `./build/mdserver/` 目录下，并在各自目录下创建 log 文件夹。

随后即可选择 target 并运行。

## 打开服务器网络端口

通过如下命令查看对应端口是否打开。

`firewall-cmd --query-port=8089/tcp`

打开端口。

`firewall-cmd --zone=public --add-port=8089/tcp --permanent`

重启防火墙。

`firewall-cmd --reload`

## 解决 Downloading VS Code Server 问题

从 output 的 Remote SSH 中找到并复制 commit_id。

进入或创建 Linux 文件路径 `.vscode-server/cli/server/Stable-${commit_id}/server/`

通过下述命令下载所需要的包。

`wget https://vscode.cdn.azure.cn/stable/${commit_id}/vscode-server-linux-x64.tar.gz`

然后再进行解压缩，更换路径的操作。

`tar -zxvf vscode-server-linux-x64.tar.gz -C ./`

`mv vscode-server-linux-x64/* .`

`touch 0`

重启 vscode 进行 SSH 连接。