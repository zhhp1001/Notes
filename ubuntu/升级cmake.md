## 1.查看cmake版本

```bash
cmake --version
```

## 2 卸载过去的版本

```bash
sudo apt-get autoremove cmake
```

最好卸载，不然可能会出现如下错误：

```bash
CMake Error: Could not find CMAKE_ROOT !!!
CMake has most likely not been installed correctly.
Modules directory not found in
/usr/local/share/cmake-3.5
CMake Error: Error executing cmake::LoadCache(). Aborting.
```

**依赖项**

- gcc
- g++
- build-essential
- libssl-dev

## 3.安装需要的版本

1. 下载

```bash
cd ~
wget https://cmake.org/files/v3.13/cmake-3.13.2.tar.gz
tar xvf cmake-3.13.2.tar.gz
cd cmake-3.13.2
```

2.安装

```bash
./bootstrap --prefix=/usr
 make
 sudo make install
```

3.检查

```bash
cmake --version
```