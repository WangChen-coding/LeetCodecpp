验证栈序列

```cpp
class Solution {
public:
	bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
		stack<int>S;
		int i = 0;
		for(auto j:pushed) {
			S.push(j);
			while (!S.empty() && popped[i] == S.top()) {
				S.pop();
				i++;
			}
		}
		if (!S.empty()) {
			return false;
		}
		return true;
	}
};
```

思路：

1. 将输入序列中的元素依次添加到栈中。添加的过程中同时判断栈顶的元素是否与弹出序列的首元素相同
2. 若相同，则弹出栈顶元素并将弹出序列的指针移动到下一个位置。若不同，则不断将输入序列的元素添加到栈中。
3. 最终若栈中元素没有弹空，说明输入序列不合法



遍历的过程中有可能出现，栈为空的情况，此刻若再取栈顶的值，会报错

本题的核心就是将栈顶的元素不断与输出序列中的元素对比。栈不为空的前提下，若相等，弹出栈顶元素，输出序列后移，直到不相等为止。若不相等，就不断添加输入序列到栈中。



本例中遍历输入序列的i和输出序列不能用相同的值。采用范围for遍历输入序列，整数i遍历输出序列