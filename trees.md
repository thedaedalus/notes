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

when apart of a class no need to the explicit check on the node. but you need checks on the left and right branches

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

when apart of a class no need to the explicit check on the node. but you need checks on the left and right branches

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

## Notes on tree concepts

### Recursion

- A function that calls itself.

- Needs:

>- **Base case** – when to stop recursing.
>- **Recursive case** – when it calls itself on a “smaller” or “simpler” input.

- For trees, recursion is natural because each child is itself a (smaller) tree.

### Trees (binary trees / BSTs)

- A tree node usually has:

>- ``val`` – the value stored.
>- ``left`` – left child (another node or ``None``).
>- ``right`` – right child (another node or ``None``).

- **Binary Search Tree (BST)** rule:

>- Left subtree values < node’s value.
>- Right subtree values > node’s value.

- Traversals:

>- ``Preorder``: node → left → right.
>- ``Inorder``: left → node → right.
>- ``Postorder``: left → right → node

Example preorder:

```python
def preorder(node, visited):
    if node is None:
        return visited
    visited.append(node.val)       # node
    preorder(node.left, visited)   # left
    preorder(node.right, visited)  # right
    return visited
```

### Using None as a sentinel

- ``None`` is Python’s “no value here” marker.

- In trees, ``None`` commonly means:

>- “This child doesn’t exist.”

- Patterns:

>- Checking for a missing node:
>
>```Python
>if node is None:
>    return
>```
>
>- Checking if a child exists:
>
>```Python
>if node.left is not None:
>       ...
>```
>
>-Using ``val=None`` as “empty root before first insert”.

### Truthy / Falsy checks

- In ``if`` conditions, Python treats values as **True** or **False**.
- **Falsy** values (act like ``False``):

>- ``None``
>- ``0``
>- ``""``(empty string)
>- ``[]``,``{}``,``set()``, etc

- **Truthy**: almost everything else.
- So:

>- ``if x:`` is really if x is truthy".
>- ``if x is not None:`` is stricter: it only checks for ``None``, not for other falsy values like ``0``.

Examples:

```Python
if x:              # True if x is truthy
    ...

if x is None:      # True only if x is exactly None
    ...

if x is not None:  # True for any non-None value (0, "", etc. still allowed)
    ...
```

For trees:

- ``if self.left:`` is shorthand for “if there is a left child (not None)”.
- ``if self.val:`` can be dangerous if ``val`` could be ``0`` or ``""``; safer is ``if self.val is not None:``.

```Python
if node.val is not None:
    ...
```
