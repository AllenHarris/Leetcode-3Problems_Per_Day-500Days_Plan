# [027 Remove Element](https://leetcode.com/problems/remove-element/)

## 难度：Easy

##  题目

Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## 分析

### 输入

1. 整型数组

2. 整型数值


### 输出

去除数组中含有的给定数值后的数组长度

### 要求

1. 不使用额外的数组空间，须在原数组内修改，空间复杂度为O(1)
2. 不用管超出去重数组长度后面的元素

### 解题思想

本题的思路和 [026 Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) 一致，

使用双指针

## 代码

```C++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        //特殊条件，当数组为空时
        if(!nums.size()){
            return 0;
        }
        //数组不为空时
        int index=0;
        for(int i=0; i < nums.size(); ++i){
            if(nums[i] != val){
                nums[index++] = nums[i];
            }
        }
        return index;	//index从零开始，遍历从0开始，由于满足条件是index已自增1，故直接返回index即可
    }
};
```

### 算法改进

前面的算法进行了很多不必要的复制操作，改进的算法主要是减少不必要的复制操作。

当我们遇到 nums[i] = val 时，我们可以将当前元素与最后一个元素进行交换，并释放最后一个元素。这实际上使数组的大小减少了 1。

请注意，被交换的最后一个元素可能是您想要移除的值。但是不要担心，在下一次迭代中，我们仍然会检查这个元素。

```C++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        //特殊条件，当数组为空时
        if(!nums.size()){
            return 0;
        }
        //数组不为空时
        int index=0;
        int length = nums.size();
        while(index < length){
            if(nums[index] == val){
                nums[index] = nums[length - 1];
                length--;
            }
            else
                index++;
        }
        return length;
    }
};
```

### 使用Vector容器的特性

```C++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        vector<int> :: iterator it;
        for(it = nums.begin(); it != nums.end(); it++){
            if(*it == val){
                nums.erase(it);
                it--;
            }
        }
        return nums.size();
    }
};
```

以上三种算法优秀程度依次递增。

## 时间复杂度

显而易见：O(n)

## 空间复杂度

显而易见：O(1)

