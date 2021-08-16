LeetCode215数组中第k大元素

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
		priority_queue<int, vector<int>, greater<int>> Q;
		for (int i = 0; i < nums.size(); i++) {
			if (Q.size() < k) {
				Q.push(nums[i]);
			}
			else if (nums[i] > Q.top()) {
				Q.pop();
				Q.push(nums[i]);
			}
		}
		return Q.top();
    }
};
```

