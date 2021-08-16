```cpp
class Solution {
public:
	vector<vector<int>> subsetsWithDup(vector<int>& nums) {
		vector<int>item;
		vector<vector<int>>result;
		set<vector<int>>res_set;
		int i = 0;
		sort(nums.begin(), nums.end());
		result.push_back(item);
		generate(i, nums, result, item, res_set);
		return result;
	}
private:
	void generate(int i, vector<int>& nums, vector<vector<int>>& result, vector<int>& item, set<vector<int>>& res_set) {
		if (i == nums.size()) {
			return;
		}
		item.push_back(nums[i]);
		if (res_set.find(item) == res_set.end()) {
			result.push_back(item);
			res_set.insert(item);
		}
		generate(i + 1, nums, result, item, res_set);
		item.pop_back();
		generate(i + 1, nums, result, item, res_set);
	}
};
```

思路：

1. 本题的条件中包含了重复的元素，而且顺序不定，所以有可能不同位置取到的子集是重复的，所以第一步先将数组排序。
2. 使用set去重，将添加新值的item在set中查询，是否存在，若不存在，则将item放到结果中，同时也放入set中，以便下一轮的查重。