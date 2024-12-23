# MST_Kruskal

A. Finding MST using Kruskal's algorithm steps:

1. Start with an empty set (this will become our MST).

2. Sort all edges in ascending order based on their weights
- For example, if you have edges: (A-B: 4), (B-C: 2), (A-C: 3)
- They would be sorted as: (B-C: 2), (A-C: 3), (A-B: 4).
- For each edge in the sorted list, starting from the smallest weight.

3. Check if including this edge creates a cycle in our current set
- If no cycle is formed, add the edge to our set
- If a cycle would be formed, skip this edge and move to the next one

4. Stop when we have included (V-1) edges, where V is the number of vertices
- This is because a tree with V vertices must have exactly (V-1) edges

• Pseudocode:
Algorithm Kruskal(G):
    Input: Graph G = (V, E) where V is vertices and E is edges
    Output: Set of edges forming Minimum Spanning Tree

    MST = {} // Empty set for Minimum Spanning Tree edges
    forest = {} // Empty set of trees (initially each vertex is its own tree)
    
    // Create initial forest where each vertex is its own tree
    for each vertex v in V:
        MakeSet(v)
    
    // Sort all edges in ascending order by weight
    sortedEdges = Sort(E) by weight
    
    for each edge (u, v) in sortedEdges:
        // If vertices u and v belong to different trees
        if Find(u) ≠ Find(v):
            MST = MST ∪ {(u, v)}  // Add edge to MST
            Union(u, v)           // Merge trees containing u and v
            
        // Stop when we have V-1 edges (a tree property)
        if |MST| equals |V| - 1:
            break
            
    return MST

// Helper functions for Union-Find operations:
Function MakeSet(v):
    parent[v] = v
    rank[v] = 0

Function Find(v):
    if parent[v] ≠ v:
        parent[v] = Find(parent[v])
    return parent[v]

Function Union(u, v):
    root_u = Find(u)
    root_v = Find(v)
    
    if rank[root_u] < rank[root_v]:
        parent[root_u] = root_v
    else if rank[root_u] > rank[root_v]:
        parent[root_v] = root_u
    else:
        parent[root_v] = root_u
        rank[root_u] = rank[root_u] + 1


B. Algorithm Analysis: 
1. MakeSet(v) --> is executed once for each vertex and as we have V vertices, The total complexity -->  O(V)
2. Sort(E) --> Sorts all edges in ascending order by weigh and since edges are E . It's time complexity --> O(E log E)
3. Find(u) and Union(u, v)   are executed in almost constant time --> O(1)
4. Let number of edges is n, and as it's MST so no of vertices is n+1 
So total Time complexity is  O(n+1)+ O(n log n)+O(1)

• and by discarding non-dominant terms --> Total Time Complexity is O(n Log n)
