# project007

*Dijkstra's Shortest Path Algorithm*

Input:
- `vec`: A 2D vector representing the graph with each row containing (u, v, w) denoting an edge from vertex u to vertex v with weight w.
- `vertices`: The total number of vertices in the graph.
- `edges`: The total number of edges in the graph.
- `source`: The source vertex from which the shortest paths are calculated.

Output:
- `dist`: A vector of integers representing the shortest distance from the source vertex to every other vertex.

Algorithm:

1. Create an empty adjacency list `adj` to represent the graph.

2. Populate the adjacency list `adj` with edges and their corresponding weights:
   - For each edge (u, v, w) in `vec`:
     - Add (v, w) to `adj[u]` (since it's an undirected graph, add (u, w) to `adj[v]` as well).

3. Initialize a vector `dist` of size `vertices` with all elements set to `INT_MAX`, representing initial distances.

4. Create an empty set `st` to store pairs (distance, vertex).

5. Set the distance of the `source` vertex to 0 and insert (0, `source`) into `st`.

6. While `st` is not empty:
   - Get the top element `(node_distance, top_node)` from `st`.
   - Remove the top element from `st`.
   - For each neighbor of `top_node` in `adj`:
     - Calculate the new distance `node_distance + neighbor.weight`.
     - If the new distance is less than the current distance in `dist` for the neighbor:
       - Find and erase the existing record of the neighbor from `st` if it exists.
       - Update `dist[neighbor]` with the new distance.
       - Insert `(new_distance, neighbor)` into `st`.

7. Return the vector `dist` containing the shortest distances.

Time Complexity:
- The time complexity of Dijkstra's algorithm with a binary heap is O((V + E) log V), where V is the number of vertices and E is the number of edges in the graph.

This algorithm efficiently finds the shortest path between a given source vertex and all other vertices in a weighted, undirected graph using Dijkstra's shortest path algorithm.

# Code

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

# Output:
