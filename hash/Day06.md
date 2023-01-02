## Day06：Leetcode  242.有效的字母异位词  349.两个数组的交集  202.快乐数  1.两数之和

### Leetcode  242.有效的字母异位词

> [Leetcode题目链接](https://leetcode.cn/problems/valid-anagram/submissions/)

#### 题目简介

#### 思路

#### 题解

- 题解一：暴力破解

- 题解二：利用hash表

  ```c++
  class Solution {
  public:
      bool isAnagram(string s, string t) {
          int record[26] = {0};
          for (int i = 0; i < s.size(); i++) {
              record[s[i] - 'a']++;
          }
          for (int i = 0; i < t.size(); i++) {
              record[t[i] - 'a']--;
          }
          for (int i = 0; i < 26; i++) {
              if (record[i] != 0) {
                  return false;
              }
          }
          return true;
      }
  };
  ```

### Leetcode  349.两个数组的交集

> [Leetcode题目链接](https://leetcode.cn/problems/intersection-of-two-arrays/)

#### 题目简介

#### 思路

#### 题解

```c++
部分代码不懂
```

### Leetcode  202.快乐数  

> [Leetcode题目链接](https://leetcode.cn/problems/happy-number/)

#### 题目简介

#### 思路

#### 题解

```c++
代码运行出错
```

### Leetcode  1.两数之和

#### 题目简介

#### 思路

#### 题解

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map <int,int> map;
        for(int i = 0; i < nums.size(); i++) {
            // 遍历当前元素，并在map中寻找是否有匹配的key
            auto iter = map.find(target - nums[i]); 
            if(iter != map.end()) {
                return {iter->second, i};
            }
            // 如果没找到匹配对，就把访问过的元素和下标加入到map中
            map.insert(pair<int, int>(nums[i], i)); 
        }
        return {};
    }
};
```



