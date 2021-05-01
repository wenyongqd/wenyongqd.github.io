---
title: LeetCode Binary Search Summary
date: 2020-07-31 23:04:01
tags:
---

<!-- TOC -->

- [第一类： 需查找和目标值完全相等的数](#第一类-需查找和目标值完全相等的数)
- [第二类： 查找第一个不小于目标值的数，可变形为查找最后一个小于目标值的数](#第二类-查找第一个不小于目标值的数可变形为查找最后一个小于目标值的数)
- [第三类： 查找第一个大于目标值的数，可变形为查找最后一个不大于目标值的数](#第三类-查找第一个大于目标值的数可变形为查找最后一个不大于目标值的数)
- [第四类： 用子函数当作判断关系（通常由 mid 计算得出）](#第四类-用子函数当作判断关系通常由-mid-计算得出)
- [第五类： 其他（通常 target 值不固定）](#第五类-其他通常-target-值不固定)

<!-- /TOC -->

> 二分查找法作为一种常见的查找方法，将原本是线性时间提升到了对数时间范围，大大缩短了搜索时间，具有很大的应用场景，而在 LeetCode 中，要运用二分搜索法来解的题目也有很多，但是实际上二分查找法的查找目标有很多种，而且在细节写法也有一些变化

### 第一类： 需查找和目标值完全相等的数

这是最简单的一类，也是我们最开始学二分查找法需要解决的问题，比如我们有数组 [2, 4, 5, 6, 9]，target = 6，那么我们可以写出二分查找法的代码如下：

```java
int find(vector<int>& nums, int target) {
    int left = 0, right = nums.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid;
    }
    return -1;
}
```

会返回 3，也就是 target 的在数组中的位置。注意二分查找法的写法并不唯一，主要可以变动地方有四处：

第一处是 right 的初始化，可以写成 nums.size() 或者 nums.size() - 1。

第二处是 left 和 right 的关系，可以写成 left < right 或者 left <= right。

第三处是更新 right 的赋值，可以写成 right = mid 或者 right = mid - 1。

第四处是最后返回值，可以返回 left，right，或 right - 1。

但是这些不同的写法并不能随机的组合，像博主的那种写法，若 right 初始化为了 nums.size()，那么就必须用 left < right，而最后的 right 的赋值必须用 right = mid。但是如果我们 right 初始化为 nums.size() - 1，那么就必须用 left <= right，并且 right 的赋值要写成 right = mid - 1，不然就会出错。所以博主的建议是选择一套自己喜欢的写法，并且记住，实在不行就带简单的例子来一步一步执行，确定正确的写法也行。
第一类应用实例:
[Intersection of Arrays](http://www.cnblogs.com/grandyang/p/5507129.html)

### 第二类： 查找第一个不小于目标值的数，可变形为查找最后一个小于目标值的数

这是比较常见的一类，因为我们要查找的目标值不一定会在数组中出现，也有可能是跟目标值相等的数在数组中并不唯一，而是有多个，那么这种情况下 nums[mid] == target 这条判断语句就没有必要存在。比如在数组 [2, 4, 5, 6, 9] 中查找数字 3，就会返回数字 4 的位置；在数组 [0, 1, 1, 1, 1] 中查找数字 1，就会返回第一个数字 1 的位置。我们可以使用如下代码：

```java
int find(vector<int>& nums, int target) {
    int left = 0, right = nums.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) left = mid + 1;
        else right = mid;
    }
    return right;
}
```

最后我们需要返回的位置就是 right 指针指向的地方。在 C++ 的 STL 中有专门的查找第一个不小于目标值的数的函数 lower_bound，在博主的解法中也会时不时的用到这个函数。但是如果面试的时候人家不让使用内置函数，那么我们只能老老实实写上面这段二分查找的函数。

这一类可以轻松的变形为查找最后一个小于目标值的数，怎么变呢。我们已经找到了第一个不小于目标值的数，那么再往前退一位，返回 right - 1，就是最后一个小于目标值的数。

第二类应用实例：
[Heaters](http://www.cnblogs.com/grandyang/p/6181626.html), [Arranging Coins](http://www.cnblogs.com/grandyang/p/6026066.html), [Valid Perfect Square](http://www.cnblogs.com/grandyang/p/5619296.html), [Max Sum of Rectangle No Larger Than K](http://www.cnblogs.com/grandyang/p/5617660.html), [Russian Doll Envelopes](http://www.cnblogs.com/grandyang/p/5568818.html)

第二类变形应用：[Valid Triangle Number](http://www.cnblogs.com/grandyang/p/7053730.html)

### 第三类： 查找第一个大于目标值的数，可变形为查找最后一个不大于目标值的数

这一类也比较常见，尤其是查找第一个大于目标值的数，在 C++ 的 STL 也有专门的函数 upper_bound，这里跟上面的那种情况的写法上很相似，只需要添加一个等号，将之前的 nums[mid] < target 变成 nums[mid] <= target，就这一个小小的变化，其实直接就改变了搜索的方向，使得在数组中有很多跟目标值相同的数字存在的情况下，返回最后一个相同的数字的下一个位置。比如在数组 [2, 4, 5, 6, 9] 中查找数字 3，还是返回数字 4 的位置，这跟上面那查找方式返回的结果相同，因为数字 4 在此数组中既是第一个不小于目标值 3 的数，也是第一个大于目标值 3 的数，所以 make sense；在数组 [0, 1, 1, 1, 1] 中查找数字 1，就会返回坐标 5，通过对比返回的坐标和数组的长度，我们就知道是否存在这样一个大于目标值的数。参见下面的代码：

```java
int find(vector<int>& nums, int target) {
    int left = 0, right = nums.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] <= target) left = mid + 1;
        else right = mid;
    }
    return right;
}
```

这一类可以轻松的变形为查找最后一个不大于目标值的数，怎么变呢。我们已经找到了第一个大于目标值的数，那么再往前退一位，返回 right - 1，就是最后一个不大于目标值的数。比如在数组 [0, 1, 1, 1, 1] 中查找数字 1，就会返回最后一个数字 1 的位置 4，这在有些情况下是需要这么做的。

第三类应用实例：
[Kth Smallest Element in a Sorted Matrix](http://www.cnblogs.com/grandyang/p/5727892.html)

第三类变形应用示例：

[Sqrt(x)](http://www.cnblogs.com/grandyang/p/4346413.html)

### 第四类： 用子函数当作判断关系（通常由 mid 计算得出）

这是最令博主头疼的一类，而且通常情况下都很难。因为这里在二分查找法重要的比较大小的地方使用到了子函数，并不是之前三类中简单的数字大小的比较，比如 Split Array Largest Sum 那道题中的解法一，就是根据是否能分割数组来确定下一步搜索的范围。类似的还有 Guess Number Higher or Lower 这道题，是根据给定函数 guess 的返回值情况来确定搜索的范围。对于这类题目，博主也很无奈，遇到了只能自求多福了。

第四类应用实例：

[Split Array Largest Sum](http://www.cnblogs.com/grandyang/p/5933787.html)， [Guess Number Higher or Lower](http://www.cnblogs.com/grandyang/p/5666502.html)，[Find K Closest Elements](http://www.cnblogs.com/grandyang/p/7519466.html)，[Find K-th Smallest Pair Distance](http://www.cnblogs.com/grandyang/p/8627783.html)，[Kth Smallest Number in Multiplication Table](http://www.cnblogs.com/grandyang/p/8367505.html)，[Maximum Average Subarray II](http://www.cnblogs.com/grandyang/p/8021421.html)，[Minimize Max Distance to Gas Station](http://www.cnblogs.com/grandyang/p/8970057.html)，[Swim in Rising Water](http://www.cnblogs.com/grandyang/p/9017300.html)，[Koko Eating Bananas](https://www.cnblogs.com/grandyang/p/10807121.html)，[Nth Magical Number](https://www.cnblogs.com/grandyang/p/11148889.html)

### 第五类： 其他（通常 target 值不固定）

有些题目不属于上述的四类，但是还是需要用到二分搜索法，比如这道 Find Peak Element，求的是数组的局部峰值。由于是求的峰值，需要跟相邻的数字比较，那么 target 就不是一个固定的值，而且这道题的一定要注意的是 right 的初始化，一定要是 nums.size() - 1，这是由于算出了 mid 后，nums[mid] 要和 nums[mid+1] 比较，如果 right 初始化为 nums.size() 的话，mid+1 可能会越界，从而不能找到正确的值，同时 while 循环的终止条件必须是 left < right，不能有等号。

类似的还有一道 H-Index II，这道题的 target 也不是一个固定值，而是 len-mid，这就很意思了，跟上面的 nums[mid+1] 有异曲同工之妙，target 值都随着 mid 值的变化而变化，这里的 right 的初始化，一定要是 nums.size() - 1，而 while 循环的终止条件必须是 left <= right，这里又必须要有等号，是不是很头大 -.-!!!

其实仔细分析的话，可以发现其实这跟第四类还是比较相似，相似点是都很难 -.-!!!，第四类中虽然是用子函数来判断关系，但大部分时候 mid 也会作为一个参数带入子函数进行计算，这样实际上最终算出的值还是受 mid 的影响，但是 right 却可以初始化为数组长度，循环条件也可以不带等号，大家可以对比区别一下～

第五类应用实例：

[Find Peak Element](https://www.cnblogs.com/grandyang/p/4217175.html#4111463)

[H-Index II](http://www.cnblogs.com/grandyang/p/4782695.html)
