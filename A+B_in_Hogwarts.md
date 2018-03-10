## A+B in Hogwarts 


> If you are a fan of Harry Potter, you would know the world of magic has its own currency system -- as Hagrid explained it to Harry, "Seventeen silver Sickles to a Galleon and twenty-nine Knuts to a Sickle, it's easy enough." Your job is to write a program to compute A+B where A and B are given in the standard form of "Galleon.Sickle.Knut" (Galleon is an integer in \[0, 1e7], Sickle is an integer in \[0, 17), and Knut is an integer in \[0, 29)).

> Input Specification:

> Each input file contains one test case which occupies a line with A and B in the standard form, separated by one space.

> Output Specification:

> For each test case you should output the sum of A and B in one line, with the same format as the input.
> Sample Input:

> 3.2.1 10.16.27

> Sample Output:

> 14.1.28

从最低的knut开始算起，相加取模作为新的knut，把和除以29作为进位，以后依次。。。

```
#pragma warning (disable:4996)
#include <cstdio>
using namespace std;
int main()
{
	int g1, g2, s1, s2, k1, k2, g, s, k;
	scanf("%d.%d.%d %d.%d.%d", &g1, &s1, &k1, &g2, &s2, &k2);
	int tmp = 0;
	k = (k1 + k2) % 29;
	tmp = (k1 + k2) / 29;
	s = (s1 + s2 + tmp) % 17;
	tmp = (s1 + s2 + tmp) / 17;
	g = g1 + g2 + tmp;
	printf("%d.%d.%d", g, s, k);
	return 0;
}
```
