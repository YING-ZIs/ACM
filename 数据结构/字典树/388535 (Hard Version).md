#  ð[388535 (Hard Version)](https://codeforces.com/contest/1658/problem/D2)

    
    
    ä¸éå¥½é¢åï¼ï¼ï¼
    
  é¦åæä»¬éè¦ç¥éï¼å¯¹äºä¸åçæ°å¼æä¸åä¸ä¸ªæ°ï¼æå¾çæ°ä¸å®ä¹é½ä¸ç¸åã
  
  æä»¬çaæ°ç»æ¯éè¿å° l, råçæ°å¼æä¸xå¾å°çï¼é£ä¹ä¹å°±è¯´æäºå¶ä¸­ä¸å®æä¸ä¸ªæ°æ¯a[i] = l ^ xå¾å°çï¼
  é£ä¹æä»¬æä»¬éåæ¯ä¸ä¸ªæ°ï¼è®©a[i] ^ l ,å°±ä¸å®ä¼åºç° x ã
+  ä½åºç°äºxæä»ä¹ç¨å¢ï¼

   è¿å°±ç¨å°äºä¹åå­å¸æ çç¨å¤ï¼æ±ä¸ä¸ªæ°ä¸æ°ç»ä¸­çæ°çå¼ææå¤§å¼ææå°å¼ã
   æä»¬å¦æè®©è¿ä¸ªæ°å»åæä»¬ça[]æ°ç»æ±åæå¤§ï¼æå°çå¼æå¼ï¼å¦æå¶æ°å¥½ç­äºl,ré£ä¹å°±æ¯è¯´æä»¬è®©x
   å»å¼æä¸açæ°ç»ä¸­çæ¯ä¸ä¸ªæ°é½ä¼è½å¨[l,r]åï¼åæ¶æ¯ä¸ä¸ªæ°å¼æä¸xé½æ¯ä¸ç¸ç­çï¼æä»¥ä»ä»¬å°±ä¸å®æ¯
   [l,r]çå¨é¨æ°ã
   
   
   é£ä¹æä»¬å°±å°æ¯ä¸ä¸ªæ°æå¥å°å­å¸æ ä¸­ï¼ç¶åæ±æå¤§æå°å¼ï¼åä¸l,ræ¯è¾å°±å¯ä»¥äºã
   
   åæ¶æ±åæå¤§æå°å¼ï¼åºè¯¥ä»é«ä½åä½ä½ï¼å ä¸ºè¿æ ·è´ªå¿æè½ä½¿å¾å¼æå¤§ä¸æå°ã
   
   
```C++
#include <bits/stdc++.h>

using namespace std;
using i64 = long long;

int cnt;
struct Trie{

    int tr[1 << 17][2];
    void init(){
        memset(tr, 0, sizeof(int) * (cnt + 1) * 2);//åå§åå°æå·§
        cnt = 0;
    }
    void insert(int val){
        int p = 0;
        for(int i = 16; i >= 0 ; i--){
            int u = val >> i & 1;
            if(!tr[p][u]){
                tr[p][u] = ++cnt;
            }
            p = tr[p][u];
        }
    }
    int Max(int val){
        int p = 0, sum = 0;
        for(int i = 16; i >= 0 ; i--){
            int u = val >> i & 1;
            if(tr[p][!u]){
                sum += 1 << i;
                p = tr[p][!u];
            } else {
                p = tr[p][u];
            }
        }
        return sum;
    }
    int Min(int val){
        int p = 0, sum = 0;
        for(int i = 16; i >= 0 ; i--){
            int u = val >> i & 1;
            if(tr[p][u]){
                p = tr[p][u];
            } else {
                sum += 1 << i;
                p = tr[p][!u];
            }
        }
        return sum;
    }

}tree;
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
    ios::sync_with_stdio(false);cin.tie(nullptr);

    int t;  cin >> t;
    while(t--){
        tree.init();
        int l, r;  cin >> l >> r;
        vector<int>a(r - l + 1);
        for(int &x : a)  cin >> x,tree.insert(x);

        for(auto x : a){
            int io = x ^ l;
            int Max = tree.Max(io);
            int Min = tree.Min(io);
            if(Max == r && Min == l){
                cout << io << endl;
                break;
            } 
        }
    }

    return 0;
}
```

```diff
!   2022-04-03ðâ
```
