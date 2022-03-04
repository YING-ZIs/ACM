#  🥣[B - Triple Shift](https://atcoder.jp/contests/arc136/tasks/arc136_b)

    首先我们来考虑一下这个交换的操作，他其实是把选中的连续的三个数逆时针进行旋转。
    
    > 那么我们先说对于所有元素都不相同的情况：
    
    我们考虑对于B数组的前n - 2 个元素，我们总可以保证A数组的对应元素到达与B相同的位置，因为选择三个旋转就能保证。
    那么也就剩下了最后的 2 个元素而对于他们两个我们不可以进行旋转操作了, 那么如果他们两个的顺序与B中的恰好相同，那么就说明
    了可以转化为B,但是我们怎么判断最后的两个数的位置关系呢？
    
    其实我们可以简单验证旋转操作对于整个数组的逆序对数并不会造成影响。
    所以我们可以比较两个数组的逆序对数奇偶性是否相同来进行判断。
    因为总可以通过旋转将A与B的前n - 2个元素进行对应，而旋转并不改变逆序对数，如果他们的逆序对数相同，那也就说明了剩下的两个一定是
    对应相同的。
    
    > 那么我们来考虑第二种情况(存在元素相同)：
    
    如果我们把每一个元素都用一个唯一的标号进行区分，把相同的假设值都为v的元素定义为v1,v2,v3......。那么我们先将B中的元素进行从新编号，
    然后再对A中的进行编号，如果在这种状态下，A与B的逆序对奇偶性相同（v1 > v2 > v3 > ....，而比较其他值时没有区别），则上述说明，可以达到，
    而如果不同的，我们只需要将A中的v1与v2的定义位置对调，这个操作是可以改变逆序对奇偶性的，那么奇偶性就相同了。
    所以如果有元素相同，那么就一定可以变成相同的。
    
```C++
#include <bits/stdc++.h>

using namespace std;
using i64 = long long;
const int maxn  = 1e5 + 10;

int visa[maxn],visb[maxn],a[maxn],b[maxn], c[maxn];
i64 cnt;
void merge(int l,int mid,int r,int a[]){

    int i = l,j = mid + 1, k = l;
    while(i <= mid && j <= r){
        if(a[i] > a[j]){
            cnt += mid - i + 1;
            c[k++] = a[j++];
        } else {
            c[k++] = a[i++];
        }
    }
    while(i <= mid) c[k++] = a[i++];    
    while(j <= r)   c[k++] = a[j++];
    for(int i = l ; i <= r;  i++){
        a[i] = c[i];
    } 
}
void merge_sort(int l,int r,int a[]){

    if(l >= r) return;

    int mid = l + r >> 1;
    merge_sort(l , mid,a);
    merge_sort(mid + 1, r,a);
    merge(l,mid,r,a);

}
int main()
{
#ifndef ONLINE_JUDGE
freopen("in.txt","r",stdin);
freopen("out.txt","w",stdout);
#endif

    ios::sync_with_stdio(false);cin.tie(nullptr);

    int n;
    cin >> n;
    bool ok = false;
    for(int i = 1; i <= n ; i++){
        cin >> a[i];
        visa[a[i]] ++;
        if(visa[a[i]] == 2) ok = true;
    }
    for(int i = 1; i <= n ; i++){
        cin >> b[i];
        visb[b[i]]++;
    }
    for(int i = 1; i <= 5000 ; i++){
        if(visa[i] != visb[i]){
            cout << "No" << endl;
            return 0;
        }
    }

    if(ok){
        cout << "Yes" << endl;
        return 0;
    }
    cnt = 0;
    merge_sort(1, n,a);
    i64 ans = cnt;
    cnt = 0;
    merge_sort(1,n ,b);

    if((ans & 1) == (cnt & 1)){
        cout << "Yes" << endl;
    } else {
        cout << "No" << endl;
    }

    return 0;
}
```

```diff
!    🤡2022-03-04
```
