### 基本思路

设 $dp_{i,j}$ 为第 $i$ 天时在第 $j$ 个小屋的方案数，$r_j$ 为第 $j$ 个小屋共有多少条路连接（即 $s_j+l_j$）。

易得转移方程为

$$
dp_{i,j} = \sum_{k=1}^{m}dp_{i-1,k} \cdot (r_j\cdot r_k-l_j\cdot l_k) 
$$

（因为至少走一条短路，所以减去全长路的情况）

### 代码实现

```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
const int MOD = 1e9 + 7;
int n, m, s[105], l[105], r[105], dp[1005][105];
// dp[i][j]:第 i 天时在第 j 个小屋的方案数
signed main(){
	cin >> m >> n;
	for(int i = 1; i <= m; i++) cin >> s[i];
	for(int i = 1; i <= m; i++){
		cin >> l[i];
		r[i] = l[i] + s[i];
	}
	dp[0][1] = 1;
	for(int i = 1; i <= n; i++){ //天数
		for(int j = 1; j <= m; j++){ //小屋编号
			int sum = 0;
			for(int k = 1; k <= m; k++){
				sum += (r[j] * r[k] - l[j] * l[k]) * dp[i - 1][k];
				sum %= MOD;
			}
			dp[i][j] = sum;
		}
	}
	int sum = 0;
	for(int i = 1; i <= m; i++){
		sum += dp[n][i];
		sum %= MOD;
	}
	cout << sum;
	return 0;
}
```
