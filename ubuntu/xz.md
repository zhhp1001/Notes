# Linux下安装xz的方法

1. ```bash
   cd /usr/local/pkg
   ```

2. ```bash
   wget https://tukaani.org/xz/xz-5.2.3.tar.gz //下载到/usr/local/pkg目录下
   ```

3. ```bash
   tar xvf xz-5.2.3.tar.gz
   ```

4. ```bash
   cd xz-5.2.3
   ```

5. ```bash
   ./configure --prefix=/usr/local/xz  //将xz软件安装到/usr/local/xz目录下
   ```

   > 此处，如果出现如下错误：
   > configure: error: in `/usr/local/xz’:
   >
   > configure: error: no acceptable C compiler found in $PATH
   > See `config.log’ for more details
   > 说明缺少GCC软件套件
   > 执行：yum install gcc
   > 安装完成后 ，执行：./configure --prefix=/usr/local/xz

6. ```bash
   make
   ```

7. ```bash
   make install
   ```

8. ```bash
   vi /etc/profile
   ```

   设置环境变量，添加如下内容:

   ```bash
   export XZ_HOME=/usr/local/xz
   export PATH=$XZ_HOME/bin:$PATH
   ```

9. ```bash
   source /etc/profile   //使修改生效
   ```

  至此, XZ 的安装配置就完成了.

### 解压tar.xz包

**文件是node-v8.11.1-linux-x64.tar.xz，这是两层压缩，外面是xz压缩，里层是tar压缩，所以分两步实现解压。**

```bash
xz -d node-v8.11.1-linux-x64.tar.xz

tar -xvf node-v8.11.1-linux-x64.tar.xz
```

**也可以直接解压**

```bash
tar -xf node-v8.11.1-linux-x64.tar.xz
```

https://linuxize.com/post/how-to-extract-unzip-tar-xz-file/