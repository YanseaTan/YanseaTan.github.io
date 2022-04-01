# LeetCode 刷题记录

- [LeetCode 刷题记录](#leetcode-刷题记录)
  - [数据结构](#数据结构)
    - [数组](#数组)
      - [26. 删除有序数组中的重复项](#26-删除有序数组中的重复项)
  - [算法](#算法)
    - [双指针](#双指针)

## 数据结构

### 数组

#### 26. 删除有序数组中的重复项

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

## 算法

### 双指针

[26. 删除有序数组中的重复项](#26-删除有序数组中的重复项)