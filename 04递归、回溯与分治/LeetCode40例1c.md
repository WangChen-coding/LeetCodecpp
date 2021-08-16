```cpp
class Solution {
public:
	vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
		vector<int>item;
		vector<vector<int>>result;
		set<vector<int>>res_set;
		vector<int>nums;
		for (auto x : candidates) {
			if (x <= target) {
				nums.push_back(x);
			}
		}
		int i = 0;
		sort(nums.begin(), nums.end());
		generate(i, nums, result, item, res_set, target, 0);
		return result;
	}
private:
	void generate(int i, vector<int>& nums, vector<vector<int>>& result, vector<int>& item, set<vector<int>>& res_set, int target, int sum) {
		if (i >= nums.size() || sum > target) {
			return;
		}
		sum += nums[i];
		item.push_back(nums[i]);
		if (sum == target && res_set.find(item) == res_set.end()) {
			result.push_back(item);
			res_set.insert(item);
		}
		generate(i + 1, nums, result, item, res_set, target, sum);
		sum -= nums[i];
		item.pop_back();
		generate(i + 1, nums, result, item, res_set, target, sum);
	}
};
```

思路：

本题最重要的就是剪枝，若item中的数大于target的时候，就返回，不再继续深入