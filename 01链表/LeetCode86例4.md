LeetCode86 

```c++
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
class Solution {
public:
	ListNode* partition(ListNode* head, int x) {
		ListNode less_head(0);
		ListNode more_head(0);
		ListNode* less_ptr = &less_head;
		ListNode* more_ptr = &more_head;
		while (head) {
			if (head->val < x) {
				less_ptr->next = head;
				less_ptr = head;
			}
			else {
				more_ptr->next = head;
				more_ptr = head;
			}
			head = head->next;
		}
		less_ptr->next = more_head.next;
		more_ptr->next = NULL;
		return less_head.next;

	}
};
int main() {
	ListNode a;
	ListNode b;
	ListNode c;
	ListNode d;
	ListNode e;
	ListNode w;
	ListNode y;
	ListNode z;
	a.val = 10;
	b.val = 20;
	c.val = 30;
	d.val = 40;
	e.val = 50;
	w.val = 1;
	y.val = 2;
	z.val = 3;
	a.next = &b;
	b.next = &c;
	c.next = &d;
	d.next = &e;
	e.next = &w;
	w.next = &y;
	y.next = &z;
	z.next = NULL;
	ListNode* head = &a;
	while (head) {

		printf("%d\n", head->val);
		head = head->next;
	}

	Solution solve;
	std::cout << std::endl;
	head = solve.partition(&a, 25);
	while (head) {

		printf("%d\n", head->val);
		head = head->next;
	}

}

```

