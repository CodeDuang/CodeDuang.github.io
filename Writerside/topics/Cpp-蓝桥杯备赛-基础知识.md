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
#include<iostream>
using namespace std;
#define hi cout
int a = 10;
int main(){
    hi<<a<<endl;
    a = 12;
    hi<<a<<endl; 
}
/* 输出：
10
12
*/
```

### 3.堆栈结构

C++总共有四大存储区：堆、栈、常量区、静态区（全局区）
- 堆：一般由程序员分配释放，若程序员不释放，程序结束时由OS回收。
- 栈：由编译器自动分配释放。
- 常量区：程序结束释放。
- 静态区（全局区）：全局变量和静态变量的存放是放在一块的，初始化的全局变量和静态变量在一块区域，未初始化的全局变量和未初始化的静态变量在相邻的另外一块区域。程序结束进行释放。


```C++
#include<iostream>
using namespace std;

int a = 10; //静态区（全局区）初始化
char *p1; //静态区（全局区）未初始化
int main(){
    int b = 20; //栈
    char s[] = "abc ";//指针常量s在栈区，"abc "在常量区
    char *p2 = "123456 "; //123456\0在常量区，p3在栈上。
    char *p3; //栈
    static int c =0； //全局（静态）初始化区
    
    //分配得来得10和20字节的区域就在堆区。
	p1 = (char *)malloc(10);
	p2 = (char *)malloc(20);
	
	strcpy(p3, "123456 "); //123456\0放在常量区，编译器可能会将它与p2所指向的 "123456 "优化成一块。


}

```
