地址：https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

# 题目：

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

# 理解：

给定一个二叉树的前序和中序遍历，求二叉树。

# 思路：

按照手动的思想，对于一个前序遍历，第一个元素一定是当前的根结点。找到该根结点在中序数组中的位置，则该元素之前的位置就是左子树，后面的位置是右子树，而左子树的元素一定在前序遍历的数组中连续出现。因此可以确定左子树和右子树的前序遍历子数组的位置。使用递归的思想求解。

# 实现：

1. C++

```cpp
class Solution {
public:
	TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
		return helper(preorder, 0, inorder, 0, inorder.size() - 1);
	}

	TreeNode* helper(vector<int>& preorder, int pl, vector<int>& inorder, int il, int ir) {
		if (pl >= preorder.size() || il > ir)
			return nullptr;
		TreeNode *root = new TreeNode(preorder[pl]);
		int partition = 0;
		for (int i = il; i <= ir; i++) {
			if (inorder[i] == preorder[pl]) {
				partition = i;
				break;
			}
		}
		root->left = helper(preorder, pl + 1, inorder, il, partition - 1);
		root->right = helper(preorder, pl + partition - il + 1, inorder, partition + 1, ir);
		return root;
	}
};
```

2. Go

```go
func buildTree(preorder []int, inorder []int) *TreeNode {
	return helper(preorder, inorder, 0, 0, len(preorder)-1)
}

func helper(preorder []int, inorder []int, preBeg int, inBeg int, inEnd int) *TreeNode {
	if preBeg >= len(preorder) || inBeg > inEnd {
		return nil
	}
	root := new(TreeNode)
	root.Val = preorder[preBeg]
	var partition int
	for i := inBeg; i <= inEnd; i++ {
		if inorder[i] == root.Val {
			partition = i
			break
		}
	}
	root.Left = helper(preorder, inorder, preBeg+1, inBeg, partition-1)
	root.Right = helper(preorder, inorder, preBeg+partition-inBeg+1, partition+1, inEnd)
	return root
}
```
