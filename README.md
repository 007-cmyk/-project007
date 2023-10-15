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
// 
#include <bits/stdc++.h> 
using namespace std;
vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source) {
    // adjacency list is created
    unordered_map<int, list<pair<int, int>>> adj;
    for(int i = 0 ; i < edges ; ++i)
    {
        int u = vec[i][0];
        int v = vec[i][1];
        int w = vec[i][2];
        adj[u].push_back(make_pair(v,w));
        adj[v].push_back(make_pair(u,w));
    }
    vector<int> dist(vertices);
    for(int i = 0 ; i < vertices ; ++i)
    {
        dist[i] = INT_MAX;
    }
    set<pair<int,int>> st;
    dist[source] = 0;
    st.insert(make_pair(0 , source));
    while(!st.empty())
    {
        auto top = *(st.begin());
        int node_distance = top.first;
        int top_node = top.second;
        //erase top record
        st.erase(st.begin());
        //traverse on neighbours
        for(auto neighbour : adj[top_node]){
            if(node_distance + neighbour.second < dist[neighbour.first])
            {
                auto record = st.find(make_pair(dist[neighbour.first] , neighbour.first));
                if(record != st.end()){
                    st.erase(record);
                }
                dist[neighbour.first] = node_distance + neighbour.second;
                st.insert(make_pair(dist[neighbour.first] , neighbour.first));
            }
        }
    }
    return dist;
}
int main() {
    // Number of vertices and edges in the graph
    int vertices = 6;
    int edges = 9;
    
    // Sample graph represented as a 2D vector (u, v, w)
    vector<vector<int>> graph = {
        {0, 1, 2},
        {0, 2, 4},
        {1, 2, 1},
        {1, 3, 7},
        {2, 4, 3},
        {3, 4, 1},
        {3, 5, 5},
        {4, 5, 2},
        {2, 5, 7}
    };
    
    int source;  // Source vertex
    cout<<"ENTER THE SOURCE VERTEX : ";
    cin>>source;
    vector<int> shortestDistances = dijkstra(graph, vertices, edges, source);
    
    // Output the shortest distances from the source vertex
    for (int i = 0; i < vertices; i++) {
        cout << "Shortest distance from " << source << " to " << i << " is: " << shortestDistances[i] << endl;
    }
    
    return 0;
}
#
