方法一：顺序合并

```c++
class Solution {
public:
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
		ListNode temp_head(0);
		ListNode* pre = &temp_head;
		while (l1 && l2) {
			if (l1->val < l2->val) {
				pre->next = l1;
				l1 = l1->next;
			}
			else {
				pre->next = l2;
				l2 = l2->next;
			}
			pre = pre->next;
		}
		if (l1) {
			pre->next = l1;
		}
		if (l2) {
			pre->next = l2;
		}
		return temp_head.next;
	}
	ListNode* mergeKLists(vector<ListNode*>& lists) {
		ListNode* head = NULL;
		for (size_t i = 0; i < lists.size(); i++) {
			head = mergeTwoLists(head, lists[i]);
		}
		return head;
	}
};
```

方法二：使用stl的sort方法

```c++
bool cmp(ListNode* l1, ListNode* l2) {
	return l1->val < l2->val;
}
class Solution {
public:

	ListNode* mergeKLists(vector<ListNode*>& lists) {
		vector<ListNode*>node_vec;
		for (size_t i = 0; i < lists.size(); i++) {
			ListNode* head = lists[i];
			while (head) {
				node_vec.push_back(head);
				head = head->next;
			}
		}
		if (node_vec.size() == 0) {
			return NULL;
		}
		sort(node_vec.begin(), node_vec.end(), cmp);
		for (int i = 1; i < node_vec.size(); i++) {
			node_vec[i - 1]->next = node_vec[i];
		}
		node_vec[node_vec.size() - 1]->next = NULL;
		return node_vec[0];
	}
};
```

方法三：分治

```cpp
class Solution {
public:
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
		ListNode temp_head(0);
		ListNode* pre = &temp_head;
		while (l1 && l2) {
			if (l1->val < l2->val) {
				pre->next = l1;
				l1 = l1->next;
			}
			else {
				pre->next = l2;
				l2 = l2->next;
			}
			pre = pre->next;
		}
		if (l1) {
			pre->next = l1;
		}
		if (l2) {
			pre->next = l2;
		}
		return temp_head.next;
	}
	ListNode* mergeKLists(vector<ListNode*>& lists) {
		if (lists.size() == 0) {
			return NULL;
		}
		if (lists.size() == 1) {
			return lists[0];
		}
		if (lists.size() == 2) {
			return mergeTwoLists(lists[0], lists[1]);
		}
		int mid = lists.size() / 2;
		vector<ListNode*>sub1_lists;
		vector<ListNode*>sub2_lists;
		for (int i = 0; i < mid; i++) {
			sub1_lists.push_back(lists[i]);
		}
		for (int i = mid; i < lists.size(); i++) {
			sub2_lists.push_back(lists[i]);
		}
		ListNode* L1 = mergeKLists(sub1_lists);
		ListNode* L2 = mergeKLists(sub2_lists);
		return mergeTwoLists(L1, L2);
	}
};
```

思路：

1. 找到递归基，序列为空，直接返回空，序列为1，返回头指针。有两个序列则两个序列merge
2. 大于两个序列，分治。从中间分开，存到vector中。
3. 将上面分开的序列，递归调用k合并函数
4. 最终返回的两个头节点，merge。