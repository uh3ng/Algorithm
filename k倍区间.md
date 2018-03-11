### k倍区间

[题目链接](http://lx.lanqiao.cn/problem.page?gpid=T444)

* 问题描述

　
  给定一个长度为N的数列，A1, A2, ... AN，如果其中一段连续的子序列Ai, Ai+1, ... Aj(i <= j)之和是K的倍数，我们就称这个区间[i, j]是K倍区间。

  你能求出数列中总共有多少个K倍区间吗？

* 输入格式
　　
  
  第一行包含两个整数N和K。(1 <= N, K <= 100000)
　　以下N行每行包含一个整数Ai。(1 <= Ai <= 100000)

* 输出格式
　　

  输出一个整数，代表K倍区间的数目。

* 样例输入
<pre>
5 2
1
2
3
4
5
</pre>

* 样例输出

  6

* 数据规模和约定
　　
  
  峰值内存消耗（含虚拟机） < 256M , CPU消耗 < 2000ms

** 前缀和记录，然后扫一遍，只要区间两端点的前缀和%k相等，那么这段区间就是所求区间，只需每次加上之前的与当前位置前缀和%k相等的数量就行。**

```cpp
#pragma warning (disable:4996)
#include<iostream>  
#include<cstdio>  
#include<cstring>  
using namespace std;
typedef long long ll;
const int maxn = 1e5 + 5;
ll sum[maxn], cnt[maxn], n, k;

int main(void)
{
	while (cin >> n >> k)
	{
		memset(sum, 0, sizeof(sum));
		memset(cnt, 0, sizeof(cnt));
		ll ans = 0;
		for (int i = 1; i <= n; i++)  
		{
			ll t;
			scanf("%lld", &t);
			sum[i] = (sum[i - 1] + t) % k;
			ans += cnt[sum[i]];    //只有找到成对的端点才会增加
			cnt[sum[i]]++;
		}
		printf("%lld\n", ans + cnt[0]);
	}
	return 0;
}
```
