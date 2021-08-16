给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。



```c++
#include <stdio.h>
#include<iostream>
struct ListNode {
	int val;
	ListNode* next;
	ListNode() : val(0), next(nullptr) {}
	ListNode(int x) : val(x), next(nullptr) {}
	ListNode(int x, ListNode* next) : val(x), next(next) {}

};
class Solution {
public:
	ListNode* reverseBetween(ListNode* head, int left, int right) {
		int change_len = right - left + 1;
		ListNode* pre_head = nullptr;
		ListNode* result = head;
		while (head && --left) {
			pre_head = head;
			head=head->next;
		}
		ListNode* modify_list_tail = head;
		ListNode* newhead = nullptr;
		while (head && change_len--) {
			ListNode* next = head->next;
			head->next = newhead;
			newhead = head;
			head = next;
		}
		modify_list_tail->next = head;
		if (pre_head) {
			pre_head->next = newhead;
		}
		else {
			result = newhead;
		}
		return result;
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
	Solution solve;
	ListNode* head = &a;
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
	std::cout << std::endl;
	head = &a;
	head = solve.reverseBetween(head, 4, 4);
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
}

```

解题思路：

1. 首先找到需要反转的链表头结点（反转后，就是反转部分的尾结点modify_list_tail）与其前驱结点prehead。
2. 从head开始，有right-left+1个节点需要反转。
3. 反转后，将完成反转的序列与之前的链表连接。前驱节点的指针域指向newhead（反转序列的头结点），反转序列的尾节点指向后继节点。

注意：需要考虑left为1，即从原始链表的头结点就开始反转，所以没有前驱节点，返回后的链表头结点就是newhead。

链表遍历的过程，同时需要考虑是否超出当前的链表范围，所以使用while(head&&终止循环条件)来确保程序安全