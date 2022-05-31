### DFS

https://leetcode.com/problems/number-of-islands/solution/

1. How can we format the problem as one graph, what is node and edge.
Treat the (2d grid map) as an (undirected) graph and there is an edge between (two horizontally or vertically adjacent nodes of value '1').

2. How to trigger the DFS and what to do during each DFS process.
Linear scan the 2D grid map, if a node contains a '1' then it is a root node to trigger a Depth First Search. 
During the DFS, we only visit the node of '1' and every visited node should be set as '0' to mark as visited nodes.

3. How to calculate the result
We count the number of root nodes which trigger DFS. This number would be the number of islands for each DFS starting at some root identifies an island.

  
