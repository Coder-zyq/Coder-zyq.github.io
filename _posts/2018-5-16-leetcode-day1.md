---
layout: post
title: 'LeetCode day 1'
subtitle: ' coder-zyq'
date: 2018-05-16
categories: LeetCode  
cover: 'http://img.article.pchome.net/00/34/54/50/pic_lib/wm/Black04.jpg'
tags: LeetCode C++ algorithm

---
# leetcode 刷题

```C
刷题为考研和春招做准备，尽量贴答案和相应知识点
```

## Two Sum
### problem 
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

给定一个数组，找出两个数之和等于target，输出对应的下标，假设只有一个答案，并且一个元素不能使用两次。
### solution
```C++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		vector<int> result;
		
		for (unsigned int i = 0; i < nums.size(); i++) {
			for (unsigned int j = i + 1; j < nums.size(); j++) {
				if (nums[i] + nums[j] == target) {
					result.push_back(i);
					result.push_back(j);
					return result;
				}
				if (nums[i] > target) continue;
			}
		}
		return result;
	}
};
```

### 涉及知识点总结,希望自己不要再犯。
1. system("pause")   
用于直接调用Dos命令Pause。
说明：
void system(char* cmd); 
参数cmd，DOS命令，如Pause, cls 
返回值：无。
运行到此处时，会显示“Press any key to continue”

2. vector使用总结
放[另外一篇文章-vectorr总结](https://)

3. vector.size() 返回unsigned int 类型，所以要将i设置为unsigned int 类型。

### O(n) 解法
```c++
vector<int> twoSum(vector<int> &numbers, int target)
{
    //Key is the number and value is its index in the vector.
	unordered_map<int, int> hash;
	vector<int> result;
	for (int i = 0; i < numbers.size(); i++) {
		int numberToFind = target - numbers[i];

            //if numberToFind is found in map, return them
		if (hash.find(numberToFind) != hash.end()) {
			result.push_back(hash[numberToFind] );
			result.push_back(i );			
			return result;
		}

            //number was not found. Put it in the map.
		hash[numbers[i]] = i;
	}
	return result;
}
```
attention：map find用法 ，见博客[map详解](https://)