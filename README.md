# -project007
# Algorithm

1.Initialize:
Create a set of visited nodes (initialized as empty).
Create a set of unvisited nodes (initialized with all nodes).
Assign a distance value to every node. Initialize it as infinity for all nodes, except the source node, which is set to 0.
Set the current node as the source node.

2.For the current node, consider all of its neighbors:
Calculate their tentative distances from the source node. The distance from the source node to a neighbor is the sum of the distance value of the current node and the weight of the edge connecting them.
Compare the newly calculated tentative distance to the current assigned value and assign the smaller one.

3.After considering all of the neighbors of the current node, mark the current node as visited:
A visited node will not be checked again.

4.Select the unvisited node with the smallest tentative distance:
Set it as the new "current node" for the next iteration.

5.Repeat steps 2-4 until the destination node is marked as visited or until there are no unvisited nodes left.

6.Backtrack to find the shortest path:
Once the destination node is marked as visited, the algorithm can be stopped. The shortest path can be obtained by backtracking from the destination node to the source node using the information stored in each node's "previous" field.
# Code
[Code.txt](https://github.com/007-cmyk/-project007/files/12916782/Code.txt)
