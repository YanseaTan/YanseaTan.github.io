# PC 环境搭建

*Summarized on 2022.11.29 by [YanseaTan](https://yansea.cc)*

## 工具

### VSCode

下载链接 az*.net 替换为 `vscode.cdn.azure.cn`，记得勾选右键扩展

### github ssh

`ssh-keygen -t rsa -C "yanseatan@163.com"`

win: `clip < ~/.ssh/id_rsa.pub`

mac: `pbcopy < ~/.ssh/id_rsa.pub`

`ssh -T git@github.com`

### QT

[下载器地址](https://download.qt.io/official_releases/online_installers/)

下载器设置中添加用户镜像源：`https://mirrors.tuna.tsinghua.edu.cn/qt/online/qtsdkrepository/windows_x86/root/qt/` 提升下载速度

安装时选中 MinGW 组件就够了，Tools 里基本也都不用选

## C++

添加 MinGW 的 bin 子目录到 PATH 环境变量中

## python

删除所有包：

`pip freeze > python_modules.txt`

`pip uninstall -r python_modules.txt -y`