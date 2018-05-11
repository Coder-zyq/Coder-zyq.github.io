---
layout: post
title: '算法训练 1 leetCode'
subtitle: '15331404 张益强'
date: 2018-03-16
 
cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'
tags: 算法 LeetCode
---

# LeetCode 算法训练
## 题目描述
> There are a total of n courses you have to take, labeled from 0 to n - 1.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]
Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?


For example:

``` 2, [[1,0]] ```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

```**题目大意就是，有一组边，[a，b]，要经过b，必须先经过a，判断是否没有冲突，可以想象为判断树中是否不存在环，如果存在，则可能性为false，不存在环，则为true。**

```


> 拓扑排序


## 代码
```
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites)
{
    vector<unordered_set<int>> matrix(numCourses); // save this directed graph
    for(int i = 0; i < prerequisites.size(); ++ i)
        matrix[prerequisites[i][1]].insert(prerequisites[i][0]);
    
    vector<int> d(numCourses, 0); // in-degree
    for(int i = 0; i < numCourses; ++ i)
        for(auto it = matrix[i].begin(); it != matrix[i].end(); ++ it)
            ++ d[*it];
    
    for(int j = 0, i; j < numCourses; ++ j)
    {
        for(i = 0; i < numCourses && d[i] != 0; ++ i); // find a node whose in-degree is 0
        
        if(i == numCourses) // if not find
            return false;
        
        d[i] = -1;
        for(auto it = matrix[i].begin(); it != matrix[i].end(); ++ it)
            -- d[*it];
    }
    
    return true;
}
};
```
