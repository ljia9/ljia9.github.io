---
layout: post
title:  "BST traversals overview"
date:   2016-08-24 8:00:00
categories: [notes]
---

Because binary search trees connect a single data point to two data points rather than another single point like in the case of arrays or linked lists, there are different ways to traverse them, that is different orders. There are three general approaches to traversing a bst, and they are all easy to code thanks to recursion.

Firstly, pre-order traversal goes down the left spine of the bst after visiting the root and then picks up wherever there is a right node from the lowest level up to the top and down the right spine. This method is useful for directly copying the bst.

```python
# Example:
#      3
#    /   \
#   5     2
#  / \   / \
# 1   4 6   7
# 
# Output: 3 5 1 4 2 6 7
def preOrder(root):
    curr = root
    if curr is not None:
      print curr.data,
      preOrder(curr.left)
      preOrder(curr.right)
```

Next, in-order traversal goes from the bottom of the tree up, but looking at the left node then the parent node and lastly the right node. In such a way, the nodes are given in non-decreasing order. This can be used for validating the operator used to set up the bst.

```python
# Example:
#      3
#    /   \
#   5     2
#  / \   / \
# 1   4 6   7
# 
# Output: 1 5 4 3 6 2 7
def inOrder(root):
    curr = root
    if curr is not None:
      inOrder(curr.left)
      print curr.data
      inOrder(curr.right)
```

Finally, post-order traversal looks at the left node, then the right, and lastly the parent node. This traversal is used for deleting or freeing nodes from the bst.

```python
# Example:
#      3
#    /   \
#   5     2
#  / \   / \
# 1   4 6   7
# 
# Output: 1 4 5 6 7 2 3
def postOrder(root):
    curr = root
    if curr is not None:
      postOrder(curr.left)
      postOrder(curr.right)
      print curr.data
```

For all these algorithms, the time complexity is O(n) which is intuitive since we only visit each node once. When it comes to writing more complex methods of bsts, it is important to determine which kind of traversal fits the desired output of your method.
