🔽[Interacdive Problem](https://codeforces.com/contest/1624/problem/F)
======

    🛰️这道是一道二分的题，有点难搞啊
    
    首先这道题我们想要二分出x,但是我们不能单纯的去取他的值，我们可以利用
    %  的思想，于是我们可操作的便十分有限。
    我们每一次都求出mid表示我们想象中的x的值，然后求出c = (n-mid%n)的值，这个值就是我们进一位所需要的
    最小的值，也是保证其可以加上一个值之后可以向上取到一个整数（进一位）。
    
    所以我们先求一下现在的值 a = mid/n 如果加上 c 之后我们在求一下 b = mid+c/n
    如果 b = a + 1的话那么说明 mid 的值就等于 x. 我们马上就可以求出这个值了
    如果b > a+1的话，那么说明我们预估的mid 的值要比当前x的真实值要小，我们就让l=mid;
    否则，说明我们预估的x 的值太大，就可以把r=mid-1。
    所以我们可以直接让c+1取和返回的值就可以了。
    
```C++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>

using namespace std;
const int maxn = 100;
int k[maxn],p[maxn],a[maxn];
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
	int n;cin >> n;
	int l=1,r=n-1;
	while(l < r){
		int mid= l + r + 1 >> 1;
		int c = n-mid%n,k=mid/n+1;
		cout << "+ " << c << endl;
		int x;cin >> x;
		if(x >= k) l=mid;
		else       r=mid-1;
		l+=c;r+=c;
	}cout << "! "<< l << endl;
	return 0;
}
```

```diff
!      🚴2021-01-12
```
