## Day03：Leetcode  707.移除链表元素  707.设计链表  206.反转链表

### Leetcode  707.移除链表元素

> [Leetcode题目链接]([203. 移除链表元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-linked-list-elements/))

#### 题目简介

#### 思路

#### 题解

- 带头结点的链表

  ```c++
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     ListNode *next;
   *     ListNode() : val(0), next(nullptr) {}
   *     ListNode(int x) : val(x), next(nullptr) {}
   *     ListNode(int x, ListNode *next) : val(x), next(next) {}
   * };
   */
  //不带头结点
  class Solution {
  public:
      ListNode* removeElements(ListNode* head, int val) {
          //删除头结点
          while (head != NULL && head->val == val) {
              ListNode* tmp = head;
              head = head->next;
              delete tmp;
          }
          //删除非头节点
          ListNode* cur = head;
          while (cur != NULL && cur->next != NULL) {
              if (cur->next->val == val) {
                  ListNode* tmp = cur->next;
                  cur->next = cur->next->next;
                  delete tmp;
              }
              else {
                  cur = cur->next;
              }
          }
          return head;
      }
  };
  ```

  

- 不带头结点的链表

  ```c++
  
  ```

### Leetcode  707.设计链表

> [Leetcode题目链接]([707. 设计链表 - 力扣（LeetCode）](https://leetcode.cn/problems/design-linked-list/))

#### 思路

#### 题解



### Leetcode  206.反转链表

> [Leetcode题目链接]([Loading Question... - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-linked-list/))

#### 思路



#### 题解

- 头插法反转链表

- 双指针法

  ```c++
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     ListNode *next;
   *     ListNode() : val(0), next(nullptr) {}
   *     ListNode(int x) : val(x), next(nullptr) {}
   *     ListNode(int x, ListNode *next) : val(x), next(next) {}
   * };
   */
  class Solution {
  public:
      ListNode* reverseList(ListNode* head) {
          ListNode* pre = NULL;
          ListNode* p = head;
          ListNode* q;
          while (p) {
              q = p->next;
              p->next = pre;
              pre = p;
              p = q;
          }
      return pre;
      }
  };
  ```

  

- 递归法

