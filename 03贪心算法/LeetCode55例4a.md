```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        vector<int>index;
        for (int i = 0; i < nums.size(); i++) {
            index.push_back(i + nums[i]);
        }
        int jump = 0;
        int max_length = index[0];
        while (jump < index.size() && jump <= max_length) {
            if (max_length < index[jump]) {
                max_length = index[jump];
            }
            jump++;
        }
        if (jump == index.size()) {
            return true;
        }
        return false;
    }
};
```

