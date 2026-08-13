# [Version Control]通过文件夹管理python版本的方法

```Bash
mkdir -p /opt/python
cd /opt/python

wget https://www.python.org/ftp/python/3.9.19/Python-3.9.19.tgz
tar -xf Python-3.9.19.tgz
cd Python-3.9.19
./configure --prefix=/opt/python/3.9.19 --enable-optimizations --with-ensurepip=install
make -j4
make install
cd ..
rm -rf Python-3.9.19.tgz Python-3.9.19


sudo ln -s /opt/python/3.9.19/bin/python3 /usr/local/bin/python39
sudo ln -s /opt/python/3.9.19/bin/pip3 /usr/local/bin/pip39
```

