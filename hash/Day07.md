## Day07：Leetcode  454.四数相加Ⅱ  383.赎金信  15.三数之和  18.四数之和.md

### Leetcode  454.四数相加Ⅱ

#### 题解

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> umap; //key:a+b的数值，value:a+b数值出现的次数
        // 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中
        for (int a : nums1) {
            for (int b : nums2) {
                umap[a + b]++;
            }
        }
        int count = 0; // 统计a+b+c+d = 0 出现的次数
        // 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就把map中key对应的value也就是出现次数统计出来。
        for (int c : nums3) {
            for (int d : nums4) {
                if (umap.find(0 - (c + d)) != umap.end()) {
                    count += umap[0 - (c + d)];
                }
            }
        }
        return count;
    }
};
```

### Leetcode  383.赎金信

#### 题解

- 题解一：暴力破解

  ```c++
  // 时间复杂度: O(n^2)
  // 空间复杂度：O(1)
  class Solution {
  public:
      bool canConstruct(string ransomNote, string magazine) {
          for (int i = 0; i < magazine.length(); i++) {
              for (int j = 0; j < ransomNote.length(); j++) {
                  // 在ransomNote中找到和magazine相同的字符
                  if (magazine[i] == ransomNote[j]) {
                      ransomNote.erase(ransomNote.begin() + j); // ransomNote删除这个字符
                      break;
                  }
              }
          }
          // 如果ransomNote为空，则说明magazine的字符可以组成ransomNote
          if (ransomNote.length() == 0) {
              return true;
          }
          return false;
      }
  };
  ```
  
 - 题解二：hash

   ```c++
   class Solution {
   public:
       bool canConstruct(string ransomNote, string magazine) {
           int record[26] = {0};
           //add
           if (ransomNote.size() > magazine.size()) {
               return false;
           }
           for (int i = 0; i < magazine.length(); i++) {
               // 通过recode数据记录 magazine里各个字符出现次数
               record[magazine[i]-'a'] ++;
           }
           for (int j = 0; j < ransomNote.length(); j++) {
               // 遍历ransomNote，在record里对应的字符个数做--操作
               record[ransomNote[j]-'a']--;
               // 如果小于零说明ransomNote里出现的字符，magazine没有
               if(record[ransomNote[j]-'a'] < 0) {
                   return false;
               }
           }
           return true;
       }
   };
   ```

### Leetcode  15.三数之和

#### 题解

```c++

```

### Leetcode  18.四数之和

#### 题解

```c++

```

