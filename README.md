#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Graph {
    int vertices;
    vector<vector<int>> adj;

public:
    // Constructor
    Graph(int v) {
        vertices = v;
        adj.resize(v);
    }

    // Add edge
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);   // For undirected graph
    }

    // ---------------- DFS ----------------
    void DFSUtil(int vertex, vector<bool>& visited) {
        // Mark current vertex as visited
        visited[vertex] = true;

        // Visit and display current vertex
        cout << vertex << " ";

        // Recursively visit every unvisited adjacent vertex
        for (int neighbour : adj[vertex]) {
            if (!visited[neighbour]) {
                DFSUtil(neighbour, visited);
            }
        }
    }

    void DFS(int source) {
        vector<bool> visited(vertices, false);

        cout << "DFS Traversal: ";
        DFSUtil(source, visited);
        cout << endl;
    }

    // ---------------- BFS ----------------
    void BFS(int source) {
        vector<bool> visited(vertices, false);
        queue<int> q;

        // Mark source as visited and insert into queue
        visited[source] = true;
        q.push(source);

        cout << "BFS Traversal: ";

        // Repeat until queue becomes empty
        while (!q.empty()) {
            // Remove a vertex from the queue
            int vertex = q.front();
            q.pop();

            // Visit and display vertex
            cout << vertex << " ";

            // Insert all unvisited adjacent vertices
            for (int neighbour : adj[vertex]) {
                if (!visited[neighbour]) {
                    visited[neighbour] = true;
                    q.push(neighbour);
                }
            }
        }

        cout << endl;
    }
};

int main() {
    // Create graph with 6 vertices: 0 to 5
    Graph g(6);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 5);

    // Perform DFS and BFS starting from vertex 0
    g.DFS(0);
    g.BFS(0);

    return 0;
}
