# LeetCode 刷题记录

*Posted by [YanseaTan](https://yansea.cc)*

- [LeetCode 刷题记录](#leetcode-刷题记录)
  - [数组](#数组)
    - [1. 两数之和](#1-两数之和)
    - [26. 删除有序数组中的重复项](#26-删除有序数组中的重复项)
    - [36. 有效的数独](#36-有效的数独)
    - [48. 旋转图像](#48-旋转图像)
    - [55. 跳跃游戏](#55-跳跃游戏)
    - [66. 加一](#66-加一)
    - [122. 买卖股票的最佳时机 II](#122-买卖股票的最佳时机-ii)
    - [136. 只出现一次的数字](#136-只出现一次的数字)
    - [189. 轮转数组](#189-轮转数组)
    - [217. 存在重复元素](#217-存在重复元素)
    - [283. 移动零](#283-移动零)
    - [2016. 增量元素之间的最大差值](#2016-增量元素之间的最大差值)
  - [字符串](#字符串)
    - [344. 反转字符串](#344-反转字符串)
  - [哈希表](#哈希表)
    - [350. 两个数组的交集 II](#350-两个数组的交集-ii)
  - [技巧](#技巧)
    - [双指针](#双指针)
    - [贪心](#贪心)

<br><br><br>

## 数组

### 1. 两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出**和为目标值** target  的那**两个**整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

自己（暴力，我觉得挺好）：

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i,a;
        for(i = 0; i < nums.size() - 1; i++){
            for(a = i + 1; a < nums.size(); a++){
                if(nums[i] + nums[a] == target){
                    return {i,a};
                }
            }
        }
        return {};
    }
};
```

官方（哈希）：

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hashtable;
        for (int i = 0; i < nums.size(); ++i) {
            auto it = hashtable.find(target - nums[i]);
            if (it != hashtable.end()) {
                return {it->second, i};
            }
            hashtable[nums[i]] = i;
        }
        return {};
    }
};
```

<br><br><br>

### 26. 删除有序数组中的重复项

给你一个**升序排列**的数组 nums ，请你**原地**删除重复出现的元素，使每个元素**只出现一次**，返回删除后数组的新长度。元素的**相对顺序**应该保持 一致 。不要使用额外的空间，你必须在**原地**修改输入数组 并在使用 O(1) 额外空间的条件下完成。

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n = nums.size();
        if(n == 0){
            return 0;
        }
        int fast = 1;
        int slow = 1;
        while(fast < n){
            if(nums[fast] != nums[fast - 1]){
                nums[slow] = nums[fast];
                slow++;
            }
            fast++;
        }
        return slow;
    }
};
```

<br><br><br>

### 36. 有效的数独

请你判断一个 9 x 9 的数独是否有效。只需要根据以下规则 ，验证已经填入的数字是否有效即可。空白格用 '.' 表示。

官方：

```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        //记录数独的每一行每个数字出现的次数
        int rows[9][9];
        //记录数独的每一列每个数字出现的次数
        int columns[9][9];
        //记录数独的每一个小九宫格中的每个数字的出现次数
        int subboxes[3][3][9];
        
        //初始化数组
        memset(rows,0,sizeof(rows));
        memset(columns,0,sizeof(columns));
        memset(subboxes,0,sizeof(subboxes));
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                char c = board[i][j];
                if (c != '.') {
                    //char 转 int，并减1
                    int index = c - '0' - 1;
                    rows[i][index]++;
                    columns[j][index]++;
                    subboxes[i / 3][j / 3][index]++;
                    if (rows[i][index] > 1 || columns[j][index] > 1 || subboxes[i / 3][j / 3][index] > 1) {
                        return false;
                    }
                }
            }
        }
        return true;
    }
};
```

<br><br><br>

### 48. 旋转图像

给定一个 n × n 的二维矩阵 matrix 表示一个图像。请你将图像顺时针旋转 90 度。你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要 使用另一个矩阵来旋转图像。

官方：

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for(int i = 0; i < n / 2; i++){
            for(int j = 0; j < (n + 1) / 2; j ++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[n - j - 1][i];
                matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
                matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
                matrix[j][n - i - 1] = temp;
            }
        }
    }
};
```

<br><br><br>

### 55. 跳跃游戏

给出一个非负整数数组，你最初定位在数组的第一个位置，数组中的每个元素的值代表你在那个位置可以跳跃的最大长度。判断你是否能到达数组的最后一个位置。

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return true;
        int max = 0;
        for(int i = 0; i < n - 1; i++){
            if(nums[i] + i > max) max = nums[i] + i;
            if(max >= n - 1) return true;
            else if(nums[i] == 0 && max == i) return false;
        }
        return false;
    }
};
```

<br><br><br>

### 66. 加一

给定一个由**整数**组成的**非空**数组所表示的非负整数，在该数的基础上加一。最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。你可以假设除了整数 0 之外，这个整数不会以零开头。

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        for (int i = n - 1; i >= 0; --i) {
            //从后往前判断是不是9，一直到不是9的那位进行加1
            if (digits[i] != 9) {
                ++digits[i];
                //让从后往前数所有是9的变成0
                for (int j = i + 1; j < n; ++j) {
                    digits[j] = 0;
                }
                return digits;
            }
        }
        //digits 中所有的元素均为 9
        vector<int> ans(n + 1);
        //默认除首位外都是0
        ans[0] = 1;
        return ans;
    }
};
```

<br><br><br>

### 122. 买卖股票的最佳时机 II

给定一个数组 prices ，其中 prices[i] 表示股票第 i 天的价格。在每一天，你可能会决定购买和/或出售股票。你在任何时候**最多**只能持有**一股**股票。你也可以购买它，然后在**同一天**出售。返回你能获得的**最大**利润 。

自己：

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int profit = 0;
        for(int i = 0; i < prices.size() - 1; i++){
            int diff = prices[i + 1] - prices[i];
            if(diff > 0){
                profit += diff;
            }
        }
        return profit;
    }
};
```

官方：

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {   
        int ans = 0;
        int n = prices.size();
        for (int i = 1; i < n; ++i) {
            ans += max(0, prices[i] - prices[i - 1]);
        }
        return ans;
    }
};
```

<br><br><br>

### 136. 只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

提示：运用了位运算，异或运算满足交换律和结合律，即 a⊕b⊕a=b⊕a⊕a=b⊕(a⊕a)=b⊕0=b。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for(int i : nums){
            res ^= i;
        }
        return res;
    }
};
```

<br><br><br>

### 189. 轮转数组

给你一个数组，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int newN[nums.size()];
        for(int i = 0; i < nums.size(); i++){
            newN[i] = nums[i];
        }
        for(int i = 0; i < nums.size(); i++){
            nums[(i + k) % nums.size()] = newN[i];
        }
    }
};
```

<br><br><br>

### 217. 存在重复元素

给你一个整数数组 nums 。如果任一值在数组中出现**至少两次**，返回 true ；如果数组中每个元素互不相同，返回 false 。

自己（暴力，超时）：

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int n = nums.size();
        if(n < 2) return false;
        for(int i = 0; i < n - 1; i++){
            for(int j = i + 1; j < n; j++){
                if(nums[j] == nums[i]) return true;
            }
        }
        return false;
    }
};
```

官方（直接调用了排序算法 sort()，喵喵喵？）：

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        for(int i = 1; i < n; i++){
            if(nums[i] == nums[i - 1]) return true;
        }
        return false;
    }
};
```

<br><br><br>

### 283. 移动零

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。**请注意**，必须在不复制数组的情况下原地对数组进行操作。

自己（双指针）：

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        if(n < 2) return;
        int fast = 1;
        int slow = 0;
        while(fast < n){
            if(nums[slow] == 0 && nums[fast] != 0){
                nums[slow] = nums[fast];
                nums[fast] = 0;
                slow++;
            }
            if(nums[slow] != 0) slow++;
            fast++;
        }
    }
};
```

官方（双指针，更好）：

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size(), left = 0, right = 0;
        while (right < n) {
            //右指针如果不是零，左右指针的值交换，并都向右走一步；如果右指针是零，右指针直接向右走一步
            if (nums[right]) {
                swap(nums[left], nums[right]);
                left++;
            }
            right++;
        }
    }
};
```

<br><br><br>

### 2016. 增量元素之间的最大差值

给你一个下标从 0 开始的整数数组 nums ，该数组的大小为 n ，请你计算 nums[j] - nums[i] 能求得的最大差值，其中 0 <= i < j < n 且 nums[i] < nums[j] 。返回最大差值。如果不存在满足要求的 i 和 j ，返回 -1 。

自己（双指针）：

```c++
class Solution {
public:
    int maximumDifference(vector<int>& nums) {
        int n = nums.size();
        int fast = 1, slow = 0, maxDiff = -1;
        while(n - fast){
            maxDiff = max(maxDiff, nums[fast] - nums[slow]);
            if(nums[slow] > nums[fast]){
                slow = fast;
                fast++;
            }
            else fast++;
        }
        if(maxDiff) return maxDiff;
        else return -1;
    }
};
```

<br><br><br>

## 字符串

### 344. 反转字符串

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

自己（双指针）：

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int n = s.size();
        //n - 1 这个要注意不要写成 n
        int l = 0, r = n - 1;
        char temp;
        while(l < r){
            temp = s[r];
            s[r] = s[l];
            s[l] = temp;
            l++;
            r--;
        }
    }
};
```

<br><br><br>

## 哈希表

### 350. 两个数组的交集 II

给你两个整数数组 nums1 和 nums2 ，请你以数组形式返回两数组的交集。返回结果中每个元素出现的次数，应与元素在两个数组中都出现的次数一致（如果出现次数不一致，则考虑取较小值）。可以不考虑输出结果的顺序。

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        if (nums1.size() > nums2.size()) {
            //运用递归让长度较小的数组作为 nums1
            return intersect(nums2, nums1);
        }
        //创建哈希表
        unordered_map <int, int> m;
        //让 num 遍历 nums1，让出现过的数字的个数（m）加1
        for (int num : nums1) {
            ++m[num];
        }
        //创建数组，向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）
        vector<int> intersection;
        for (int num : nums2) {
            //如果哈希表中存在 nums2 中的数 num，则向数组中添加，且哈希表中对应数的个数减1
            if (m.count(num)) {
                intersection.push_back(num);
                --m[num];
                //如果 num 键中的数字（m）为0，则删除此键
                if (m[num] == 0) {
                    m.erase(num);
                }
            }
        }
        return intersection;
    }
};
```

<br><br><br>

## 技巧

### 双指针

[26. 删除有序数组中的重复项](#26-删除有序数组中的重复项)

[283. 移动零](#283-移动零)

[344. 反转字符串](#344-反转字符串)

[2016. 增量元素之间的最大差值](#2016-增量元素之间的最大差值)

### 贪心

[122. 买卖股票的最佳时机 II](#122-买卖股票的最佳时机-ii)

[2016. 增量元素之间的最大差值](#2016-增量元素之间的最大差值)