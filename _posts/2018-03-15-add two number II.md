---
layout: post

title: 'LeetCode--Add two Number II'

subtitle: '15331404 张益强'

date: 2018-03-17

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---

## LeetCode--Add two Number II
[TOC]

---
### 题目描述
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

### 算法解释
这一次的也是加法，直接是7243+564 = 7807；
要求不能将list倒转，也就是要求，从最高位加起。

一眼就想到的办法，直接求出 7243和564，然后为sum构造list。
（我们要有点创造力）

复习了stack，list
坑

> 一定是先使用top后pop，否则容易犯非空的错
> 构造一个逆的list。好好学，认真看。
> 还是先把list倒转，就i不用花费心思处理其他

### 代码

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> s1;
        stack<int> s2;
        
        while(l1!=NULL) {
            s1.push(l1->val);
            l1 = l1->next;
        } 
        while(l2!=NULL) {
            s2.push(l2->val);
            l2 = l2->next;
        }
        
        ListNode* list = new ListNode(0);
        int sum = 0;
        while(!s1.empty() || !s2.empty()) {
            if (!s1.empty()) {
                sum += s1.top();
                s1.pop();
            }
            if (!s2.empty()) {
                sum += s2.top();
                s2.pop();
            }
            list->val = sum % 10;
            ListNode* head = new ListNode(sum / 10);
            head->next = list;
            list = head;
            sum /= 10;
            
            
        }
        return list->val >0?list:list->next;
        
    }
};
```











































