# [Cpp]蓝桥杯备赛-基础知识

参考：  
[蓝桥杯常用知识点+算法汇总](https://www.cnblogs.com/csx-zzh/p/13821900.html)   
[杂项 | 算竞常用 C++ STL 用法](https://io.zouht.com/154.html)


### 1.C++的常用类型
包括：int、float、double、bool、char、string

★数值后缀：用于指定字面量的类型
```C++
#include<iostream>
using namespace std;

int main(){
    /*
    1.5默认是double类别
    1.5f表示float类别
    1.5l表示long double类型
    10u表示unsigned int无符号整数
    10ll表示long long类型整数
    10ull表示unsigned long long类型整数
    */
    float a = 1.5; //这里1.5是double类型，会发生隐式类型转换为float
    float b = 1.5f; //这里1.5f是float类型，不会发生类型转换
    cout<<sizeof(1.5)<<" "<<sizeof(1.5f)<<endl;  //输出：8 4 (试着解释一下这是为什么？)
    cout<<sizeof("a")<<" "<<sizeof('a')<<endl;  //输出：2 1 (试着解释一下这是为什么？)
}
```
### 2.宏定义与全局变量

宏定义：一旦定义，其值不能改变，因为它在预处理阶段就已经被替换掉了

全局变量：全局变量定义在所有函数之外，可以被任何函数访问。它的生存期从程序启动到程序结束

```C++
#incldue<iostream>
using namespace std;
#define hi cout
int a = 10;
int main(){
    hi<<a<<end;
    a = 12;
    hi<<a<<endl;
}
```
