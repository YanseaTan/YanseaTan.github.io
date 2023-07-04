# 使用 QT 时的相关问题和解决方案

*Summarized on 2023.01.06 by [YanseaTan](https://yansea.cc)*

- [使用 QT 时的相关问题和解决方案](#使用-qt-时的相关问题和解决方案)
  - [文字编码](#文字编码)
    - [使用 MSVC 编译时汉字乱码问题](#使用-msvc-编译时汉字乱码问题)
  - [其他](#其他)
    - [Release 版本封装打包](#release-版本封装打包)


## 文字编码

### 使用 MSVC 编译时汉字乱码问题

原因：不带 BOM 的 UTF-8 格式文件会被 MSVC 以 GBK 进行编码。

1. QT界面菜单栏->工具->选项->文本编辑器->行为，修改成`如果编码是UTF-8则添加`;
2. QT界面菜单栏->编辑->Slect Encoding...->UTF-8->按编码保存;
3. 在需要的头文件中加入`#pragma execution_character_set("utf-8")`即可。

## 其他

### Release 版本封装打包

利用 Qt 自带工具，进入 exe 文件目录，输入：`windeployqt --release *.exe`。

然后再将其他必要文件拷贝至该目录即可。