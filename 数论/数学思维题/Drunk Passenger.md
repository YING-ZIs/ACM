ðï¸[Drunk Passenger](https://codeforces.com/gym/103373/problem/D)
===

    åè®¾ænä¸ªäºº
    (1)æä»¬ç¥éå¯¹äºéæ±ï¼å¦æä»éæ©æä»¬çä½ç½®çè¯ï¼é£å°±ä¸å®ä¼ä½¿å¾æä»¬çä½ç½®è¢«å æï¼èéæ±ä¸è½éæ©èªå·±çä½ç½®ï¼
    æä»¥è¿ç§æåµä¸ä½ç½®è¢«å æ®çæ¦çæ¯1/(n-1)ã
    
    (2)ç¶åå¦ä¸ç§æåµå°±æ¯ä»ä¼å æ®å¶ä»äººçä½ç½®ã
    æä»¬å¯ä»¥æ¨åºçæ¯ï¼åè®¾ç°å¨çæéæåµæ¯ [éæ±ï¼1ï¼2ï¼3ï¼ï¼ï¼ï¼xï¼ï¼ï¼èªå·±]ï¼æ­¤æ¶éæ±å æ®äºxçä½ç½®ï¼é£ä¹ä»1å·å°x-1è¿ä¸ªåºé´
    åçäººé½æ¯ä¼åå¨åä½ï¼å ä¸ºé¢ç®ä¸­æè¯´ï¼å¦æä½ç½®æ²¡æè¢«å æ®å°±ä¼å½ååä½ï¼é£ä¹å°±è¯´æäºæä»¬éè¦å¼å§è®¨è®ºçæ¯ä»xå°èªå·±è¿ä¸ªéåä¸­çäººã
    æä»¬ä»å°å°å¤§å»æ¨ã
    
    æä»¬ä¸é¢è®¨è®ºç1ä»£è¡¨ä¸é¢çxï¼æä»¬ä¸åè®¨è®º(1)çæåµï¼å¹¶ä¸æä»¬åè®¨è®ºåºä½ç½®ä¸è¢«å æ®çæ¦çp,é£ä¹è¢«å æ®çå°±æ¯1-pï¼
      <1> åå¦åªæ[éæ±ï¼1ï¼èªå·±]ä¸ä¸ªäºº
          é£ä¹å¦æéæ±å æ®äº1çä½ç½®ï¼æ­¤æ¶æçä½ç½®ä¸è¢«å æ®çæ¦çä½ 1/2
      <2> *åå¦åªæ[éæ±ï¼1ï¼2,èªå·±]ä¸ä¸ªäºº,
          å ä¸ºéæ±å æ®äº1çä½ç½®ï¼åå¦1å æ®éæ±çä½ç½®æ­¤æ¶å©ä¸ç2ä¼èªå¨å½ä¸ºï¼æä¹å°±ä¼åååä½ã
          é£ä¹è¿ç§æåµä¸ï¼ä¸è¢«å æ®çæ¦çä¸ºp1 = 1/3
          *å¦æ1å æ®äº2çä½ç½®ï¼é£ä¹æ­¤æ¶å°±åè½¬åæäº<1>ä¸­çæåµï¼å©ä¸ä¸ä¸ªæçä½ç½®åéæ±çä½ç½®ï¼
          é£ä¹è¿ç§æåµä¸ï¼ä¸è¢«å æ®çæ¦çä¸ºp2 = (1/3)*(1/2)
          æä»¥æ»çæ¦çæ¯p1 + p2 = 1/3+(1/3)*(1/2) = 1/2
      <3> å å¥æ[éæ±ï¼1ï¼2ï¼3ï¼èªå·±]
          å¦æ1å æ®äºéæ±çä½ç½®ï¼é£ä¹å©ä¸çé½ä¼åå°åä½
          é£ä¹p1 = 1/4
          å¦æ1å æ®äº2çä½ç½®ï¼é£ä¹å°±å<2>çç¶æä¸æ ·äº
          æä»¥æ¦çæ¯p2 = (1/4)*(1/2)
          å¦æ1å æ®äº3çä½ç½®ï¼é£ä¹æä»¬ç¥é2ä¾¿ä¼èªå¨åååä½ï¼é£ä¹å°±å¦å<1>çç¶æäºï¼
          æä»¥æ¦çæ¯p3 = (1/4)*(1/2)
          é£ä¹æ»çæ¦çæ¯ p1+p2+p3 = 1/2
        
      ä»¥æ­¤ç±»æ¨ï¼åè®¾æ[éæ±,1,2,3,.....n-2,èªå·±](n-2 æ¯å ä¸ºè¿æéæ±åèªå·±)
      å¦æ1éæ©éæ±çä½ç½®ï¼é£ä¹2å°n-2é½ä¼åå°èªå·±çä½ç½®
      é£ä¹æ­¤æ¶p1 = 1/(n-1)
      å¦æ1ï¼éæ©2å°±ä¼æ°å¥½è½¬åä¸ºä¸ä¸ä¸ªç¶æï¼èå¦æä»éæ©3-(n-2)é½ä¼è½¬åä¸ºä¹åç
      å ä¸ºä»2å°è¿ä¸ªäººä¹åçäººé½ä¼åå°åä½ï¼èä¹åçææç¶æä¸èªå·±è½åå°åä½çæ¦çé½æ¯1/2
      æä»¥p2 = (n-3)/(n-1)*(1/2) (n-3çåå æ¯é¤å»1ï¼éæ±ï¼èªå·±çä½ç½®)
      æä»¥æ»çæ¦çæ¯p1+p2 = 1/2
      ååªè¦éæ±éä¾¿å æ®åé¢ä¸ä¸ªäººçä½ç½®ï¼é£ä¹æ­¤ç§ç¶æä¸æçä½ç½®ä¸è¢«å æ®çæ¦çé½æ¯1/2
    
    æä»¥ç»¼å(1)å(2)
    p1 = 1/(n-1)
    p2 = ( (n-2)/(n-1) )*( 1/2 ) (è¿én-2çæææ¯ï¼éæ±éä¾¿å¨é¤éæ±åæçä½ç½®ä¸æä¸ä¸ªäººçä½ç½®)
    æä»¥æ»çæ¦çæ¯P =  p1+p2 = n/(2n-2)
    
ACä»£ç 
===
```C++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <vector>

using namespace std;
typedef  long long ll;
const int maxn = 2e5+10;

int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
    scanf("%d",&n);
    double x = 1.0*n/2/(n-1);
    printf("%lf",x);
	return 0;
}
```
    
```diff
!     âï¸2021-01-13
```
    
    
    
    
