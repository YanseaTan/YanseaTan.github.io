# 系统环境搭建

*Summarized on 2022.11.29 by [YanseaTan](https://yansea.cc)*

## 工具

### VSCode

下载提速：

下载链接 az*.net 替换为 `vscode.cdn.azure.cn`，记得勾选右键扩展

使用 `code .` 打开文件夹：

Shift + Command + P，调起命令窗口，输入 `Shell Command`，下方出现 Install 'code' command in PATH 选项，点击以安装

### git

创建 SSH：

`ssh-keygen -t rsa -C "yanseatan@163.com"`

win: `clip < ~/.ssh/id_rsa.pub`

mac: `pbcopy < ~/.ssh/id_rsa.pub`

`ssh -T git@github.com`

克隆仓库地址写法：

`git clone git@github.com:YanseaTan/policy-client.git`

### QT

[下载器地址](https://download.qt.io/official_releases/online_installers/)

下载器设置中添加用户镜像源：`https://mirrors.tuna.tsinghua.edu.cn/qt/online/qtsdkrepository/windows_x86/root/qt/` 提升下载速度

## C++

添加 MinGW 的 bin 子目录到 PATH 环境变量中

## python

删除所有包：

`pip freeze > python_modules.txt`

`pip uninstall -r python_modules.txt -y`