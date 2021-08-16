例1-a：链表逆序 lt206 easy

[LeetCode206](https://leetcode-cn.com/problems/reverse-linked-list/)

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
	 ListNode* reverseList(ListNode* head) {
		 ListNode* newhead = nullptr;
		 while (head) {
			 ListNode* next = head->next;
			 head->next = newhead;
			 newhead = head;
			 head = next;
		 }
		 return newhead;
	 }
 };
 class Solution1 {
 public:
	 ListNode* reverseList(ListNode* head) {
		 ListNode* newhead = nullptr;
		 while (head) {
			 ListNode* temp = head;
			 head = head->next;
			 temp->next = newhead;
			 newhead = temp;
		 }
		 return newhead;
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
	Solution1 solve;
	ListNode* head = &a;
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}
	std::cout << std::endl;
	head = solve.reverseList(&a);
	while (head) {
		printf("%d\n", head->val);
		head = head->next;
	}

}
```

方法一：

1. 备份原始链表的头结点，将head->next赋值给next节点
2. 将head节点的指针域指向新链表的头结点
3. 将head节点变为newhead节点
4. 将next节点变为head节点

方法二：

1. 创建临时节点temp保存head节点
2. 将head节点后移到下一个位置
3. temp节点的指针域指向newhead
4. temp节点变为新的headnew节点