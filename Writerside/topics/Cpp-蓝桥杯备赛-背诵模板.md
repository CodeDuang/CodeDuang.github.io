# [Cpp]蓝桥杯备赛-背诵模板

## bfs模板
题源：[蓝桥杯-走迷宫](https://www.lanqiao.cn/problems/1216/learning/)

```C++
#include<iostream>
#include<queue>
using namespace std;

const int MAXN = 105;

int n,m;
int mapp[MAXN][MAXN];
int vis[MAXN][MAXN];
int start_x,start_y;
int end_x,end_y;

int d[4][2]={{1,0},{-1,0},{0,1},{0,-1}};

void bfs(){
    queue<pair<int ,int >> q;
    q.push(make_pair(start_x,start_y));
    vis[start_x][start_y]=1;
    int step=0; 
    while(!q.empty()){
        int len = q.size();
        while(len--){
            int x = q.front().first;
            int y = q.front().second;
            q.pop();
            if(x == end_x && y == end_y){
                cout << step ;
                return ;
            }
            for(int i = 0 ; i < 4 ;i++){
                int dx = x + d[i][0];
                int dy = y + d[i][1];
                if(dx > 0 && dx <= n && dy > 0 && dy <= m && !vis[dx][dy] && mapp[dx][dy] == 1){
                    q.push(make_pair(dx,dy));
                    vis[dx][dy] = 1;
                }
            }
        }
        step ++ ;
    }
    cout << -1;
}

int main(void){
    cin>>n>>m;
    for(int i = 1 ; i <= n ; i++){
        for(int j = 1 ; j <= m ; j++){
            cin>>mapp[i][j];
        }
    }
    cin>>start_x>>start_y>>end_x>>end_y;
    bfs();
    return 0;
}
```