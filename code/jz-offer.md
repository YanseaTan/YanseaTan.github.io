# 剑指 Offer 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [剑指 Offer 刷题记录](#剑指-offer-刷题记录)
  - [数组](#数组)
    - [JZ3 数组中重复的数字](#jz3-数组中重复的数字)
    - [JZ4 二维数组中的查找](#jz4-二维数组中的查找)
    - [JZ11 旋转数组的最小数字](#jz11-旋转数组的最小数字)
    - [？JZ12 矩阵中的路径](#jz12-矩阵中的路径)
    - [？JZ13 机器人的运动范围](#jz13-机器人的运动范围)
  - [字符串](#字符串)
    - [JZ5 替换空格](#jz5-替换空格)
  - [链表](#链表)
    - [JZ6 从尾到头打印链表](#jz6-从尾到头打印链表)
  - [二叉树](#二叉树)
    - [？JZ7 重建二叉树](#jz7-重建二叉树)
  - [栈](#栈)
    - [？JZ9 用两个栈实现队列](#jz9-用两个栈实现队列)
  - [动态规划](#动态规划)
    - [JZ10-I 斐波那契数列](#jz10-i-斐波那契数列)
    - [JZ10-II 青蛙跳台阶问题](#jz10-ii-青蛙跳台阶问题)
    - [JZ14-I 剪绳子](#jz14-i-剪绳子)
  - [技巧](#技巧)
    - [递归](#递归)
    - [二分查找](#二分查找)
    - [？回溯](#回溯)
    - [？深度优先搜索 DFS](#深度优先搜索-dfs)
    - [？广度优先搜索 BFS](#广度优先搜索-bfs)

## 数组

### JZ3 数组中重复的数字

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组[2,3,1,0,2,5,3]，那么对应的输出是2或者3。存在不合法的输入的话输出-1

```c++
class Solution {
public:
    int duplicate(vector<int>& numbers) {
        int n = numbers.size();
        for(int i = 0; i < n - 1; i++){
            for(int j = i + 1; j < n; j++){
                if(numbers[i] == numbers[j]) return numbers[i];
            }
        }
        return -1;
    }
};
```

### JZ4 二维数组中的查找

在一个二维数组array中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

自己（暴力）：

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        //首先要判断为空，否则遇到空的二维数组时会报错
        if(matrix.size() == 0 || matrix[0].size() == 0) return false;
        int m = matrix.size();
        int n = matrix[0].size();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(target == matrix[i][j]) return true;
            }
        }
        return false;
    }
};
```

其他（线性搜索，推荐）：

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        //从矩阵左下角往右上角走，逐一比较
        int i = matrix.size() - 1, j = 0;
        while(i >= 0 && j < matrix[0].size())
        {
            if(matrix[i][j] > target) i--;
            else if(matrix[i][j] < target) j++;
            else return true;
        }
        return false;
    }
};
```

### JZ11 旋转数组的最小数字

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。给你一个可能存在**重复**元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为 1。  

自己（暴力）：

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int n = numbers.size();
        if(n == 1) return numbers[0];
        for(int i = 1; i < n; i++){
            if(numbers[i] < numbers[i - 1]) return numbers[i];
        }
        //没有这行会报错，要必须有返回值，同时也要对应所有数都一样的情况
        return numbers[0];
    }
};
```

官方（二分查找，推荐）：

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int n = numbers.size();
        if(n == 1) return numbers[0];
        int l = 0, r = n - 1, m;
        while(l < r){
            m = (l + r) / 2;
            if(numbers[r] < numbers[m]) l = m + 1;
            else if(numbers[r] > numbers[m]) r = m;
            else r--;
        }
        return numbers[l];
    }
};
```

### ？JZ12 矩阵中的路径

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

其他（回溯，递归，比较困难）：

```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        rows = board.size();
        cols = board[0].size();
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(dfs(board, word, i, j, 0)) return true;
            }
        }
        return false;
    }
private:
    int rows, cols;
    bool dfs(vector<vector<char>>& board, string word, int i, int j, int k) {
        if(i >= rows || i < 0 || j >= cols || j < 0 || board[i][j] != word[k]) return false;
        if(k == word.size() - 1) return true;
        board[i][j] = '\0';
        bool res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || 
                      dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i , j - 1, k + 1);
        board[i][j] = word[k];
        return res;
    }
};
```

### ？JZ13 机器人的运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的**数位之和**大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

```c++

```

## 字符串

### JZ5 替换空格

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int sizeOld = s.size();
        int n = 0;
        for(int i = 0; i < sizeOld; i++){
            //注意要用单引号！
            if(s[i] == ' ') n += 2;
        }
        //需要先对原字符串扩容
        s.resize(sizeOld + n);
        int sizeNew = s.size();
        for(int i = sizeOld - 1, j = sizeNew - 1; i < j; i--, j--){
            if(s[i] != ' '){
                s[j] = s[i];
            }
            else{
                s[j] = '0';
                s[j - 1] = '2';
                s[j - 2] = '%';
                j -= 2;
            }
        }
        return s;
    }
};
```

## 链表

### JZ6 从尾到头打印链表

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

自己：

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        if(head == nullptr) return res;
        //如果没不判断的话会报错
        while(head != nullptr && head->next != nullptr){
            int j = head->val;
            //使用了 vector 容器的插入
            res.insert(res.begin(), j);
            head = head->next;
        }
        int j = head->val;
        res.insert(res.begin(), j);
        return res;
    }
};
```

使用栈：

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> result;
        stack<int> s;
        while(head) {
            s.push(head->val);
            head = head->next;
        }
        while(!s.empty()) {
            result.push_back(s.top());
            s.pop();
        }
        return result;
    }
};
```

使用递归：

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        if(!head)
            return {};
        vector<int> a=reversePrint(head->next);
        a.push_back(head->val);
        return a;
    }
};
```

## 二叉树

### ？JZ7 重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

```c++

```

## 栈

### ？JZ9 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

```c++

```

## 动态规划

### JZ10-I 斐波那契数列

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：F(0) = 0，F(1) = 1，F(N) = F(N - 1) + F(N - 2)，其中 N > 1。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

自己（递归！以为自己是天才，结果超时！小丑竟是我自己）：

```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        return fib(n - 1) + fib(n - 2);
    }
};
```

官方（动态规划）：

```c++
class Solution {
public:
    int fib(int n) {
        if(n < 2) return n;
        //题目要求的取模数字
        int MOD = 1000000007;
        int i = 0, j = 0, k = 1;
        for(int m = 2; m <= n; m++){
            i = j;
            j = k;
            k = (i + j) % MOD;
        }
        return k;
    }
};
```

### JZ10-II 青蛙跳台阶问题

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

自己（跟上道题思路一样）：

```c++
class Solution {
public:
    int numWays(int n) {
        if(n < 2) return 1;
        int i = 0, j = 1, k = 1;
        for(int m = 2; m <= n; m++){
            i = j;
            j = k;
            k = (i + j) % 1000000007;
        }
        return k;
    }
};
```

### JZ14-I 剪绳子

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

自己（偏暴力）：

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n == 2) return 1;
        if(n == 3) return 2;
        if(n == 4) return 4;
        int res = 1;
        //尽量分成长度为3的段，得到的乘积最大
        int m = n / 3;
        if(n % 3 == 0){
            for(int i = 0; i < m; i++){
                res *= 3;
            }
        }
        else if(n % 3 == 1){
            for(int i = 0; i < m - 1; i++){
                res *= 3;
            }
            res *= 4;
        }
        else if(n % 3 == 2){
            for(int i = 0; i < m; i++){
                res *= 3;
            }
            res *= 2;
        }
        return res;
    }
};
```

其他（动态规划，推荐）:

```c++
class Solution {
public:
    int cuttingRope(int n) {
        vector<int> dp(n + 1);
        //dp[i] 的意思为当 n = i 时的最大乘积
        dp[2] = 1;
        for(int i = 3; i <= n; i++){
            for(int j = 1; j < i - 1; j++){
                //选择最大值：（本身，直接分两半相乘，本身[下角标减 j 后]的最大值 * 减去的 j
                dp[i] = max(dp[i], max((i - j) * j, dp[i - j] * j));
            }
        }
        return dp[n];
    }
};
```

## 技巧

### 递归

[JZ6 从尾到头打印链表](#jz6-从尾到头打印链表)

### 二分查找

[JZ11 旋转数组的最小数字](#jz11-旋转数组的最小数字)

### ？回溯

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)

### ？深度优先搜索 DFS

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)

### ？广度优先搜索 BFS

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)