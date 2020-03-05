---
layout: post
title:  "Algorithms - Part 1"
date:   2020-03-05 16:23:31 +1300
categories: Algorithms
---

This article is all about solving the algorithm problem.

**Algorithm to find the unique pair of numbers from a given set of list.**

Here I will be expressing my views on the problem and looking for the solution. I think doing algorithm is a best way to exercise your brain and learn about data structure. This is something which doesn't need anything other than logic, thinking and learning about data structure. Unlike other areas in computer science where we need to learn and remember a lot of information to apply. We will use javascript and C++ to implement our algorithm here.

This question is borrowed from leetcode.

{% highlight ruby %}

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

{% endhighlight %}

**Discussion** - Finding a number in an array has a time complexity of O(n).

Can we use other datastructure that has a lower time complexity?

**What is O(log n)?**
It means what is the power of 2 to get the number n. 

So, let's say the given answer is at index 8, it will take 8 iterations to reach to that number if the time complexity is O(n). Now, assume the time complexity is 0(logn), now it will take just 3 iterations to reach to the same number.
How it works because O(log n) is a binary search, where the search needs to be done in the subset and not on the whole complete set. Example, think of a phone number search in contact list of phone. When we type 'S', we get the subset of all the contacts starting from the letter 'S'. Thus, this is nothing but a search of log n time complexity search.

**Idea to find the solution -**

a) Work on how to solve the problem - give a first thought and then we can work on improving it.

Pick first number let's say 2 the target is 9, so look for a number 7 since 9 - 2 = 7. If we didn't find the number, then move to next number i.e. 7 now look for 2. Also, if we didn't find the number then iterate to the next number i.e. 11, now look for the number -2. This way, iterate until you reach the end.

b) Work on Data structure.
The idea is good but it takes time to iterate and this is a brute force method. This will take O(n^2) time complexity.
For each input from an array, you are traversing again to find the complementary number to achieve the target. This takes time since we are using nested loop. Thus, the complexity will be O(n^2).

So, the idea here is to use a data structure that will minimize the lookup. For e.g., map in C++ has a time compexity of O(log n), because you just need a key to look for a value.

c) Implementation.

a) Take value from an array and insert it onto a map. 
b) Now, while you are inserting the value in a map, also look for the complementary number that will suffice the target.

Here is the implementation in C++

{% highlight ruby %}

class Solution {
public:
vector<int> twoSum(vector<int>& nums, int target)
{
    map<int, int> mymap;
    map<int,int>::iterator j;
    for (unsigned int i = 0; i < nums.size(); i++)
    {
        mymap.insert(std::pair<int,int>(nums[i], i));

        if ((j = mymap.find(target - nums[i])) != mymap.end() && (j->second != i))
        {
        {
            return {i, j->second};
        }

    }
    return {};
}
};

{% endhighlight %}

Here is the implementation in Javascript.

{% highlight ruby %}

console.time('start');
var twoSum = function(nums, target) {
    
let mymap = new Map();

for(let i = 0; i < nums.length; i++)
{
   if(mymap.has(target - nums[i]))
    {
        return [i, mymap.get(target - nums[i])];
    }
    mymap.set(nums[i], i);
}
};
console.timeEnd('Finished')

console.log(twosum([3,2,4],6));

{% endhighlight %}

It takes 0.74 milliseconds in my machine. The time it takes to execute depends mainly on the CPU speed. But this number has no meaning since the efficiency of algorithm is obtained using Big O notation i.e. time compexity. This brings an end to this article.
