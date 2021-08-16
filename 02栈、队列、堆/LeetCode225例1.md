LeetCode225用队列实现栈

```cpp
class MyStack {
public:
	/** Initialize your data structure here. */
	MyStack() {


	}
	/** Push element x onto stack. */
	void push(int x) {
		queue<int>temp_queue;
		temp_queue.push(x);
		while (!_data.empty()) {
			temp_queue.push(_data.front());
			_data.pop();
		}
		while (!temp_queue.empty()) {
			_data.push(temp_queue.front());
			temp_queue.pop();
		}
	}

	/** Removes the element on top of the stack and returns that element. */
	int pop() {
		int x = _data.front();
		_data.pop();
		return x;
	}

	/** Get the top element. */
	int top() {
		return _data.front();
	}

	/** Returns whether the stack is empty. */
	bool empty() {
		return _data.empty();
	}
private:
	queue<int>_data;
};
```

思路：

1. 将类中的队列数据储存方式改成与栈一样的形式
2. push操作的时候，创建一个临时队列，先将push元素添加到临时队列中，再将类中的模拟栈队列中的元素依次添加到临时队列中。
3. 将临时队列中的数依次弹出到类队列中



先将新元素加入临时队列，再将数据队列倒入临时队列中，再将临时队列倒入数据队列

