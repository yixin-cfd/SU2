### mpich 安装
```bash
 wget https://www.mpich.org/static/downloads/4.2.3/mpich-4.2.3.tar.gz
 tar -zxvf ./mpich-4.2.3.tar.gz 
 cd mpich-4.2.3/
 ./configure -enable-fortran  --prefix=/home/Soft/mpich-4.2.3
 make
 sudo make install
```
放入到 bash 中

```bash
# >>> mpich >>>
export PATH="/home/Soft/mpich-4.2.3/bin:$PATH"
export PKG_CONFIG_PATH=/home/Soft/mpich-4.2.3/lib/pkgconfig:$PKG_CONFIG_PATH
# <<< mpich <<<
```

### SU2安装

```bash
 ./meson.py build -Denable-autodiff=true -Dwith-mpi=enabled -Denable-tests=true  --prefix=/home/yixin/Data/Code/CPP/SU2
 (./meson.py build -Denable-autodiff=true -Dwith-mpi=enabled -Denable-tests=true --prefix=/home/yixin/Data/Code/CPP/SU2 -Dcustom-mpi=true
)编译的mpi用这个找mpi库
./ninja -C build install
```