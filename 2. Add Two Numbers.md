地址：https://leetcode.com/problems/add-two-numbers/

# 题目：

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

# 理解：

给两个非空链表，求和。头结点是个位数。依次相加即可。

# 思路：

按照手动的思想，对于一个前序遍历，第一个元素一定是当前的根结点。找到该根结点在中序数组中的位置，则该元素之前的位置就是左子树，后面的位置是右子树，而左子树的元素一定在前序遍历的数组中连续出现。因此可以确定左子树和右子树的前序遍历子数组的位置。使用递归的思想求解。

# 实现：

1. C++

```cpp
class Solution {
public:
	ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		int carry = 0;
		ListNode *pHead = new ListNode(0), *p=pHead;
		while (l1 || l2) {
			int tmp = carry;
			if (l1) {
				tmp += l1->val;
				l1 = l1->next;
			}
			if (l2) {
				tmp += l2->val;
				l2 = l2->next;
			}
			p->next = new ListNode(tmp % 10);
			carry = tmp / 10;
			p = p->next;
		}
		if (carry)
			p->next = new ListNode(1);
		return pHead->next;
	}
};
```

2. Go

```go
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	carry := 0
	newHead := new(ListNode)
	p:=newHead
	for l1 != nil || l2 != nil {
		if l1 != nil {
			carry += l1.Val
			l1 = l1.Next
		}
		if l2 != nil {
			carry += l2.Val
			l2 = l2.Next
		}
		p.Next = new(ListNode)
		p=p.Next
		p.Val = carry % 10
		carry /= 10
	}
    if carry>0 {
        p.Next = new(ListNode)
        p.Next.Val = 1
    }
	return newHead.Next
}
```