LeetCode113

```cpp
class Solution {
public:
	vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
		vector<vector<int>>result;
		vector<int>path;
		int path_value = 0;
		preorder(root, path_value, targetSum, path, result);
		return result;
	}
	void preorder(TreeNode* node, int& path_value, int sum, vector<int>& path, vector<vector<int>>& result) {
		if (node==nullptr) {
			return;
		}
		path_value += node->val;
		path.push_back(node->val);
		if (!node->left && !node->right && path_value == sum) {
			result.push_back(path);
		}
		preorder(node->left, path_value, sum, path, result);
		preorder(node->right, path_value, sum, path, result);
		path_value -= node->val;
		path.pop_back();
	}
};
```

思路：

1. 从根节点深度遍历二叉树，先序遍历时，将该节点的值储存在path栈中，使用path_value累加节点值。
2. 当遍历至叶节点的时候，即左右孩子都为空，检查path_value是否为sum，若相等，将path栈中的结果进入到result中。
3. 在后序遍历时，将该节点弹出，并从path_value中减去该节点值















完整代码

```c++
#include<iostream>
#include<vector>
using namespace std;

struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode() : val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
	
};

class Solution {
public:
	vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
		vector<vector<int>>result;
		vector<int>path;
		int path_value = 0;
		preorder(root, path_value, targetSum, path, result);
		return result;
	}
	void preorder(TreeNode* node, int& path_value, int sum, vector<int>& path, vector<vector<int>>& result) {
		if (node==nullptr) {
			return;
		}
		path_value += node->val;
		path.push_back(node->val);
		if (!node->left && !node->right && path_value == sum) {
			result.push_back(path);
		}
		preorder(node->left, path_value, sum, path, result);
		preorder(node->right, path_value, sum, path, result);
		path_value -= node->val;
		path.pop_back();
	}
};
int main() {
	TreeNode a(5);
	TreeNode b(4);
	TreeNode c(8);
	TreeNode d(11);
	TreeNode e(13);
	TreeNode f(4);
	TreeNode g(7);
	TreeNode h(2);
	TreeNode x(5);
	TreeNode y(1);
	a.left = &b;
	a.right = &c;
	b.left = &d;
	d.left = &g;
	d.right = &h;
	c.left = &e;
	c.right = &f;
	f.left = &x;
	f.right = &y;
	Solution solve;
	vector<vector<int>>result = solve.pathSum(&a, -2);
	for (int i = 0; i < result.size(); i++) {
		for (int j = 0; j < result[i].size(); j++) {
			printf("[%d]", result[i][j]);
		}
		cout << endl;
	}
	return 0;
}
```

