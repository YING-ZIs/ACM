#  🚼[D. Infinite Set](https://codeforces.com/contest/1635/problem/D)

  真的感叹这题还能这样写~~~
  
  
+    dp通项公式的求解
  首先我们定义f(x) = k ,表示  2^k <= x <= 2^(k + 1), 那么对于一个x他的f(x)一定是确定的
  
  我们再来考虑一下变换的公式，  
  f(2x + 1) = k + 1(1), f(4x) = k + 2(2)
  
  对于4x较为简单，  
                   因为  2^k <= x <= 2^(k + 1)  
                   所以  2^(k + 2) <= 4x <= 2^(k + 3)  
  
  故 f(4x) = x + 2  
  
  对于2x + 1  
        因为 2^k <= x <= 2^(k + 1)  
        所以 2^(k+1) <= 2x <= 2^(k + 2)      
      
        又因为2x一定是一个偶数，2^(k + 2)也是一个偶数，所以2x + 1一定不会超过2^(k + 2)  
        所以等式  2^(k+1) <= 2x + 1 <= 2^(k + 2) 也是成立的  
      
      
 那么我们来考虑f(x) = k  
 对于f(x) = k的数的集合可以通过两种数得到， 即f(x) = k - 1, f(x) = k - 2  
 即将f(x) = k - 1的数通过(1)变换可以得到f(x) = k  
   将f(x) = k - 2的数通过(2)变换可以得到f(x) = k  
   
 这不就是dp的思想吗？  
 
 
 我们定义dp[i]表示f(x) = i 的元素的个数
 那么我们可以得出递推公式 dp[i] = dp[i - 1] + dp[i - 2]
 
 又因为我们需要求出小于 x^p的元素,那我们只需统计到 p - 1 就可以了
 

+    重复元素的处理


    通过dp[i] = dp[i] + dp[i - 1] + dp[i - 2]我们可以求出dp[i]的值,但是我们并不知道刚求出的值与已存在的是否重复
    了.
    
    那我们只需要判断一下这个元素是否可以通过之前的数得到就可以了.
    
    我们即使将这个数进行逆操作,记录一下他的parent是否已经存在了,如果存在那就说明我们可以通过parent通过若干次变换得到
    他,那他也就不用被记录了。而这个操作是O(log(n))的，因为他至少会被减少一倍。
    
AC代码
```C++
#include <bits/stdc++.h>

#define endl "\n"
using namespace std;
using i64 = long long;
const int mod = 1e9 + 7;

set<int>s;
bool ok;
void dfs(int x){
    
    if(x < 3) return;
    int y = -1;
    if(x & 1){
        y = (x - 1) / 2;
    } else if (x % 4 == 0){
        y = x / 4;
    }
    if(s.count(y)){
        ok = true;
        return;
    }
    dfs(y);
}

int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif
    ios::sync_with_stdio(false);cin.tie(nullptr);

    int n, p;  cin >> n >> p;
    vector<int>a(n + 1),b;
    for(int i = 1; i <= n ; i++)  cin >> a[i], s.insert(a[i]);

    vector<bool>vis(n + 1);
    for(int i = 1; i <= n ; i++){
        ok = false;
        dfs(a[i]);
        vis[i] = ok;
    }
    for(int i = 1; i <= n; i++){
        if(!vis[i]) b.push_back(a[i]);
    }   
    
    vector<i64>dp(p + 1);

    for(auto x : b){
        int k = 32 - __builtin_clz(x) - 1;
        if(k < p) dp[k] = (dp[k] + 1) % mod;
    }
    for(int i = 1 ; i < p ; i++) {
        if(i - 1 >= 0) dp[i] = (dp[i] + dp[i - 1]) % mod;
        if(i - 2 >= 0) dp[i] = (dp[i] + dp[i - 2]) % mod;
    }

    i64 ans = 0;
    for(int i = 0 ; i < p ; i++)  ans = (ans + dp[i]) % mod;
    cout << ans << endl;


    return 0;
}
```
```diff
!    2022-04-04🎳
```
