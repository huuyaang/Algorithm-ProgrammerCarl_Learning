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

- 利用unordered_set

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果，之所以用set是为了给结果集去重
        unordered_set<int> nums_set(nums1.begin(), nums1.end());
        for (int num : nums2) {
            // 发现nums2的元素 在nums_set里又出现过
            if (nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};
```

- 利用数组

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果，之所以用set是为了给结果集去重
        int hash[1005] = {0}; // 默认数值为0
        for (int num : nums1) { // nums1中出现的字母在hash数组中做记录
            hash[num] = 1;
        }
        for (int num : nums2) { // nums2中出现话，result记录
            if (hash[num] == 1) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};
```

### Leetcode  202.快乐数  

> [Leetcode题目链接](https://leetcode.cn/problems/happy-number/)

#### 题目简介

#### 思路

#### 题解

```c++
class Solution {
public:
    // 取数值各个位上的单数之和
    int getSum(int n) {
        int sum = 0;
        while (n) {
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
        return sum;
    }
    bool isHappy(int n) {
        unordered_set<int> set;
        while(1) {
            int sum = getSum(n);
            if (sum == 1) {
                return true;
            }
            // 如果这个sum曾经出现过，说明已经陷入了无限循环了，立刻return false
            if (set.find(sum) != set.end()) {
                return false;
            } else {
                set.insert(sum);
            }
            n = sum;
        }
    }
};
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