# Binary Trees in python

## Code template

```Python
class Node:
    def __init__(self, val=None):
        self.val = val
        self.left = None
        self.right = None
        
```

### 1. Preorder(node,left,right)

```Python
    def preorder(node, visited):
        if node is None:
            return visited
    
        # visit node
        visited.append(node.val)
    
        # left subtree
        preorder(node.left, visited)
    
        # right subtree
        preorder(node.right, visited)
    
        return visited
    
```

### 2. Inorder(left,node,right)

```Python
    def inorder(node, visited):
        if node is None:
            return visited
    
        inorder(node.left, visited)
        visited.append(node.val)
        inorder(node.right, visited)
    
        return visited
```

### 3. Postorder (left, right, node)

```Python
def postorder(node, visited):
    if node is None:
        return visited

    postorder(node.left, visited)
    postorder(node.right, visited)
    visited.append(node.val)

    return visited
```

### 4. As a method on the class

When it's a method, you mentally subsitute ``node`` with ``self``. and drop the explicit ``node is None`` check, replacing it with guards on ``self.left``/``self.right``:

```python
class BSTNode:
    def preorder(self, visited):
        if self.val is not None:
            visited.append(self.val)
        if self.left is not None:
            self.left.preorder(visited)
        if self.right is not None:
            self.right.preorder(visited)
        return visited
```
