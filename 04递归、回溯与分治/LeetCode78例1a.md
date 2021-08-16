LeetCode78

方法一 回溯法

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>>result;
        vector<int>item;
        result.push_back(item);
        generate(0, nums, item, result);
        return result;
    }
private:
    void generate(int i, vector<int>& nums, vector<int>& item, vector<vector<int>>& result) {
        if (i >= nums.size()) {
            return;
        }
        item.push_back(nums[i]);
        result.push_back(item);
        generate(i + 1, nums, item, result);
        item.pop_back();
        generate(i + 1, nums, item, result);
    }
};
```

思路：

1. 到达一个节点后，先判断i是否超出数组的范围
2. 若在范围内，将这个位置的值加入到item中，再添加到结果集中。
3. 此刻有两条路可以选择，是否将该值保留在后续的结果中。
4. 不断深入到尽头，然后逐步回退，选择另一条路。





方法二：位运算

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>>result;
        int all_set = 1 << nums.size();
        for (int i = 0; i < all_set; i++) {
            vector<int> item;
            for (int j = 0; j < nums.size(); j++) {
                if (i & (1 << j)) {
                    item.push_back(nums[j]);
                }
            }
            result.push_back(item);
        }
        return result;
    }
};
```

思路：

1. 用二进制数的01表示子集中该元素是否存在，i的二进制数表示当前子集对应位置的元素是否存在。
2. 用i和高位到低位的数依次比较，若存在，就把nums这个位置上对应的值push进去，若不为0，则跳过。
3. 将遍历后，添加完对应元素的item，添加到结果中