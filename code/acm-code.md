# ACM 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [ACM 刷题记录](#acm-刷题记录)
  - [数组](#数组)
    - [明明的随机数](#明明的随机数)
    - [最高分是多少](#最高分是多少)
  - [字符串](#字符串)
    - [进制转换](#进制转换)
    - [字符移位](#字符移位)
  - [动态规划](#动态规划)
    - [上台阶](#上台阶)
    - [三角形](#三角形)
  - [贪心](#贪心)
    - [机器人跳跃问题](#机器人跳跃问题)
  - [数学](#数学)
    - [找零](#找零)
    - [汽水瓶](#汽水瓶)
  - [ACM 模式输入输出练习](#acm-模式输入输出练习)

## 数组

### 明明的随机数

明明生成了N个1到500之间的随机整数。请你删去其中重复的数字，即相同的数字只保留一个，把其余相同的数去掉，然后再把这些数从小到大排序，按照排好的顺序输出。

输入描述：

> 第一行先输入随机整数的个数 N 。接下来的 N 行每行输入一个整数，代表明明生成的随机数。

输出描述：

> 输出多行，表示输入数据处理后的结果

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main(){
    int n, val;
    cin>>n;
    vector<int> res;
    for(int i = 0; i < n; i++){
        cin>>val;
        res.push_back(val);
    }
    sort(res.begin(), res.end());
    vector<int> num;
    num.push_back(res[0]);
    for(int i = 1; i <= n; i++){
        if(res[i] != res[i - 1])
            num.push_back(res[i]);
    }
    for(int i = 0; i < num.size() - 1; i++){
        cout<<num[i]<<endl;
    }
    return 0;
}
```

这个评论解法非常妙：

```c++
#include <iostream>
using namespace std;
int main() {
    int N, n;
    while (cin >> N) {
        int a[1001] = { 0 };
        while (N--) {
            cin >> n;
            a[n] = 1;
        }
        for (int i = 0; i < 1001; i++)
            if (a[i])
            cout << i << endl;
    }
    return 0;
}
```

### 最高分是多少

老师想知道从某某同学当中，分数最高的是多少，现在请你编程模拟老师的询问。当然，老师有时候需要更新某位同学的成绩.

输入描述：

> 每组输入第一行是两个正整数N和M（0 < N <= 30000,0 < M < 5000）,分别代表学生的数目和操作的数目。学生ID编号从1编到N。第二行包含N个整数，代表这N个学生的初始成绩，其中第i个数代表ID为i的学生的成绩。接下来又M行，每一行有一个字符C（只取‘Q’或‘U’），和两个正整数A,B,当C为'Q'的时候, 表示这是一条询问操作，假设A < B，他询问ID从A到B（包括A,B）的学生当中，成绩最高的是多少。当C为‘U’的时候，表示这是一条更新操作，要求把ID为A的学生的成绩更改为B。
> 
> 注意：输入包括多组测试数据。

输出描述：

> 对于每一次询问操作，在一行里面输出最高成绩.

输入例子：

> 5 7
> 
> 1 2 3 4 5
> 
> Q 1 5
> 
> U 3 6
> 
> Q 3 4
> 
> Q 4 5
> 
> U 4 5
> 
> U 2 9
> 
> Q 1 5

输出例子：

> 5
> 
> 6
> 
> 5
> 
> 9

```c++
#include<iostream>
using namespace std;

int main(){
    int n, m, temp;
    //注意有多组数据
    while(cin>>n>>m){
        int stu[n];
        for(int i = 0; i < n; i++){
            cin>>temp;
            stu[i] = temp;
        }
        char c;
        int a, b;
        for(int j = 0; j < m; j++){
            cin>>c>>a>>b;
            if(c == 'Q'){
                if(a > b){
                    int d = a;
                    a = b;
                    b = d;
                }
                int max = 0;
                for(int i = a - 1; i < b; i++)
                    if(stu[i] > max) max = stu[i];
                cout<<max<<endl;
            }
            else stu[a - 1] = b;
        }
    }
    return 0;
}
```

## 字符串

### 进制转换

写出一个程序，接受一个十六进制的数，输出该数值的十进制表示。

输入描述：

> 输入一个十六进制的数值字符串。

输出描述：

> 输出该数值的十进制字符串。不同组的测试用例用\n隔开。

```c++
#include<iostream>
#include<math.h>
using namespace std;

int main(){
    string s;
    int count, sum;
    while(cin>>s){
        count = s.length();
        sum = 0;
        for(int i = count - 1; i >=0; i--){
            if(s[i] >= '0' && s[i] <= '9')
                sum += (s[i] - 48) * pow(16, count - i - 1);
            else if(s[i] >= 'A' && s[i] <= 'F')
                sum += (s[i] - 55) * pow(16, count - i - 1);
        }
        cout<<sum<<endl;
    }
    return 0;
}
```

### 字符移位

小Q最近遇到了一个难题：把一个字符串的大写字母放到字符串的后面，各个字符的相对位置不变，且不能申请额外的空间。

输入描述：

> 输入数据有多组，每组包含一个字符串s，且保证:1<=s.length<=1000.

输出描述：

> 对于每组数据，输出移位后的字符串。

输入例子:

> AkleBiCeilD

输出例子：

> kleieilABCD

```c++
#include<iostream>
using namespace std;

bool isCap(char c){
    if(c >= 'A' && c <= 'Z') return true;
    else return false;
}

int main(){
    int n, left, right;
    string s;
    while(cin>>s){
        n = s.length();
        left = n - 2;
        right = n - 1;
        while(isCap(s[right])){
            right--;
            left--;
        }
        while(left > -1){
            if(isCap(s[left])){
                char temp = s[left];
                for(int i = left; i < right; i++){
                    s[i] = s[i + 1];
                }
                s[right] = temp;
                right--;
            }
            left--;
        }
        cout<<s<<endl;
    }
    return 0;
}
```

## 动态规划

### 上台阶

有一楼梯共m级，刚开始时你在第一级，若每次只能跨上一级或二级，要走上第m级，共有多少走法？注：规定从一级到一级有0种走法。

输入描述：

> 输入数据首先包含一个整数n(1<=n<=100)，表示测试实例的个数，然后是n行数据，每行包含一个整数m，（1<=m<=40), 表示楼梯的级数。

输出描述：

> 对于每个测试实例，请输出不同走法的数量。

```c++
#include<iostream>
using namespace std;

//自定函数要写在 main 函数前面
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

输入描述：

> 本题包含若干组测试数据。对于每一组测试数据。第一行一个n，表示木棍的数量。满足 1<=n<=100000

输出描述：

> 输出最少数量

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

## 贪心

### 机器人跳跃问题

机器人正在玩一个古老的基于DOS的游戏。游戏中有N+1座建筑——从0到N编号，从左到右排列。编号为0的建筑高度为0个单位，编号为i的建筑的高度为H(i)个单位。 起初， 机器人在编号为0的建筑处。每一步，它跳到下一个（右边）建筑。假设机器人在第k个建筑，且它现在的能量值是E, 下一步它将跳到第个k+1建筑。它将会得到或者失去正比于与H(k+1)与E之差的能量。如果 H(k+1) > E 那么机器人就失去 H(k+1) - E 的能量值，否则它将得到 E - H(k+1) 的能量值。游戏目标是到达第个N建筑，在这个过程中，能量值不能为负数个单位。现在的问题是机器人以多少能量值开始游戏，才可以保证成功完成游戏？

输入描述：

> 第一行输入，表示一共有 N 组数据. 第二个是 N 个空格分隔的整数，H1, H2, H3, ..., Hn 代表建筑物的高度

输出描述：

> 输出一个单独的数表示完成游戏所需的最少单位的初始能量

```c++
#include<iostream>
using namespace std;

int main(){
    int n, temp, e = 0;
    cin>>n;
    int h[n];
    for(int i = 0; i < n; i++){
        cin>>temp;
        h[i] = temp;
    }
    //倒过来推导，跳到最后一个恰好为零的话，前一个剩余能量为 e(前一个) = (e + h[i]) / 2 ，再向前取个整
    for(int i = n - 1; i >= 0; i--){
        if((e + h[i]) % 2 == 0)
        e = (e + h[i]) / 2;
        else
        e = (e + h[i]) / 2 + 1;
    }
    cout<<e<<endl;
    return 0;
}
```

## 数学

### 找零

Z国的货币系统包含面值1元、4元、16元、64元共计4种硬币，以及面值1024元的纸币。现在小Y使用1024元的纸币购买了一件价值为N(0< N ≤1024)的商品，请问最少他会收到多少硬币？

输入描述：

> 一行，包含一个数N。

输出描述：

> 一行，包含一个数，表示最少收到的硬币数。

```c++
#include<iostream>
using namespace std;

int main(){
    int n, last, num = 0;
    cin>>n;
    last = 1024 - n;
    num += last / 64;
    last = last % 64;
    num += last / 16;
    last = last % 16;
    num += last / 4;
    last = last % 4;
    num += last;
    cout<<num<<endl;
    return 0;
}
```

### 汽水瓶

某商店规定：三个空汽水瓶可以换一瓶汽水，允许向老板借空汽水瓶（但是必须要归还）。小张手上有n个空汽水瓶，她想知道自己最多可以喝到多少瓶汽水。

输入描述：

> 输入文件最多包含 10 组测试数据，每个数据占一行，仅包含一个正整数 n（ 1<=n<=100 ），表示小张手上的空汽水瓶数。n=0 表示输入结束，你的程序不应当处理这一行。

输出描述：

> 对于每组测试数据，输出一行，表示最多可以喝的汽水瓶数。如果一瓶也喝不到，输出0。

```c++
#include<iostream>
using namespace std;

int main(){
    int n;
    while(cin>>n && n != 0){
        cout<<n / 2<<endl;
    }
    return 0;
}
```

## ACM 模式输入输出练习

- A+B(1)

输入描述：

> 输入包括两个正整数a,b(1 <= a, b <= 1000),输入数据包括多组。

输出描述：

> 输出a+b的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int a, b;
    while(cin>>a>>b){
        cout<< a + b <<endl;
    }
    return 0;
}
```

- A+B(2)

输入描述：

> 输入第一行包括一个数据组数t(1 <= t <= 100), 接下来每行包括两个正整数a,b(1 <= a, b <= 1000)

输出描述：

> 输出a+b的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int t, a, b;
    cin>>t;
    for(int i = 0; i < t; i++){
        cin>>a>>b;
        cout<< a + b <<endl;
    }
    return 0;
}
```

- A+B(3)

输入描述：

> 输入包括两个正整数a,b(1 <= a, b <= 10^9),输入数据有多组, 如果输入为0 0则结束输入

输出描述：

> 输出a+b的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int a, b;
    while(cin>>a>>b && !(a == 0 && b == 0)){
        cout<< a + b <<endl;
    }
    return 0;
}
```

- A+B(4)

输入描述：

> 输入数据包括多组。每组数据一行,每行的第一个整数为整数的个数n(1 <= n <= 100), n为0的时候结束输入。接下来n个正整数,即需要求和的每个正整数。

输出描述：

> 每组数据输出求和的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int n, a, res;
    while(cin>>n && n != 0){
        //每次初始化需要输出的 res
        res = 0;
        for(int i = 0; i < n; i++){
            cin>>a;
            res += a;
        }
        cout<<res<<endl;
    }
    return 0;
}
```

- A+B(5)

输入描述：

> 输入的第一行包括一个正整数t(1 <= t <= 100), 表示数据组数。接下来t行, 每行一组数据。每行的第一个整数为整数的个数n(1 <= n <= 100)。接下来n个正整数, 即需要求和的每个正整数。

输出描述：

> 每组数据输出求和的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int t, n, a, res;
    cin>>t;
    for(int i = 0; i < t; i++){
        res = 0;
        cin>>n;
        for(int j = 0; j < n; j++){
            cin>>a;
            res += a;
        }
        cout<<res<<endl;
    }
    return 0;
}
```

- A+B(6)

输入描述：

> 输入数据有多组, 每行表示一组输入数据。每行的第一个整数为整数的个数n(1 <= n <= 100)。接下来n个正整数, 即需要求和的每个正整数。

输出描述：

> 每组数据输出求和的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int n, a, res;
    while(cin>>n){
        res = 0;
        for(int i = 0; i < n; i++){
            cin>>a;
            res += a;
        }
        cout<<res<<endl;
    }
    return 0;
}
```

- A+B(7)

输入描述：

> 输入数据有多组, 每行表示一组输入数据。每行不定有n个整数，空格隔开。(1 <= n <= 100)。

输出描述：

> 每组数据输出求和的结果

```c++
#include<iostream>
using namespace std;

int main(){
    int a, res = 0;
    while(cin>>a){
        res += a;
        //当输入发生换行时
        if(cin.get() == '\n'){
            cout<<res<<endl;
            res = 0;
        }
    }
    return 0;
}
```

- 字符串排序(1)

输入描述：

> 输入有两行，第一行n。第二行是n个字符串，字符串之间用空格隔开

输出描述：

> 输出一行排序后的字符串，空格隔开，无结尾空格

```c++
#include<iostream>
//vector 容器
#include<vector>
//进行排序所需的的库
#include<algorithm>
using namespace std;

int main(){
    int n;
    string str;
    //string 类型的 vector 容器
    vector<string> s;
    cin>>n;
    for(int i = 0; i < n; i++){
        cin>>str;
        s.push_back(str);
    }
    //排序
    sort(s.begin(), s.end());
    for(int i = 0; i < n - 1; i++){
        cout<<s[i]<<' ';
    }
    cout<<s[n - 1]<<endl;
    return 0;
}
```

- 字符串排序(2)

输入描述：

> 多个测试用例，每个测试用例一行。每行通过空格隔开，有n个字符，n＜100

输出描述：

> 对于每组测试用例，输出一行排序过的字符串，每个字符串通过空格隔开

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main(){
    int n = 0;
    string str;
    vector<string> s;
    while(cin>>str){
        //记录当前行字符串数量
        n++;
        s.push_back(str);
        //如果输入了换行，则进行一次输出
        if(cin.get() == '\n'){
            sort(s.begin(), s.end());
            for(int i = 0; i < n - 1; i++){
                cout<<s[i]<<' ';
            }
            cout<<s[n - 1]<<endl;
            //初始化字符串数量和 vector 容器
            n = 0;
            s.clear();
        }
    }
    return 0;
}
```

- 字符串排序(3)

输入描述：

> 多个测试用例，每个测试用例一行。每行通过,隔开，有n个字符，n＜100

输出描述：

> 对于每组用例输出一行排序后的字符串，用','隔开，无结尾空格

```c++
#include<iostream>
#include<vector>
#include<algorithm>
//流的输入输出需要的库
#include<sstream>
using namespace std;

int main(){
    int n = 0;
    string str;
    vector<string> s;
    while(cin>>str){
        //创建一个流
        stringstream ss;
        string a;
        //注意这里是 <<
        ss<<str;
        //字符用单引号 ' ' ，字符串用双引号 " "
        while(getline(ss, a, ',')){
            n++;
            s.push_back(a);
        }
        sort(s.begin(), s.end());
        for(int i = 0; i < n - 1; i++){
            cout<<s[i]<<',';
        }
        cout<<s[n - 1]<<endl;
        n = 0;
        s.clear();
    }
    return 0;
}
```