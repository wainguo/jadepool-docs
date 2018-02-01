# 门罗币Miner：**xmr-stak** for Linux

## 1.安装依赖（仅需要支持CPU挖矿，可略过这一步，直接跳到"2.编译"）

### AMD APP SDK 3.0 安装(AMD GPUs)

- 下载并安装最新版本 [http://developer.amd.com/amd-accelerated-parallel-processing-app-sdk/](http://developer.amd.com/amd-accelerated-parallel-processing-app-sdk/)

### Cuda 8.0+ 安装(NVIDIA GPUs)

- 下载并安装 [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)
- 最小安装，可在安装过程中，选择 `Custom installation options` 
    - CUDA/Develpment
    - CUDA/Runtime
    - Driver components

## 2.编译
### 各种系统下的安装编译

这里以仅需要支持CPU挖矿为，所以cmake3编译选项指定了`-DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF`编译选项。如果需要同时支持GPU挖矿，可以去掉这两个编译选项。

* CentOS环境
```
    sudo yum install centos-release-scl epel-release
    sudo yum install git cmake3 devtoolset-4-gcc* hwloc-devel libmicrohttpd-devel openssl-devel make
    scl enable devtoolset-4 bash
    git clone https://github.com/fireice-uk/xmr-stak.git
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake3 .. -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
    make install
```

* Ubuntu / Debian环境
```
    sudo apt install libmicrohttpd-dev libssl-dev cmake build-essential libhwloc-dev git
    git clone https://github.com/fireice-uk/xmr-stak.git
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake .. -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
    make install
```

* Ubuntu 14.04环境
```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt update
    sudo apt install gcc-5 g++-5 make
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 1 --slave /usr/bin/g++ g++ /usr/bin/g++-5
    curl -L http://www.cmake.org/files/v3.4/cmake-3.4.1.tar.gz | tar -xvzf - -C /tmp/
    cd /tmp/cmake-3.4.1/ && ./configure && make && sudo make install && cd -
    sudo update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force
    sudo apt install libmicrohttpd-dev libssl-dev libhwloc-dev
    git clone https://github.com/fireice-uk/xmr-stak.git
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake .. -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
    make install
```

* Arch环境
```
    sudo pacman -S base-devel hwloc openssl cmake libmicrohttpd
    git clone https://github.com/fireice-uk/xmr-stak.git
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake .. -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
    make install
```

* Fedora环境
```
    sudo dnf install gcc gcc-c++ hwloc-devel libmicrohttpd-devel libstdc++-static make openssl-devel cmake
    git clone https://github.com/fireice-uk/xmr-stak.git
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake .. -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF
    make install
```


## 3.运行
### 首次运行
```
$ cd bin/
$ ./xmr-stak 
```
然后依次根据提示输入：
```
- Currency: 'monero' or 'aeon'
```
这里输入挖矿品种：monero
```
- Pool address: e.g. pool.usxmrpool.com:3333
```
这里输入矿池地址：xmr.jadepool.com:3333
```
- Username (wallet address or pool login):
```
这里输入门罗钱包地址（请替换为您的门罗钱包地址）：45M3yC2WxL99gQ22QRzN26c5NBV8b3cq3aJoyMDZQuGbQT38NytuKdV2uX7M4CEYXAYHUj51GdyEDFPy7SntP6gRLDvK1aN
```
- Password (mostly empty or x):
```
这里输入矿池Miner登录密码，留空直接回车或x
```
- Does this pool port support TLS/SSL? Use no if unknown. (y/N)
```
这里输入是否支持TLS，输入：N
```
- Do you want to use nicehash on this pool? (y/n)
```
是否启用nicehash，这里输入：n
```
- Do you want to use multiple pools? (y/n)
```
是否使用多路矿池，这里输入：n

然后会自动生成配置文件，并启动,可看到类似下面的日志打印
```
Configuration stored in file 'config.txt'
-------------------------------------------------------------------
xmr-stak 2.2.0 2ae7260

Brought to you by fireice_uk and psychocrypt under GPLv3.
Based on CPU mining code by wolf9466 (heavily optimized by fireice_uk).

Configurable dev donation level is set to 2.0%

You can use following keys to display reports:
'h' - hashrate
'r' - results
'c' - connection
-------------------------------------------------------------------
[2018-01-31 19:20:27] : Start mining: MONERO
[2018-01-31 19:20:27] : CPU configuration stored in file 'cpu.txt'
[2018-01-31 19:20:27] : Starting 2x thread, affinity: 0.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 2x thread, affinity: 1.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 2.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 3.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 4.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 5.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 6.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Starting 1x thread, affinity: 7.
[2018-01-31 19:20:27] : hwloc: memory pinned
[2018-01-31 19:20:27] : Fast-connecting to xmr.jadepool.com:3333 pool ...
[2018-01-31 19:20:28] : Pool xmr.jadepool.com:3333 connected. Logging in...
[2018-01-31 19:20:29] : Difficulty changed. Now: 5000.
[2018-01-31 19:20:29] : Pool logged in.
```
按Ctrl+C退出运行。

可以看到首次运行已经在bin文件所在目录下自动生成了配置文件`config.txt`和`cpu.txt`（如果支持GPU，还会生成'gpu.txt'文件）
编辑config.txt，修改其中的配置`daemon_mode`的值改为true，这样以后启动会background后台运行
```
"daemon_mode" : true,
```

此外Miner提供了内置的web服务，可以监控Miner的运行状态，默认该web服务是关闭的，如果想要启用可以修改`config.txt`中的`httpd_port`，默认`httpd_port`值为0，表示关闭web服务，如果启用可以配置为非0端口号，例如：
```
"httpd_port" : 3128,
"http_login" : "myname",
"http_pass" : "mypassword",
```
其中`http_login`和`http_pass`为访问该web服务的用户名和密码，可根据需要修改，`http_login`留空可禁用登录鉴权功能。

## 4.配置修改
### 基于CPU的配置 

首次运行，xmr-stak会自动探测并设置cpu线程数，这个文件默认可以不用修改。

如果希望调试相关参数对算力的影响可以尝试修改下面的参数：
编辑`cpu.txt`文件，修改`low_power_mode`对应的值true，利用cpu缓存提升挖矿效率，同时还可以节能。根据服务器cpu核心数量，修改启动的Miner线程数，比如8核cpu的配置如下（注意编号从0开始，8核最大编号为7）：
```
"cpu_threads_conf" :
 [
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 0 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 1 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 2 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 3 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 4 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 5 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 6 },
      { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 7 },
 ],
```

## 5.常见问题
## 运行提示错误"Error: MEMORY ALLOC FAILED: mmap failed"

在Linux下需要开启大页存取支持 
```
sudo sysctl -w vm.nr_hugepages=128
```

同时需要提高max locked memory：ulimit -l. 修改文件/etc/security/limits.conf，在末尾加入如下两行配置
```
    * soft memlock 262144
    * hard memlock 262144
```
保存后，为使修改的配置生效，需要登出，并重新登入 (不需要系统reboot，只要重新登入即可)。