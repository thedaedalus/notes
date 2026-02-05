Implement a simple undirected graph using an **adjacency list**.

**Data structure:**

- Use a `dict` where:
    - Keys are vertices (e.g. `0`, `1`, `2`, …).
    - Values are **sets** of neighboring vertices.
- Example:
    
    ```python
    graph = {
        0: {1, 4},
        1: {0, 2, 3, 4},
        2: {1, 3},
        3: {1, 2, 4},
        4: {0, 1, 3},
    }
    ```
    

**`Graph` class requirements:**

- `__init__(self)`
    
    - Initialize an empty adjacency list:
        
        ```python
        self.graph = {}
        ```
        
- `add_edge(self, u, v)` (undirected edge):
    
    1. If `u` is not in `self.graph`, create an empty set for it.
    2. If `v` is not in `self.graph`, create an empty set for it.
    3. Add `v` to `u`’s neighbor set.
    4. Add `u` to `v`’s neighbor set.
    
    - Important: use `.add()` on sets, don’t overwrite them with `=`.

**Key ideas:**

- An adjacency list is just a **dict-of-sets** that describes which nodes are connected.
- Using sets automatically avoids duplicate neighbors.
- Undirected graph ⇒ every edge `(u, v)` must be stored in **bo**