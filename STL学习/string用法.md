## string用法

### 定义string类型变量

头文件`#include<string>`

只需要在string后面跟变量名即可`string str;`

### 访问string中的内容

* 通过下标访问，从0到size-1都可访问
* 通过迭代器访问，定义迭代器`string::iterator it;`,通过解引用迭代器进行访问