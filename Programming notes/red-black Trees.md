# Red-Black Trees

A **Red-Black Tree** is a self-balancing binary search tree. This means it can efficiently store and retrieve data while automatically adjusting its structure to maintain balance.

The "self-balancing" aspect is crucial because it guarantees that operations like insertion, deletion, and searching will always take a logarithmic amount of time, ``O(log n)``, regardless of the order in which data is added.

It achieves this balance by adhering to a set of specific "red-black properties":

  1. **Node Colour**: Every node is either Red or Black.
  2. **Root Colour**: The root of the tree is always Black.
  3. **Red Node Children**: If a node is Red, then both its children must be Black. This means you can't have two consecutive Red nodes along any path from the root to a leaf.
  4. **Black Height**: For each node, all simple paths from the node to descendant leaf nodes contain the same number of Black nodes. This is often referred to as the "black height" of the tree.
  5. **Nil Nodes**: All leaf nodes (nodes with no children) are NIL nodes and are coloured Black. (In some implementations, these NIL nodes are conceptual and not explicitly stored, but their black colour property is still fundamental).

When you insert or delete a node, these properties can be violated. To restore them, the tree performs a series of rotations and recolouring's. These operations are carefully designed to rearrange the tree's structure and change node colours in a way that re-establishes all five properties, thus maintaining the tree's balance.

In essence, Red-Black Trees are a clever way to ensure that a binary search tree remains efficient even with frequent modifications, making them a cornerstone of many data management systems!
