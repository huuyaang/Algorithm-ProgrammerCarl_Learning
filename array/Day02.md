## Day02：Leetcode  977.有序数组的平方  209.长度最小的字数组  59.螺旋矩阵Ⅱ

### Leetcode 977.有序数组的平方

> [Leetcode题目链接](https://leetcode.cn/problems/squares-of-a-sorted-array/)

#### 题目简介

#### 思路

#### 题解

- 暴力破解

  ``` c++
  class Solution {
  public:
      vector<int> sortedSquares(vector<int>& nums) {
          for (int i = 0; i < nums.size(); i++) {
              nums[i] = nums[i] * nums[i];
          }
          sort(nums.begin(), nums.end());
          return nums;
      }
  };
  ```

- 双指针

  ```c++
  class Solution {
  public:
      vector<int> sortedSquares(vector<int>& nums) {
          int i = 0, j = nums.size() - 1, l = nums.size();
          vector<int> NewNums(nums.size(), 0);
          while (i <= j) {
              if (nums[i] * nums[i] >= nums[j] * nums[j]) {
                  NewNums[--l] = nums[i] * nums[i];
                  i++;
              }
              else {
                  NewNums[--l] = nums[j] * nums[j];
                  j--;
              }
          }
          return NewNums;
      }
  };
  ```

  

### Leetcode 209.长度最小的字数组

> [Leetcode题目链接](https://leetcode.cn/problems/minimum-size-subarray-sum/)

#### 题目简介

#### 思路

#### 题解

- 暴力破解（目前Leetcode暴力破解超时）

- 滑动窗口

  ```c++
  class Solution {
  public:
      int minSubArrayLen(int target, vector<int>& nums) {
          int i = 0;
          int sum = 0;
          int result = INT32_MAX;
          int sublength = 0;
          for (int j = 0;j < nums.size(); j++) {
              sum += nums[j];
              while (sum >= target) {
                  sublength = j - i + 1;
                  sum = sum - nums[i];
                  i++;
                  result = result < sublength ? result : sublength;
              }
          }
          return result == INT32_MAX ? 0 : result;
      }
  };
  ```

  

#### 相关题目

- Leetcode 904.水果成篮
- Leetcode 76.最小覆盖子串

### Leetcode 59.螺旋矩阵Ⅱ

> [Leetcode题目链接](https://leetcode.cn/problems/spiral-matrix-ii/)

#### 题目简介

#### 思路

#### 题解

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, 0)); // 使用vector定义一个二维数组
        int startx = 0, starty = 0; // 定义每循环一个圈的起始位置
        int loop = n / 2; // 每个圈循环几次，例如n为奇数3，那么loop = 1 只是循环一圈，矩阵中间的值需要单独处理
        int mid = n / 2; // 矩阵中间的位置，例如：n为3， 中间的位置就是(1，1)，n为5，中间位置为(2, 2)
        int count = 1; // 用来给矩阵中每一个空格赋值
        int offset = 1; // 需要控制每一条边遍历的长度，每次循环右边界收缩一位
        int i,j;
        while (loop --) {
            i = startx;
            j = starty;

            // 下面开始的四个for就是模拟转了一圈
            // 模拟填充上行从左到右(左闭右开)
            for (j = starty; j < n - offset; j++) {
                res[startx][j] = count++;
            }
            // 模拟填充右列从上到下(左闭右开)
            for (i = startx; i < n - offset; i++) {
                res[i][j] = count++;
            }
            // 模拟填充下行从右到左(左闭右开)
            for (; j > starty; j--) {
                res[i][j] = count++;
            }
            // 模拟填充左列从下到上(左闭右开)
            for (; i > startx; i--) {
                res[i][j] = count++;
            }

            // 第二圈开始的时候，起始位置要各自加1， 例如：第一圈起始位置是(0, 0)，第二圈起始位置是(1, 1)
            startx++;
            starty++;

            // offset 控制每一圈里每一条边遍历的长度
            offset += 1;
        }

        // 如果n为奇数的话，需要单独给矩阵最中间的位置赋值
        if (n % 2) {
            res[mid][mid] = count;
        }
        return res;
    }
};
```

#### 相关题目

- Leetcode 54.螺旋矩阵
- 剑指Offer 29.顺时针打印矩阵

