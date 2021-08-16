```cpp
class Solution {
public:
	vector<string> generateParenthesis(int n) {
		vector<string>result;
		generate("", n, n, result);
		return result;
	}
private:
	void generate(string item, int left, int right, vector<string>& result) {
		if (left == 0 && right == 0) {
			result.push_back(item);
			return;
		}
		if (left > 0) {
			generate(item+"(", left - 1, right, result);
		}
		if (left < right) {
			generate(item + ")", left, right - 1, result);
		}
	}
};
```

思路：

1. 括号必须成对存在，并且必须先有左括号，才能有右括号
2. 当左右括号的可用数量都为零的时候，将item添加到结果中
3. 当左括号存在可用数量的时候，向item中添加左括号。进入递归，当左括号可用数量小于右括号可用数量时，即前面有可配对的左括号，此时添加右括号，进入递归。

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
#include<set>
using namespace std;

class Solution {
public:
	vector<string> generateParenthesis(int n) {
		vector<string>result;
		generate("", n, n, result);
		return result;
	}
private:
	void generate(string item, int left, int right, vector<string>& result) {
		if (left == 0 && right == 0) {
			result.push_back(item);
			return;
		}
		if (left > 0) {
			generate(item+"(", left - 1, right, result);
		}
		if (left < right) {
			generate(item + ")", left, right - 1, result);
		}
	}
};

int main() {
	Solution s;
	vector<string>result = s.generateParenthesis(3);
	for (int i = 0; i < result.size(); i++) {
		printf("%s\n", result[i].c_str());
	}

	return 0;
}
```

