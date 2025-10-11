# [Cpp]linux网络开发基础知识


### 1.常用命令

```Bash
#编译为对象文件（g++ -c [cpp程序名] -o [对象文件名]）
#其中-c表示将后面的cpp编译为对象文件，-o表示指定文件名
g++ -c cppProjectName.cpp -o objectName.o

#链接对象文件文可执行文件（g++ [对象文件名] -o [可执行文件名]）
g++ objectName.o -o run.exe
#另外一种写法(对于gcc命令来说需要-lstc++手动的指定C++库)
gcc objectName.o -lstdc++ -o run.exe
```


