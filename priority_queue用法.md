##priority_queue用法

### priority_queue定义

头文件`#include<queue>`

语法`priority_queue<typename> name;`,typename可以是任何基本数据类型或容器。

### priority_queue如何访问堆顶元素

与队列不同，优先级队列没有front和back函数，只能通过top函数访问堆顶元素，时间复杂度为O(1)。

### 如何将元素压入priority_queue中

调用push函数，时间复杂度为O(logN)，其中N为当前优先级队列的元素个数。

### 如何将元素从priority_queue中弹出

调用pop函数，返回为空，可以令堆顶元素弹出，时间复杂度为O(logN)，N为当前优先级队列中元素个数。

### 如何判断priority_queue是否为空

调用empty函数，返回true为空，返回false非空。时间复杂度O(1)。

### 如何获得当前priority_queue中元素个数

调用size函数，返回优先级队列中元素个数，时间复杂度O(1)。

### 如何设置priority_queue基础数据类型的优先级

此处的基础类型是指int、double、char等可以直接使用的数据类型，默认的优先级设置为数值大的优先级高，对于char类型来说字典序大的优先级高。因此队首元素就是优先级队列中元素最大的那个。对于基本类型来说，下面的两个定义是等价的

```cpp
priority_queue<int>q;
priority_queue<int,vector<int>,less<int>>q;
```

第二种定义中，第二个参数`vector<int>`表示承载底层数据结构heap的容器，若数据类型为char或double，需要对应做出修改；第三个参数`less<int>`则是对第一个参数的比较类，less表示数字大的优先级越高，而`greater<int>`表示数字小的优先级高。若想让优先级队列将最小的放在堆顶，需要这样定义

```cpp
priority_queue<int,vector<int>,greater<int>>q;
```

### 如何设置priority_queue结构体类型的优先级

若想将结构体加入优先级队列，首先需要设置结构体中数据的优先级。需要重载小于号运算符。示例

```cpp
struct fruit{
    string name;
    int price;
    friend bool operator < (const fruit &f1,const fruit &f2){
        return f1.price<f2.price;
    }
};
```

需要加friend函数声明。return时也使用小于号返回，则此时fruit类型的优先级队列以价格最高的水果为最高优先级。接下来是写在结构体外的定义方法，同时将其用结构体包装起来。使用&和const提高效率，保证数据安全。

```cpp
struct cmp{
    bool operator()(const fruit &f1,const fruit &f2){
        return f1.price<f2.price;
    }
};
```

```cpp
priority_queue<fruit,vector<fruit>,cmp>q;//定义
```

