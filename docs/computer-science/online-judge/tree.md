# Tree

## Maximum Depth of Binary Tree

[LeetCode 104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

> Given the root of a binary tree, return its maximum depth.

### Breadth-first Search

```py
class Solution:
  def maxDepth(self, root: TreeNode) -> int:
    queue = deque([root])
    visited = set([root])
    result = 0
    while queue:
      for _ in range(len(queue)):
        node = queue.popleft()
        for child in (node.left, node.right):
          if child in visited:
            continue
          visited.add(child)
          queue.append(child)
      result += 1
    return result
```

### Depth-first Search

```py
class Solution:
  def maxDepth(self, root: TreeNode) -> int:
    if not root:
      return 0
    left = self.maxDepth(root.left)
    right = self.maxDepth(root.right)
    return max(right, left) + 1
```

## Same Tree

[LeetCode 100](https://leetcode.com/problems/same-tree/)

> Given the roots of two binary trees p and q, write a function to check if they are the same or not.

```py
class Solution:
  def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
    if not p and not q:
      return True
    if not p or not q:
      return False
    return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

## Invert Binary Tree

[LeetCode 226](https://leetcode.com/problems/invert-binary-tree/)

```py
class Solution:
  def invertTree(self, root: TreeNode) -> TreeNode:
    if not root:
      return
    root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
    return root
```

## Binary Tree Level Order Traversal

[LeetCode 102](https://leetcode.com/problems/binary-tree-level-order-traversal/)

> Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

```py
class Solution:
  def levelOrder(self, root: TreeNode) -> List[List[int]]:
    if not root:
      return []
    queue = deque([root])
    result = []
    while queue:
      result.append([node.val for node in queue])
      for _ in range(len(queue)):
        node = queue.popleft()
        for child in (node.left, node.right):
          if not child:
            continue
          queue.append(child)
    return result
```

## Serialize and Deserialize Binary Tree

[LeetCode 297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

```py
class Codec:
  def serialize(self, root):
    if not root:
      return ''
    queue = deque([root])
    result = []

    while queue:
      node = queue.popleft()
      if not node:
        result.append('null')
        continue
      queue.append(node.left)
      queue.append(node.right)
      result.append(str(node.val))

    return ' '.join(result)

  def deserialize(self, data):
    if not data:
      return
    nodes = data.split()
    root = TreeNode(int(nodes[0]))
    queue = deque([root])
    index = 1
    while queue:
      node = queue.popleft()
      if nodes[index] != 'null':
        node.left = TreeNode(int(nodes[index]))
        queue.append(node.left)
      index += 1
      if nodes[index] != 'null':
        node.right = TreeNode(int(nodes[index]))
        queue.append(node.right)
      index += 1
    return root
```

## Subtree of Another Tree

[LeetCode 572](https://leetcode.com/problems/subtree-of-another-tree/)

> Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

```py
class Solution:
  def isSubtree(self, root: TreeNode, subRoot: TreeNode) -> bool:
    def isSameTree(root, subRoot):
      if not root and not subRoot:
        return True
      if not root or not subRoot:
        return False
      return root.val == subRoot.val and isSameTree(root.left, subRoot.left) and isSameTree(root.right, subRoot.right)

    queue = deque([root])
    while queue:
      node = queue.popleft()
      if isSameTree(node, subRoot):
        return True
      for child in (node.left, node.right):
        if not child:
          continue
        queue.append(child)
    return False
```

## Construct Binary Tree from Preorder and Inorder Traversal

[LeetCode 105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

> Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

- Preorder traversal: `[root, ...left_children, ...right_children]`
- Inorder traversal: `[...left_children, root, ...right_children]`
- Postorder traversal: `[...left_children, ...right_children, root]`

```py
class Solution:
  def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
    def build(pre_left, pre_right, in_left, in_right):
      if pre_left > pre_right:
        return

      pre_root = pre_left
      in_root = node_map[preorder[pre_root]]
      left_size = in_root - in_left
      node = TreeNode(preorder[pre_root])

      node.left = build(pre_left + 1, pre_left + left_size, in_left, in_root - 1)
      node.right = build(pre_left + left_size + 1, pre_right, in_root + 1, in_right)
      return node

    node_map = { node: index for index, node in enumerate(inorder) }
    return build(0, len(preorder) - 1, 0, len(inorder) - 1)
```

## Construct Binary Tree from Inorder and Postorder Traversal

[LeetCode 106](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

- Preorder traversal: `[root, ...left_children, ...right_children]`
- Inorder traversal: `[...left_children, root, ...right_children]`
- Postorder traversal: `[...left_children, ...right_children, root]`

```py
class Solution:
  def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
    def build(in_left, in_right, post_left, post_right):
      if in_left > in_right:
        return
      post_root = post_right
      in_root = node_map[postorder[post_right]]
      left_size = in_root - in_left

      root = TreeNode(postorder[post_right])
      root.left = build(in_left, in_root - 1, post_left, post_left + left_size - 1)
      root.right = build(in_root + 1, in_right, post_left + left_size, post_right - 1)
      return root

    node_map = { element: index for index, element in enumerate(inorder)}
    return build(0, len(inorder) - 1, 0, len(inorder) - 1)
```

## Validate Binary Search Tree

[LeetCode 98](https://leetcode.com/problems/validate-binary-search-tree/)

> Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

### Recursion

```py
class Solution:
  def isValidBST(self, root: TreeNode) -> bool:
    def validate(root, lo, hi):
      if not root:
        return True
      if root.val > hi or root.val < lo:
        return False
      left = validate(root.left, lo, root.val)
      right = validate(root.right, root.val, hi)
      return left and right

    return validate(root, float('-inf'), float('inf'))
```

### Inorder Traversal

```py
class Solution:
  def __init__(self):
    self.pre = float('-inf')

  def isValidBST(self, root: TreeNode) -> bool:
    if not root:
      return True
    if not self.isValidBST(root.left) or self.pre >= root.val:
      return False
    self.pre = root.val
    return self.isValidBST(root.right)
```

## Recover Binary Search Tree

[LeetCode 99](https://leetcode.com/problems/recover-binary-search-tree/)

> You are given the `root` of a binary search tree (BST), where exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

Let's assume that the inorder traversal of the binary search tree is `[1, 6, 3, 4, 5, 2, 7]`, then the node `2` and `6` should be swapped. To find these nodes, run an inorder traversal and record the previous node.

- If `pre.val > node.val`, then `pre` is the first node.
- If the first node exists and `pre.val > node.val`, then `node` is the second node.
- Swap the value of the first node and second node.

```py
class Solution:
  def recoverTree(self, root: TreeNode) -> None:
    self.pre = TreeNode(float('-inf'))
    def inorder(node):
      if not node:
        return
      inorder(node.left)

      if node.val < self.pre.val:
        swap[1] = node
        if not swap[0]:
          swap[0] = self.pre
        else:
          return
      self.pre = node

      inorder(node.right)

    swap = [None, None]
    inorder(root)
    swap[0].val, swap[1].val = swap[1].val, swap[0].val
    return root
```

## Lowest Common Ancestor of a Binary Tree

[LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

> Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

```py
class Solution:
  def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
    pass
```

## Lowest Common Ancestor of a Binary Search Tree

[LeetCode 235](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

> Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

```py
class Solution:
  def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
    pass
```