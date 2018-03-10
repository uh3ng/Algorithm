## Have Fun with Numbers

[题目链接](https://www.patest.cn/contests/pat-a-practise/1023)

Notice that the number 123456789 is a 9-digit number consisting exactly the numbers from 1 to 9, with no duplication. Double it we will obtain 246913578, which happens to be another 9-digit number consisting exactly the numbers from 1 to 9, only in a different permutation. Check to see the result if we double it again!
Now you are suppose to check if there are more numbers with this property. That is, double a given number with k digits, you are to tell if the resulting number consists of only a permutation of the digits in the original number.

Input Specification:

Each input file contains one test case. Each case contains one positive integer with no more than 20 digits.

Output Specification:

For each test case, first print in a line "Yes" if doubling the input number gives a number that consists of only a permutation of the digits in the original number, or "No" if not. Then in the next line, print the doubled number.

Sample Input:

1234567899

Sample Output:

Yes

2469135798


大数模拟，输出的时候不管是Yes还是No都要有运算结果
```cpp
#pragma warning (disable:4996)
#include <cstdio>
#include <cstring>
#include <stack>
using namespace std;
const int M = 25;
char oldNum[M];
int cntOld[10], cntNew[10];
stack<int> st;
void doIt(int n)
{
	bool f = true;
	int x = 0, y = 0;
	for (int pos = n-1; pos >= 0; pos--)
	{
		cntOld[oldNum[pos] - '0']++;
		x += (oldNum[pos] - '0') * 2;
		//printf("x = %d\n", x);
		y = x % 10;
		x /= 10;
		cntNew[y]++;
		st.push(y);
	}
	if (x)
	{
		st.push(x);
		cntNew[x]++;
	}
	for (int i = 0; i < n; i++)
		if (cntOld[i] != cntNew[i])
		{
			f = false;
			printf("No\n");
			break;
		}
	if (f)
		printf("Yes\n");
	while (!st.empty())
	{
		printf("%d", st.top());
		st.pop();
	}
	return;
}
int main()
{
	scanf("%s", oldNum);
	doIt(strlen(oldNum));
	return 0;
}
```
