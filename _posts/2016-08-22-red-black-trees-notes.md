---
layout: post
title:  "Red-black trees overview"
date:   2016-08-22 11:50:00
categories: [notes]
---

We want to store key value pairs in some data structure that has quick look time and quick implementation i.e. logarithmic time. Well, a normal BST will do the trick but it doesn't guarentee logarithmic time. It the worst case where the insertion order is not shuffled, there can be a tree that is simply a linked listed one after the other so that lookups are O(N) time. So we should look for a better implementaiton.

A good implementation is the 2-3 tree which is a tree data structure that allows for a parent node with 2 or 3 branching nodes. To handle cases for 3 nodes, the tree allows for up to two keys in a node so that the keys will be able to compare each of the 3 branching nodes and maintain sorted order. The hardest cases for keeping sorted order in insertions involve adding a key to a node that already has 3 nodes; in this case, temporary make a 4 node which will sort the new insertions and divide into 2 two nodes and problem solved, the sort order is maintained and the tree has been reorganized to balance all keys. Thus this structure it turns out is capable of always maintaining sorted order and of being perfectly balanced. The complexity of basic search, insert, and delete methods is O(clogN) with the tree having a height of at most logN.

Good. That works. However, we don't really like this implementation because for one it isn't really a BST and for two because the code implementation can be messy. So we transfer the properties of a 2-3 tree to a new representation: a red black tree.

The red black tree uses the color red to represent the link between two keys in a single node aka the 3 nodes in the 2-3 trees. So, we can easily translate a 2-3 tree to a red black tree. For our convinience we limit the red links to appear on only the left of nodes, so we will only talk about left leaning red black trees.

So the rules of 2-3 trees are translated to red-black trees which are namely these: no red links on the right, no red links for two branching nodes from a parent node, and no consecutive red links between two  keys in two layers (this would map a four node in the 2-3 tree). 

With these rules, we have to come up with ways to shift the RB tree if violations do occur. They are these: rotate the keys either left or right to shift the red link onto the left of a parent node but with a rearranged order of keys so that the rotation maintains sort order, or color flip the branching links to from red to black and make the parent node's link to its parent be red. These three simple operations (which are very easy to code) will cover the rules we ahve set up and handle all cases of new insertions. Nice.

Therefore, we have implemented the 2-3 tree in an actual BST structure with some nice code. Here are the major additions to the BST for insertion.

```java
// insert the key-value pair in the subtree rooted at h
private Node put(Node h, Key key, Value val) { 
    if (h == null) return new Node(key, val, RED, 1);

    int cmp = key.compareTo(h.key);
    if      (cmp < 0) h.left  = put(h.left,  key, val); 
    else if (cmp > 0) h.right = put(h.right, key, val); 
    else              h.val   = val;

    // fix-up any right-leaning links
    if (isRed(h.right) && !isRed(h.left))      h = rotateLeft(h);
    if (isRed(h.left)  &&  isRed(h.left.left)) h = rotateRight(h);
    if (isRed(h.left)  &&  isRed(h.right))     flipColors(h);
    h.size = size(h.left) + size(h.right) + 1;

    return h;
}

// make a left-leaning link lean to the right
private Node rotateRight(Node h) {
    // assert (h != null) && isRed(h.left);
    Node x = h.left;
    h.left = x.right;
    x.right = h;
    x.color = x.right.color;
    x.right.color = RED;
    x.size = h.size;
    h.size = size(h.left) + size(h.right) + 1;
    return x;
}

// make a right-leaning link lean to the left
private Node rotateLeft(Node h) {
    // assert (h != null) && isRed(h.right);
    Node x = h.right;
    h.right = x.left;
    x.left = h;
    x.color = x.left.color;
    x.left.color = RED;
    x.size = h.size;
    h.size = size(h.left) + size(h.right) + 1;
    return x;
}

// flip the colors of a node and its two children
private void flipColors(Node h) {
    // h must have opposite color of its two children
    // assert (h != null) && (h.left != null) && (h.right != null);
    // assert (!isRed(h) &&  isRed(h.left) &&  isRed(h.right))
    //    || (isRed(h)  && !isRed(h.left) && !isRed(h.right));
    h.color = !h.color;
    h.left.color = !h.left.color;
    h.right.color = !h.right.color;
}
```

Note that the main reason why it is possible to handle all cases of insertion is because the insertion method is recursive (like that of the original BST) so with each insertion onto a new node, a reordering can take place to keep sort order as best it can. Also, the code above is from the standard Princeton Algorithms class by Sedgewick and Wayne; if you want to create a persistent RBT you can just amend the code.

Note: Stack iterator for RBT has O(H) size, O(logN) performance for a balanced BST, and O(N) to visit all nodes but amortized time O(1) time per visit Hibbard deletion (like BST) for deleting nodes.
