LeetCode141环形链表

方法一

```cpp
class Solution1 {
public:
	ListNode* detectCycle(ListNode* head) {
		std::set<ListNode*>node_set;
		while (head) {
			if (node_set.find(head) != node_set.end()) {
				return head;
			}
			node_set.insert(head);
			head = head->next;
		}
		return NULL;
	}
};
```

思路：

1. 遍历链表，将链表中节点对应的指针（地址），插入到set
2. 遍历链表的时，在插入链表节点之前，需要在set中查找，第一个在set中发现的节点，就是链表环的起点

方法二：

```cpp
class Solution {
public:
	ListNode* detectCycle(ListNode* head) {
		ListNode* fast = head;
		ListNode* slow = head;
		ListNode* meet = NULL;
		while (fast) {
			slow = slow->next;
			fast = fast->next;
			if (!fast) {
				break;
			}
			fast = fast->next;
			if (fast == slow) {
				meet = fast;
				break;
			}
		}
		if (meet == NULL) {
			return NULL;
		}
		while (head&&meet) {
			if (head == meet) {
				return head;
			}
			head = head->next;
			meet = meet->next;
		}
		return NULL;
	}
};
```

思路：

1. 等快指针追到慢指针的时候，为meet点
2. 从head和meet点出发，两者相遇的点，就是环的入口。



```cpp
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
	z.next = &e;

	Solution solve;
	
	ListNode* head = solve.detectCycle(&a);

	printf("%d\n", head->val);
}
```

