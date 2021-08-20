## Vector用法

### vector定义

头文件`#include<vector>`

`vector<typename> name`typename可以是基本数据类型，也可以是STL标准容器，如果typename是STL容器时，>>之间最好加上空格，一些c11之前的编译器会将其视为移位操作，编译出错。

### vector容器内元素的访问

一般有两种访问方式

* 通过下标访问，直接`vector[index]`即可，index的范围是从0到size-1,访问这个范围之外的元素可能会运行出错。
* 通过迭代器访问。定义`vector<int>::iterator it;`,通过解引用`*it`访问vector中的元素

通过`vi[i]`与`*(vi.begin()+i)`访问是等价的

### vector迭代器的加减法

可以使用++ --运算符，但是只有vector和string才可以直接与整数相加减

### 向vector后面添加一个元素

push_back()函数，可以向vector后添加一个元素，时间复杂度为O(1)

### 删除vector的尾元素

调用pop_back()函数可以删除vector的尾元素，时间复杂度O(1)

### 获取vector元素个数

调用size函数，返回vector元素个数，返回类型为unsigned类型，时间复杂度O(1)

### 清除vector所有元素

调用clear函数，清空vector函数中所有元素，时间复杂度O(N)

### 在vector指定位置插入一个元素

调用insert(it,x),在迭代器it处插入元素x，其后元素顺延，时间复杂度O(N)

### 删除vector指定位置的元素

* 单个元素erase(it)，删除迭代器it处的元素
* erase(first,last)，删除[first,last）内的所有元素。删除所有元素erase（vi.begin(),vi.end())