## map用法

### map定义

头文件`#include<map>`

定义`map<typename1,typename2> mp;`第一个是键的值key，第二个是键映射后的值value

底层使用红黑树实现，map会以键从小到大的顺序自动排序且不允许重复

### 访问map中的元素

* 通过下标访问，通过mp[key],通过key可以获得对应的value值
* 通过迭代器进行访问，定义迭代器`map<typename1,typename2>::iterator it;`通过`it->first`访问键，`it->second`访问值

### 查找map中键为key的迭代器

调用find(key)，返回键为key的映射的迭代器，时间复杂度为O(logN)，N为map中映射的个数

### 删除map中的元素

* erase(it),通过迭代器it删除单个元素，时间复杂度为O(1)
* erase(key)删除键为key的映射，时间复杂度O(logN)
* 删除区间erase(first,last),删除迭代器[first,last)区间的映射

### 获取map中映射对数

调用size函数，获得映射对数，时间复杂度O(1)

### 清除map中所有映射

clear()清空map中所有元素，复杂度为O(N)

