tag : #tree 

#### Introduction : 

A red black tree is a binary search tree with additional information of color stored. By constraining the node colors on any simple path from root to leaf, red black trees ensure that **no such path is more than twice as long as any other, so that the tree is approximately balanced**. A red black tree is binary search tree that satisfies following properties : 
1. Every node is either red or black.
2. The root is black.
3. Every leaf (null) node is black.
4. If node is red then both children are black.
5. For each node, all simple paths from the node to descendent leaves contains same number of black nodes.