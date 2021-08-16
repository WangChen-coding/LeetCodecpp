LeetCode45 跳跃游戏2

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        if (nums.size() < 2) {
            return 0;
        }
        //当前可达到的最远位置
        int current_max_index = nums[0];
        //各个位置可以达到的最远位置
        int pre_max_max_index = nums[0];
        int jump_min = 1;
        for (int i = 1; i < nums.size(); i++) {
            //如果当前位置无法再向前遍历，则增加跳跃次数，更新当前可到达的最远位置
            if (i > current_max_index) {
                jump_min++;
                current_max_index = pre_max_max_index;

            }
            //遍历过程中，比较之前记录的最远位置和当前位置能挑到的最远位置
            //若当前位置的值+当前位置的下标较大，便更新最远位置
            if (pre_max_max_index < nums[i] + i) {
                pre_max_max_index = nums[i] + i;
            }
        }
        return jump_min;
    }
};
```

思路：

​	要想跳跃的次数最少，那么就需要保证每次跳跃达到的效果是最大的，即在一定区间内，跳跃的步长最大。

1. 设置current_max_index为当前可达到的最远位置，初始值就是数组的第一个数。
2. 设置pre_max_max_index为遍历各位置过程中，各位置能达到的最远位置
3. jump_min为最少跳跃次数
4. 利用i遍历数组，如果i超过current_max_index，说明当前遍历超过当前位置能跳到的最远位置，所以必须再跳一次，同时将当前可跳到的最远位置更新为在遍历过程中不断判断更新的pre_max_max_index.
5. 遍历过程中，如果当前位置的值加上当前位置的下标，即该位置能跳的最远位置。与之前记录的位置比较，若当前可以跳的更远，则更新pre_max_max_index