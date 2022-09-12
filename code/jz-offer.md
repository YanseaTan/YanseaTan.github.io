# 剑指 Offer 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [剑指 Offer 刷题记录](#剑指-offer-刷题记录)
  - [数组](#数组)
    - [JZ3 数组中重复的数字](#jz3-数组中重复的数字)
    - [JZ4 二维数组中的查找](#jz4-二维数组中的查找)
    - [JZ11 旋转数组的最小数字](#jz11-旋转数组的最小数字)
    - [JZ12 矩阵中的路径](#jz12-矩阵中的路径)
    - [？JZ13 机器人的运动范围](#jz13-机器人的运动范围)
    - [JZ17 打印从1到最大的n位数](#jz17-打印从1到最大的n位数)
    - [JZ21 调整数组顺序使奇数位于偶数前面](#jz21-调整数组顺序使奇数位于偶数前面)
    - [JZ29 顺时针打印矩阵](#jz29-顺时针打印矩阵)
    - [JZ39 数组中出现次数超过一半的数字](#jz39-数组中出现次数超过一半的数字)
    - [JZ42 连续子数组的最大和](#jz42-连续子数组的最大和)
    - [JZ44 数字序列中某一位的数字](#jz44-数字序列中某一位的数字)
    - [JZ47 礼物的最大价值](#jz47-礼物的最大价值)
    - [JZ49 丑数](#jz49-丑数)
  - [字符串](#字符串)
    - [JZ5 替换空格](#jz5-替换空格)
    - [JZ15 二进制中1的个数](#jz15-二进制中1的个数)
    - [?JZ19 正则表达式匹配](#jz19-正则表达式匹配)
    - [JZ20 表示数值的字符串](#jz20-表示数值的字符串)
    - [JZ38 字符串的排列](#jz38-字符串的排列)
    - [JZ45 把数组排成最小的数](#jz45-把数组排成最小的数)
    - [JZ46 把数字翻译成字符串](#jz46-把数字翻译成字符串)
    - [JZ48 最长不含重复字符的子字符串](#jz48-最长不含重复字符的子字符串)
    - [JZ50 第一个只出现一次的字符](#jz50-第一个只出现一次的字符)
  - [链表](#链表)
    - [JZ6 从尾到头打印链表](#jz6-从尾到头打印链表)
    - [JZ18 删除链表的节点](#jz18-删除链表的节点)
    - [JZ22 链表中倒数第k个节点](#jz22-链表中倒数第k个节点)
    - [JZ24 反转链表](#jz24-反转链表)
    - [JZ25 合并两个排序的链表](#jz25-合并两个排序的链表)
  - [二叉树](#二叉树)
    - [？JZ7 重建二叉树](#jz7-重建二叉树)
    - [JZ26 树的子结构](#jz26-树的子结构)
    - [JZ27 二叉树的镜像](#jz27-二叉树的镜像)
    - [JZ28 对称的二叉树](#jz28-对称的二叉树)
    - [JZ32-I 从上到下打印二叉树](#jz32-i-从上到下打印二叉树)
    - [JZ32-II 从上到下打印二叉树 II](#jz32-ii-从上到下打印二叉树-ii)
  - [栈](#栈)
    - [？JZ9 用两个栈实现队列](#jz9-用两个栈实现队列)
    - [JZ30 包含min函数的栈](#jz30-包含min函数的栈)
    - [JZ31 栈的压入、弹出序列](#jz31-栈的压入弹出序列)
  - [队列](#队列)
  - [数学](#数学)
    - [JZ10-I 斐波那契数列](#jz10-i-斐波那契数列)
    - [JZ10-II 青蛙跳台阶问题](#jz10-ii-青蛙跳台阶问题)
    - [JZ14-I 剪绳子](#jz14-i-剪绳子)
    - [JZ16 数值的整数次方](#jz16-数值的整数次方)
  - [技巧](#技巧)
    - [递归](#递归)
    - [动态规划](#动态规划)
    - [二分查找](#二分查找)
    - [双指针](#双指针)
    - [模拟](#模拟)
    - [？回溯](#回溯)
    - [？深度优先搜索 DFS](#深度优先搜索-dfs)
    - [？广度优先搜索 BFS](#广度优先搜索-bfs)
    - [位运算](#位运算)
    - [快速幂](#快速幂)

<br><br><br>

## 数组

### JZ3 数组中重复的数字

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组[2,3,1,0,2,5,3]，那么对应的输出是2或者3。存在不合法的输入的话输出-1

暴力解：

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

哈希表：

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int, bool> map;
        for (int num : nums)
        {
            if (map[num])
            {
                return num;
            }
            map[num] = true;
        }
        return -1;
    }
};
```

原地交换（推荐）：

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        while (i < nums.size())
        {
            if (nums[i] == i)
            {
                i++;
                continue;
            }
            if (nums[nums[i]] == nums[i])
            {
                return nums[i];
            }
            swap(nums[nums[i]], nums[i]);
        }
        return -1;
    }
};
```

<br><br><br>

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

<br><br><br>

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

<br><br><br>

### JZ12 矩阵中的路径

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
                //i，j 是 board 的，0 是 word 的
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
        bool res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i , j - 1, k + 1);
        //回溯
        board[i][j] = word[k];
        return res;
    }
};
```

<br><br><br>

### ？JZ13 机器人的运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的**数位之和**大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

```c++

```

<br><br><br>

### JZ17 打印从1到最大的n位数

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

自己（没考虑大树情况）：

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        int x = 1;
        for(int i = 0; i < n; i++){
            x *= 10;
        }
        vector<int> res;
        for(int i = 1; i < x; i++){
            res.push_back(i);
        }
        return res;
    }
};
```

其他：

```c++
class Solution {
private:
    vector<int> nums;
    string s;
public:
    vector<int> printNumbers(int n) {
        s.resize(n, '0');
        dfs(n, 0);
        return nums;
    }
    
    // 枚举所有情况
    void dfs(int end, int index) {
        if (index == end) {
            save(); return;
        }
        for (int i = 0; i <= 9; ++i) {
            s[index] = i + '0';
            dfs(end, index + 1);
        }
    }
    
    // 去除首部0
    void save() {
        int ptr = 0;
        while (ptr < s.size() && s[ptr] == '0') ptr++;
        if (ptr != s.size())
            nums.emplace_back(stoi(s.substr(ptr)));
    }
};
```

<br><br><br>

### JZ21 调整数组顺序使奇数位于偶数前面

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

自己（快慢双指针）：

```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int n = nums.size();
        if(n < 2) return nums;
        int fast = 1;
        int slow = 0;
        while(fast < n){
            if(nums[slow] % 2 == 1){
                slow++;
            }
            else if(nums[fast] % 2 == 1){
                int temp = nums[fast];
                nums[fast] = nums[slow];
                nums[slow] = temp;
                slow++;
            }
            fast++;
        }
        return nums;
    }
};
```

<br><br><br>

### JZ29 顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.size() == 0) return {};
        vector<int> res;
        //初始化四个边界
        int t = 0, b = matrix.size() - 1, l = 0, r = matrix[0].size() - 1;
        while(true){
            for(int i = l; i <= r; i++) res.push_back(matrix[t][i]);
            //在缩减边界的同时判断是否出界
            if(++t > b) break;
            for(int i = t; i <= b; i++) res.push_back(matrix[i][r]);
            if(--r < l) break;
            for(int i = r; i >= l; i--) res.push_back(matrix[b][i]);
            if(--b < t) break;
            for(int i = b; i >= t; i--) res.push_back(matrix[i][l]);
            if(++l > r) break;
        }
        return res;
    }
};
```

<br><br><br>

### JZ39 数组中出现次数超过一半的数字

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。你可以假设数组是非空的，并且给定的数组总是存在多数元素。

自己（暴力）：

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int length = nums.size();
        if(length < 3) return nums[0];
        sort(nums.begin(), nums.end());
        int count = 1;
        for(int i = 0; i < length;) {
            while(nums[++i] == nums[i]) {
                count++;
                if(count > length / 2) {
                    return nums[i];
                }
            }
            count = 1;
        }
        return -1;
    }
};
```

其他（排序后，中间的数一定是那个多数的数）：

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
};
```

其他（投票法）：

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int vote = 0, x = 0;
        for(int num : nums) {
            if(vote == 0) x = num;
            vote += num == x ? 1 : -1;
        }
        return x;
    }
};
```

<br><br><br>

### JZ42 连续子数组的最大和

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

示例：

> 输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
> 输出: 6

自己，双指针：

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = nums[0];
        int length = nums.size();
        if (length == 1)
        {
            return nums[0];
        }
        int left = 0;
        int right = 1;
        int tmp = nums[left];
        while (right < length)
        {
            if (nums[right] > tmp && tmp < 0)
            {
                left = right;
                tmp = nums[left];
            }
            else
            {
                tmp += nums[right];
            }
            ++right;
            ans = max(ans, tmp);
        }
        return ans;
    }
};
```

题解，动态规划：

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = nums[0];
        for (int i = 1; i < nums.size(); ++i)
        {
            // nums[i] 更新为以原来 nums[i] 为结尾时最大的前 i 项和，只要判断前一个是否大于零就行
            nums[i] += max(nums[i - 1], 0);
            ans = max(ans, nums[i]);
        }
        return ans;
    }
};
```

<br><br><br>

### JZ44 数字序列中某一位的数字

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

自己，暴力：

```c++
class Solution {
public:
    int findNthDigit(int n) {
        if (n >= 0 && n <= 9) return n;
        long nums[9] = {10, 190, 2890, 38890, 488890, 5888890, 68888890, 788888890, 8888888890};
        int tmp = 0;
        int id = 0;
        int left = 0;
        int ten = 1;
        int num = 0;
        string s;
        char c;
        int ans = 0;
        for (int i = 1; i < 9; ++i)
        {
            if (n < nums[i])
            {
                tmp = n - nums[i - 1];
                id = tmp / (i + 1);
                left = tmp % (i + 1);
                for (int j = 0; j < i; ++j)
                {
                    ten *= 10;
                }
                num = ten + id;
                s = to_string(num);
                c = s[left];
                ans = c - '0';
                break;
            }
        }
        return ans;
    }
};
```

<br><br><br>

### JZ47 礼物的最大价值

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

示例：

> 输入: 
> [
>  [1,3,1],
>  [1,5,1],
>  [4,2,1]
> ]
> 输出: 12
> 解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物

题解，动态规划：

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        // 先把第一行第一列算出来，作为后续状态转移方程的初始解
        for (int i = 1; i < m; ++i)
        {
            grid[i][0] += grid[i - 1][0];
        }
        for (int i = 1; i < n; ++i)
        {
            grid[0][i] += grid[0][i - 1];
        }
        for (int i = 1; i < m; ++i)
        {
            for (int j = 1; j < n; ++j)
            {
                grid[i][j] = grid[i][j] + max(grid[i - 1][j], grid[i][j - 1]);
            }
        }
        return grid[m - 1][n - 1];
    }
};
```

<br><br><br>

### JZ49 丑数

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

示例：

> 输入: n = 10
> 输出: 12
> 解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。

题解，动态规划：

```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> dp(n + 1);
        dp[1] = 1;
        int a = 1;
        int b = 1;
        int c = 1;
        for (int i = 2; i <= n; ++i)
        {
            int n2 = dp[a] * 2;
            int n3 = dp[b] * 3;
            int n5 = dp[c] * 5;
            dp[i] = min(n2, min(n3, n5));
            if (dp[i] == n2)
            {
                ++a;
            }
            if (dp[i] == n3)
            {
                ++b;
            }
            if (dp[i] == n5)
            {
                ++c;
            }
        }
        return dp[n];
    }
};
```

<br><br><br>

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
        //j 前面没有 int 了
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

<br><br><br>

### JZ15 二进制中1的个数

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 汉明重量).）。

其他（位运算）：

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        while(n){
            res++;
            //通过位运算公式 n & (n - 1)可以消去二进制n的最右边的一个 1
            n = n & (n - 1);
        }
        return res;
    }
};
```

<br><br><br>

### ?JZ19 正则表达式匹配

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

```c++

```

<br><br><br>

### JZ20 表示数值的字符串

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。

数值（按顺序）可以分成以下几个部分：

1. 若干空格
2. 一个 小数 或者 整数
3. （可选）一个 'e' 或 'E' ，后面跟着一个 整数
4. 若干空格

小数（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（'+' 或 '-'）
2. 下述格式之一：
   1. 至少一位数字，后面跟着一个点 '.'
   2. 至少一位数字，后面跟着一个点 '.' ，后面再跟着至少一位数字
   3. 一个点 '.' ，后面跟着至少一位数字

整数（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（'+' 或 '-'）
2. 至少一位数字

部分数值列举如下：

> ["+100", "5e2", "-123", "3.1416", "-1E-16", "0123"]

部分非数值列举如下：

> ["12e", "1a3.14", "1.2.3", "+-5", "12e+5.4"]

自己，创建好判断正整数、负整数、小数以及含e（E）数的函数：

```c++
class Solution {
public:
    bool iszz(string s)
    {
        if (s[0] == '+' && s.size() > 1 || s[0] >= '0' && s[0] <= '9')
        {
            for (int i = 1; i < s.size(); ++i)
            {
                if (s[i] < '0' || s[i] > '9')
                {
                    return false;
                }
            }
            return true;
        }
        return false;
    }

    bool isfz(string s)
    {
        if (s[0] == '-' && s.size() > 1)
        {
            for (int i = 1; i < s.size(); ++i)
            {
                if (s[i] < '0' || s[i] > '9')
                {
                    return false;
                }
            }
            return true;
        }
        return false;
    }

    bool isxs(string s)
    {
        int cnt = 0;
        string left;
        string right;
        for (int i = 0; i < s.size(); ++i)
        {
            if (cnt == 0 && s[i] != '.')
            {
                left.push_back(s[i]);
            }
            if (cnt == 1)
            {
                right.push_back(s[i]);
            }
            if (s[i] == '.')
            {
                ++cnt;
            }
            if (cnt > 1)
            {
                return false;
            }
        }
        if (!cnt)
        {
            return false;
        }
        if (left.empty() && !right.empty() && iszz(right) && right[0] != '+')
        {
            return true;
        }
        if (!left.empty() && (iszz(left) || isfz(left)) && right.empty())
        {
            return true;
        }
        if (!left.empty() && (iszz(left) || isfz(left) || (left.size() == 1 && (left[0] == '+' || left[0] == '-'))) && !right.empty() && iszz(right))
        {
            return true;
        }
        return false;
    }

    bool ise(string s)
    {
        int cnt = 0;
        string left;
        string right;
        for (int i = 0; i < s.size(); ++i)
        {
            if (s[i] == 'e' || s[i] == 'E')
            {
                ++cnt;
            }
            if (cnt > 1)
            {
                return false;
            }
            if (cnt == 0 && s[i] != 'e' && s[i] != 'E')
            {
                left.push_back(s[i]);
            }
            if (cnt == 1 && s[i] != 'e' && s[i] != 'E')
            {
                right.push_back(s[i]);
            }
        }
        if (!cnt)
        {
            return false;
        }
        if (left.empty() || right.empty())
        {
            return false;
        }
        if ((iszz(left) || isfz(left) || isxs(left)) && (iszz(right) || isfz(right)))
        {
            return true;
        }
        return false;
    }

    string deleteSpace(string s)
    {
        for (int i = 0; i < s.size();)
        {
            if (s[i] == ' ')
            {
                s.erase(s.begin());
            }
            else
            {
                break;
            }
        }
        for (int i = s.size() - 1; i >= 0; --i)
        {
            if (s[i] == ' ')
            {
                s.erase(s.begin() + i);
            }
            else
            {
                break;
            }
        }
        return s;
    }

    bool isNumber(string s)
    {
        string ss = deleteSpace(s);
        cout << ss;
        for (int i = 0; i < ss.size(); ++i)
        {
            if (ss[i] == ' ')
            {
                return false;
            }
        }
        if (ss.empty())
        {
            return false;
        }
        if (iszz(ss) || isfz(ss) || isxs(ss) || ise(ss))
        {
            return true;
        }
        return false;
    }
};
```

<br><br><br>

### JZ38 字符串的排列

输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例：

> 输入：s = "abc"
> 输出：["abc","acb","bac","bca","cab","cba"]

回溯，dfs，无序哈希集合：

```c++
class Solution {
public:
    void dfs(int x, string s, set<string>& uset)
    {
        if (x == s.size())
        {
            uset.emplace(s);
        }
        for (int i = x; i < s.size(); ++i)
        {
            swap(s[x], s[i]);
            dfs(x + 1, s, uset);    //递归下一个位置
            swap(s[x], s[i]);       //回溯
        }
    }

    vector<string> permutation(string s) {
        set<string> uset;
        dfs(0, s, uset);
        vector<string> ans;
        for (set<string>::iterator i=uset.begin(); i!=uset.end(); ++i)
        {
            ans.push_back(*i);
        }
        return ans;
    }
};
```

利用哈希集合进行剪枝优化：

```c++
class Solution {
public:
    void dfs(int x, string s, vector<string>& ans)
    {
        if (x == s.size())
        {
            ans.push_back(s);
        }
        set<int> ss;
        for (int i = x; i < s.size(); ++i)
        {
            if (ss.find(s[i]) != ss.end())      // 如果这次循环出现相同字母，则剪枝
            {
                continue;
            }
            ss.emplace(s[i]);
            swap(s[x], s[i]);
            dfs(x + 1, s, ans);     // 递归下一个位置
            swap(s[x], s[i]);       // 回溯
        }
    }

    vector<string> permutation(string s) {
        vector<string> ans;
        dfs(0, s, ans);
        return ans;
    }
};
```

<br><br><br>

### JZ45 把数组排成最小的数

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

示例：

> 输入: [3,30,34,5,9]
> 输出: "3033459"

自己，暴力比较：

```c++
class Solution {
public:
    void compare(string& a, string& b)
    {
        string sa = a + b;
        string sb = b + a;
        if (sa > sb)
        {
            swap(a, b);
        }
    }

    string minNumber(vector<int>& nums) {
        string num;
        vector<string> ss;
        for (int x : nums)
        {
            num = to_string(x);
            ss.push_back(num);
        }
        for (int i = 0; i < ss.size() - 1; ++i)
        {
            for (int j = i + 1; j < ss.size(); ++j)
            {
                compare(ss[i], ss[j]);
            }
        }
        num.clear();
        for (string x : ss)
        {
            num += x;
        }
        return num;
    }
};
```

<br><br><br>

### JZ46 把数字翻译成字符串

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例：

> 输入: 12258
> 输出: 5
> 解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"

自己：动态规划

```c++
class Solution {
public:
    int translateNum(int num) {
        string s = to_string(num);
        int nums[12];   // int num 最多是十位数
        nums[0] = 1;
        nums[1] = 1;
        string tmp;
        for (int i = 1; i < s.size(); ++i)
        {
            tmp.push_back(s[i - 1]);
            tmp.push_back(s[i]);
            if (tmp < "26" && tmp >= "10")
            {
                nums[i + 1] = nums[i - 1] + nums[i];
            }
            else
            {
                nums[i + 1] = nums[i];
            }
            tmp.clear();
        }
        return nums[s.size()];
    }
};
```
 
<br><br><br>

### JZ48 最长不含重复字符的子字符串

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

示例：

> 输入: "abcabcbb"
> 输出: 3 
> 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
 
自己，哈希，暴力：

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        set<char> cset;
        int length = s.size();
        if (length == 0)
        {
            return 0;
        }
        int ans = 1;
        int tmp = 1;
        for (int i = 0; i < length - 1; ++i)
        {
            tmp = 1;
            cset.clear();
            cset.emplace(s[i]);
            for (int j = i + 1; j < length; ++j)
            {
                if (cset.count(s[j]))
                {
                    break;
                }
                cset.emplace(s[j]);
                ++tmp;
            }
            ans = max(ans, tmp);
        }
        return ans;
    }
};
```

<br><br><br>

### JZ50 第一个只出现一次的字符

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

哈希映射：

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        int l = s.size();
        if (l == 0)
        {
            return ' ';
        }
        if (l == 1)
        {
            return s[0];
        }
        map<char, bool> cmap;
        for (char c : s)
        {
            if (cmap.count(c))
            {
                cmap[c] = false;
            }
            else
            {
                cmap[c] = true;
            }
        }
        for (char c : s)
        {
            if (cmap[c])
            {
                return c;
            }
        }
        return ' ';
    }
};
```

<br><br><br>

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
        while(head != nullptr){
            int j = head->val;
            //使用了 vector 容器的插入
            res.insert(res.begin(), j);
            head = head->next;
        }
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

<br><br><br>

### JZ18 删除链表的节点

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。返回删除后的链表的头节点。

自己：

```c++
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val) {
        int n = 1;
        ListNode* temp = head;
        while(temp != nullptr && temp->next != nullptr){
            if(temp->val == val) break;
            temp = temp->next;
            n++;
        }
        if(n == 1){
            head = head->next;
            return head;
        }
        else{
            ListNode* r = head;
            for(int i = 0; i < n - 2; i++){
                r = r->next;
            }
            r->next = r->next->next;
        }
        return head;
    }
};
```

其他（思路一样，更简洁）：

```c++
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val) {
        //这一步就比我简洁了很多
        if(head->val == val) return head->next;
        ListNode *pre = head, *cur = head->next;
        while(cur != nullptr && cur->val != val) {
            pre = cur;
            cur = cur->next;
        }
        if(cur != nullptr) pre->next = cur->next;
        return head;
    }
};
```

<br><br><br>

### JZ22 链表中倒数第k个节点

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

自己（顺序查找，需要先遍历得到链表长度 n）：

```c++
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        int n = 0;
        ListNode* temp = head;
        while(temp != nullptr){
            temp = temp->next;
            n++;
        }
        for(int i = 0; i < n - k; i++){
            head = head->next;
        }
        return head;
    }
};
```

官方（双指针，不需要遍历得到链表长度 n，推荐）：

```c++
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast && k > 0){
            fast = fast->next;
            k--;
        }
        while(fast){
            fast = fast->next;
            slow = slow->next;
        }
        return slow;
    }
};
```

<br><br><br>

### JZ24 反转链表

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

其他（双指针）：

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr;
        ListNode* cur = head;
        while(cur){
            ListNode* temp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }
};
```

<br><br><br>

### JZ25 合并两个排序的链表

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

自己（递归）：

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == nullptr) return l2;
        if(l2 == nullptr) return l1;
        if(l1->val <= l2->val){
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else{
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```

<br><br><br>

## 二叉树

### ？JZ7 重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

```c++

```

<br><br><br>

### JZ26 树的子结构

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)；B是A的子结构， 即 A中有出现和B相同的结构和节点值。

其他（先序遍历，递归）：

```c++
class Solution {
public:
    bool recur(TreeNode* A, TreeNode* B){
        if(B == nullptr) return true;
        if(A == nullptr || A->val != B->val) return false;
        return recur(A->left, B->left) && recur(A->right, B->right);
    }
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        return (A != nullptr && B != nullptr) && (recur(A, B) || isSubStructure(A->left, B) || isSubStructure(A->right, B));
    }
};
```

<br><br><br>

### JZ27 二叉树的镜像

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

自己（递归）：

```c++
class Solution {
public:
    TreeNode* mirrorTree(TreeNode* root) {
        if(root != nullptr){
            TreeNode* temp = root->left;
            root->left = mirrorTree(root->right);
            root->right = mirrorTree(temp);
        }
        return root;
    }
};
```

<br><br><br>

### JZ28 对称的二叉树

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

自己（先镜像，再比较，结果只能返回 true，原因是镜像的过程中把 root 本身也会修改掉，哪怕我换了个名字叫 temp2）：

```c++
class Solution {
public:
    TreeNode* mirrorTree(TreeNode* temp2){
        if(temp2 != nullptr){
            TreeNode* temp = temp2->left;
            temp2->left = mirrorTree(temp2->right);
            temp2->right = mirrorTree(temp);
        }
        return temp2;
    }
    bool dfs(TreeNode* a, TreeNode* b){
        if(a == nullptr && b == nullptr) return true;
        if(a == nullptr || b == nullptr) return false;
        if(a->val != b->val) return false;
        return dfs(a->left, b->left) && dfs(a->right, b->right);
    }
    bool isSymmetric(TreeNode* root) {
        TreeNode* temp2 = root;
        TreeNode* newRoot = mirrorTree(temp2);
        return dfs(root, newRoot);
    }
};
```

其他（省去镜像步骤，直接左右对比）：

```c++
class Solution {
public:
    bool dfs(TreeNode* L, TreeNode* R){
        if(L == nullptr && R == nullptr) return true;
        if(L == nullptr || R == nullptr || L->val != R->val) return false;
        //关键在于这一步
        return dfs(L->left, R->right) && dfs(L->right, R->left);
    }
    bool isSymmetric(TreeNode* root) {
        if(root == nullptr) return true;
        return dfs(root->left, root->right);
    }
};
```

<br><br><br>

### JZ32-I 从上到下打印二叉树

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

其他（利用队列queue先进先出的特性）：

```c++
class Solution {
public:
    vector<int> levelOrder(TreeNode* root) {
        if(root == nullptr) return {};
        vector<int> res;
        //存储二叉树类型的队列（关键）
        queue<TreeNode*> q;
        q.push(root);
        while(q.size()){
            TreeNode* temp = q.front();
            q.pop();
            res.push_back(temp->val);
            //每次推进去的都是一整个二叉树分支 root 的地址
            if(temp->left) q.push(temp->left);
            if(temp->right) q.push(temp->right);
        }
        return res;
    }
};
```

<br><br><br>

### JZ32-II 从上到下打印二叉树 II

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

其他（同上，多了个维度）：

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == nullptr) return {};
        vector<vector<int>> res;
        queue<TreeNode*> q;
        q.push(root);
        while(q.size()){
            //注意在 for 外面定义
            vector<int> resTemp;
            //这个就很有意思了，只需要把开始循环时的 size 赋给 i，后续 size 大小和 i 无关
            for(int i = q.size(); i > 0; i--){
                TreeNode* temp = q.front();
                q.pop();
                resTemp.push_back(temp->val);
                if(temp->left) q.push(temp->left);
                if(temp->right) q.push(temp->right);
            }
            res.push_back(resTemp);
        }
        return res;
    }
};
```

<br><br><br>

## 栈

### ？JZ9 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

```c++

```

<br><br><br>

### JZ30 包含min函数的栈

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

```c++
class MinStack {
public:
    //分两个栈，一个正常顺序存储，一个不断存储当前最小值
    stack<int> norm;
    stack<int> minStack;

    MinStack() {
        //初始化
        while(!norm.empty()){
            norm.pop();
        }
        while(!minStack.empty()){
            minStack.pop();
        }
        //防止 min() 比较时没有数可以比
        minStack.push(INT_MAX);
    }
    
    void push(int x) {
        norm.push(x);
        //不加 std:: 会报错
        int minVal = std::min(minStack.top(), x);
        minStack.push(minVal);
    }
    
    void pop() {
        norm.pop();
        //因为每次都会填进去东西，因此他们数量是一样的，minStack会重复存储最小值
        minStack.pop();
    }
    
    int top() {
        return norm.top();
    }
    
    int min() {
        return minStack.top();
    }
};
```

<br><br><br>

### JZ31 栈的压入、弹出序列

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

自己（模拟）：

```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        int n = pushed.size();
        if(n < 3 ) return true;
        stack<int> st;
        int i = 0, j = 0;
        while(j < n){
            st.push(pushed[i]);
            while(st.top() == popped[j]){
                st.pop();
                j++;
                if(st.empty() && j != n) break;
                if(j == n) return true;
            }
            i++;
            if(i == n) return false;
        }
        return true;
    }
};
```

<br><br><br>

## 队列

[JZ32-I 从上到下打印二叉树](#jz32-i-从上到下打印二叉树)

<br><br><br>

## 数学

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

<br><br><br>

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

<br><br><br>

### JZ14-I 剪绳子

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0] * k[1] * ... * k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

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

<br><br><br>

### JZ16 数值的整数次方

实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，x ^ n）。不得使用库函数，同时不需要考虑大数问题。

自己（暴力，超时）：

```c++
class Solution {
public:
    double myPow(double x, int n) {
        double res = 1;
        if(n == 0 || x == 1) return 1;
        else if(n > 0){
            for(int i = 0; i < n; i++){
                res *= x;
            }
            return res;
        }
        else{
            for(int i = 0; i > n; i--){
                res *= x;
            }
            return 1 / res;
        }
    }
};
```

其他（快速幂，推荐）：

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if(x == 0) return 0;
        double res = 1;
        long m = n;
        if(m < 0){
            x = 1 / x;
            m = - m;
        }
        while(m){
            if((m & 1) == 1) res *= x;
            x *= x;
            m >>= 1;
        }
        return res;
    }
};
```

<br><br><br>

## 技巧

### 递归

[JZ6 从尾到头打印链表](#jz6-从尾到头打印链表)

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ25 合并两个排序的链表](#jz25-合并两个排序的链表)

[JZ26 树的子结构](#jz26-树的子结构)

[JZ27 二叉树的镜像](#jz27-二叉树的镜像)

[JZ28 对称的二叉树](#jz28-对称的二叉树)

### 动态规划

[JZ10-I 斐波那契数列](#jz10-i-斐波那契数列)

[JZ10-II 青蛙跳台阶问题](#jz10-ii-青蛙跳台阶问题)

[JZ14-I 剪绳子](#jz14-i-剪绳子)

[JZ19 正则表达式匹配](#jz19-正则表达式匹配)

[JZ42 连续子数组的最大和](#jz42-连续子数组的最大和)

[JZ45 把数组排成最小的数](#jz45-把数组排成最小的数)

[JZ47 礼物的最大价值](#jz47-礼物的最大价值)

[JZ49 丑数](#jz49-丑数)

### 二分查找

[JZ11 旋转数组的最小数字](#jz11-旋转数组的最小数字)

### 双指针

[JZ21 调整数组顺序使奇数位于偶数前面](#jz21-调整数组顺序使奇数位于偶数前面)

[JZ22 链表中倒数第k个节点](#jz22-链表中倒数第k个节点)

[JZ24 反转链表](#jz24-反转链表)

[JZ42 连续子数组的最大和](#jz42-连续子数组的最大和)

### 模拟

[JZ29 顺时针打印矩阵](#jz29-顺时针打印矩阵)

[JZ31 栈的压入、弹出序列](#jz31-栈的压入弹出序列)

### ？回溯

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)

[JZ38 字符串的排列](#jz38-字符串的排列)

### ？深度优先搜索 DFS

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)

[JZ38 字符串的排列](#jz38-字符串的排列)

### ？广度优先搜索 BFS

[JZ12 矩阵中的路径](#jz12-矩阵中的路径)

[JZ13 机器人的运动范围](#jz13-机器人的运动范围)

[JZ32-I 从上到下打印二叉树](#jz32-i-从上到下打印二叉树)

[JZ32-II 从上到下打印二叉树 II](#jz32-ii-从上到下打印二叉树-ii)

### 位运算

[JZ15 二进制中1的个数](#jz15-二进制中1的个数)

### 快速幂

[JZ16 数值的整数次方](#jz16-数值的整数次方)