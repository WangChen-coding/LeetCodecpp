```cpp
class Solution {
public:
	void flatten(TreeNode* root) {
		vector<TreeNode*>node_vec;
		preorder(root, node_vec);
		for (int i = 1; i < node_vec.size(); i++) {
			node_vec[i - 1]->left = NULL;
			node_vec[i - 1]->right = node_vec[i];
		}
	}
private:
	void preorder(TreeNode* root, vector<TreeNode*>&node_vec) {
		if (!root) {
			return;
		}
		node_vec.push_back(root);
		preorder(root->left, node_vec);
		preorder(root->right, node_vec);
	}
};
```

思路

将树的前序遍历节点依次添加到数组中，再将数组中各节点的左节点置为空，右节点指向下一个位置的节点。

自己出错的地方

1. 传到函数的数组没有标引用
2. 对于数组的最终遍历处理，范围的把握出错。数组下标的范围应该是0到size-1. 