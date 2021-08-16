```cpp
#include <stdio.h>
#include<iostream>
#include<set>
#include<map>
#include<vector>
using namespace std;
struct ListNode {
	int val;
	ListNode* next;
	ListNode() : val(0), next(nullptr) {}
	ListNode(int x) : val(x), next(nullptr) {}
	ListNode(int x, ListNode* next) : val(x), next(next) {}
	
};
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
};



int main() {
	ListNode a(10);
	ListNode b(20);
	ListNode c(30);
	ListNode d(40);
	ListNode e(15);
	ListNode w(30);
	ListNode y(40);
	ListNode z(50);

	a.next = &b;
	b.next = &c;
	c.next = &d;
	d.next = NULL;
	e.next = &w;
	w.next = &y;
	y.next = &z;
	z.next = NULL;
	ListNode* head = &a;
	while (head) {
		printf("val=%d\n", head->val);

		head = head->next;
	}
	cout << endl;
	head = &e;
	while (head) {
		printf("val=%d\n", head->val);

		head = head->next;
	}
	cout << endl;
	Solution solve;
	head = solve.mergeTwoLists(&a, &e);
	while (head) {
		printf("val=%d\n", head->val);

		head = head->next;
	}
}
```

思路：

1. 创建一个临时节点和指向该节点的指针，分别有一个节点指针指向链表各自的头节点
2. 比较两个节点指针所指节点值的大小，谁指向的值小，将该值接到合并链表上，同时临时节点指针和该链表指针都后移
3. 若一个链表遍历结束，直接将另一个链表的剩余部分接在总链表后面
4. 返回临时节点的后一个节点，即两个链表最小的那一个