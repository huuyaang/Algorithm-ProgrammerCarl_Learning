## Day01：Leetcode 704.二分查找、27.移出元素

### Leetcode 704.二分查找
> [Leetcode题目链接](https://leetcode.cn/problems/binary-search/)

#### 题目简介：

给定一个<u>**有序不重复**</u>数组`nums`，查找目标值`target`，查找成功返回数组下标，查找失败返回-1.

#### 解题思路：

- 情况一：左闭右闭

```c
int search(int* nums, int numsSize, int target){
    int left = 0, right = numsSize - 1;
    while (left <= right) {
        int middle = left + ((right - left) / 2);
        if ( nums[middle] == target ) {
            return middle;
        }
        else if ( nums[middle] < target ) {
            left += 1;
        }
        else {
            right -= 1;
        }
    }
    return -1;
}
```
- 情况二：左闭右开

```c
int search (int* nums, int numsSize, int target) {
    int left = 0, right = numsSize - 1;
    while (left <= right) {
        int middle = left + ((right - left) / 2);
        if (nums[middle] < target) {
            left = middle + 1;
        }
        else if (nums[middle] > target) {
            right = middle - 1;
        }
        else {
            return middle;
        }
    }
    return -1;
}
```

#### 相关题目：

- Leetcode 35.搜索插入位置
- Leetcode 34.在排序数组中查找元素的第一个和最后一个位置
- Leetcode 69.x的平方根
- Leetcode 367.有效的完全平方数

### Leetcode 27.移除元素

> [Leetcode题目链接](https://leetcode.cn/problems/remove-element/)

#### 题目简介：

给定一个数组`nums`和一个值`val`，<u>**原地**</u>移除所有值等于`val`的元素，并返回移除后数组的新长度。要求**<u>不使用额外的数组空间</u>**，空间复杂度要求O(1)并**原地**修改输入数组，元素的顺序可以改变，无需考虑数组中超出新长度后面的元素。

#### 解题思路：

- 思路一：暴力破解

```c++
// 时间复杂度：O(n^2)
// 空间复杂度：O(1)
class Solution {
public:
    int removeElement (vector<int>& nums, int val) {
        int size = nums.size();
        for (int i = 0; i < size; i++) {
            if (nums[i] == val) { // 发现需要移除的元素，就将数组集体向前移动一位
                for (int j = i + 1; j < size; j++) {
                    nums[j - 1] = nums[j];
                }
                i--; // 因为下标i以后的数值都向前移动了一位，所以i也向前移动一位
                size--; // 此时数组的大小-1
            }
        }
        return size;
    }
};
```

- 思路二：双指针
  - 双指针解法一（快慢指针法）（不改变元素相对位置，需要移动较多的元素，复杂度稍高）
  
  
  ```c++
  //时间复杂度O(n)
  //空间复杂度O(1)
  class Solution {
  public:
      int removeElement (vector<int>& nums, int val) {
          int SlowIndex = 0;
          for (int FastIndex = 0; FastIndex < nums.size(); FastIndex++) {
              if (val != nums[FastIndex]) {
                  nums[SlowIndex++] = nums[FastIndex];
              }
          }
          return SlowIndex;
      }
  };
  ```
  
  - 双指针解法二（双向双指针法）（改变相对位置，可以使移动的元素更少，复杂度较低）
  
  ```c++
  /**
  * 相向双指针方法，基于元素顺序可以改变的题目描述改变了元素相对位置，确保了移动最少元素
  * 时间复杂度：O(n)
  * 空间复杂度：O(1)
  */
  class Solution {
  public:
      int removeElement(vector<int>& nums, int val) {
          int leftIndex = 0;
          int rightIndex = nums.size() - 1;
          while (leftIndex <= rightIndex) {
              // 找左边等于val的元素
              while (leftIndex <= rightIndex && nums[leftIndex] != val){
                  ++leftIndex;
              }
              // 找右边不等于val的元素
              while (leftIndex <= rightIndex && nums[rightIndex] == val) {
                  -- rightIndex;
              }
              // 将右边不等于val的元素覆盖左边等于val的元素
              if (leftIndex < rightIndex) {
                  nums[leftIndex++] = nums[rightIndex--];
              }
          }
          return leftIndex;   // leftIndex一定指向了最终数组末尾的下一个元素
      }
  };
  ```
  


#### 出现的错误：

heap溢出

#### 相关题目：

- Leetcode 26.删除排序数组中的重复项
- Leetcode 283.移动零
- Leetcode 844.比较含退格的字符串
- Leetcode 977.有序数组的平方