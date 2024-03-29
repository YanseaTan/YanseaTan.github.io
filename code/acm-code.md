# ACM 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [ACM 刷题记录](#acm-刷题记录)
  - [数组](#数组)
    - [明明的随机数](#明明的随机数)
    - [最高分是多少](#最高分是多少)
    - [序列找数](#序列找数)
    - [赛马](#赛马)
    - [查找数字](#查找数字)
    - [找到1的组数](#找到1的组数)
    - [质数因子](#质数因子)
  - [字符串](#字符串)
    - [进制转换](#进制转换)
    - [字符移位](#字符移位)
    - [扭蛋机](#扭蛋机)
    - [数字转字符串](#数字转字符串)
    - [字符集合](#字符集合)
    - [计算某字符出现次数](#计算某字符出现次数)
    - [提取不重复的整数](#提取不重复的整数)
    - [句子逆序](#句子逆序)
    - [字符串排序](#字符串排序)
    - [密码验证合格程序](#密码验证合格程序)
    - [简单密码](#简单密码)
    - [删除字符串中出现次数最少的字符](#删除字符串中出现次数最少的字符)
    - [DNA匹配](#dna匹配)
  - [动态规划](#动态规划)
    - [上台阶](#上台阶)
    - [三角形](#三角形)
    - [01背包](#01背包)
  - [贪心](#贪心)
    - [机器人跳跃问题](#机器人跳跃问题)
    - [连续最大和](#连续最大和)
    - [最大乘积](#最大乘积)
  - [数学](#数学)
    - [找零](#找零)
    - [汽水瓶](#汽水瓶)
    - [数字翻转](#数字翻转)
    - [搬圆桌](#搬圆桌)
    - [求解f(n)](#求解fn)
    - [猜数](#猜数)
    - [坐标移动](#坐标移动)
    - [计算字符重新排列数](#计算字符重新排列数)
    - [集合P](#集合p)
  - [ACM 模式输入输出练习](#acm-模式输入输出练习)

<br><br><br>

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

<br><br><br>

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

<br><br><br>

### 序列找数

从非负整数序列 0, 1, 2, ..., n中给出包含其中n个数的子序列，请找出未出现在该子序列中的那个数。

输入描述：

> 输入为n+1个非负整数，用空格分开。其中：首个数字为非负整数序列的最大值n，后面n个数字为子序列中包含的数字。

输出描述：

> 输出为1个数字，即未出现在子序列中的那个数。

示例：

> 输入：3 3 0 1
> 
> 输出：2

```c++
#include<iostream>
using namespace std;

int main(){
    int max, temp;
    cin>>max;
    int nums[9999];
    for(int i = 0; i < max; i++){
        cin>>temp;
        nums[temp] = 1;
    }
    max++;
    while(max--){
        if(!nums[max]) cout<<max<<endl;
    }
    return 0;
}
```

<br><br><br>

### 赛马

沫璃有2*n匹马，每匹马都有一个速度v。现在沫璃将马分成两个队伍，每个队伍各有n匹马，两个队之间进行n场比赛，每场比赛两队各派出一匹马参赛，每匹马都恰好出场一次。沫璃想知道是否存在一种分配队伍的方法使得无论怎么安排比赛，第一个队伍都一定能获得全胜。两匹马若速度不一样，那么速度快的获胜，若速度一样，则都有可能获胜。

输入描述：

> 第一行一个数T(T<=100)，表示数据组数。
> 
> 对于每组数据，第一行一个整数n , (1<=n<=100)
> 
> 接下来一行，2*n个整数，第i个整数vi表示第i匹马的速度, (1 <= vi <= 1000)

输出描述：

> 对于每组数据，输出一行，若存在一种分配方法使得第一个队伍全胜输出YES，否则输出NO

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main(){
    int t, n, v;
    while(cin>>t){
        for(int i = 0; i < t; i++){
        cin>>n;
        vector<int> m(2 * n);
        for(int j = 0; j < 2 * n; j++){
            cin>>v;
            m[j] = v;
        }
        sort(m.begin(), m.end());
        if(m[n - 1] == m[n]) cout<<"NO"<<endl;
        else cout<<"YES"<<endl;
        }
    }
    return 0;
}
```

<br><br><br>

### 查找数字

给定数组，任意相邻两个元素的差的绝对值为1，设计一个算法，在该数组中可以查找某个元素的位置，如果该元素的值多次出现，返回第一次的位置。例如{4, 5, 6, 5, 6, 7, 8, 9, 10, 9}元素9出现了两次，第一次出现的位置7。

```c++
#include<iostream>
using namespace std;

int main(){
    // 举一个输入的例子，注意普通数组的格式
    int a[] = {4,5,6,5,6,7,8,9,10,9};
    int target, n = sizeof(a);
    while(cin>>target){
        int i = 0;
        while(i < n && i >=0){
            if(a[i] == target){
                cout<<i<<endl;
                break;
            }
            i += abs(target - a[i]);
        }
    }
    return 0;
}
```

<br><br><br>

### 找到1的组数

一个只包含0和1的阵列，找到1的组的个数，每个组的定义是横向和纵向相邻的值都为1。

```c++
#include<iostream>
#include<vector>
using namespace std;

// 注意要用引用 &，才会对矩阵内容实际进行修改
void clear(int i, int j, vector<vector<int>> &matrix){
    if(i < matrix.size() && i >= 0 && j < matrix[0].size() && j >= 0){
        if(matrix[i][j] == 1){
            matrix[i][j] = 0;
            clear(i - 1, j, matrix);
            clear(i + 1, j, matrix);
            clear(i, j - 1, matrix);
            clear(i, j + 1, matrix);
        }
    }
}

bool dfs(int i, int j, vector<vector<int>> &matrix){
    if(matrix[i][j] == 1){
        clear(i, j, matrix);
        return true;
    }
    else return false;
}

int findOne(vector<vector<int>> &matrix){
    int m = matrix.size();
    int n = matrix[0].size();
    int count = 0;
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(dfs(i, j, matrix)) count++;
        }
    }
    return count;
}

int main(){
    // 输入好 matrix
    cout<<findOne(matrix)<<endl;
    return 0;
}
```

<br><br><br>

### 质数因子

输入一个正整数，按照从小到大的顺序输出它的所有质因子（重复的也要列举）（如180的质因子为2 2 3 3 5 ）

```c++
#include<iostream>
using namespace std;

int main()
{
    int x = 0;
    cin >> x;
    for (int i = 2; i * i <= x; ++i)
    {
        if (x % i == 0)
        {
            cout << i << ' ';
            x /= i;
            i = 1;
        }
    }
    cout << x;
    return 0;
}
```

<br><br><br>

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

<br><br><br>

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

<br><br><br>

### 扭蛋机

22娘和33娘接到了小电视君的扭蛋任务：

一共有两台扭蛋机，编号分别为扭蛋机2号和扭蛋机3号，22娘使用扭蛋机2号，33娘使用扭蛋机3号。扭蛋机都不需要投币，但有一项特殊能力：

扭蛋机2号：如果塞x（x范围为>=0整数）个扭蛋进去，然后就可以扭到2x+1个

扭蛋机3号：如果塞x（x范围为>=0整数）个扭蛋进去，然后就可以扭到2x+2个

22娘和33娘手中没有扭蛋，需要你帮她们设计一个方案，两人“轮流扭”（谁先开始不限，扭到的蛋可以交给对方使用），用“最少”的次数，使她们能够最后恰好扭到N个交给小电视君。

输入描述：

> 输入一个正整数，表示小电视君需要的N个扭蛋。

输出描述：

> 输出一个字符串，每个字符表示扭蛋机，字符只能包含"2"和"3"。

```c++
#include<iostream>
using namespace std;

int main(){
    int n;
    string temp, res;
    cin>>n;
    while(n){
        if(n % 2){
            res = "2" + res;
            n = (n - 1) / 2;
        }
        else{
            res = "3" + res;
            n = (n - 2) / 2;
        }
    }
    cout<<res<<endl;
    return 0;
}
```

<br><br><br>

### 数字转字符串

将给定的数转换为字符串，原则如下：1对应 a，2对应b，…..26对应z，例如12258可以转换为"abbeh", "aveh", "abyh", "lbeh" and "lyh"，个数为5，编写一个函数，给出可以转换的不同字符串的个数。

```c++
#include<iostream>
#include<vector>
using namespace std;

int main() {
    string str;
    while(cin>>str){
        int n = str.size();
        vector<int> dp(n + 1);
        dp[n] = 1;
        for (int i = n - 1; i >= 0; i--) {
            if (str[i] == '0') {
                dp[i] = 0;
            }
            else {
                dp[i] = dp[i + 1];
                // 确保不是最后一位
                if (i < n - 1) {
                    // string 转 int
                    int num = (str[i] - '0') * 10 + str[i + 1] - '0';
                    if (num <= 26) {
                        dp[i] += dp[i + 2];
                    }
                }
            }
        }
        cout << dp[0] << endl;
    }
    return 0;
}
```

<br><br><br>

### 字符集合

输入一个字符串，求出该字符串包含的字符集合，按照字母输入的顺序输出。

数据范围：输入的字符串长度满足 1 <= n <= 100，且只包含大小写字母，区分大小写。

本题有多组输入。

输入描述：

> 每组数据输入一个字符串，字符串最大长度为100，且只包含字母，不可能为空串，区分大小写。

输出描述：

> 每组数据一行，按字符串原有的字符顺序，输出字符集合，即重复出现并靠后的字母不输出。

自己用的无序哈希集合：

```c++
#include<iostream>
#include<string>
#include<unordered_set>
using namespace std;
int main()
{
    unordered_set<char> uset;
    string tmp;
    while(cin >> tmp)
    {
        for (int i = 0; i < tmp.size(); ++i)
        {
            uset.emplace(tmp[i]);
        }
        for (int i = 0; i < tmp.size(); ++i)
        {
            if (uset.count(tmp[i]))
            {
                cout << tmp[i];
                uset.erase(tmp[i]);
            }
        }
        cout << endl;
    }
    return 0;
}
```

<br><br><br>

### 计算某字符出现次数

写出一个程序，接受一个由字母、数字和空格组成的字符串，和一个字符，然后输出输入字符串中该字符的出现次数。（不区分大小写字母）

数据范围：1 ≤ n ≤ 1000 

输入描述：

> 第一行输入一个由字母和数字以及空格组成的字符串，第二行输入一个字符。

输出描述：

> 输出输入字符串中含有该字符的个数。（不区分大小写字母）

自己：

```c++
#include<iostream>
using namespace std;

int main()
{
    int nums[1001] = {0};
    char c;
    while (cin >> c)
    {
        if (c >= 'a' && c <= 'z')
        {
            // 小写字母比大写字母大 32
            c -= 32;
        }
        nums[c]++;
    }
    cout << nums[c] - 1 << endl;
    return 0;
}
```

<br><br><br>

### 提取不重复的整数

输入一个 int 型整数，按照从右向左的阅读顺序，返回一个不含重复数字的新的整数。

保证输入的整数最后一位不是 0 。

输入实例：

> 9876673

输出示例：

> 37689

自己：

```c++
#include <iostream>
#include <string>
using namespace std;
 
int main()
{
    string num;
    cin >> num;
    int nums[10] = {0};
    for (int i = num.size() - 1; i >= 0; --i)
    {
        if (nums[num[i] - '0'] == 0)
        {
            cout << num[i];
            nums[num[i] - '0']++;
        }
    }
    return 0;
}
```

<br><br><br>

### 句子逆序

将一个英文语句以单词为单位逆序排放。例如“I am a boy”，逆序排放后为“boy a am I”

所有单词之间用一个空格隔开，语句中除了英文字母外，不再包含其他字符

```c++
#include<iostream>
#include<string>
#include<vector>
using namespace std;

int main()
{
    string s;
    vector<string> ss;
    while (cin >> s)
    {
        ss.push_back(s);
    }
    for (int i = ss.size() - 1; i >= 0; --i)
    {
        cout << ss[i] << ' ';
    }
    return 0;
}
```

<br><br><br>

### 字符串排序

给定 n 个字符串，请对 n 个字符串按照字典序排列。

输入描述：

> 输入第一行为一个正整数n(1≤n≤1000),下面n行为n个字符串(字符串长度≤100),字符串中只含有大小写字母。

输出描述：

> 数据输出n行，输出结果为按照字典序排列的字符串。

自己：

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
using namespace std;

int main()
{
    int n = 0;
    cin >> n;
    string s;
    vector<string> svec;
    for (int i = 0; i < n; ++i)
    {
        cin >> s;
        svec.push_back(s);
    }
    sort(svec.begin(), svec.end());
    for (auto x : svec)
    {
        cout << x << endl;
    }
    return 0;
}
```

<br><br><br>

### 密码验证合格程序

密码要求:

1. 长度超过8位

2. 包括大小写字母.数字.其它符号,以上四种至少三种

3. 不能有长度大于2的包含公共元素的子串重复 （注：其他符号不含空格或换行）

输入描述：

> 一组字符串。

输出描述：

> 如果符合要求输出：OK，否则输出NG

自己：

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string s;
    while (cin >> s)
    {
        if (s.size() < 9)
        {
            cout << "NG" << endl;
        }
        else
        {
            int countN = 0;
            int countA = 0;
            int counta = 0;
            int countO = 0;
            for (auto x : s)
            {
                if (x >= '0' && x <= '9')
                {
                    countN = 1;
                }
                else if (x >= 'A' && x <= 'Z')
                {
                    countA = 1;
                }
                else if (x >= 'a' && x <= 'z')
                {
                    counta = 1;
                }
                else
                {
                    countO = 1;
                }
            }
            int count = countA + counta + countN + countO;
            
            bool flag = true;
            for (int i = 0; i < s.size() - 6; ++i)
            {
                for (int j = i + 3; j < s.size() - 3; ++j)
                {
                    if (s[j] == s[i])
                    {
                        if ((s[j + 1] == s[i + 1]) && (s[j + 2] == s[i + 2]))
                        {
                            flag = false;
                            break;
                        }
                    }
                }
                if (flag == false)
                {
                    break;
                }
            }
            
            if (count > 2 && flag)
            {
                cout << "OK" << endl;
            }
            else
            {
                cout << "NG" << endl;
            }
        }
    }
    return 0;
}
```

<br><br><br>

### 简单密码

现在有一种密码变换算法。

九键手机键盘上的数字与字母的对应： 1--1， abc--2, def--3, ghi--4, jkl--5, mno--6, pqrs--7, tuv--8 wxyz--9, 0--0，把密码中出现的小写字母都变成九键键盘对应的数字，如：a 变成 2，x 变成 9。

而密码中出现的大写字母则变成小写之后往后移一位，如：X ，先变成小写，再往后移一位，变成了 y ，例外：Z 往后移是 a 。

数字和其它的符号都不做变换。

自己：

```c++
#include<iostream>
#include<string>
using namespace std;

int main()
{
    string s;
    cin >> s;
    for (char x : s)
    {
        if (x >= 'a' && x <= 'c')
        {
            cout << '2';
        }
        else if (x >= 'd' && x <= 'f')
        {
            cout << '3';
        }
        else if (x >= 'g' && x <= 'i')
        {
            cout << '4';
        }
        else if (x >= 'j' && x <= 'l')
        {
            cout << '5';
        }
        else if (x >= 'm' && x <= 'o')
        {
            cout << '6';
        }
        else if (x >= 'p' && x <= 's')
        {
            cout << '7';
        }
        else if (x >= 't' && x <= 'v')
        {
            cout << '8';
        }
        else if (x >= 'w' && x <= 'z')
        {
            cout << '9';
        }
        else if (x >= 'A' && x <= 'Y')
        {
            cout << (char)(x + 33);
        }
        else if (x == 'Z')
        {
            cout << 'a';
        }
        else
        {
            cout << x;
        }
    }
    return 0;
}
```

<br><br><br>

### 删除字符串中出现次数最少的字符

实现删除字符串中出现次数最少的字符，若出现次数最少的字符有多个，则把出现次数最少的字符都删除。输出删除这些单词后的字符串，字符串中其它字符保持原来的顺序。

数据范围：输入的字符串长度满足 1 ≤ n ≤ 20  ，保证输入的字符串中仅出现小写字母

自己：

```c++
#include<iostream>
#include<vector>
using namespace std;
 
int main()
{
    string s;
    cin >> s;
    int nums[128] = {0};
    for (auto x : s)
    {
        nums[x]--;
    }
    int minN = -20;
    vector<int> id;
    for (int i = 0; i < 128; ++i)
    {
        if (nums[i] == 0)
        {
            continue;
        }
        if (nums[i] > minN)
        {
            minN = nums[i];
        }
    }
    for (int i = 0; i < 128; ++i)
    {
        if (minN == nums[i])
        {
            id.push_back(i);
        }
    }
    bool flag = false;
    for (char x : s)
    {
        for (int y : id)
        {
            if (x == y)
            {
                flag = true;
                break;
            }
        }
        if (flag)
        {
            flag = false;
            continue;
        }
        cout << x;
    }
    return 0;
}
```

<br><br><br>

### DNA匹配

有一种特殊的DNA，仅仅由核酸A和T组成，长度为n，顺次连接

科学家有一种新的手段，可以改变这种DNA。每一次，科学家可以交换该DNA上两个核酸的位置，也可以将某个特定位置的核酸修改为另一种核酸。

现在有一个DNA，科学家希望将其改造成另一种DNA，希望你计算最少的操作次数。

输入描述：

> 输入包含两行，第一行为初始的DNA，第二行为目标DNA，保证长度相同。

输出描述：

> 输出最少的操作次数

```c++
#include <iostream>

using namespace std;

int main()
{
    string a;
    string b;
    cin >> a >> b;
    int cntA = 0;
    int cntT = 0;
    for (int i = 0; i < a.size(); ++i)
    {
        if (a[i] == b[i])
        {
            continue;
        }
        else
        {
            if (a[i] == 'A')
            {
                ++cntA;
            }
            else
            {
                ++cntT;
            }
        }
    }
    cout << max(cntA, cntT);
    return 0;
}
```

<br><br><br>

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

<br><br><br>

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

<br><br><br>

### 01背包

已知一个背包最多能容纳体积之和为v的物品，现有 n 个物品，第 i 个物品的体积为 v_i, 重量为 w_i，求当前背包最多能装多大重量的物品?

输入描述：

> 第一行输入两个正整数 v 和 n。表示背包最大体积和物品数量。后续 n 行每行输入两个正整数 v_i 和 w_i，表示每个物品的体积和重量

输出描述：

> 输出背包能装的最大重量

动态规划：

```c++
#include<iostream>
#include<vector>
using namespace std;

int main()
{
    int v, n;
    cin >> v >> n;
    vector<int> val, weight;
    // 初始化都塞进去一个零
    val.push_back(0);
    weight.push_back(0);
    int tmp = 0;
    for (int i = 0; i < n; ++i)
    {
        cin >> tmp;
        val.push_back(tmp);
        cin >> tmp;
        weight.push_back(tmp);
    }
    // 初始化一个二维 vector 数组，使其都为零，一共有 n + 1 行，v + 1 列
    vector<vector<int>> dp(n + 1, vector<int>(v + 1, 0));
    // 从只放第一个物品，背包剩余容量为 v 式开始递推，自右向左，自上而下
    for (int i = 1; i <= n; ++i)
    {
        for (int j = v; j > 0; --j)
        {
            if (j >= val[i])
            {
                dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - val[i]] + weight[i]);
            }
            else
            {
                dp[i][j] = dp[i - 1][j];
            }
        }
    }
    cout << dp[n][v];
    return 0;
}
```

<br><br><br>

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

<br><br><br>

### 连续最大和

一个数组有 N 个元素，求连续子数组的最大和。 例如：[-1,2,1]，和最大的连续子数组为[2,1]，其和为 3

输入描述：

> 输入为两行。 第一行一个整数n(1 <= n <= 100000)，表示一共有n个元素 第二行为n个数，即每个元素,每个整数都在32位int范围内。以空格分隔。

输出描述：

> 所有连续子数组中和最大的值。

自己（单独考虑了全为负的情况，有点啰嗦了）：

```c++
#include<iostream>
using namespace std;

int main(){
    int n, num, sum = 0, maxPos, maxNeg = -1;
    bool para = false;
    cin>>n;
    int nums[n];
    for(int i = 0; i < n; i++){
        cin>>num;
        nums[i] = num;
    }
    for(int i = 0; i < n; i++){
        if(nums[i] >= 0){
            para = true;
            for(int j = i; j < n; j++){
                sum += nums[j];
                if(sum > maxPos) maxPos = sum;
                if(sum < 0 || j == n - 1){
                    i = j;
                    sum = 0;
                    break;
                }
            }
        }
        else{
            if(nums[i] > maxNeg) maxNeg = nums[i];
        }
    }
    if(para) cout<<maxPos<<endl;
    else cout<<maxNeg<<endl;
    return 0;
}
```

其他（更简洁）：

```c++
#include<iostream>
#include<vector>
using namespace std;
int main()
{
    int n;
    cin>>n;
    vector<int> in(n);
    for(int i=0;i<n;i++)
        cin>>in[i];
    vector<int> dp(n);
    //先默认赋值
    dp[0]=in[0];
    int maxVal=in[0];
    for(int i=1;i<n;i++)
    {
        //关键是这一行
        dp[i]=max(in[i],dp[i-1]+in[i]);
        if(dp[i]>maxVal)
            maxVal=dp[i];
    }
    cout<<maxVal<<endl;
    return 0;
}
```

<br><br><br>

### 最大乘积

给定一个无序数组，包含正数、负数和0，要求从中找出3个数的乘积，使得乘积最大，要求时间复杂度：O(n)，空间复杂度：O(1)

输入描述：

> 输入共2行，第一行包括一个整数n，表示数组长度 第二行为n个以空格隔开的整数，分别为A1,A2, … ,An

输出描述：

> 满足条件的最大乘积

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main(){
    long int n, num, max1 = 0, max2 = 0;
    cin>>n;
    vector<long int> nums;
    for(int i = 0; i < n; i++){
        cin>>num;
        nums.push_back(num);
    }
    sort(nums.begin(), nums.end());
    if(nums[n - 3] > 0) max2 = nums[n - 3] * nums[n - 2] * nums[n - 1];
    if(nums[n - 1] > 0) max1 = nums[0] * nums[1] * nums[n - 1];
    else max1 = nums[n - 3] * nums[n - 2] * nums[n - 1];
    cout<<max(max1, max2)<<endl;;
    return 0;
}
```

官方（逻辑更完整）：

```c++
#include<iostream>
//INT_MAX, INT_MIN 需要
#include<limits.h>
using namespace std;
int main()
{
    int i, n, num;
    long long max_mul;
    /* max1, max2, max3 分别为最大值，次大值，第三大值
     * min1, min2 分别为最小值，次小值*/
    long long max1, max2, max3, min1, min2;
    max1 = max2 = max3 = INT_MIN;
    min1 = min2 = INT_MAX;
    cin >> n;
    for(i = 0; i < n; i++)
    {
        cin >> num;
        if(num < min1)
        {
            min2 = min1;
            min1 = num;
        }
        else if(num < min2)
        {
            min2 = num;
        }

        if(num > max1)
        {
            max3 = max2;
            max2 = max1;
            max1 = num;
        }
        else if(num > max2)
        {
            max3 = max2;
            max2 = num;
        }
        else if(num > max3)
        {
            max3 = num;
        }
    }
    max_mul = max1*max2*max3 > max1*min1*min2 ? max1*max2*max3 : max1*min1*min2;
    cout << max_mul << endl;
    return 0;
}
```

<br><br><br>

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

<br><br><br>

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

<br><br><br>

### 数字翻转

对于一个整数X，定义操作rev(X)为将X按数位翻转过来，并且去除掉前导0。例如:

如果 X = 123，则rev(X) = 321；如果 X = 100，则rev(X) = 1.

现在给出整数x和y,要求rev(rev(x) + rev(y))为多少？

输入描述：

> 输入为一行，x、y(1 ≤ x、y ≤ 1000)，以空格隔开

输出描述：

> 输出rev(rev(x) + rev(y))的值

```c++
#include<iostream>
#include<vector>
using namespace std;

int rev(int num){
    int last, n, res;
    vector<int> nums;
    while(num != 0){
        last = num % 10;
        nums.push_back(last);
        num /= 10;
    }
    n = nums.size();
    res = nums[0];
    for(int i = 1; i < n; i++){
        res = res * 10 + nums[i];
    }
    return res;
}

int main(){
    int x, y;
    cin>>x>>y;
    cout<<rev(rev(x) + rev(y))<<endl;
    return 0;
}
```

<br><br><br>

### 搬圆桌

现在有一张半径为r的圆桌，其中心位于(x,y)，现在他想把圆桌的中心移到(x1,y1)。每次移动一步，都必须在圆桌边缘固定一个点然后将圆桌绕这个点旋转。问最少需要移动几步。

输入描述：

> 一行五个整数r,x,y,x1,y1(1≤r≤100000,-100000≤x,y,x1,y1≤100000)

输出描述：

> 输出一个整数，表示答案

```c++
#include<iostream>
#include<math.h>
using namespace std;

int main(){
    int r, n;
    double x, y, x1, y1;
    while(cin>>r>>x>>y>>x1>>y1){
        double D = sqrt((x - x1) * (x - x1) + (y - y1) * (y - y1));
        double N = D / (2 * r);
        n = (int)N;
        n == N ? cout<<n<<endl : cout<<n + 1<<endl;
    }
    return 0;
}
```

<br><br><br>

### 求解f(n)

求解f(n), f(n) = 1 – 2 + 3 – 4 + 5 - … + n

```c++
#include<iostream>
using namespace std;

int main(){
    int n, res = 0;
    while(cin>>n){
        // 时间复杂度高，需遍历
        // for(int i = 1; i <= n; i++){
        //     if(i % 2) res += i;
        //     else res -= i;
        // }
        // 时间复杂度低，找数学规律
        if(n % 2) res = (n + 1) / 2;
        else res = -n / 2;
        cout<<res<<endl;
        // 初始化
        res = 0;
    }
    return 0;
}
```

<br><br><br>

### 猜数

编写猜数游戏程序，语言不限。给定某个整数，从键盘上反复输入数据进行猜测。如果未猜中，程序提示输入过大或者过小；如果猜中，则输出猜的次数，最多允许猜10次。

```c++
#include<iostream>
#include<time.h>
using namespace std;

int main(){
    int num, guessNum, count = 0;
    //设置随机数种子，使每次运行获取到的随机数值不同。
    srand(time(NULL));
    //获取1-100的随机数。
    num = rand() % 100 + 1;
    cout<<"Guess number:"<<endl;
    while(cin>>guessNum && count++ <10){
        if(guessNum < num) cout<<"Too small"<<endl;
        else if(guessNum > num) cout <<"Too big"<<endl;
        else cout << count << endl;
    }
    return 0;
}
```

<br><br><br>

### 坐标移动

开发一个坐标计算工具， A表示向左移动，D表示向右移动，W表示向上移动，S表示向下移动。从（0,0）点开始移动，从输入字符串里面读取一些坐标，并将最终输入结果输出到输出文件里面。

输入描述：

> 合法坐标为A(或者D或者W或者S) + 数字（两位以内），坐标之间以;分隔。非法坐标点需要进行丢弃。如AA10;  A1A;  $%$;  YAD; 等。

输出描述：

> 最终坐标，以逗号分隔。

自己：

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
    int x = 0;
    int y = 0;
    string s;
    cin >> s;
    vector<char> tmp;
    for (int i = 0; i < s.size(); ++i)
    {
        tmp.push_back(s[i]);
        if (s[i] == ';')
        {
            if (tmp.size() == 3 && tmp[1] >= '0' && tmp[1] <= '9')
            {
                if (tmp[0] == 'A')
                {
                    x -= (tmp[1] - '0');
                }
                else if (tmp[0] == 'D')
                {
                    x += (tmp[1] - '0');
                }
                else if (tmp[0] == 'W')
                {
                    y += (tmp[1] - '0');
                }
                else if (tmp[0] == 'S')
                {
                    y -= (tmp[1] - '0');
                }
            }
            else if (tmp.size() == 4 && tmp[1] >= '0' && tmp[1] <= '9' && tmp[2] >= '0' && tmp[2] <= '9')
            {
                if (tmp[0] == 'A')
                {
                    x -= ((tmp[1] - '0') * 10 + (tmp[2] - '0'));
                }
                else if (tmp[0] == 'D')
                {
                    x += ((tmp[1] - '0') * 10 + (tmp[2] - '0'));
                }
                else if (tmp[0] == 'W')
                {
                    y += ((tmp[1] - '0') * 10 + (tmp[2] - '0'));
                }
                else if (tmp[0] == 'S')
                {
                    y -= ((tmp[1] - '0') * 10 + (tmp[2] - '0'));
                }
            }
            tmp.clear();
            continue;
        }
    }
    cout << x << ',' << y << endl;
    return 0;
}
```

<br><br><br>

### 计算字符重新排列数

给一串可能重复的大写字母，输出可能的排列情况

```c++
// we have defined the necessary header files here for this problem.
// If additional header files are needed in your program, please import here.
#include<vector>
#include<algorithm>

int jiecheng(int a)
{
    int num = 1;
    for (int i = 2; i <= a; ++i)
    {
        num *= i;
    }
    return num;
}

int main()
{
    // please define the C++ input here. For example: int a,b; cin>>a>>b;;
    // please finish the function body here.
    // please define the C++ output here. For example:cout<<____<<endl;
    vector<char> s;
    char tmp;
    while (cin >> tmp)
    {
        s.push_back(tmp);
    }
    sort(s.begin(), s.end());
    int length = s.size();
    int ans = jiecheng(length);
    int count = 1;
    for (int i = 0; i < length - 1; ++i)
    {
        if (s[i + 1] == s[i])
        {
            ++count;
        }
        else if (s[i + 1] != s[i] && count > 1)
        {
            ans /= jiecheng(count);
            count = 1;
        }
    }
    ans /= jiecheng(count);
    cout << ans;
    return 0;
}

```

<br><br><br>

### 集合P

P为给定的二维平面整数点集。定义 P 中某点x，如果x满足 P 中任意点都不在 x 的右上方区域内（横纵坐标都大于x），则称其为“最大的”。求出所有“最大的”点的集合。（所有点的横坐标和纵坐标都不重复, 坐标轴范围在[0, 1e9) 内）

输入描述：

> 第一行输入点集的个数 N， 接下来 N 行，每行两个数字代表点的 X 轴和 Y 轴。 对于 50%的数据,  1 <= N <= 10000; 对于 100%的数据, 1 <= N <= 500000;

输出描述：

> 输出“最大的” 点集合， 按照 X 轴从小到大的方式输出，每行两个数字分别代表点的 X 轴和 Y轴。

自己，哈希映射：

```c++
#include <iostream>
#include <map>
#include <vector>
#include <algorithm>

using namespace std;

int main()
{
    int n = 0;
    cin >> n;
    int x = 0;
    int y = 0;
    map<int ,int> imap;
    vector<int> ivec;
    for (int i = 0; i < n; ++i)
    {
        cin >> x >> y;
        imap[y] = x;
        ivec.push_back(y);
    }
    // 从大到小排序
    sort(ivec.begin(), ivec.end(), greater<int>());
    cout << imap[ivec[0]] << ' ' << ivec[0] << endl;
    int tmp = imap[ivec[0]];
    for (int i = 1; i < ivec.size(); ++i)
    {
        if (imap[ivec[i]] > tmp)
        {
        cout << imap[ivec[i]] << ' ' << ivec[i] << endl;
        tmp = imap[ivec[i]];
        }
    }
    return 0;
}
```

<br><br><br>

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