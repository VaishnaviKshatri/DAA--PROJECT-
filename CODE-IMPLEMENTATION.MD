### *1. IT Sector*  
- *Tries*:  
  - Manage and search large amounts of data such as employee records or client databases efficiently.  

- *String Matching Algorithms*:  
  - *Rabin-Karp*: Validate user credentials in IT systems.  

- *Sorting Algorithms*:  
  - Organize IT projects by priority or deadlines.

---

### *2. Agriculture*  
- *Segment Trees*:  
  - Monitor and analyze crop yields in different regions.  

- *HashMaps*:  
  - Track inventory of seeds, fertilizers, and equipment.  

- *Graph Algorithms*:  
  - *BFS/DFS*: Design irrigation networks for optimal water distribution.

---

### *3. Commercial Sector*  
- *Heap*:  
  - Allocate resources to high-demand businesses.  

- *Graph Algorithms*:  
  - *Bellman-Ford Algorithm*: Analyze trade routes and shipping costs.  

- *HashMaps*:  
  - Store data on shop inventories and sales patterns.

---

### *4. Solar-Powered Infrastructure*  
- *Segment Trees*:  
  - Monitor solar panel efficiency across installations.  

- *Heap*:  
  - Prioritize energy distribution to critical areas during peak hours.  

- *Graph Algorithms*:  
  - *Kruskal’s Algorithm*: Plan solar grid connectivity with minimal costs.

---

- #include <iostream>
- #include <climits>

using namespace std;

class Dijkstra
{
public:
    int cost[100][100];
    int v; // Number of vertices
   -  int dist[10]; 
   - int path[10]; 
   - int visited[10]; 

    void read_cost(int cost[100][100], int v);
    void initiate(int arr[10], int n);
    void shortest_path(int src);
    void print_path(int src);
};

void Dijkstra::read_cost(int cost[100][100], int v)
{
    cout << "Enter the cost matrix:\n";
    for (int i = 0; i < v; i++)
    {
        for (int j = 0; j < v; j++)
        {
            cin >> cost[i][j];
            if (cost[i][j] == 0 && i != j)
            {
                cost[i][j] = INT_MAX; // Set non-edges to infinity
            }
        }
    }
}

void Dijkstra::initiate(int arr[10], int n)
{
    for (int i = 0; i < n; i++)
    {
        arr[i] = 0;
    }
}

void Dijkstra::shortest_path(int src)
{
    // Initialize distances and visited array
    for (int i = 0; i < v; i++)
    {
        dist[i] = INT_MAX;
        visited[i] = 0;
        path[i] = -1;
    }
    dist[src] = 0; // Distance to source is 0

    for (int count = 0; count < v - 1; count++)
    {
        // Find the vertex with the minimum distance
        int min_dist = INT_MAX, u;

        for (int i = 0; i < v; i++)
        {
            if (!visited[i] && dist[i] < min_dist)
            {
                min_dist = dist[i];
                u = i;
            }
        }

        visited[u] = 1; // Mark the chosen vertex as visited

        // Relax the edges of the chosen vertex
        for (int i = 0; i < v; i++)
        {
            if (!visited[i] && cost[u][i] != INT_MAX && dist[u] != INT_MAX && dist[u] + cost[u][i] < dist[i])
            {
                dist[i] = dist[u] + cost[u][i];
                path[i] = u; // Update the path
            }
        }
    }
}

void Dijkstra::print_path(int src)
{
    cout << "Vertex\tDistance from Source\tPath" << endl;
    for (int i = 0; i < v; i++)
    {
        cout << i << "\t" << dist[i] << "\t\t";

        // Print the path
        int temp = i;
        while (temp != -1 && temp != src)
        {
            cout << temp << " <- ";
            temp = path[temp];
        }
        if (i != src)
            cout << src;

        cout << endl;
    }
}

int main()
{
    Dijkstra d;
    int src;

    cout << "Enter the number of vertices: ";
    cin >> d.v;

    d.read_cost(d.cost, d.v);

    cout << "Enter the source vertex: ";
    cin >> src;

    d.shortest_path(src);
    d.print_path(src);

    return 0;
}

---

#include <iostream>

using namespace std;

class d {
public:
    int u;
    int v;
    int w;
};

// Function to check if two vertices are in the same set
int find(int arr[50], int u, int v) {
    if (arr[u] == arr[v]) {
        return 1;
    } else {
        return 0;
    }
}

// Function to union two sets
void union_set(int arr[50], int u, int v, int n) {
    int temp = arr[u];
    for (int i = 0; i < n; i++) {
        if (arr[i] == temp) {
            arr[i] = arr[v];
        }
    }
}

// Function to merge two sorted arrays into a single sorted array
void Merge(d B[], int p, d C[], int q, d A[]) {
    int i = 0, j = 0, k = 0;

    while (i < p && j < q) {
        if (B[i].w <= C[j].w) {
            A[k++] = B[i++];
        } else {
            A[k++] = C[j++];
        }
    }
    while (i < p) {
        A[k++] = B[i++];
    }
    while (j < q) {
        A[k++] = C[j++];
    }
}

// Function to sort an array using Merge Sort
void MergeSort(d A[], int n) {
    if (n > 1) {
        int mid = n / 2;

        d B[50], C[50];
        for (int i = 0; i < mid; i++) {
            B[i] = A[i];
        }
        for (int i = mid; i < n; i++) {
            C[i - mid] = A[i];
        }

        MergeSort(B, mid);
        MergeSort(C, n - mid);
        Merge(B, mid, C, n - mid, A);
    }
}

int main() {
    int n, e;
    cout << "Enter the number of vertices and edges: ";
    cin >> n >> e;

    d d1[50];
    cout << "Enter the edges (u v w):" << endl;
    for (int i = 0; i < e; i++) {
        cin >> d1[i].u >> d1[i].v >> d1[i].w;
    }

    // Sort the edges by weight
    MergeSort(d1, e);

    int arr[50];
    for (int i = 0; i < n; i++) {
        arr[i] = i;
    }

    d mst[50];
    int mstCount = 0;
    int cost = 0;

    for (int i = 0; i < e; i++) {
        if (!find(arr, d1[i].u, d1[i].v)) {
            mst[mstCount++] = d1[i];
            cost += d1[i].w;
            union_set(arr, d1[i].u, d1[i].v, n);
        }
    }

    cout << "Edges in the Minimum Spanning Tree (u v w):" << endl;
    for (int i = 0; i < mstCount; i++) {
        cout << mst[i].u << " " << mst[i].v << " " << mst[i].w << endl;
    }

    cout << "Total weight of MST: " << cost << endl;

    return 0;
}
