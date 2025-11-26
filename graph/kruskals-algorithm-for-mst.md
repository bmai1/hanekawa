---
icon: tree-palm
---

# kruskal's algorithm for MST

To build a MST (all nodes are connected, minimum total edge weight):

* Sort edges by weight (usually with disjoint set union find)
* Add the edges to the MST until all nodes are connected

Kruskal's MST algorithm:

```cpp
#include <bits/stdc++.h>
#include "graph.cpp"

using namespace std;

// for pq (min-heap) to compare edge weight
struct CompareEdge {
    bool operator()(const Edge& e1, const Edge& e2) const {
        return e1.weight > e2.weight;
    }
};

unordered_map<Vertex, unordered_set<Vertex, Vertex::HashFunction>, Vertex::HashFunction> vertexMap;

// could be optimized with union-find (HELP)
void merge(unordered_set<Vertex, Vertex::HashFunction>& a, unordered_set<Vertex, Vertex::HashFunction>& b) {
    for (const Vertex& vertex : a) {
        b.insert(vertex);
    }
    for (const Vertex& vertex : b) {
         vertexMap[vertex] = b;
    }
}

vector<Edge> kruskal(Graph graph) {
    vector<Edge> MST;
    unordered_set<Edge, Edge::HashFunction> edges = graph.getEdges();
    priority_queue<Edge, vector<Edge>, CompareEdge> pq(edges.begin(), edges.end());

    for (const Vertex& vertex : graph.getVertices()) {
        vertexMap[vertex] = {vertex};
    }

    while (!pq.empty()) {
        Edge curr = pq.top();
        pq.pop();

        unordered_set<Vertex, Vertex::HashFunction>& s1 = vertexMap[curr.source];
        unordered_set<Vertex, Vertex::HashFunction>& s2 = vertexMap[curr.destination];

        if (s1 != s2) {
            MST.push_back(curr);
            merge(s1, s2);
        }
    }

    return MST;
}

int main() {
    vector<Edge> edges = {
        Edge(Vertex("0"), Vertex("1"), 4),
        Edge(Vertex("0"), Vertex("2"), 2),
        Edge(Vertex("1"), Vertex("3"), 5),
        Edge(Vertex("2"), Vertex("3"), 1),
        Edge(Vertex("3"), Vertex("4"), 3)
    };

    Graph graph(edges);

    vector<Edge> MST = kruskal(graph);
    for (const Edge& edge : MST) {
        cout << edge.source.getLabel() << "->" << edge.destination.getLabel() << " ";
    }
    cout << endl;

    return 0;
}
```

