LeetCode376摆动序列

```c++
class Solution {
public:
	int wiggleMaxLength(vector<int>& nums) {
		if (nums.size() < 2) {
			return nums.size();
		}
		static const int BEGIN = 0;
		static const int UP = 1;
		static const int DOWN = 2;
		int STATE = BEGIN;
		int max_length = 1;
		for (int i = 1; i < nums.size(); i++) {
			switch (STATE)
			{
			case BEGIN:
				if (nums[i - 1] < nums[i]) {
					max_length++;
					STATE = UP;
				}
				else if (nums[i - 1] > nums[i]) {
					max_length++;
					STATE = DOWN;
				}
				break;
			case UP:
				if (nums[i - 1] > nums[i]) {
					STATE = DOWN;
					max_length++;
				}
				break;
			case DOWN:
				if (nums[i - 1] < nums[i]) {
					STATE = UP;
					max_length++;
				}
				break;
			default:
				break;
			}
		}
		return max_length;
	}
};
```

使用状态转换机，switch case 进行处理