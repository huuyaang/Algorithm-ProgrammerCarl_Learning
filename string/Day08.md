## Day08：344.反转字符串  541.反转字符串Ⅱ  剑指Offer 05替换空格  151.反转字符串里的单词  剑指Offer58-Ⅱ左旋转字符串

### 344.反转字符串

> [344. 反转字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-string/)

#### 题解

```c++
void reverseString(vector<char>& s) {
    for (int i = 0, j = s.size() - 1; i < s.size()/2; i++, j--) {
        swap(s[i],s[j]);
    }
}
```

#### swap的两种实现方式

- 方式一：交换数值

  ```c++
  int tmp = s[i];
  s[i] = s[j];
  s[j] = tmp;
  ```

- 方式二：位运算

  ```c++
  s[i] ^= s[j];
  s[j] ^= s[i];
  s[i] ^= s[j];
  ```

### 541.反转字符串Ⅱ

> [541. 反转字符串 II - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-string-ii/)

#### 题解

- 解法一：使用C++库函数reverse的版本如下：

  ```c++
  class Solution {
  public:
      string reverseStr(string s, int k) {
          for (int i = 0; i < s.size(); i += (2 * k)) {
              // 1. 每隔 2k 个字符的前 k 个字符进行反转
              // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
              if (i + k <= s.size()) {
                  reverse(s.begin() + i, s.begin() + i + k );
              } else {
                  // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
                  reverse(s.begin() + i, s.end());
              }
          }
          return s;
      }
  };
  ```

- 解法二：实现自己的reverse函数

  ```c++
  class Solution {
  public:
      void reverse(string& s, int start, int end) {
          for (int i = start, j = end; i < j; i++, j--) {
              swap(s[i], s[j]);
          }
      }
      string reverseStr(string s, int k) {
          for (int i = 0; i < s.size(); i += (2 * k)) {
              // 1. 每隔 2k 个字符的前 k 个字符进行反转
              // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
              if (i + k <= s.size()) {
                  reverse(s, i, i + k - 1);
                  continue;
              }
              // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
              reverse(s, i, s.size() - 1);
          }
          return s;
      }
  };
  ```

- 解法三：

  ```c++
  class Solution {
  public:
      string reverseStr(string s, int k) {
          int n = s.size(),pos = 0;
          while(pos < n){
              //剩余字符串大于等于k的情况
              if(pos + k < n) reverse(s.begin() + pos, s.begin() + pos + k);
              //剩余字符串不足k的情况 
              else reverse(s.begin() + pos,s.end());
              pos += 2 * k;
          }
          return s;
      }
  };
  ```

### 剑指Offer 05替换空格

> [剑指 Offer 05. 替换空格 - 力扣（LeetCode）](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

#### 题解

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int count = 0; // 统计空格的个数
        int sOldSize = s.size();
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == ' ') {
                count++;
            }
        }
        // 扩充字符串s的大小，也就是每个空格替换成"%20"之后的大小
        s.resize(s.size() + count * 2);
        int sNewSize = s.size();
        // 从后先前将空格替换为"%20"
        for (int i = sNewSize - 1, j = sOldSize - 1; j < i; i--, j--) {
            if (s[j] != ' ') {
                s[i] = s[j];
            } else {
                s[i] = '0';
                s[i - 1] = '2';
                s[i - 2] = '%';
                i -= 2;
            }
        }
         return s;
    }
};
```

### 151.反转字符串里的单词

> [151. 反转字符串中的单词 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-words-in-a-string/)

#### 题解

从前向后遍历，遇到空格了就erase

```c++
//版本一 
void removeExtraSpaces(string& s) {
    int slowIndex = 0, fastIndex = 0; // 定义快指针，慢指针
    // 去掉字符串前面的空格
    while (s.size() > 0 && fastIndex < s.size() && s[fastIndex] == ' ') {
        fastIndex++;
    }
    for (; fastIndex < s.size(); fastIndex++) {
        // 去掉字符串中间部分的冗余空格
        if (fastIndex - 1 > 0
                && s[fastIndex - 1] == s[fastIndex]
                && s[fastIndex] == ' ') {
            continue;
        } else {
            s[slowIndex++] = s[fastIndex];
        }
    }
    if (slowIndex - 1 > 0 && s[slowIndex - 1] == ' ') { // 去掉字符串末尾的空格
        s.resize(slowIndex - 1);
    } else {
        s.resize(slowIndex); // 重新设置字符串大小
    }
}
```

### 剑指Offer58-Ⅱ左旋转字符串

> [剑指 Offer 58 - II. 左旋转字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

#### 题解

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(), s.begin() + n);
        reverse(s.begin() + n, s.end());
        reverse(s.begin(), s.end());
        return s;
    }
};
```

