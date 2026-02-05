
## 1. My BFS Implementation (Visit on Discover)
```python
class Graph:
    def breadth_first_search(self, v):
        visited = []
        queue = []
        queue.append(v)
        visited.append(v)
        while queue:
            curr = queue.pop(0)
            for neighbour in sorted(self.graph[curr]):
                if neighbour not in visited:
                    visited.append(neighbour)
                    queue.append(neighbour)
        return visited
```
**Key ideas:**

- Use a **queue** (FIFO) for BFS:
    - Enqueue with `append`
    - Dequeue with `pop(0)`
- Mark nodes as visited **when they are discovered** (when enqueuing).
- `sorted(self.graph[curr])` makes traversal order deterministic.
---
## 2. Alternative BFS Style (Visit on Process)

```python
def breadth_first_search(self, v):
    visited = []
    queue = []
    queue.append(v)

    while queue:
        curr = queue.pop(0)
        visited.append(curr)

        for neighbour in sorted(self.graph[curr]):
            if neighbour not in visited and neighbour not in queue:
                queue.append(neighbour)

    return visited
```

**Differences from my version:**

- Marks nodes as visited **when processed** (when dequeued).
- Avoids duplicates by checking:
    - `neighbour not in visited`
    - and `neighbour not in queue`

Both are valid BFS and produce the same order in this problem.

---

## 3. Stack vs Queue (DFS vs BFS)

- **Stack behavior** (LIFO, like DFS):
    - `append()` + `pop()`
- **Queue behavior** (FIFO, like BFS):
    - `append()` + `pop(0)`
    - (In real projects, prefer `collections.deque` with `popleft()`)

---

## 4. Common BFS Bugs and Symptoms

- **Infinite loop:**
    - Forgetting to add `curr` to `visited`.
    - Incorrect `if` condition when enqueuing neighbors.
- **Wrong visit order:**
    - Using `pop()` (stack) instead of `pop(0)` (queue).
    - Not sorting neighbors when deterministic order is required.

---

## 5. BFS Checklist

1. Initialize:
    
    ```python
    visited = []
    queue = [start]
    ```
    
2. Loop:
    
    ```python
    while queue:
        curr = queue.pop(0)
        # Either:
        #   visited.append(curr)  # visit-on-process
        # or:
        #   mark as visited when enqueuing neighbors (visit-on-discover)
    ```
    
3. For each neighbor:
    - Ensure you don’t enqueue the same node endlessly:
        
        ```python
        if neighbour not in visited and neighbour not in queue:
            queue.append(neighbour)
        ```
        
4. Return `visited` in the order nodes were discovered.