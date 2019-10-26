# C语言题目



## 1.计算1至10所有整数的和

```c
#include <stdio.h>
int main()
{
	int sum=0;
	int a =0;
	for (int i = 1; a <= 10;i++) {
		sum += a;
		a++;
	}
	printf("1至10整数的和为%d", sum);
	return 0;
}
```

## 2.输入两个数，求最大值

```c

#include <stdio.h>
int max(int a, int b);//函数声明
int main()
{
	int a;
	int b;
	int c = 0;
	printf("请输入两个整数：\n");
	scanf_s("%d%d", &a, &b);//输入一个数后回车再输入下一个数【注】
	c = max(a, b);
	printf("\n这两个数中，最大的是：%d", c);
	return 0;
}

int max(int a,int b)
{
	if (a>b)
	{
		return a;//返回最大的数
	}
	else {
		return b;
	}
}
```

> 【注】如果是scanf_s("%d,%d",&a,&b);则在终端窗口中应输入13,16再回车（数字是举例）。

## 3.计算三角形的面积

要求用户输入三角形的三边长，然后根据
$$
area=\sqrt{s(s-a)(s-b)(s-c)},其中s=\frac{a+b+c}{2}
$$
求出面积。

```c
#include <stdio.h>
#include <math.h>
//计算三角形面积
int main(void)
{
	float a, b, c,s,area;
	printf("请输入三角形的三边长：");
	scanf_s("%f%f%f", &a, &b, &c);
	s = (a + b + c) / 2;
	area = sqrt(s * (s - a) * (s - b) * (s - c));
	printf("三角形的面积为：%.2f", area);
	return 0;
}
```

> 注意，因为要用到sqrt()函数，所以要包含math.h头文件。

## 4.输入判断，并求其平方根，结果以整数显示

```c
#include <stdio.h>
#include <math.h>
int main(void)
{
	int num, a;
	printf("请输入一个小于1000的整数：");
	scanf_s("%d", &num);
	while (num >= 1000)
	{
		printf("请重新输入：");
		scanf_s("%d", &num);
	}
	a = sqrt(num);
	printf("平方根为%d", a);
	return 0;
}
```

## 5.程序4.6

```c
#include <stdio.h>
#include <math.h>

int main(void)
{
	float x, y;
	printf("请输入一个数x=");
	scanf_s("%f", &x);
	if (x < 1)
	{
		y = x;
		printf("y=%f", y);
	}
	else if (x<10)
	{
			y = 2 * x - 1;
			printf("y=%f", y);
	}
	else
		{
			y = 3 * x - 11;
			printf("y=%f", y);
		}
	
	return 0;
}
```

## 6.闰年问题

```c
#include <stdio.h>

int isleap(int year)
{
	return(((year % 4 == 0) && (year % 100 != 0)) || (year % 400 == 0));
}

int main()
{
	int start_year,end_year,count=0;
	printf("请输入起始年份：");
	scanf("%d", &start_year);
	printf("请输入终止年份：");
	scanf("%d", &end_year);
	for (int i = start_year; i <= end_year; i++)
	{
		if (isleap(i))
		{
			printf("%6d", i);
			count++;
			if (count % 10 == 0) putchar('\n');

		}
	}
	if (count % 10 != 0) putchar('\n');
	printf("共%d个闰年", count);
	return 0;
}
```



## 7.if语句和switch语句练习题

问题简化

|       利润I        | 提成 |
| :----------------: | :--: |
|    [0,100 000]     | 10%  |
| (100 000,200 000]  | 7.5% |
| (200 000,400 000]  |  5%  |
| (400 000,600 000]  |  3%  |
| (600 000,1000 000] | 1.5% |
|    (1000 000,)     |  1%  |

```c
#include <stdio.h>//第一种方法：用if-else语句实现

int main() {
	double profit=0.0, bonus=0.0;
	printf("请输入一个数字:");
	scanf("%lf", &profit);
	printf("利润是 RMB%.2lf\n", profit);
	if (profit <= 100000)
		bonus = profit * 0.1;
	else if (profit <= 200000)
		bonus = (profit - 100000) * 0.075 + 100000 * 0.1;
	else if (profit <= 400000)
		bonus = (profit - 200000) * 0.05 + 100000 * 0.075 + 100000 * 0.1;
	else if (profit <= 600000)
		bonus = (profit - 400000) * 0.03 + 200000 * 0.05 + 100000 * 0.075 + 100000 * 0.1;
	else if (profit <= 1000000)
		bonus = (profit - 600000) * 0.015 + 200000 * 0.03 + 200000 * 0.05 + 100000 * 0.075 + 100000 * 0.1;
	else
		bonus = (profit - 1000000) * 0.01 + 400000 * 0.015 + 200000 * 0.03 + 200000 * 0.05 + 100000 * 0.075 + 100000 * 0.1;
	printf("你的奖金为RMB%.2lf", bonus);
	return 0;
}

```

```c
#include <stdio.h>//第二种方法：用switch语句

int main() {
	double profit = 0, bonus = 0;
	int temp;
	printf("请输入一个数：");
	scanf("%lf", &profit);
	printf("利润为 RMB%.2lf\n", profit);
	temp =(int)profit / 100000;
	if (temp > 10) temp = 11;
	switch (temp)
	{
	case 11:bonus = (profit - 1000000) * 0.01;
		profit = 1000000;
	case 10:
	case 9 :
	case 8 :
	case 7:bonus = bonus + (profit - 600000) * 0.015;
		profit = 600000;
	case 6 :
	case 5:bonus = bonus + (profit - 400000) * 0.03;
		profit = 400000;
	case 4 :
	case 3:bonus = bonus + (profit - 200000) * 0.05;
		profit = 200000;
	case 2 :
	case 1:bonus = bonus + (profit - 100000) * 0.075;
		profit = 100000;
	case 0:bonus = bonus+profit * 0.1;
	}
	printf("奖金为 RMB%.2lf", bonus);
	return 0;
}
```

## 8.加法表、乘法表

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int arr[]={1,2,3,4,5,6,7,8,9};
    int i,j;
    for(i=0;i<9;i++)
    {

        for(j=i;j<9;j++)
        {
            printf("%d+%d=%2d\t",arr[i],arr[j],arr[i]+arr[j]);//将+改为*即为乘法表
        }
        putchar('\n');
    }
    return 0;
}

```

<img src="https://b2.bmp.ovh/imgs/2019/10/cef5b221c300cea9.png" alt="输出结果" />

![乘法表结果](https://b2.bmp.ovh/imgs/2019/10/ac34d0c29b6c6e9d.png)


## 9.用双重循环打印菱形图案

```c
#include<stdio.h>

void printUpTriangle(int n)//定义上半部分三角形
{
	int i, j;
	for (i = 1; i < n + 1; i++)
	{
		for (j = 1; j < n + i; j++)
		{
			if (j <= n - i) printf(" ");
			else  printf("*");
		}
		putchar('\n');
	}
}
void printDownTriangle(int n)//定义下半部分三角形
{
	int i, j;
	for (i = n - 1; i >= 0; i--)//注意这里i=n-1是为了中间最长的只有一行
	{
		for (j = 1; j < n + i; j++)
		{
			if (j <= n - i) printf(" ");
			else  printf("*");
		}
		putchar('\n');
	}
}

int main()
{
	int n;
	printf("请输入一个数：");
	scanf("%d", &n);
	printUpTriangle(n);
	printDownTriangle(n);
    return 0;
}

```

输出结果如图所示：

![](https://s2.ax1x.com/2019/10/26/KBv5X4.png)

