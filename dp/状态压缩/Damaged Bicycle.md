#  ð§¢[CCPC Harbin 2021. (G. Damaged Bicycle)](http://oj.daimayuan.top/problem/380)

    ççå¥½é¾åï¼ï¼
    å­¦é¿å¯æ¯é çè¿éé¢æ¿çæåçé¶çåï¼ï¼ï¼
    ççæè§å°äºèªå·±åæ¿ççå·®è·ð¢
    
>    ç¶ådp + ææ

    é¦åæä»¬æ¥ç³»ç»çæèä¸ä¸è¿éé¢ã
    
    é¦åæä»¬ä¸å®æ¯ä¼èµ¶ç´§æ¾å°ä¸ä¸ªè½¦ç¶åéªåå»ï¼æèè¯´èµ°åå»ã
    é£ä¹æä»¬éè¦èèçç¹å°±åªæèµ·å§ä½ç½®åææçè½¦çä½ç½®(å³ç´å¥è½¦è¿å»ç)ã
    
    æä»¬å°è¾¾ä¸ä¸ªè½¦ç¹ä¼æä¸¤ç§æåµã
    
    good:
    å¦ææ¯å¥½çï¼æä»¬å°±ç´æ¥éªåå»äºï¼ç´æ¥èµ·é£ã
    
    badï¼
    ç¶åæä»¬å¦æç°å¨çè¿ä¸ªè½¦æ¯åè½¦ï¼é£ä¹æä»¬æä¸¤ç§éæ©ï¼
    (1)ç´æ¥å¼æï¼ ç¶åæ¢æ æ çèµ°åå»ã
    (2)æä»¬èµ¶ç´§å»æ¾ä¸ä¸è¾è½¦è¿æ²¡æå»è¿çè½¦
    
    
    å¯¹äºbadçä¸¤ä¸ªæåµæä»¬åªéè¦éæ©å¶ä¸­ä¸ä¸ªå°±å¯ä»¥äºï¼å¹¶ä¸æ¯1/2çæ¦çã
    å ä¸ºå¯¹äºæ¯ä¸ä¸ªè½¦åæçæ¦çæ¯ç¡®å®çï¼æä»¬å°±å¯ä»¥æ±åºä»è¿ä¸ªç¹åå»çæææ¶é´ï¼
    åæ¶èµ°åå»çæ¶é´æä»¬ä¹æ¯ç¥éçï¼
    é£ä¹æä»¬å°±åªéè¦æä¸­çéæ©å¶ä¸­èæ¶æå°çå°±å¯ä»¥äºï¼ç¶åå ä¸éªåå»çã
    
    è¿éæä»¬å®ä¹ dp[S][u]è¡¨ç¤ºï¼ æ­¤æ¶å¤äºuå¥½ç¹ï¼å¹¶ä¸å·²ç»éåè¿Sçåå»çæå°æææ¶é´ã
    é£ä¹æä»¬çç¶ådpçéåå°±æ¯éåºçã
    
    å¯¹äºç»æç¶æå°±æ¯æå·²ç»éåè¿ææç¶æï¼å¹¶ä¸å¤äºè¿ä¸ªç¹ï¼é£ä¹å¯¹äºbadç¶ææå°±åªå¯ä»¥éæ©èµ°åå»ã
    
    è¿ä¸ªç¨dfsè½å¤å¤å¥½çè§£éè¿ä¸ªè½¬ç§»è¿ç¨ã
    
    å¯¹äºå½æ¶åªæ¯æ³å°äºææï¼åçº¯çä»èµ·å§æ¾å°ç¦»ä»æè¿çè½¦ï¼ä¸æ­éå½ï¼å°é£æ¶ä¸ä¸å®å°±æ¯æ¯æ¬¡ç¦»ç°å¨è¿ä¸ªç¹
    æè¿å°±æ¯æå¥½ç­ç¥ï¼æä»¥ç¶åææ¯æ­£ç¡®çã
    
ACcode
```C++
#include <bits/stdc++.h>

#define endl '\n'
using namespace std;
using i64 = long long;
const int maxn = 1e5 + 10, INF = 0x3f3f3f3f;
typedef pair<int,int> Pii;

int vis[20][maxn], dis[20][maxn];
double w, r, pi[20];
int n, m, bike[20], id[20], k;
vector<Pii>v[maxn];
struct info{
            
    int u, w;
    info(){};
    info(int u,int w):u(u), w(w){};
    friend bool operator < (info x,info y){
        return x.w > y.w;
    }
};
priority_queue<info>q;

void dijistra(int k){

    for(int i = 1; i <= n ; i++){
        dis[k][i] = INF;
        vis[k][i] = 0;
    }
    dis[k][bike[k]] = 0;
    q.push(info(bike[k],0));

    while(!q.empty()){

        info x = q.top(); q.pop();
        if(vis[k][x.u]) continue;
        vis[k][x.u] = true;

        for(auto to : v[x.u]){
            if(dis[k][to.first] > dis[k][x.u] + to.second){
                dis[k][to.first] = dis[k][x.u] + to.second;
                q.push(info(to.first,dis[k][to.first]));
            }
        }
    }
}

double dp[(1 << 20)][20];
double dfs(int state,int u){

    if(dp[state][u]) return dp[state][u];
    double good = (1 - pi[u]) * dis[u][n] / r;
    double bad = pi[u] * dis[u][n] / w;

    for (int mask = 0; mask < k; mask++) {

        if(state & (1 << mask)) continue;
        bad = min(bad, pi[u] * (dis[u][id[mask]] / w + dfs(state | (1 << mask), mask)));
    }
    dp[state][u] = bad + good;
    return dp[state][u];

}
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
    ios::sync_with_stdio(false);cin.tie(nullptr);

    cin >> w >> r >> n >> m;
    for (int i = 0; i < m; i++) {

        int u,to,w;
        cin >> u >> to >> w;
        v[u].push_back({to,w});
        v[to].push_back({u,w});
    }

    cin >> k;
    for (int i = 0; i < k; i++) {
        cin >> bike[i] >> pi[i];
        pi[i] /= 100; 
        id[i] = bike[i];
    }

    for(int i = 0 ;i < k; i++) {
        dijistra(i);
    }
    bike[k] = 1; pi[k] = 1;
    dijistra(k);

    if (dis[k][n] == INF) {

        cout << "-1" << endl;
        return 0;
    } else {

        dfs(0, k);
        cout << fixed << setprecision(6) << dp[0][k] << endl;
    }


    return 0;
}
```

```diff
!   ðâ2022-03-16
```
    
