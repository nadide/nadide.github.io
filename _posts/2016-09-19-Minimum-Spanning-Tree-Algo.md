---
layout: post
title: Minimum Spanning Tree (MST) Algorithms
date: 2016-09-19 12:00
excerpt: Minimum spanning tree problem is find a subset of edges that connects all nodes with minimum cost in weighted graph.
tags: [ACM-ICPC, Competitive Programming, Algorithms]
comments : true
---

![mst-image](/assets/img/algo-image/MST/mst-image.png)

Minimum spanning tree problem is find a subset of edges that connects all nodes with minimum cost in weighted graph.


An edge-weighted graph is given as input, and we will select some of edges to create minimum spanning tree. In other word, we will create a sub-graph which is a tree with minimum cost. A single graph can have many different spanning trees, but we aim to find spanning tree with minimum weight. The weight of the spanning tree is sum of the weights of edges that belongs the spanning tree.

There are three rules that we need to obey to create a minimum spanning tree:
1. Selected edges should not create circle
2. All the nodes should be connected to tree
3. And, tree should has a weight that less than or equal to the weight of the any other spanning tree

A minimum spanning tree __has (V – 1) edges__ where V is the number of vertices in the given graph. Minimum Spanning Tree example:

![mst](http://nadide.github.io/assets/img/algo-image/MST/mst.png)

There are two solutions that both have __greedy approach__.

1. __Prim's algorithm__: 
    Start with any vertex and greedily grow a tree from it.
    At each step, add the cheapest edge to tree that has exactly one endpoint in T.

2. __Kruskal's algorithm__: 
    Sort edges in ascending order of cost.
    Add the next edge to tree unless doing so would create a cycle.
        

## Prim's Algorithms

![prim](http://nadide.github.io/assets/img/algo-image/MST/prim.png)

__What does algorithm proceed?__

Prim's minimum spanning tree grows by adding next closest vertex to partial tree. 

Lets go step-by-step according to given graph below.

![prim1](http://nadide.github.io/assets/img/algo-image/MST/prim1.png)

We have a graph which has 5 vertex (V), and 7 edges (E) as an input. Our goal is to return subset of given edges that belongs the minimum spanning tree.

Prim's algorithm starts with a single vertex. Choice of the vertex doesn't effect the result, can started with any vertex.

Algorithm creates and holds two information for each vertex:

1. __Key__ that is a cost when we connect the vertex to tree
2. __Parent__ that hold the parent of the vertex in tree

We will start with vertex\_0, and make it our current position. Initial key value for vertex\_0 will be _0 (zero)_, parent will be _-1_. Because of vertex\_0 is root of the tree, parent is _-1_, and we doesn't have cost to reach vertex\_0, so it is _0_.

![prim2](http://nadide.github.io/assets/img/algo-image/MST/prim2.png)

There are listed vertexes that can be reach from vertex_0 and their costs.

- vertex\_1 : 2
- vertex\_3 : 6


At next step, algorithm updates costs of current vertex's neighbors, and assign their parent as current vertex. That means if we make connection from parent value, it will cost as much as key value.  

![prim3](http://nadide.github.io/assets/img/algo-image/MST/prim3.png)

Then, algorithm adds one of these vertexes which has minimum cost. So, we add closest vertex to tree, and move to it. In our graph, we will add vertex\_1 and make our current vertex vertex\_1.

![prim4](http://nadide.github.io/assets/img/algo-image/MST/prim4.png)


We will repeat these two steps for each current vertex. Neighbor vertexes of Vertex\_1, and edge weights between vertex\_1:

- vertex\_2 : 3
- vertex\_3 : 8

There becomes new issue, because vertex\_3 already has values but not added to tree yet. What does means? We found out a possible connection to vertex\_3 from another vertex, and now we have another connection to vertex\_3 from current. We will compare this two costs, and choose lowest one. Because of existing cost of vertex\_3 is less, we are not going to update cost of vertex\_3. We will just update vertex\_2 as key is 3, parent is 1. 

![prim5](http://nadide.github.io/assets/img/algo-image/MST/prim5.png)

##### Note: When we are updating neighbors' costs of vertex, we don't consider visited vertexs, and don't add them to tree again.


Then, we will look at all vertexes which is valued, but not added. By comparing vertex\_2 and vertex\_3  we will add and go to closest vertex, which is vertex\_2 with cost _3_. 

![prim6](http://nadide.github.io/assets/img/algo-image/MST/prim6.png)


Algorithm repeats these two steps until all vertexes are added to tree. 
These repeating steps are illustrated in below pictured.

![prim7](http://nadide.github.io/assets/img/algo-image/MST/prim7.png)

After add all vertexes, algorithms will end and will print (V - 1) edges that belongs tree.


__Basic steps__

- Step 1: Pick a vertex as a starting point _(root)_
- Step 2: Update neighbors' key value and parent 
- Step 3: Find next closest vertex, and go to Step 2
    

__Implementation of Algorithm in C++__
    
__Step 1__:
    Get inputs
    
        cin >> V >> E;
        for (i=0; i < E; ++i) {
            cin >> x >> y >> weight;
            g[x][y] = g[y][x] = weight;
        }    
    
    
__Step 2__:
    Assign initial values of vertexs' keys as infinite, and positions as not used 
  
        for (int i=0; i<v; ++i)
            key[i]=INT_MAX, used[i]=false;
    
    
__Step 3__:
    Start from a single vertex which is root
    
        current = 0;
        used[current] = true;
    
        key[current] = 0, parent[current] = -1;
    
    
__Step 4__:
    Make loop to add (V - 1) more vertex
    
        for (i=0; i < V-1; ++i) 
        {
            // Step 5;
            
            // Step 6;
        }
        
    
__Step 5__:
    Update neighbors' key value and parent 
    IF (there is an edge bt curent and I) && (I is not used) && (edge is less than I's key)
    
        for (i=0; i < V; ++i)
            if (g[current][i] && !used[i] && g[current][i] < key[i])
                key[i] = g[u][i], parent[i] = current;
    
    
__Step 6__:
    Find a vertex, and update cuurent 
    IF (I is not used) && (I has min cost) 
    
        min = INT_MAX;
        for (i=0; i < V; ++i)
            if (!used[i] && key[i]<min) 
                min = key[i], minI = i;
                
        current = minI;
        used[current] = true;

        
__Step 7__:
    Print output
    
        cout << "Edge  Weight\n";
        for (i=1; i < V; ++i)
            cout << parent[i] <<" - "<<  i  <<"   "<<  g[i][parent[i]]  << endl;
            

[Implementation of all code](https://github.com/nadide/ACM-ICPC/blob/master/codes/graph_primMST2.cpp)
        
    
## Kruskal's Algorithms

![kruskal](http://nadide.github.io/assets/img/algo-image/MST/kruskal.png)

Explanation will be added later. 


