---
title: ErikTse
createTime: 2025/07/08 17:03:15
permalink: /article/4vfoe32g/
---
# 入门算法
---
## 零散的
数组最大开 1e7
## 前缀和差分
#### 前缀
一维前缀和
有数组`a[n]`，新建数组`prefix[n]`作用是存储前 n 的和，则要求 (l, r) 范围和只需要 `prefix[r] - prefix[l - 1]` 即可
题目：https://www.starrycoding.com/problem/7
二维前缀和
`prefix[i][j] = prefix[i - 1][j] + prefix[i][j - 1] - prefix[i - 1][j - 1] + a[i][j]`
#### 差分
一维差分
输入数组`a[n]`差分数组`p[n]`前缀和数组`prefix[n]`
`p[n] = a[i] - a[i - 1]`
`prefix[i] = prefix[i - 1] + p[i]`
差分数组的前缀和 prefix[n] == a[n]
二维差分
输入数组`a[n][n]`差分数组`p[n][n]`前缀和数组`prefix[n][n]`
对(x1, y1)到(x2, y2)加c的操作：
```c++
p[x1][y1] += c;
p[x1][y2 + 1] -= c;
p[x2 + 1][y1] -= c;
p[x2 + 1][y2 + 1] += c;
```

## 位运算

|双目|0 0|1 0|0 1|1 1|
|---|---|---|---|---|
|与&|xxxxxxxxxx28 1#include <iostream>2#include <deque>3​4int main() {5    std::deque<int> d;6​7    // 插入元素8    d.push_back(1);9    d.push_front(2);10    d.insert(d.begin() + 1, 3);11​12    // 访问元素13    std::cout << "Front element: " << d.front() << std::endl;14    std::cout << "Back element: " << d.back() << std::endl;15    std::cout << "Element at index 1: " << d[1] << std::endl;16​17    // 删除元素18    d.pop_front();19    d.erase(d.begin());20​21    // 遍历元素22    for (int elem : d) {23        std::cout << elem << " ";24    }25    std::cout << std::endl;26​27    // 容量和大小28    std::cout << "Size: " << d.size() << std::endlcpp|0|0|1|
|或&#124;|0|1|1|1|
|异或^(⊕/xor)|0|1|1|0|

|单目|0|1|2|-1|
|---|---|---|---|---|
非!|1|0|0|0|
取反~
移位<< >>

一些常用的位运算
```c++
(a + b) >> 1 == (a + b) / 2
(a & 1) ^ 0 == a % 2 // 判断是否为奇数，取二进制第一位和 1 & 再和 0 ^
```

## 排序
sort 的自定义排序
写一个bool函数，true表示第一个数在第二个数之前
使用Lambda表达式进行降序排序
```cpp
std::sort(vec.begin(), vec.end(), [](int a, int b){return a > b;});
```
当数据范围比较小的时候计数排序的效率会非常高
**计数排序**
```cpp
#include <iostream>
using namespace std;
const int N = 3e6 + 9; // 输入的数据范围
int a[N];
int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        int num;
        cin >> num;
        a[num]++;
    }
    for (int i = 0; i <= 2e5; i++) // 0 <= a <= 2e5
    {
        int count = a[i];
        while (count--)
            cout << i << " ";
    }
}
```
**归并排序**
```cpp
int a[N], c[N];
void mergeSort(int a[], int left, int right) // 归并排序
{
    if (left < right)
    {
        int mid = (left + right) >> 1;

        mergeSort(a, left, mid);
        mergeSort(a, mid + 1, right);
        int i = left, j = mid + 1, k = left; // i: [left, mid] j: (mid, right] k: [left, right]
        while (i <= mid && j <= right)
        {
            if (a[i] <= a[j])
                c[k++] = a[i++];
            else
                c[k++] = a[j++];
        }
        while (i <= mid)
            c[k++] = a[i++];
        while (j <= right)
            c[k++] = a[j++];
        for (int l = left; l <= right; l++)
            a[l] = c[l];
    }
}
```
**快速搜索**
```cpp
int qSearch(int left, int right)
{
    int temp = a[left];
    while (left < right)
    {
        while (left < right && temp <= a[right])
            right--;
        a[left] = a[right];
        while (left < right && temp >= a[left])
            left++;
        a[right] = a[left];
    }
    a[left] = temp;
    return left;
}

void find(int left, int right, int target)
{
    int ans = qSearch(left, right);
    if (ans == target)
        cout << a[ans] << '\n';
    else if (ans < target)
        find(ans + 1, right, target);
    else
        find(left, ans - 1, target);
}

void solve()
{
    cin >> n >> k;
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    find(1, n, k + 1);
}
```
## 单调栈和单调队列
## 树状数组和离散化
#### 树状数组
https://blog.csdn.net/qq_40941722/article/details/104406126
https://blog.csdn.net/TheWayForDream/article/details/118436732
**lowbit(x)**
如何计算一个非负整数n在二进制下的最低为1及其后面的0构成的数？
例如： 44 = (101100)2​，最低为1和后面的0构成的数是 (100)2 = 4
所以 lowbit(44) = lowbit((101100)2) = (100)2 = 4

