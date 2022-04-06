# 赛码 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [赛码 刷题记录](#赛码-刷题记录)
  - [动态规划](#动态规划)
    - [上台阶](#上台阶)
    - [三角形](#三角形)

## 动态规划

### 上台阶

有一楼梯共m级，刚开始时你在第一级，若每次只能跨上一级或二级，要走上第m级，共有多少走法？注：规定从一级到一级有0种走法。

输入描述：输入数据首先包含一个整数n(1<=n<=100)，表示测试实例的个数，然后是n行数据，每行包含一个整数m，（1<=m<=40), 表示楼梯的级数。

输出描述：对于每个测试实例，请输出不同走法的数量。

```c++
#include<iostream>
using namespace std;

int num(int m){
  if(m == 1) return 0;
  if(m == 2) return 1;
  int a = 0, b = 1, c = 1;
  for(int i = 3; i <= m; i++){
    a = b;
    b = c;
    c = a + b;
  }
  return c;
}

int main(){
  int n, m;
  cin>>n;
  for(int i = 0; i < n; i++){
    cin>>m;
    cout<<num(m)<<endl;
  }
  return 0;
}
```

### 三角形

在迷迷糊糊的大草原上，小红捡到了n根木棍，第i根木棍的长度为i，小红现在很开心。她想选出其中的三根木棍组成美丽的三角形。但是小明想捉弄小红，想去掉一些木棍，使得小红任意选三根木棍都不能组成三角形。请问小明最少去掉多少根木棍呢？

输入描述：本题包含若干组测试数据。对于每一组测试数据。第一行一个n，表示木棍的数量。满足 1<=n<=100000

输出描述：输出最少数量

```c++
#include<iostream>
#include<vector>
using namespace std;

int res(int n){
  if(n < 4) return 0;
  int a = 1, b = 2, c = 3;
  vector<int> v = {1, 2};
  while(c <= n){
    v.push_back(c);
    a = b;
    b = c;
    c = a + b;
  }
  return n - v.size();
}

int main(){
  int n;
  while(cin>>n){
    cout<<res(n)<<endl;
  }
  return 0;
}
```

