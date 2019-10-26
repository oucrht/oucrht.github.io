# C语言迭代程序设计

## 1.数列求和

已知如下数列
$$
1-\frac{3}{2}+\frac{5}{4}-\frac{7}{8}+\frac{9}{16}...
$$
求前20项的和。

```c
#include <stdio.h>
//数列求和
int main()
{
	int sign = 1,i;
	double term=0.0, sum=0.0, mole = 1.0, deno = 1.0;
	for (i = 1; i <=5; i++)
	{
		term = sign * mole / deno;
		sum += term;
		sign = -sign;
		mole += 2;
		deno *= 2;
	}
	printf("数列的前20项的和为：%.6lf", sum);
	return 0;
}
```

## 2.斐波那契数列

已知斐波那契数列1,1,2,3,5,8,13...... 求第10项的值。

```c
#include <stdio.h>
//求斐波那契数列的第n项值
int main()
{
	int fib=0, fib1=1, fib2=1,i;
	for (i = 1; i <= 10; i++)
	{
		fib = fib1 + fib2;
		fib2 = fib1;
		fib1 = fib;
	}
	printf("数列第10项为%d", fib);
	return 0;
}
```

## 3.整数位数分离

```c
#include <stdio.h>
#include <math.h>
//整数数位分离
int main()
{
    int num, bit = 0, i, temp1, temp2;//temp1和temp2都是为了存储num值的临时变量
    double base;
    printf("请输入一个非负整数：");
    scanf("%d", &num);
    temp1 = num;//将num的值保存在temp1中
    printf("逆序为：");
    while (temp1 > 0)
    {
        printf("%d", temp1 % 10);
        temp1 /= 10;
        bit++;
    }
    if(temp1==0)
    {
        printf("%d",temp1);
        bit++;
    }
    printf("\n它是一个%d位数\n", bit);
    printf("各位数字为：");
    base = pow(10.0, bit - 1.0);
    for (i = bit - 1; i >= 0; i--)
    {
        temp2 = num;
        temp1 = temp2 / base;
        printf("%d ", temp1 % 10);
        base /= 10;
    }
    return 0;
}
```

## 4.最大公约数问题

```c
#include <stdio.h>
//整数数位分离
int gcd(int, int);
int main()
{
	int num1, num2;
	printf("请输入两个数：");
	scanf("%d%d", &num1, &num2);
	printf("最大公约数为%d",gcd(num1, num2));
	return 0;
}

int gcd(int u, int v)
{
	int r;
	while (v != 0)
	{
		r = u % v;
		u = v;
		v = r;
	}
	return u;
}
```

## 5.二分迭代法

> 二分迭代法只适用于在某区间内，函数只穿过一次x轴的情况。

```c
#include <stdio.h>
#include <math.h>
#define E 1e-7
//二分迭代法
double f(double);
int main()
{
	double x1, x2,x0;
	int find = 0;
	printf("请输入区间边界：");
	scanf("%lf%lf", &x1, &x2);
	do
	{
		x0 = (x1 + x2) / 2;//求中点
		if (f(x0) == 0.0) find = 1;//如果中点恰好是函数的根则输出改值
		else if (f(x0) > 0) x2 = x0;//如果中点函数值大于0，说明根在中点左侧（这里假设X1<0,x2>0）
		else x1 = x0;
	} while (!find && fabs(x1 - x2) >= E);
	printf("x0=%lf", x0);
}

double f(double x)
{
	return(x * x * x - 2*x * x + 4);
}

```

`输出结果x0=-1.130395`

![函数图片](C:\Users\rht\Pictures\md文档临时图片.png)

## 6.牛顿迭代法

通过求导得出某一点的切线，进而求得切线与x轴的交点坐标，再以该交点横坐标为新的起始值，重复这一过程.

切线与x轴的交点的横坐标如下：
$$
x=x_0-\frac{f(x)}{f'(x)}
$$
<img src="https://s2.ax1x.com/2019/10/26/KBjMrj.png" style="zoom:80%;" />

 ```c
#include <stdio.h>
#include <math.h>//导入math.h
#define E 1e-5//计算定义精度
double f(double);
double df(double);
int main()
{
	double x, x0 = 1.5;//x0表示起始坐标的横坐标
	do
	{
		x = x0;
		x0 = x0 - f(x0) / df(x0);//这里见上面的说明
	} while (fabs(x - x0) >= E);//判断是否满足定义的精度
	printf("根是%lf", x0);
}
double f(double x)//定义原函数
{
	return(2 * x * x * x - 4 * x * x + 3 * x - 6);
}
double df(double x)//定义原函数的导函数
{
	return(6 * x * x - 8 * x + 3);
}

 ```
