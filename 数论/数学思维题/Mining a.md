ð¡[Mining a](https://codeforces.com/gym/102460)
=======
```diff    
    ð¡å¯¹äºå¼æâè¿æ¯ä¸å¤ªçæï¼æåºæ¬çæ§è´¨é½ä¸ç¥éã
    
!   è¿éé¢ç¨å°çæ§è´¨æ¯ c = a â b ï¼é£ä¹ a = c â b
    
    å¯¹äºåå¼ï¼æä¹å¯ä»¥åè®¾x = aâb , y=bï¼
    é£ä¹æä»¬ç°å¨çä»»å¡å°±æ¯æ±åºä¸x,yç¶åå¼ææ±åæå¤§å¼ã
    
    æä»¬å¯¹å¼å­å±å¼å¹¶è¿è¡åå­åè§£å¯åæï¼(å°½éå¾åå­ç¸ä¹å»åç®ï¼è¿æ ·æè½ææå°æ±åºåä¸ªåéä¹é´çå³ç³»)
    
    (x-n)*(y-n) = n*n
    
    æä»¬å¯ä»¥åè®¾y = n+k,é£ä¹x = (n^2)/k+n;
    æä»¥æä»¬ç°å¨éåkçåå¼ï¼å ä¸ºx,yé½æ¯æ´æ°ï¼æä»¥å°±æ¯(n^2) % k == 0ï¼æä»¥k çåå¼å°±å¨1~nä¹é´ã
    åå ä¸ºè¿éé¢çéæ¶æ¯2sæä»¥æ¯å¯ä»¥çã
    
```
```C++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <sstream>
#include <queue>

#define fi first
#define se second
using namespace std;
typedef long long ll;
typedef pair<int,int>PII;
const int maxn  = 1e3+10;
const int mod = 1e9+7;

int n;
void solve(){

	ll ans=0;
	for(int i = 1; i <= n ; i++){
		if((1ll*n*n) % i != 0 )continue;
		ll x = 1ll*n*n/i+n;
		ll y =n+i;
		ans=max(ans,x^y);
	}printf("%lld\n",ans);
}
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
	int t;scanf("%d",&t);
	while(t--){
		scanf("%d",&n);
		solve();
	}
	return 0;
}
```
```diff
!    ð2021-01-15 
```
