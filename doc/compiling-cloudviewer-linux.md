# 在 Linux 编译 CloudViewer

该文档介绍在 Linux 系统编译运行 CloudViewer，以 Ubuntu 18 为例。

## 目录

- [环境搭建](#环境搭建)
  - [PCL安装](#PCL安装)
  - [Qt安装](#Qt安装)
  - [环境变量配置](#环境变量配置)
- [CloudViewer编译运行](#CloudViewer编译运行)

## 环境搭建

### PCL安装

```shell
sudo apt-get install libpcl-dev
```

### Qt安装

下载 Qt（以 5.10.1 为例）。

```shell
wget http://download.qt.io/archive/qt/5.10/5.10.1/qt-opensource-linux-x64-5.10.1.run
```

修改可执行文件的权限。

```shell
sudo chmod a+x ./qt-opensource-linux-x64-5.10.1.run
```

运行安装程序。

```shell
./qt-opensource-linux-x64-5.10.1.run
```

将会弹出图形安装界面，勾选必要的组件，完成安装。

<img  src="http://nightn.com/cloudviewer/img2/linux-qt-install-component.png" width="400" />

### 环境变量配置

修改 `/etc/profile` 文件，在文件末尾加上 Qt 路径（具体由用户名和 Qt 版本而定）：

```bash
export PATH="/home/nightn/Qt5.10.1/Tools/QtCreator/bin:$PATH"
export PATH="/home/nightn/Qt5.10.1/5.10.1/gcc_64/bin:$PATH"
```

如下图所示：

<img src="http://nightn.com/cloudviewer/img2/linux-qt-env.png" width="500" />

## CloudViewer编译运行

克隆项目：

```shell
git clone https://github.com/nightn/CloudViewer.git
```

使用 cmake 配置和生成。

```shell
cmake -H. -Bbuild
```

使用 make 构建。

```shell
cd build
make
```

运行 CloudViewer。

```shell
./src/CloudViewer
```

运行结果：

<img src="http://nightn.com/cloudviewer/img2/linux-cloudviewer.png" width="600" />

### make遇到的bug
* ``/usr/lib/x86_64-linux-gnu/libSM.so: undefined reference to `uuid_generate@UUID_1.0``<br>
**ans:**把anacondax(取决于你的版本)/lib下的libuuid[库文件移走](https://blog.csdn.net/u014734886/article/details/93029349)
* ``anaconda3/lib/libfontconfig.so.1: undefined reference to `FT_Done_MM_Var''<br>
**ans:**[复制一个库文件](https://stackoverflow.com/questions/53910698/undefined-reference-to-ft-done-mm-var/56581845#56581845)，提到建立软连接，我尝试两行代码都提示文件已存在，但解决了这个bug
* 以上两个bug解决了,make通过,程序运行起来了


