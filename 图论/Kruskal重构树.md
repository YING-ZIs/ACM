#   Kruskal重构树


   个人感觉这个算法还是相当有用的。
   
   
   其是对与当前的一个图按照一种优先原则进行建树，大致的过程分为：  
   
   (1) 建树,使用的依然是Kruskal算法  
   (2) 建好的树进行dfs，更新出其fa数组，与求值的数组，为我们的倍增做准备  
   (3) 按所需，对树进行查询  
    
   
   通过Kruskal重建的树，每一个叶子节点是我们原来的图中的节点，而其权值代表的是点值，此时其他的
   度非0的点，其代表的都为边，权值即为边值。
   
   此时建好的树有以下性质(假设我们此时建的是最小生成树)：
   
   (1)其是一个二叉树  
   (2)在原图中任意两个点之前的路径中所需要走的最大的边的值为我们新建的树种两个点的LCA的权值  
   (3)对于当前一个度非0的点(即为边),我们在遍历以其构成的子树中在原图中的所有点时，可以保证边都小于等于当前点的权值  
   (4)因为我们是按照最小生成树去建树的，我们保证了两点之间所经历的边的最大值最小  
   
   
   
   
##  title  
  ###  Life is a Game  
  
    
  # 🥂[Life is a Game](https://ac.nowcoder.com/acm/contest/24872/H)
  
   题的大致意思就是我们从一个点开始出发，每遍历到一个点我们的总的积分就会增加一定的值，我们如果想要到经过一条边，我们就需要
   至少b[x]的积分，问我们最多能获得多少的积分。
   
   那我们的过程就是从一个点到另外的一些点，我们肯定贪心的想走一些权值更小的边，那么我们如果按，最小生成树建成的边就可以保证每
   两个点之间的所要经过的边的最大值最小，也就正好符合我们Kruskal重构树的性质。
   对于Kruskal重构树其最大的便利在于对答案的计算。
   
   我们想如果我们此时的获得总的积分为x，我们能够到达一个边（转化为能够到达新建树的一个点），我们也就可以遍历所有其构成的子树
   的点，所以我们此时获得积分就是其子树种原点的权值的累加。
   那我们构成新树之后就是不断的往上爬，我们能够到达当前的点，我们就获得其所有点的总和，然后我们再想往上爬的时候，我们查看一下
   此时获得的积分加上最初的积分和上一个点（边）比较一下。
   因为一个点的子树的积分总和  和 上一个点的权值是固定，所以其只和我们最初的积分有关，
   如果  最初的积分 + 子树积分总和 >= 上一个点权值 那么我们就可以爬上去
   
   所以我们设定每一个点其父亲的新权值为父亲的权值减去子树的积分和。
   这就转换为一般的问题了，看我们的小白兔最多可以跳到哪里，如果我们的最初积分大于那个节点的值我们就可以蹦过去。
   那就是我们的倍增呀！！！
   
```C++
#include <bits/stdc++.h>

using namespace std;
using i64 = long long;
const int maxn = 1 << 20;

struct node{
	int u, v, w;
};
int n, m, q, root;
int a[maxn], Fa[maxn], W[maxn], fa[maxn][20];
vector<int> adj[maxn];

int find_fa (int x) {
	return Fa[x] == x ? x : Fa[x] = find_fa(Fa[x]);
}
void kruskal (vector<node> c) {
	
	for (int i = 1; i <= 2 * n - 1; i++) Fa[i] = i;
	int cnt = 0;
	sort(c.begin(), c.end(), [&](node x, node y){
		return x.w < y.w;	
	});
	
	for (auto u : c) {
		int x = find_fa(u.u);
		int y = find_fa(u.v);
		int w = u.w;
		if (x != y) {
			
			root = ++cnt + n;
			Fa[x] = root;
			Fa[y] = root;
			adj[root].push_back(x);
			adj[root].push_back(y);
			W[root] = w;
			
			if (cnt == n - 1) {
				return;
			}
		}
	}
}


int sum[maxn], cost[maxn][20];

void dfs1 (int u, int pre) {
	
	sum[u] = a[u];
	for (auto x : adj[u]) {
		dfs1(x, u);
		sum[u] += sum[x];
	}
}

void dfs2 (int u, int pre) {
	fa[u][0] = pre, cost[u][0] = W[pre] - sum[u];
	for (int i = 1 ; i < 20 ; i++) {
		cost[u][i] = max(cost[u][i - 1], cost[fa[u][i - 1]][i - 1]);
		fa[u][i] = fa[fa[u][i - 1]][i - 1];
	} 
	for (auto x : adj[u]) {
		dfs2(x, u);
	}
}
int main () {
	ios::sync_with_stdio(false);cin.tie(0);
	
	cin >> n >> m >> q;
	for (int i = 1; i <= n; i++) cin >> a[i];
	
	vector<node>c(m);
	for (int i = 0; i < m; i++) {
		int u, to, w;
		cin >> u >> to >> w;
		c[i] = {u, to, w};
	}
	
	kruskal(c);
	dfs1(root, 0);
	dfs2(root, 0);

	while (q--) {
		int x, k;
		cin >> x >> k;

		for (int i = 19 ; i >= 0 ; i--) {
			if (cost[x][i] <= k && fa[x][i]) {
				x = fa[x][i];
			}
		}
		
		cout << sum[x] + k << endl;
	}
	
	return 0;
}

```
   
```diff
!   2022-06-11🎨
```
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
  