那么lowbit运算时怎么实现的呢？
44的二进制=(101100)，我们对44的二进制数取反+1，也即~44+1,得到-44
-44的二进制=(010100)，然后我们把44和-44的二进制进行按位与运算，也即按位&得到,二进制000100，也就是十进制的4

所以lowbit(x) = x&(-x)
**区间修改区间求和**
http://t.csdnimg.cn/8RzMG

差分数组：c[i]=a[i]-a[i-1]
然后可以发现 a[i]=a[1]+a[2]-a[1]+a[3]-a[2]+…+a[i]-a[i-1]=c[1]+c[2]+…+c[i]

1，区间修改单点查询
修改a[l]到a[r]值 的时候，只需修改c[l]和c[r+1],然后求一次c[i]的前缀和就可以。
2，区间修改区间查询
还是利用差分的思想。区间求和的公式为：
sum(1,n)
=a[1]+a[2]+a[3]+…+a[n-1]+a[n]
=c[1]+(c[1]+c[2])+…+(c[1]+c[2]+…+c[n])
=n*(c[1]+c[2]+…+c[n])-(0*c[1]+1*c[2]+2*c[3]+…+(n-1)*c[n]).
再利用一个c2数组，使c2[i]=(i-1)*(a[i]-a[i-1])=(i-1)*c[i];
区间修改就有
add(c[l], val), add(c[r+1], -val);
add(c2[l], (l-1)*v),add(c2[r+1], -r*v);
求和时
sum1 = getsum(c, r)*r-getsum(c2,r);
sum2 = getsum(c, l - 1)*(l - 1) - getsum(c2, l - 1);
所以ans=sum1-sum2;

```cpp
#include<bits/stdc++.h>
using namespace std;
using long long ll;
const int maxn = 1e5 + 5;
ll c[maxn], c2[maxn], a[maxn];
int m, n;
void updata(ll r[], int pos, ll val)
{
    while ()
}
LL getsum(LL r[],int pos)
{
    LL ret = 0;
    for (; pos; pos -= pos&(-pos))
        ret += r[pos];
    return ret;
}
int main()
{
    while (scanf("%d%d", &n, &m) != EOF) {
        for (int i = 1; i <= n; i++) {
            scanf("%lld",&a[i]);
            add(c, i, a[i] - a[i - 1]);
            add(c2, i, (i - 1)*(a[i] - a[i - 1]));
        }
        for (int i = 1; i <= m; i++) {
            int op, l, r;
            LL val;
            scanf("%d",&op);
            if (op == 1) {
                scanf("%d%d%lld",&l,&r,&val);
                add(c, l, val);
                add(c, r + 1, -val);
                add(c2, l, (l - 1)*val);
                add(c2, r + 1, -r*val);
            }
            else {
                scanf("%d%d",&l,&r);
                LL sum1 = getsum(c, r)*r-getsum(c2,r);
                LL sum2 = getsum(c, l - 1)*(l - 1) - getsum(c2, l - 1);
                printf("%lld\n",sum1-sum2);
            }
        }
    }
    return 0;
}
```

# 数据结构
## 单调栈
