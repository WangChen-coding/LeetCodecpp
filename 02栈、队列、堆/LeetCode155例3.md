LeetCode155 最小栈

```cpp
class MinStack {
public:
	/** initialize your data structure here. */
	MinStack() {

	}

	void push(int val) {
		_data.push(val);
		if (_min.empty()) {
			
		}
		else {
			if (val > _min.top()) {
				val = _min.top();
			}
			
		}
        _min.push(val);
	}

	void pop() {
		_data.pop();
		_min.pop();
	}

	int top() {
		return _data.top();
	}

	int getMin() {
		return _min.top();
	}
private:
	stack<int> _data;
	stack<int> _min;
};
```

思路：

​	创建一个最小值栈，对应数据栈，每次操作数据栈，同步判断修改最小值栈。若加入的元素大于最小值栈顶的元素，则复制一份最小值栈顶元素添加到最小值栈顶，若添加元素小于最小值，则将该元素添加到最小值栈中。

若需弹出，则同步弹出两个栈。若需查看栈顶元素，则查看数据栈，查看 最小元素，查看最小栈。