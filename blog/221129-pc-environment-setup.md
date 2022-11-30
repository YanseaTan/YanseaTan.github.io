# PC 环境搭建

*Summarized on 2022.11.29 by [YanseaTan](https://yansea.cc)*

## 工具

VSCode 下载链接 az*.net 替换为 `vscode.cdn.azure.cn`，记得勾选右键扩展

github ssh 相关：

`ssh-keygen -t rsa -C "yanseatan@163.com"`

win: `clip < ~/.ssh/id_rsa.pub`

mac: `pbcopy < ~/.ssh/id_rsa.pub`

`ssh -T git@github.com`

## C++

添加 MinGW 的 bin 子目录到 PATH 环境变量中

## python

删除所有包：

`pip freeze > python_modules.txt`

`pip uninstall -r python_modules.txt -y`