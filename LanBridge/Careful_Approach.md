### A Careful Approach  
问题描述

　　如果你认为参加一个编程比赛让你感到有压力，那么请你想象你是一个空中交通管制员。因为人命关天，所以一个空中交通管制员必须在时刻变化的环境中专注于任务，解决不可预知的事件。

　　让我们将目光转向飞机的着陆流程。飞机进入目的地飞航情报区之后，就会报告自己的位置、方向和速度，然后管制员就需要制定计划让所有飞机按指令安全着陆。一般来说，连续的两次着陆之间间隔时间越长，就越安全。因为这些额外的时间能够让工程师有机会对天气变化以及其他突发事件作出反应。

　　幸运的是，有一部分计划的制定可以自动化——这就是你来这里的原因。你会得到有关飞机着陆的脚本。每一个飞机都有一个安全着陆时间窗。你算出的指令必须要符合每个飞机的时间窗。另外，飞机的着陆时间点要尽量均匀，使得连续两次着陆的最小间隔尽量大。例如，如果三架飞机分别着陆于10:00am、10:05am、10:15am，那么最小间隔是五分钟，在头两架飞机之间。所有间隔不一定一样，但是最小的间隔要尽量大。
输入格式

　　多组数据。每个数据第一行为一个整数n，为飞机架数。接下来n行，每行两个整数a[i]，b[i]表示这架飞机只能在闭区间[a[i],b[i]]间降落。a[i]和b[i]的单位是分钟。输入的最后一行是一个零。

输出格式

　　对于每组数据，先输出第几组，然后输出最小间隔，单位为分和秒，舍入到最近的整数。格式参见样例。

样例输入
<pre>
3
0 10
5 15
10 15
2
0 10
10 20
0
</pre>

样例输出
<pre>
Case 1: 7:30
Case 2: 20:00
</pre>

数据规模和约定
　　20% n<=5
　　100% 2<=n<=8, 0<=a[i], b[i]<=1440, 数据组数不大于20.

**第一感觉是二分，然而需要找一个降落顺序，如果单纯排序的话结果不一定正确，采用学长讲的枚举每个序列，可以直接用next_permutation生成全排列，数据规模也不大，时间够用**

```cpp
#include <cstdio>
#include <string>
#include <algorithm>
#include <math.h>
using namespace std;  
const int M = 10;  
int num[M], pos[M];  
int n;  
double ans;
struct node
{  
    int a,b;  
}s[M];   
bool check(double len)  
{  
    double x = s[pos[1]].a;  
    for(int i = 2;i <= n;++i)  
    {  
        x += len;  
        if(x > s[pos[i]].b)  
            return 0;  
        if(x < s[pos[i]].a)  
            x = s[pos[i]].a;  
    }  
    return 1;  
}  
int main()  
{  
    int T = 1;  
    while(~scanf("%d",&n))  
    {  
        if(n == 0) break;  
        for(int i = 1;i <= n;++i)  
        {  
            num[i] = i;  
            scanf("%d %d",&s[i].a,&s[i].b);  
        }  
        ans = 0;  
        do{  
            for(int i = 1;i <= n;++i)  
            {  
                pos[num[i]] = i;  
            }  
            double l = 0,r = 1440, mid;  
            while(r - l > 1e-6)  
            {  
                mid = (l + r) / 2;  
                if(check(mid))  
                    l = mid;  
                else  
                    r = mid;  
            }  
            ans = max(ans,r);  
        } while (next_permutation(num + 1, num + 1 + n));  //生成全排列
        ans *= 60;  
        printf("Case %d: %d:%02d\n",T++,(int)ans / 60,int(fmod(ans,60) + 0.5));  //fmod用于取余
    }  
    return 0;  
}  
```
