构建选项
```bash
./meson.py setup (--wipe) build -Denable-autodiff=true -Dwith-mpi=enabled -Denable-cgns=true --prefix=/home/jlx/program/SU2
```
编译&安装
```bash
./ninja -j95 -C build install
```

配置环境变量
```bash
export SU2_RUN=/home/jlx/program/SU2/bin
export PATH=$SU2_RUN:$PATH
export PYTHONPATH=$SU2_RUN:$PYTHONPATH
```
运行
```bash
mpirun -n 64  --use-hwthread-cpus SU2_CFD ./inv_NACA0012.cfg
```


**可能问题**
1. 运行时出现如下警告信息：
```bash
PMIx was unable to find a usable compression library
on the system. We will therefore be unable to compress
large data streams. This may result in longer-than-normal
startup times and larger memory footprints. We will
continue, but strongly recommend installing zlib or
a comparable compression library for better user experience.

You can suppress this warning by adding "pcompress_base_silence_warning=1"
to your PMIx MCA default parameter file, or by adding
"PMIX_MCA_pcompress_base_silence_warning=1" to your environment.
```

解决方法：
安装zlib开发包
```bash
sudo apt-get install zlib1g-dev
```

重新编译openmpi

```bash

./configure --prefix=/opt/openmpi-5.0.8
make -j 64
sudo make install


export PATH=$PATH:/opt/openmpi-5.0.8/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/openmpi-5.0.8/lib
```

2. 内存不足编译失败
增大交换内存
```bash
sudo fallocate -l 24G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```