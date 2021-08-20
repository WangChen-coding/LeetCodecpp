## set用法

### set定义

头文件`#include<set>`

`set<typename> name;`定义一个内部自动有序且不包含重复元素的容器，底层使用红黑树实现

### set内元素的访问

只能通过迭代器访问 通过解引用迭代器获得容器中的元素

### set中插入元素

调用insert(x)可以将x插入到set容器中，并且自动去重排序，时间复杂度为O(logN)

### 查找set中的某个元素

调用find(value)返回set中对应值为value的迭代器，时间复杂度为O(logN)

### 删除set中的元素

* 删除单个元素erase(it),删除it迭代器位置的元素，时间复杂度为O(1)，可以结合find函数使用
* 删除单个元素erase(value),删除set中值为value的元素，时间复杂度为O(logN)
* 删除一个区间内的所有元素，erase(first,last)删除[first,last）位置的元素

### 获取set中元素个数

调用size函数，返回set内元素个数，时间复杂度O(1)

### 清除set中所有元素

调用clear函数，清空set中所有元素，时间复杂度O(N)

### 不需要去重的集合应该使用什么

multiset

### 不需要排序，只需要去重的集合应该使用什么

unordered_set，以散列代替set内部的红黑树



