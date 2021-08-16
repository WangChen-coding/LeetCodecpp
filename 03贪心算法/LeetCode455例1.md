LeetCode455

```c++
class Solution {
public:
	/// <summary>
	/// 分发糖果
	/// </summary>
	/// <param name="g">孩子的需求因子</param>
	/// <param name="s">糖果的大小</param>
	/// <returns></returns>
	int findContentChildren(vector<int>& g, vector<int>& s) {
		sort(s.begin(), s.end());
		sort(g.begin(), g.end());
		int child = 0;
		int cookie = 0;
		while (child < g.size() && cookie < s.size()) {
			//糖果大于需求，
			if (g[child] < s[cookie]) {
				child++;
			}
			cookie++;
		}
		return child;
	}
};
```

思路：

1. 首先将两个序列排好顺序
2. 然后依次比较两个序列的元素。如果当前的糖果满足当前孩子的需求，则将这个糖果分配给这个孩子，如果当前的糖果不满足需求，则将取更大的糖果看是否满足孩子的需求。最终，当没有更多糖果或者更多孩子时，循环退出。（如果糖果数量和孩子需求数量一致的话，因为糖果不一定满足孩子的需求，所以当糖果数量不够时，循环就可以退出）