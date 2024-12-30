# [Cpp]用txt文本内容代替cin手动输入


```C++
fstream cin("in.txt"); //方法1
freopen("in.txt", "r", stdin); //方法2
```
使用上述方法，在用cin，程序就会自动读取in.txt的内容，作为cin的输入

```C++
//举例,新建一个in.txt文件，内容如下
/*
4 4
1 2 3 4
4 3 2 1
5 6 7 8
9 8 7 5
*/
#include<bits/stdc++.h>
using namespace std;
int main(){
    fstream cin("in.txt"); //方法1
    // freopen("in.txt", "r", stdin); //方法2（和方法1用法一样）
    int m,n;
    int mapp[101][101];
    cin>>m>>n;
    for(int i=1;i<=m;i++)
    for(int j=1;j<=n;j++)
        cin>>mapp[i][j];
    cout<<m<<' '<<n<<endl;
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++) cout<<mapp[i][j]<<' ';
        cout<<endl;
    }
    return 0;
}

```