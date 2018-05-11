---
layout: post

title: 'LeetCode--Add two Number I'

subtitle: '15331404 张益强'

date: 2018-03-10

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---



## LeetCode- Add two number I

[TOC]

---
### 题目描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

----

### 算法讲解
首先这道题并不难，肯定都会做，只是要做add-two-number II，就先来做I。

一开始想着最愚蠢的办法，遍历一次l1，l2，然后求和，最后再构造出相应的ListNode.

仔细想想，是可以在O（maxlength（l1，l2））
时间内跑完的。

只要用一个额外的值表示进位，记录要加到下一个节点的值就好。

提醒注意的地方

>  1. 给a？b：c 加上括号。否则会只加到l1的值。
>  2. Node* 的构造必须是new  Node* result = new Node();    
>    又或者Node a(0）；*result= &a

>  巧妙的地方是直接构造下一个结点，而不是赋值给root，最后在结果的输出的时候才root->next.（学习）
### 代码

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    	ListNode* result = new ListNode(0);
    	int extra = 0;  //表示进位 
    	ListNode* p = result;
    	while(l1||l2||extra) {
    		int sum = (l1?l1->val:0) + (l2?l2->val:0)+ extra;
    		extra = sum/10;
    		p->next = new ListNode(sum%10);
    		p = p->next;
    		l2 = l2?l2->next:l2;
    		l1 = l1?l1->next:l1;
		}
		return result->next;    
	}
};
```















































































