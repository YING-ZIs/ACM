#  [Find the Maximum](https://ac.nowcoder.com/acm/contest/32708/F)


  做完K之后我就一直在想F了，推了很多东西，当时以为可以做出来，看完大佬们的想法才知道自己
  能力还是太弱了，还得练呀！！！
  
  
  首先我们较容易推出的是我们每次都会选取对称轴处的值，这样我们就可以化简式子得出：
  
  (∑bu)²/(4 * (|V|)²)  
  在这里因为我不会再化简式子了，然后就直接设了两个线段考虑他们的合并是否更优，这确实是
  贪心的较为正规的做法，最后推出来的似乎也对？
  
  但是因为化简得问题是的对于这个表达式的含义并没有理解清楚。
                 
  其实我们可以令 X 等于这段路径上的点的b的求和的平均值。
  那么我们就可以较为清楚的求出其实式子的含义是X²/4
  所以我们只需要保证这一段路径的X的绝对值越大即可。
  
  这里可以学到的是，对于一段相连的平均值最大的集合，其值一定是2个或是3个。
  
  对于a b c d
  我们考虑从a 向 右的扩展，
  (1)b能够被加进来的条件是： b > a
  (2)然后c 能够被加进来的的条件是 (a + b + c) / 3 > (a + b) / 2 即为 c > (a + b) / 2
  (3)c 能够被加进来的的条件是 (a + b + c + d) / 4 > (a + b + c) / 3 即为 d > (a + b + c) / 3
  
  所以我们就可以得出b, c, d的大小一定都大于a,那我们完全可以舍去a，而选择剩下的集合中的某个。
  
  
  那么我们的任务就是求下相连的两个，三个的平均值的绝对值得最大值。
  那么我们在输入时其实就已经遍历过所有的相连的两个点了，接下来就是三个点的，那我们就遍历所有的点，
  对其所有连点按照b值进行排序，那我们选择的点就一定是最大的两个或者是最小的两个(负数时)
  
 这里参考的jiangly的代码，码风太赞了,既简洁又明了！！！
 
```C++
#include <bits/stdc++.h>

#define endl "\n"
using namespace std;
using i64 = long long;

vector<int> v[1000010], b(1000010);

bool cmp(int x,int y){
	return b[x] > b[y];
}
int main()
{
	ios::sync_with_stdio(false);cin.tie(0);
	
	int n;  cin >> n;
	for(int i = 1; i <= n ; i++)  cin >> b[i];
	
	double ans = -1e18;
	for(int i = 1 ; i < n ; i++){
		int u, to;  cin >> u >> to;
		v[u].push_back(to);
		v[to].push_back(u);
		ans = max(ans, 1.0 * (b[u] + b[to]) * (b[u] + b[to]) / 16);
	}
	
	for(int i = 1 ; i <= n ;i++){
		sort(v[i].begin(), v[i].end(),cmp);
		
		int m = v[i].size();
		if(m >= 2){
			int x = v[i][0], y = v[i][1];
			ans = max(ans, 1.0 * (b[i] + b[x] + b[y]) * (b[i] + b[x] + b[y]) / 36);
			x = v[i][m - 1], y = v[i][m - 2];
			ans = max(ans, 1.0 * (b[i] + b[x] + b[y]) * (b[i] + b[x] + b[y]) / 36);
		}
	}
	
	cout << fixed <<setprecision(10) << ans << endl;
	
	return 0;
}
```

```diff
!   2022-04-19🦋
```
