#  ð³ï¸[HHçé¡¹é¾](https://www.luogu.com.cn/problem/P1972)
    
    
    è¿éé¢ä¹åçæ ç¶æ°ç»çæ¹æ³åè¿ä¸ªå·®ä¸å¤ï¼ä½æ¯ç¨ä¸»å¸­æ æè§æ´å å·§å¦ã
    
    è¿éçåºé´å³ä¸ºæç§å¼æ¥ååï¼èç¹å«ä¹ä¸ºä¸ä¸ªæ°çä¸ä¸ä¸ªç¦»ä»æè¿çç¸åçæ°çä½ç½®ã
    
    è¿éæä»¬å©ç¨äºåç¼åçææ³ã
    [1 ~ (L - 1)] [L  ~  R]
    æä»¬æ³è¦ç»è®¡åºL ~ Råçæ°ï¼é£ä¹æä»¬åªéè¦ç»è®¡è¿éé¢nxtå¤§äºRçæ°å°±å¯ä»¥äºï¼å³å¨[L , R]ä¸­æ¯ä¸ä¸ªæ°æåä¸æ¬¡åºç°ç
    æä¼æè´¡ç®ï¼è¿æ ·å¯ä»¥ä¿è¯åªè®°ä¸ä¸æ¬¡ã
    èå¨1 ~ (L - 1)ä¸­ nxt > Ré£ä¹ä¸å®æ¯å¨[L, R]åä¹æ²¡æåºç°è¿çï¼æä»¥ä»ä¹è¢«è®°å½å¨äº1 - Råã
    æä»¥ç¨ Ræ¶çæ åå»L-1æ¶ççæ å°±æ¯L - Råºé´åçç¹ææçæ ï¼é£ä¹æä»¬ç»è®¡ > Rçèç¹çä¸ªæ°å°±å¯ä»¥äºã
    
    
```C++
#include <bits/stdc++.h>

#define L(x)  (tr[x].l)
#define R(x)  (tr[x].r)
#define endl "\n"
using namespace std;
using i64 = long long;
const int maxn = 1e6 + 10;

int n, q, cnt, pos[maxn], a[maxn], vis[maxn];

struct Chairman_Tree{
    int root[maxn];
    struct node{
        int w, l, r;
    }tr[maxn * 20];

    void update(int &now, int l, int r, int x){

        tr[++cnt] = tr[now], now = cnt;
        tr[now].w++;
        if(l == r) return;
        int mid = l + r >> 1;
        if(x <= mid) update(L(now), l, mid, x);
        else         update(R(now), mid + 1, r, x);
    }

    int query(int i, int j, int l,int r,int x){

        if(l == r) return tr[j].w - tr[i].w;
        int mid = l + r >> 1;
        if(x > mid) return query(R(i), R(j), mid + 1, r, x);
        else        return query(L(i), L(j), l, mid, x) + tr[R(j)].w - tr[R(i)].w;
    }
}tree;

int main() 
{
#ifndef ONLINE_JUDGE
    freopen("in.txt", "r", stdin);
    freopen("out.txt", "w", stdout);
#endif
    ios::sync_with_stdio(false); cin.tie(nullptr);

    int n;  cin >> n;
    for(int i = 1; i <= n ; i++)  cin >> a[i];
    for(int i = n ; i >= 1; i--){
        if(!vis[a[i]]){
            pos[i] = n + 1;
        } else {
            pos[i] = vis[a[i]];
        }
        vis[a[i]] = i;
    }
    
    for(int i = 1; i <= n ; i++){
        tree.root[i] = tree.root[i - 1];
        tree.update(tree.root[i], 1, n + 1, pos[i]);
    }

    int q;  cin >> q;
    while(q--){
        int l, r;  cin >> l >> r;
        cout << tree.query(tree.root[l - 1], tree.root[r], 1, n + 1, r + 1) << endl;
    }

    return 0;
}
```
```diff
!   2022-03-30ð
```
