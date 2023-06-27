# 适用于 Linux 的 Windows 子系统（WSL）

*Summarized on 2023.06.27 by [YanseaTan](https://yansea.cc)*

## 安装 Linux

以管理员身份打开 PowerShell，输入(默认安装 Ubuntu)

`wsl --install`

使系统使用发行版的首选包管理器定期更新和升级包

`sudo apt update && sudo apt upgrade`

## 卸载 Linux

查看当前环境安装的 wsl

`wsl --list`

注销（卸载）当前安装的 wsl

`wsl --unregister LinuxName`

## 安装软件

`sudo apt install gcc`

`sudo apt install unzip`

`sudo apt install cmake`

`sudo apt install net-tools`

## 卸载软件

删除已安装包（不保留配置文件）

`sudo apt-get purge gcc`

删除为了满足依赖而安装的，但现在不再需要的软件包（包括已安装包），保留配置文件

`sudo apt-get autoremove gcc`

只删除已经过期的 deb

`apt-get autoclean`

## 常用命令

查看当前路径

`pwd`

当前位置下目录

`ls`

创建文件夹

`mkdir fileName`

删除文件夹和其中的文件

`rm -rf`