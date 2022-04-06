# ACM 模式输入输出练习

*Posted by [YanseaTan](https://yansea.cc)*

- [ACM 模式输入输出练习](#acm-模式输入输出练习)
  - [A+B(1)](#ab1)
  - [A+B(2)](#ab2)
  - [A+B(3)](#ab3)
  - [A+B(4)](#ab4)
  - [A+B(6)](#ab6)
  - [A+B(7)](#ab7)
  - [字符串排序(1)](#字符串排序1)
  - [字符串排序(2)](#字符串排序2)
  - [字符串排序(3)](#字符串排序3)

## A+B(1)

输入描述: 输入包括两个正整数a,b(1 <= a, b <= 1000),输入数据包括多组。
输出描述: 输出a+b的结果

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

## A+B(2)

输入描述: 输入第一行包括一个数据组数t(1 <= t <= 100), 接下来每行包括两个正整数a,b(1 <= a, b <= 1000)
输出描述: 输出a+b的结果

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

## A+B(3)

输入描述: 输入包括两个正整数a,b(1 <= a, b <= 10^9),输入数据有多组, 如果输入为0 0则结束输入
输出描述: 输出a+b的结果

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

## A+B(4)

输入描述: 输入数据包括多组。每组数据一行,每行的第一个整数为整数的个数n(1 <= n <= 100), n为0的时候结束输入。接下来n个正整数,即需要求和的每个正整数。
输出描述: 每组数据输出求和的结果

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

#A+B(5)

输入描述: 输入的第一行包括一个正整数t(1 <= t <= 100), 表示数据组数。接下来t行, 每行一组数据。每行的第一个整数为整数的个数n(1 <= n <= 100)。接下来n个正整数, 即需要求和的每个正整数。
输出描述: 每组数据输出求和的结果

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

## A+B(6)

输入描述: 输入数据有多组, 每行表示一组输入数据。每行的第一个整数为整数的个数n(1 <= n <= 100)。接下来n个正整数, 即需要求和的每个正整数。
输出描述: 每组数据输出求和的结果

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

## A+B(7)

输入描述: 输入数据有多组, 每行表示一组输入数据。每行不定有n个整数，空格隔开。(1 <= n <= 100)。
输出描述: 每组数据输出求和的结果

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

## 字符串排序(1)

输入描述: 输入有两行，第一行n。第二行是n个字符串，字符串之间用空格隔开
输出描述: 输出一行排序后的字符串，空格隔开，无结尾空格

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

## 字符串排序(2)

输入描述: 多个测试用例，每个测试用例一行。每行通过空格隔开，有n个字符，n＜100
输出描述: 对于每组测试用例，输出一行排序过的字符串，每个字符串通过空格隔开

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

## 字符串排序(3)

输入描述: 多个测试用例，每个测试用例一行。每行通过,隔开，有n个字符，n＜100
输出描述: 对于每组用例输出一行排序后的字符串，用','隔开，无结尾空格

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