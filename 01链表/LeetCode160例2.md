LeetCode160 相交链表

方法一：使用哈希表

```cpp
class Solution {
public:
	ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
		std::set<ListNode*> NodeSet;
		while (headA) {
			NodeSet.insert(headA);
			headA = headA->next;
		}
		while (headB) {
			if (NodeSet.find(headB) != NodeSet.end()) {
				return headB;
			}
			headB = headB->next;
		}
		return NULL;
	}
};
```

思路：

1. 将链表A中的每个节点地址都存入到哈希表中
2. 遍历链表B，将链表B中的每个节点都在哈希表中搜索一次，只有返回的迭代器不是尾后迭代器的时候，即找到第一个相交节点。
3. 若遍历完链表B后，还没有找到，则返回空

方法二：获取链表长度，作差后，同时向后移动。

```c++
int get_list_length(ListNode* head) {
	int len = 0;
	while (head) {
		head = head->next;
		len++;
	}
	return len;
}
ListNode* forward_long_list(int long_len, int short_len, ListNode* head) {
	int delta = long_len - short_len;
	while (head && delta--) {
		head = head->next;
	}
	return head;
}
class Solution1 {
public:
	ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
		int List_A_len = get_list_length(headA);
		int List_B_len = get_list_length(headB);
		if (List_A_len > List_B_len) {
			headA = forward_long_list(List_A_len, List_B_len, headA);
		}
		else {
			headB = forward_long_list(List_B_len, List_A_len, headB);
		}
		while (headA && headB) {
			if (headA == headB) {
				return headA;
			}
			headA = headA->next;
			headB = headB->next;
		}
		return NULL;
	}
};
```

思路：

1. 遍历两个链表，获得他们的长度
2. 将较长链表的指针移动到较短链表对齐的位置
3. 同时向后移动，判断两指针指向位置是否相同，相同则找到相交节点。

```cpp
#include <stdio.h>
#include<iostream>
#include<set>
struct ListNode {
	int val;
	ListNode* next;
	ListNode() : val(0), next(nullptr) {}
	ListNode(int x) : val(x), next(nullptr) {}
	ListNode(int x, ListNode* next) : val(x), next(next) {}

};
int get_list_length(ListNode* head) {
	int len = 0;
	while (head) {
		head = head->next;
		len++;
	}
	return len;
}
ListNode* forward_long_list(int long_len, int short_len, ListNode* head) {
	int delta = long_len - short_len;
	while (head && delta--) {
		head = head->next;
	}
	return head;
}
class Solution1 {
public:
	ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
		int List_A_len = get_list_length(headA);
		int List_B_len = get_list_length(headB);
		if (List_A_len > List_B_len) {
			headA = forward_long_list(List_A_len, List_B_len, headA);
		}
		else {
			headB = forward_long_list(List_B_len, List_A_len, headB);
		}
		while (headA && headB) {
			if (headA == headB) {
				return headA;
			}
			headA = headA->next;
			headB = headB->next;
		}
		return NULL;
	}
};
class Solution {
public:
	ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
		std::set<ListNode*> NodeSet;
		while (headA) {
			NodeSet.insert(headA);
			headA = headA->next;
		}
		while (headB) {
			if (NodeSet.find(headB) != NodeSet.end()) {
				return headB;
			}
			headB = headB->next;
		}
		return NULL;
	}
};
int main() {
	ListNode a;
	ListNode b;
	ListNode c;
	ListNode d;
	ListNode e;
	a.val = 10;
	b.val = 20;
	c.val = 30;
	d.val = 40;
	e.val = 50;
	a.next = &b;
	b.next = &c;
	c.next = &d;
	d.next = &e;
	e.next = NULL;

	ListNode w;
	ListNode y;
	ListNode z;
	w.val = 1;
	y.val = 2;
	z.val = 3;
	w.next = &y;
	y.next = &z;
	z.next = &c;

	Solution solve;
	ListNode* head = &a;
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
	std::cout << std::endl;
	 head = &w;
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
	std::cout << std::endl;
	head=solve.getIntersectionNode(&a, &w);
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
```

