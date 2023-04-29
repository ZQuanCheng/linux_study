
### Bosch 实习时的设置

> Ubuntu 20.04
> 环境：cmake-3.22.0、python3.8、ROS-neotic、conan-1.56.0、g++-8、gcc-8
> 软件：VScode


> 注：
> Ubuntu20.04 自带gcc-9、g++-9，需要降级到8
> <font color="yellow">g++、gcc版本降级（9→8），采用如下方法：</font>
> https://zhuanlan.zhihu.com/p/453542931
> * 通过命令查询本机gcc已安装的版本, 发现只有gcc-9
> ```bash
> ls /usr/bin/gcc*
> ```
> * 输入命令，查看gcc-8可选的版本，可以看到候选
> ```bash
> sudo apt-cache policy gcc-8
> ```
> * 选择其中一个版本进行安装
> ```bash
> sudo apt-get install gcc-8=8.4.0-3ubuntu2
> ```
> * 再次查询本机gcc已安装的版本, 发现有gcc-8、gcc-9
> ```bash
> ls /usr/bin/gcc*
> ```
> * 改gcc-8成为默认版本
> ```bash
> # 配置优先级
> sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 80
> sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 90
> # 查看优先级
> sudo update-alternatives --config gcc
> # 选择gcc-8对应的编号1 回车即可
> ```
> * g++-8的方法同上
>


> 
>
> 依赖项中有一个不满足：cmake above 3.18.4
> <font color="yellow">cmake升级，采用如下方法：</font>
> https://huaweicloud.csdn.net/63560d52d3efff3090b58f8d.html
> 
> 1、首先下载cmake压缩包，然后再建立软链接覆盖系统原来的cmake。
> ```bash
> # 进入到下载目录下，其他目录也可以
> cd ~/Downloads 
> 
> # 下载cmake源码包
> wget https://github.com/Kitware/CMake/releases/download/v3.21.4/cmake-3.21.4-linux-x86_64.tar.gz
> 
> # 解压
> tar -xzvf cmake-3.21.4-Linux-x86_64.tar.gz
> 
> # 将解压出来的包移到 /opt 目录下
> sudo mv cmake-3.21.4-Linux-x86_64 /opt/cmake-3.21.4  
> 
> # 建立软链接
> sudo ln -sf /opt/cmake-3.21.4/bin/* /usr/bin/   
> 
> # 查看是否成功
> cmake --version
> 
> # 显示 cmake version 3.21.4
> ```
> 
> 2、cmake安装成功之后，不要忘记将cmake的文件路径添加至 .bashrc里面：
> ```bash
> # 进入~/.bashrc
> sudo gedit ~/.bashrc
> 
> # 输入以下内容
> export  PATH=$PATH:/opt/cmake-3.21.4/bin
>
> # 保存 .bashrc的更改并退出
> ```
> 3、更新source
> ```bash
> source ~/.bashrc 
> ```
>

> <font color="yellow"> python无效？ </font>
> Ubuntu20.04中已经安装了Python3，但是输入`python`指令时，收到提醒
> ```bash
> $ python
> 
> Command 'python' not found, did you mean:
> 
>   command 'python3' from deb python3
>   command 'python' from deb python-is-python3
> ```
> 但输入 python3 是不会报错的
> ```bash
> $ python3
> Python 3.8.10 (default, Sep 28 2021, 16:10:42) 
> [GCC 9.3.0] on linux
> Type "help", "copyright", "credits" or "license" for more information.
> >>>
> ```
> 解决方式
> 安裝 python-is-python3，指令如下
> ```bash
> $ sudo apt install python-is-python3
> ```
> 还原只需要移除 python-is-python3，移除指令如下
> ```bash
> $ sudo apt remove python-is-python3
> ```

> <font color="yellow"> setup conan environment </font>
> AOS releases 本质上时conan packages，
>
> ```bash
> pip install conan==1.56.0 ### 1.45.0好像不行，德秀和飞扬用的是1.56.0
> 
> # 剩下的按照教程来
> ```



> * Cmake版本为3.22.0
> * Python版本为3.8.10
> * Conan版本为1.56.0 
>
> **第一步 CMake**
> 
> 依赖项中第一个不满足：cmake above 3.18.4
> <font color="yellow">cmake升级，方法1(太麻烦)：</font>
> https://huaweicloud.csdn.net/63560d52d3efff3090b58f8d.html
> 
> 1、首先下载cmake压缩包，然后再建立软链接覆盖系统原来的cmake。
> ```bash
> # 进入到下载目录下，其他目录也可以
> cd ~/Downloads 
> 
> # 下载cmake源码包
> wget https://github.com/Kitware/CMake/releases/download/v3.21.4/cmake-3.21.4-linux-x86_64.tar.gz
> 
> # 解压
> tar -xzvf cmake-3.21.4-Linux-x86_64.tar.gz
> 
> # 将解压出来的包移到 /opt 目录下
> sudo mv cmake-3.21.4-Linux-x86_64 /opt/cmake-3.21.4  
> 
> # 建立软链接
> sudo ln -sf /opt/cmake-3.21.4/bin/* /usr/bin/   
> 
> # 查看是否成功
> cmake --version
> 
> # 显示 cmake version 3.21.4
> ```
> 
> 2、cmake安装成功之后，不要忘记将cmake的文件路径添加至 .bashrc里面：
> ```bash
> # 进入~/.bashrc
> sudo gedit ~/.bashrc
> 
> # 输入以下内容
> export  PATH=$PATH:/opt/cmake-3.21.4/bin
>
> # 保存 .bashrc的更改并退出
> ```
> 3、更新source
> ```bash
> source ~/.bashrc 
> ```
> <font color="yellow">cmake升级，方法2(非常简单)：</font>
> ```bash
> pip install cmake==3.22.0
> ```
>
> **第二步 Python3.8**
> 
> <font color="yellow"> python无效？ </font>
> Ubuntu20.04中已经安装了Python3，但是输入`python`指令时，收到提醒
> ```bash
> $ python
> 
> Command 'python' not found, did you mean:
> 
>   command 'python3' from deb python3
>   command 'python' from deb python-is-python3
> ```
> 但输入 python3 是不会报错的
> ```bash
> $ python3
> Python 3.8.10 (default, Sep 28 2021, 16:10:42) 
> [GCC 9.3.0] on linux
> Type "help", "copyright", "credits" or "license" for more information.
> >>>
> ```
> 解决方式
> 安裝 python-is-python3，指令如下
> ```bash
> $ sudo apt install python-is-python3
> ```
> 还原只需要移除 python-is-python3，移除指令如下
> ```bash
> $ sudo apt remove python-is-python3
> ```
> 
> **第三步 conan**
>
> ```bash
> pip install conan==1.56.0 ### 1.45.0好像不行，德秀和飞扬用的是1.56.0
> ```
> 
> **剩下的按照教程来**


