# Graph-notes

---

### Types

---

1. Directed - Undirected
2. Cyclic - Acyclic
3. Weighted

### Terms

Path - sequence of node only cpome once

Undirected graph -

- degree = 2 \* edges
- Tree is an undirected acyclic graph

## Graph Representation

---

n - number of Nodes

m - number of edges

m lines contains u and v

- in Undirected graph manner, we can travel to u to v as well as v to u. But in Directed graph there will be an arrow given with it.

1.  Adj Matrix

    - There will be an n nodes given. You can make 2d matrix of them.
    - Check if node is 0-based index or 1-based.
    - If it is 0-based indexed, then create 2D matrix of nXn else create 2D matrix of n+1 X n+1.
    - u and v are given so at particular index of matrix give 1, rest all places put 0.

      - if it is 1-based index,
        n=5, m=7

        int adj[n+1][n+1];

        for( int i=0 ; i<n ; i++ ) {

              int u,v;

              cin>>u>>v;

              adj[u][v]=1;

              adj[v][u]=1;

        }

    - Disadvantage
      - If there is large number of nodes available like 10<sup>5</sup> then it is not possible to create 2d matrix of 10<sup>5</sup> X 10<sup>5</sup>.

2.  Adj List

    - Data structure can be used as, vector<int> adj[n+1];
    - this will create an array of vector with n+1 indexes.
    - So, at particular indexes we will have it connections.
    - u will become an index and v will push_back at u<sup>th</sup> index.

    - If it is undirected graph, we will have 2-way connection, and if we are having Directed graph there will be only 1-way connection.

      - So from above examples, n=5,m=7 with <u>Undirected graph</u>,

        <pre>
            vector<int> adj[n+1];
        
            for(int i=0 ; i < m ; i ++ )
                int u,v;
                cin>>u>>v;
                adj[u].push_back(v);
                adj[v].push_back(u);
            }
        </pre>

    - If it is weighted graph, so there will be an extra value at particular edge we need to add.

    - So, we need to use pair then, like vector<pair<int,int>>

            vector<pair<int,int>> adj[n+1];
            for(int i=0 ; i<m ; i++) {
                int u,v, wt;
                cin>>u>>v>>wt;
                adj[u].push_back({v,wt});
                adj[v].push_back({u,wt});
            }

## <p style="color:orange">Connected Components</p>

---

- A single node is component in graph.
- So, there will be a concept of connected components in graph.
- Make sure, any of traversal you want to perform (DFS, BFS), take for loop of number of nodes first.
- Create an array of no of nodes+1 (n+1), visited[n+1].
- By default all values will bes 0.
- You will only follow traversal if given node is not visited like visited[i] == 0
- As soon as node being visited, visited[i]=1 will become 1.

    <pre>
    int visited[n+1]= {0,0,...,0};
  
    for(i=1;i<=n;i++) {
        if(!visited[i]) {
            //BFS
            //DFS
        }
    }
    </pre>

## <p style="color:orange">Traversal Techniques</p>

---

---

### <p style="color:violet;">BFS(Breadth First Search)</p>

---

- Traversing adjecent node first

    <pre style="color:white;background-color:#121212;font-size:18px">
    #include < iostream>
    #include < bits/stdc++.h>
    using namespace std;
  
    void dfsTraversal(int node, vector<bool> &visited, vector<int> adj[], vector<int> &dfs)
    {
        dfs.push_back(node);
        visited[node] = true;
        for (auto it : adj[node])
        {
            if (visited[it] == false)
            {
                dfsTraversal(it, visited, adj, dfs);
            }
        }
    }
  
    vector<int> dfsOfGraph(int V, vector<int> adj[])
    {
        // Code here
        vector<bool> visited(V + 1, false);
        vector<int> dfs;
        dfsTraversal(1, visited, adj, dfs);
        return dfs;
    }
  
    vector<int> bfsTraversal(int V, vector<int> adj[])
    {
        vector<int> bfs;
        vector<bool> visited(V + 1, false);
  
        for (int i = 1; i <= V; i++)
        {
            if (visited[i] == false)
            {
                queue<int> q;
                q.push(i);
                visited[i] = true;
  
                while (!q.empty())
                {
                    int node = q.front();
                    q.pop();
                    bfs.push_back(node);
  
                    for (auto it : adj[node])
                    {
                        if (visited[it] == false)
                        {
                            q.push(it);
                            visited[it] = true;
                        }
                    }
                }
            }
        }
        return bfs;
    }
  
    void takeInput(vector < int > *adj, int m)
    {
        int u, v;
        for (int i = 1; i <= m; i++)
        {
            cin >> u >> v;
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
    }
  
    int main()
    {
        int n, m;
        cin >> n >> m;
  
        vector<int> adj[n + 1];
  
        takeInput(adj, m);
  
        vector<int> ans = bfsTraversal(n, adj);
  
        for (auto x : ans)
        {
            cout << x << " ";
        }
        cout << endl;
  
        cin.get();
        return 0;
    }

</pre>
