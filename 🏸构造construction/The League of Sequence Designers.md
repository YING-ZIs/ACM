⚓[The League of Sequence Designers](https://codeforces.com/gym/102460)
=====
    
    现在构造思维题真的越来越多，本来以为只有cf会出这种，icpc也挺香的
    
    😧看到答案感觉挺简单的，但如果真要让我想，真的做不到呀！
    
    首先题目中有很多细节都没有注意到，首先n < 2000，这个意思是如果题目中给出的l >= 2000,那他本身就是不合法的，
    其次构造的数值都是不能大于1e6的。
    
    然后就是构造的精髓了：
    
    因为合法的l是小于2000的，那我们不如就构造一个1999的，那么不管怎么样，都是合法的。
    
    因为这个错误算法的弊端在于一旦小于0就会把左端点至于这一位，所以我们可以另第一位为-1，后面的2~1999都是大于等于1的数。
    
    并且我们假设2~1999的总和为1999+k
    
    那么错误算法的计算结果就是 1998*(1999+k)
    而实际的正确结果为         1999*(1998+k)
    
    两式相减结果证号为: k
    所以我们只需要把平均分配给2~1999这些数，
    因为如果我们单纯的把k加到第一个数的话，会使得a[i]>1e6

AC代码：
===
```C++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>

using namespace std;
typedef long long ll;
const int maxn = 1e5+10;

int k,l;

void solve(){
	
	int sum=-1;
	printf("1999\n");
	printf("-1");
	int cnt=(k+1)/1998,len=(k+1)%1998;
	for(int i = 1; i <= 1998;i++){
		if(i <= len) {
			printf(" %d",cnt+2);
		}
		else{
			printf(" %d",cnt+1);
		}

	}printf("\n");
}
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif

	int t;scanf("%d",&t);
	while(t--){
		scanf("%d %d",&k,&l);
		if(l >= 2000) printf("-1\n");
		else solve();
	}
	return 0;
}
```
```diff
!     💫2021-01-15
```
