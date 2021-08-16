LeetCode232用栈实现队列

```cpp
class MyQueue {
public:
	/** Initialize your data structure here. */
	MyQueue() {

	}

	/** Push element x to the back of queue. */
	void push(int x) {
		stack<int>temp_stack;
		while (!_data.empty()) {
			temp_stack.push(_data.top());
			_data.pop();
		}
		temp_stack.push(x);
		while (!temp_stack.empty()) {
			_data.push(temp_stack.top());
			temp_stack.pop();
		}
	}

	/** Removes the element from in front of queue and returns that element. */
	int pop() {
		int x = _data.top();
		_data.pop();
		return x;
	}

	/** Get the front element. */
	int peek() {
		return _data.top();
	}

	/** Returns whether the queue is empty. */
	bool empty() {
		return _data.empty();
	}
private:
	stack<int>_data;
};
```

思路：

1. 构造一个栈，push中创建一个临时栈。
2. 添加元素的时候，先将数据栈中的元素倒入临时栈中，再将数据添加到临时栈中，再将临时栈倒入数据栈中。