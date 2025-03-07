# Binary Tree

A binary tree is a data structure made up of linked nodes, in which each node can have at most 2 child nodes, referred to as the `left node` and `right node`.

## Terminology:

- The first node in a binary tree is known as the `root`.
- Nodes with no children are `leaves`.
- A node with child nodes is known as a `parent`.
- The children of a child node are known as `grandchildren`.
- The parent of a parent is known as an `ancestor`.
- The number of node levels when counting from the root is known as the tree `depth`.
- The `height` when counting the number of levels from a node to the root. As such, the height from each node differs.
- A `complete` binary tree is a tree in which all levels except the last have both left and right children linked to the previous level (no gaps).
- A `full` binary tree is one in which all nodes in the tree have either 2 or 0 children.
- A `balanced` binary tree is a tree in which the difference between depth of the left and right subtrees is, at most, 1 level.

## Binary Search Tree (BST)

A BST is just a binary tree in which the **left node must always be less than its parent**, and the **right node must be greater than its parent**.

The benefits of this is that, when searching, we can eliminate half of the nodes, at each level by deciding if the search value is greater than, or less than the current node.

## Complexities

| Algorithm | Average    | Worst  |
| --------- | ---------- | ------ |
| Space     | $O(n)$     | $O(n)$ |
| Search    | $O(log n)$ | $O(n)$ |
| Insert    | $O(log n)$ | $O(n)$ |
| Delete    | $O(log n)$ | $O(n)$ |

## Code

There are two main ways to code binary search tree classes:

- 2 classes: `Node` and `BinarySearchTree` - with references in Node and methods in BinarySearchTree
- 1 class: `BSTNode` with everything encapsulated in one place.

### 2 Classes

#### Node

```python
class Node:

    def __init__(self, data = None):
        self.data = data
        self.left = None
        self.right = None
```

#### Binary Search Tree

```python
class BinarySearchTree:

    def __init__(self):
        self.root = None
```

#### Helpers

```python
# find the lowest value in a tree, starting from a given node
def get_min(self, node = None):
    current = node or self.root
    while current.left:
        current = current.left
    return current

# find the largest value in a tree, starting from a givin node
def get_max(self, node = None):
    current = node or self.root
    while current.right:
        current = current.right
    return current
```

#### Inserting

There are a few ways to write methods: iterative and recursive. All examples will be recursive.

```python
def insert(self, data):
    self.root = self._insert(data, self.root)

def _insert(self, data, node):
    if node is None:
        return Node(data)

    # data must go in the left subtree
    if data < node.data:
        node.left = self._insert(data, node.left)
    # data must go in the right subtree
    elif data > node.data:
        node.right = self._insert(data, node.right)
    # return the mutated node
    return node
```

#### Search / Find

```python
def search(self, data):
    if self.root:
        return self._search(data, self.root)
    else:
        return None

def _search(self, data, node):
    # data must be in the left subtree, if it exists
    if data < node.data and node.left:
        return self._search(data, node.left)
    # data must be in the right subtree, if it exists
    elif data > node.data and node.right:
        return self._search(data, node.right)
    # data found
    elif data == node.data:
        return True
    else:
        return False
```

#### Delete

```python
def delete(self, data):
    self.root = self._delete(data, self.root)

def _delete(self, data, node):
    # ------------------------------------
    # BASE CASE
    # ------------------------------------
    # found leaf node, no more subtree
    if node is None:
        return node

    # ------------------------------------
    # SEARCH PHASE
    # ------------------------------------
    # search for the node

    # data must be in the left subtree if it exists
    if data < node.data:
        node.left = self._delete(data, node.left)
    # data must be in the right subtree if it exists
    elif data > node.data:
        node.right = self._delete(data, node.right)
    # node found - must be equal
    else:

    # ------------------------------------
    # DELETION PHASE
    # ------------------------------------
        # return the next node from left or right
        # this returns to the recursive call in the previous search phase and
        # overwrites that node with a new subtree excluding the deleted node

        # node has 1 child
        if not node.left or not node.right:
            return node.left or node.right

        # node has 2 children
        # need to get the smallest larger value
        # known as the inorder successor
        # traverse the left side of the right tree

        # Find the inorder successor (smallest node in the right subtree)
        successor = self.get_min(node.right)
        node.data = successor.data

        # data in the node has been replaced with the smallest larger value
        # remove the smallest larger value from the right subtree
        node.right = self._delete(node.data, node.right)

    return node
```

#### Traversals

##### Preorder

A "preorder" traversal is a way to visit all the nodes in a tree. It's called "preorder" because the current node is visited before its children.

Use Case:

- Creating a copy of a tree: If you want to clone the tree or perform some operation that requires starting from the root first.
- Expression Trees: Used in expression trees for evaluating or constructing expressions, where operations are usually applied to the root first (prefix notation).

```python
def preorder(self, visited, node = None):
    node = node or self.root
    if node:
        visited.append(node.data)
        self.preorder(visited, node.left)
        self.preorder(visited, node.right)
    return visited
```

##### Inorder

An "inorder" traversal is the most intuitive way to visit all the nodes in a tree. It's called "inorder" because the current node is visited between its children. It results in an ordered list of the nodes in the tree.

Use Case:

- Binary Search Tree (BST) Traversal: Inorder traversal on a BST visits the nodes in ascending order. It’s the primary method used for sorting data in a BST.
- Searching for a specific value: When searching, inorder traversal ensures that elements are processed in increasing order.

```python
def inorder(self, visited, node = None):
    node = node or self.root
    if node:
        self.inorder(visited, node.left)
        visited.append(node.data)
        self.inorder(visited, node.right)
    return visited
```

##### Postorder

A "postorder" traversal also visits all the nodes in a tree. It's called "postorder" because the current node is visited after its children.

Use Case:

- Deleting a tree: Since the root is visited last, this traversal is often used when you want to delete or free the memory of a tree’s nodes after processing both subtrees.
- Evaluating postfix expressions: Postorder is used in expression trees to evaluate postfix expressions (where the operators come after the operands).

```python
def postorder(self, visited, node = None):
    node = node or self.root
    if node:
        self.postorder(visited, node.left)
        self.postorder(visited, node.right)
        visited.append(node.data)
    return visited
```
