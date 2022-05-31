### bfs

1. How to formulate one problem as a graph
Treat the 2d grid map as an undirected map, each cell is one node and there is an edge between two horizontally or vertically adjacent nodes of value '1'.

2. How to trigger the BFS and implement it
Linear scan the 2D grid map, if a node contains '1', it is a root node that triggers a BFS. Then put it into a queue and set its value as '0' to mark as visited node.
Iteratively search the neighbors of enqueued nodes until the queue becomes empty.

3. How to calculate the result
Count the number of root nodes that trigger BFS.
