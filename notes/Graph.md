# Graphs

> These notes summarize the complete Graph module covered during our DSA sessions.
>
> **Language:** Java (Interview Focus)
>
> **Difficulty:** Beginner → Advanced
>
> **Goal:** Understand graph algorithms deeply enough to derive them during interviews rather than memorizing them.

---

# 1. Graph Fundamentals

## What is a Graph?

A graph is a data structure used to model relationships between objects.

It consists of:

- **Vertices (Nodes)** → Objects
- **Edges** → Relationships between objects

Examples:

- Cities connected by roads
- Friends in a social network
- Airports connected by flights
- Web pages connected by hyperlinks
- Courses with prerequisites
- Git commit history

Unlike trees, graphs do **not** have a root and may contain:

- Cycles
- Multiple connected components
- Multiple valid traversals

---

# Terminology

## Vertex

A node in the graph.

Example:

```text
A
```

---

## Edge

A connection between two vertices.

```text
A ----- B
```

---

## Path

A sequence of vertices connected by edges.

Example:

```text
A → C → D → E
```

---

## Cycle

A path that starts and ends at the same vertex.

Example:

```text
A → B → C → A
```

---

## Degree

Number of edges connected to a vertex.

Example:

```text
A
|\
| \
B--C
```

Degrees:

```
deg(A)=2
deg(B)=2
deg(C)=2
```

---

## In-degree

For directed graphs:

Number of incoming edges.

---

## Out-degree

For directed graphs:

Number of outgoing edges.

---

## Connected Component

A maximal set of vertices where every vertex is reachable from every other vertex.

Example:

```text
A ---- B


C ---- D ---- E
```

Components:

```
{A,B}

{C,D,E}
```

---

## Strongly Connected Component (Directed)

Every vertex can reach every other vertex.

Example:

```text
A → B
↑   ↓
└── C
```

This is one SCC.

---

# Types of Graphs

---

## 1. Undirected Graph

Edges have no direction.

```
A ----- B
```

Meaning:

```
A ↔ B
```

Examples

- Friendships
- Roads (two-way)
- Computer networks

---

## 2. Directed Graph (Digraph)

Edges have direction.

```
A → B
```

Meaning:

```
A can reach B

B cannot necessarily reach A
```

Examples

- Twitter follows
- Course prerequisites
- Flight routes
- Build dependencies

---

## 3. Weighted Graph

Each edge has a cost.

```
A --5--> B
```

The weight may represent:

- Distance
- Time
- Cost
- Probability
- Energy

---

## 4. Unweighted Graph

All edges are treated equally.

```
A ---- B
```

Equivalent to assuming every edge has weight 1.

---

## 5. Connected Graph

Every vertex is reachable.

```
A
|
B
|
C
```

---

## 6. Disconnected Graph

Contains multiple connected components.

```
A---B

C---D
```

---

## 7. Cyclic Graph

Contains at least one cycle.

```
A
|\
| \
B--C
```

---

## 8. Acyclic Graph

Contains no cycles.

Trees are the most common example.

---

# Trees are Graphs

Every tree is a graph.

Not every graph is a tree.

A tree is simply a graph satisfying:

- Connected
- No cycles
- N vertices
- Exactly N−1 edges

---

# Graph vs Tree

| Property | Tree | Graph |
|-----------|------|--------|
| Root | Yes | Optional |
| Cycles | Never | Allowed |
| Connected | Always | Not necessary |
| Parent | Exactly one (except root) | No restriction |
| Number of Edges | N−1 | Arbitrary |

---

# Directed vs Undirected Thinking

This distinction affects almost every graph algorithm.

Undirected graphs answer:

> "Are these two vertices connected?"

Directed graphs answer:

> "Can I reach one vertex from another?"

This difference leads to entirely different algorithms:

| Undirected | Directed |
|------------|-----------|
| Connected Components | Strongly Connected Components |
| Bridges | — |
| Articulation Points | — |
| MST | — |
| Cycle Detection | Different algorithm |
| Topological Sort | Not applicable | Applicable |

---

# Weighted vs Unweighted Thinking

If every edge has equal cost:

Use:

- BFS

If edges have different non-negative costs:

Use:

- Dijkstra

If negative edges exist:

Use:

- Bellman-Ford

If shortest paths between every pair are required:

Use:

- Floyd-Warshall

---

# The Most Important Question in Graph Interviews

Before thinking about an algorithm, ask:

### 1. Directed or Undirected?

This immediately eliminates half the algorithms.

---

### 2. Weighted or Unweighted?

This determines:

BFS vs Dijkstra vs Bellman-Ford.

---

### 3. Connected or Disconnected?

If disconnected:

Remember to iterate over every component.

---

### 4. Cycles allowed?

Important for:

- Trees
- Topological Sort
- Cycle Detection

---

### 5. What is being optimized?

Examples:

- Reachability
- Shortest path
- Minimum total cost
- Every edge exactly once
- Every vertex exactly once
- Connectivity after edge removal

The answer usually reveals the correct algorithm.

---

# Mental Classification of Graph Problems

Instead of memorizing algorithms, classify the problem.

## Traversal

Goal:

Visit vertices.

Algorithms:

- DFS
- BFS

---

## Connectivity

Goal:

Determine whether vertices belong together.

Algorithms:

- DFS
- BFS
- DSU

---

## Ordering

Goal:

Find dependency order.

Algorithms:

- Topological Sort

---

## Shortest Path

Goal:

Minimum cost.

Algorithms:

- BFS
- Dijkstra
- Bellman-Ford
- Floyd-Warshall

---

## Minimum Cost Network

Goal:

Connect every vertex.

Algorithms:

- Kruskal
- Prim

---

## Strong Connectivity

Goal:

Mutual reachability.

Algorithms:

- Kosaraju
- Tarjan

---

## Critical Structures

Goal:

Find important edges/vertices.

Algorithms:

- Bridges
- Articulation Points

---

## Edge Traversal

Goal:

Use every edge exactly once.

Algorithms:

- Hierholzer

---

## Partitioning

Goal:

Split into two groups.

Algorithms:

- Bipartite Check (2-coloring)

---

# Common Interview Mistakes

❌ Starting implementation before identifying graph type.

❌ Confusing graph traversal with shortest path.

❌ Using DFS for weighted shortest paths.

❌ Confusing Eulerian Path with Hamiltonian Path.

❌ Mixing concepts between directed and undirected graphs.

❌ Assuming a graph is connected without checking.

---

# Personal Learning Notes

During our discussions, the following insights proved especially valuable:

### 1. Always classify the graph first.

You consistently solved problems faster once you identified:

- Directed vs Undirected
- Weighted vs Unweighted
- Connected vs Disconnected

before thinking about algorithms.

---

### 2. Think in terms of invariants.

One of the biggest shifts in your understanding was moving away from:

> "What are the steps?"

towards

> "What property is the algorithm maintaining?"

This mindset will continue to be essential throughout Dynamic Programming and advanced algorithms.

---

# Interview Recognition Guide

| Problem Statement | Likely Topic |
|-------------------|--------------|
| Reachability | DFS / BFS |
| Shortest path (unweighted) | BFS |
| Shortest path (weighted) | Dijkstra / Bellman-Ford |
| Connect all cities cheaply | MST |
| Course schedule | Topological Sort |
| Friend circles | DSU / DFS |
| Critical roads | Bridges |
| Critical cities | Articulation Points |
| Strong groups | SCC |
| Every edge once | Hierholzer |
| Two groups | Bipartite |

---

# Revision Summary

✔ A graph models relationships.

✔ Trees are a special case of graphs.

✔ The first step in every graph interview problem is classification:

- Directed?
- Weighted?
- Connected?
- Cyclic?
- Optimization goal?

Choosing the correct algorithm becomes much easier once these questions are answered.


# 2. Graph Representation

Choosing the correct graph representation is often the **first implementation decision** in a graph problem.

The representation affects:

- Memory usage
- Traversal speed
- Edge lookup speed
- Suitability for specific algorithms

A wrong representation can turn an optimal algorithm into an inefficient one.

---

# Types of Graph Representation

The four most common representations are:

1. Adjacency Matrix
2. Adjacency List
3. Edge List
4. Implicit Graph

---

# 1. Adjacency Matrix

Store a 2D matrix where:

```text
matrix[u][v]
```

indicates whether an edge exists (or stores its weight).

Example:

```text
A ----- B
 \
  \
   C
```

Matrix:

```text
      A  B  C

A     0  1  1

B     1  0  0

C     1  0  0
```

For weighted graphs:

```text
      A  B  C

A     0  5  2

B     5  0  ∞

C     2  ∞  0
```

---

## Java Representation

```java
int[][] graph = new int[n][n];
```

---

## Complexity

Memory

```
O(V²)
```

Check if edge exists

```
O(1)
```

Iterate neighbours

```
O(V)
```

---

## Advantages

- Constant time edge lookup
- Extremely simple implementation
- Works well for dense graphs

---

## Disadvantages

- Very high memory usage
- Iterating neighbours is inefficient

---

## When to Use

- Dense graphs
- Floyd-Warshall
- Small graphs (typically ≤ 500 vertices)

---

# 2. Adjacency List

Instead of storing every possible edge,

store only the existing ones.

Example

```text
A ----- B
 \
  \
   C
```

Representation

```text
A : B, C

B : A

C : A
```

---

## Java Representation

Unweighted

```java
List<List<Integer>> graph = new ArrayList<>();
```

Weighted

```java
class Edge {
    int to;
    int weight;
}

List<List<Edge>> graph;
```

---

## Complexity

Memory

```
O(V + E)
```

Edge lookup

Worst case

```
O(degree)
```

Neighbour traversal

```
O(degree)
```

---

## Advantages

- Very memory efficient
- Fast neighbour traversal
- Standard interview representation

---

## Disadvantages

- Edge lookup isn't constant time
- Slightly more code

---

## When to Use

Almost always.

Used by

- DFS
- BFS
- Dijkstra
- Prim
- Tarjan
- Kosaraju
- Bellman-Ford (sometimes)
- Bipartite
- Bridges
- Articulation Points

---

# 3. Edge List

Simply store every edge.

Example

```text
A ----- B
 \
  \
   C
```

Representation

```text
(A,B)

(A,C)
```

Weighted

```text
(A,B,5)

(A,C,2)
```

---

## Java Representation

```java
class Edge {

    int from;

    int to;

    int weight;

}
```

```java
List<Edge> edges;
```

---

## Complexity

Memory

```
O(E)
```

Traverse all edges

```
O(E)
```

Neighbour lookup

```
O(E)
```

---

## Advantages

Very compact.

Perfect when algorithms iterate over edges rather than neighbours.

---

## Used By

Bellman-Ford

Kruskal

Many competitive programming problems

---

# 4. Implicit Graph

Some problems never explicitly give a graph.

Instead,

vertices are states.

Edges are generated dynamically.

Example:

Word Ladder

```
CAT

↓

BAT

↓

BAD
```

No graph is stored.

Neighbours are generated when required.

Other examples

- Sliding Puzzle
- Knight Moves
- Open Lock
- Maze
- Grid Problems

---

# Choosing the Right Representation

| Representation | Memory | Edge Lookup | Neighbour Traversal | Best For |
|---------------|--------|-------------|---------------------|----------|
| Matrix | O(V²) | O(1) | O(V) | Dense graphs |
| List | O(V+E) | O(degree) | O(degree) | Most graph algorithms |
| Edge List | O(E) | O(E) | O(E) | Bellman-Ford, Kruskal |
| Implicit | Depends | Generated | Generated | State-space search |

---

# Sparse vs Dense Graphs

This is an interview favourite.

---

## Sparse Graph

Very few edges.

```
E ≈ V
```

Example

```
1000 vertices

1200 edges
```

Use:

Adjacency List

---

## Dense Graph

Almost every pair of vertices has an edge.

```
E ≈ V²
```

Example

```
1000 vertices

900,000 edges
```

Adjacency Matrix becomes reasonable.

---

# Directed Graph Representation

Simply store outgoing edges.

Example

```text
A → B

A → C
```

Adjacency List

```text
A : B,C

B :

C :
```

Notice

B does not contain A.

---

# Weighted Graph Representation

Instead of storing only neighbours,

store

```
(destination, weight)
```

Example

```text
A --5--> B

A --2--> C
```

Adjacency List

```text
A

(B,5)

(C,2)
```

---

# Common Java Classes

Very common interview pattern

```java
class Edge {

    int to;

    int weight;

}
```

or

```java
class Pair {

    int vertex;

    int weight;

}
```

For Dijkstra,

PriorityQueue usually stores

```text
(vertex,

currentDistance)
```

For Prim,

PriorityQueue usually stores

```text
(vertex,

minimumEdgeWeight)
```

Although both use PriorityQueue,

the meaning of the stored value is different.

---

# Representation vs Algorithm

| Algorithm | Preferred Representation |
|-----------|-------------------------|
| DFS | Adjacency List |
| BFS | Adjacency List |
| Dijkstra | Adjacency List |
| Prim | Adjacency List |
| Tarjan | Adjacency List |
| Kosaraju | Adjacency List |
| Bridges | Adjacency List |
| Bellman-Ford | Edge List |
| Kruskal | Edge List |
| Floyd-Warshall | Adjacency Matrix |

---

# Interview Recognition

When reading a problem,

ask yourself:

### Do I repeatedly need neighbours?

Use

Adjacency List

---

### Do I repeatedly relax every edge?

Use

Edge List

---

### Do I need distance between every pair?

Use

Adjacency Matrix

---

### Is the graph hidden?

Generate neighbours on demand.

---

# Common Interview Mistakes

❌ Using an adjacency matrix for a sparse graph.

Memory becomes unnecessarily large.

---

❌ Using an edge list for DFS/BFS.

Neighbour lookup becomes O(E).

---

❌ Confusing edge list with adjacency list.

Edge List

```
(A,B)

(B,C)
```

Adjacency List

```
A : B

B : C
```

---

❌ Forgetting that directed graphs store only outgoing edges.

---

❌ Using a matrix for Dijkstra.

Neighbour iteration becomes O(V).

Priority Queue + Adjacency List is the standard implementation.

---

# Personal Learning Notes

During our lessons, a few implementation insights became important.

### 1. Same Data Structure, Different Meaning

One of the most useful observations was:

Both Prim's and Dijkstra's algorithms use:

```java
PriorityQueue<Pair>
```

However,

the value stored represents different invariants.

Dijkstra:

```
(vertex,

shortestDistanceFromSource)
```

Prim:

```
(vertex,

minimumEdgeWeightToJoinMST)
```

The data structure is identical.

The greedy criterion is different.

---

### 2. Duplicate Entries in PriorityQueue

Instead of searching and updating an existing element,

simply insert another entry.

Old entries are ignored when popped.

This keeps the implementation

```
O(log V)
```

instead of requiring an expensive search.

This approach is used in production-quality implementations of:

- Dijkstra
- Prim

---

### 3. Representation Should Match the Algorithm

One of the recurring themes throughout Graphs was:

> Algorithms don't dictate the representation.

The problem does.

For example:

- Bellman-Ford naturally iterates over all edges → Edge List.
- Floyd-Warshall updates distances between every pair → Matrix.
- DFS repeatedly explores neighbours → Adjacency List.

Recognizing this early simplifies both implementation and complexity analysis.

---

# Revision Summary

✔ Adjacency List is the default representation for almost every interview problem.

✔ Edge List is ideal for algorithms that process all edges repeatedly.

✔ Adjacency Matrix is suitable for dense graphs and all-pairs algorithms like Floyd-Warshall.

✔ Implicit graphs are common in puzzles and state-space search problems.

✔ Always choose the representation based on the operations the algorithm performs—not based on habit.


# 3. Depth First Search (DFS)

Depth First Search (DFS) is the most fundamental graph traversal algorithm.

It forms the foundation of several advanced graph algorithms, including:

- Connected Components
- Cycle Detection
- Topological Sort
- Kosaraju's Algorithm
- Tarjan's Algorithm
- Bridges
- Articulation Points

A deep understanding of DFS is essential before learning advanced graph algorithms.

---

# Intuition

Imagine exploring a maze.

At every junction:

> Keep walking until you cannot go any further.

Only then,

backtrack to the previous junction and explore another path.

That is exactly how DFS works.

Unlike BFS, which explores level by level, DFS explores one path completely before trying another.

---

# Example

```text
        A
      /   \
     B     C
    / \
   D   E
```

Possible DFS traversal:

```
A → B → D → E → C
```

Notice:

The traversal is **not unique**.

Different neighbour ordering can produce different valid DFS traversals.

---

# Recursive Definition

DFS naturally matches recursion.

Algorithm:

```
Visit current vertex

↓

Visit every unvisited neighbour recursively
```

Once every neighbour has been processed,

the recursion returns to the parent.

---

# Java Implementation

```java
void dfs(int u) {

    visited[u] = true;

    for (int v : graph.get(u)) {

        if (!visited[v])

            dfs(v);

    }

}
```

---

# Complexity

Every vertex is visited once.

Every edge is explored once.

Time

```
O(V + E)
```

Space

```
O(V)
```

Space includes:

- visited[]
- recursion stack

---

# Why visited[] is Necessary

Consider

```text
A ---- B
 \    /
  \  /
    C
```

Without visited[],

DFS becomes

```
A

↓

B

↓

C

↓

A

↓

B

↓

...
```

Infinite recursion.

Therefore,

every graph traversal must remember already visited vertices.

---

# DFS Tree

DFS does not merely visit vertices.

It constructs a **DFS Tree**.

Example

```text
A

/ \

B  C

|

D
```

One possible DFS tree

```text
A

|

B

|

D

|

C
```

The DFS tree records:

> **How each vertex was first discovered.**

This concept becomes extremely important in:

- Tarjan
- Bridges
- Articulation Points

---

# Recursive Backtracking

Suppose

```text
A

↓

B

↓

C
```

When C finishes,

execution returns to B.

After B finishes,

execution returns to A.

This process is called

**backtracking**.

Many graph algorithms perform useful work **during backtracking**, not while moving forward.

Examples:

- Topological Sort
- Tarjan
- Bridges
- Articulation Points

---

# DFS Call Stack

During recursion,

the JVM maintains a call stack.

Suppose

```text
A → B → D
```

Current recursion stack

```
Top

D

B

A
```

As recursion returns,

vertices are removed.

This stack represents the **active DFS path**.

Several algorithms depend on this idea.

---

# Recursive vs Iterative DFS

Recursive DFS uses the JVM stack.

Iterative DFS uses an explicit stack.

Example

```java
Stack<Integer> stack = new Stack<>();
```

Algorithm

```
Push source

While stack not empty

    Pop

    Visit

    Push neighbours
```

Both have identical complexity.

---

# When to Prefer Iterative DFS

Recursive DFS is simpler.

Iterative DFS is safer for:

- Very deep graphs
- Large recursion depth
- Platforms with small stack limits

Interview problems usually accept either.

---

# DFS Traversal Order

One important fact:

DFS order is **not unique**.

Example

```text
A

/ \

B  C
```

Possible traversals

```
A B C

A C B
```

Both are correct.

Only the neighbour ordering changes.

---

# Discovery Time

During DFS,

we can assign each vertex the time at which it is first discovered.

Example

```text
A = 1

B = 2

D = 3

C = 4
```

Stored in

```java
disc[]
```

Discovery times become essential for:

- Tarjan
- Bridges
- Articulation Points

---

# Finishing Time

Every recursive call eventually returns.

The moment DFS finishes processing a vertex,

it receives a finishing time.

Example

```
Discover

↓

Explore neighbours

↓

Finish
```

Finishing times are used by:

- Kosaraju
- Topological Sort (DFS)

---

# Tree Edges

A tree edge discovers a new vertex.

Example

```
A → B
```

where B was previously unvisited.

Tree edges form the DFS tree.

---

# Back Edges

A back edge points to an ancestor currently in the DFS stack.

Example

```text
A

↓

B

↓

C

↖
```

```
C → A
```

Back edges indicate a cycle.

This observation forms the basis of:

- Directed Cycle Detection
- Tarjan's Algorithm

---

# Forward and Cross Edges

In directed graphs,

additional edge types exist:

Forward Edge

```
Ancestor → Descendant
```

Cross Edge

```
Between different DFS branches
```

For interview preparation,

Tree and Back edges are significantly more important.

---

# DFS Invariants

A powerful way to understand DFS is through invariants.

At every moment,

the recursion stack represents

> **the current path being explored.**

Every advanced DFS algorithm modifies this invariant slightly.

Examples

Tarjan

```
Current SCC under construction
```

Cycle Detection

```
Current recursion path
```

Topological Sort

```
Current dependency exploration
```

Hierholzer

```
Current unfinished Eulerian walk
```

The traversal remains DFS.

Only the maintained information changes.

---

# Applications of DFS

## 1. Connected Components

Run DFS from every unvisited vertex.

Each DFS marks one connected component.

---

## 2. Cycle Detection

Directed

Use

```
visited[]

recursionStack[]
```

Undirected

Track parent vertex.

---

## 3. Topological Sort

Add vertices during backtracking.

Reverse the result.

---

## 4. Strongly Connected Components

Kosaraju

Tarjan

---

## 5. Bridges

Use

```
disc[]

low[]
```

---

## 6. Articulation Points

Again,

```
disc[]

low[]
```

---

# DFS vs BFS

| DFS | BFS |
|------|------|
| Stack / Recursion | Queue |
| Goes deep first | Goes level by level |
| May not find shortest path | Finds shortest path in unweighted graphs |
| Natural for recursion | Natural for level traversal |
| Basis of many advanced graph algorithms | Best for shortest path in unweighted graphs |

---

# Interview Recognition

If the problem asks:

- Explore everything
- Reachability
- Connected Components
- Cycles
- Topological ordering
- SCCs
- Bridges
- Articulation Points

Think:

```
DFS
```

---

# Common Interview Mistakes

❌ Forgetting visited[].

Leads to infinite recursion.

---

❌ Assuming DFS order is fixed.

Neighbour ordering changes traversal.

---

❌ Confusing recursion stack with visited[].

visited[]

```
Has this vertex ever been discovered?
```

recursionStack[]

```
Is this vertex currently in the active DFS path?
```

This distinction is essential for directed cycle detection and Tarjan's algorithm.

---

❌ Forgetting to restart DFS for disconnected graphs.

Always iterate over every vertex.

---

❌ Assuming recursion stack stores the DFS tree.

It stores only the **current path**, not the entire traversal history.

---

# Personal Learning Notes

Several concepts required extra attention during our discussions.

---

## 1. DFS Tree vs Original Graph

The DFS tree is **not** the graph itself.

It records only the edges used to discover new vertices.

Understanding this distinction became important when learning:

- Tree edges
- Back edges
- Tarjan
- Bridges

---

## 2. Back Edge Definition

Initially,

it was tempting to think:

> "Any edge to a visited vertex is a back edge."

Correct definition:

A back edge connects a vertex to one of its **ancestors currently in the DFS stack**.

Edges to already processed vertices are **not** back edges.

This distinction became essential while studying Tarjan.

---

## 3. DFS is a Framework

One of the biggest conceptual shifts during this module was realizing that:

DFS itself rarely solves the interview problem.

Instead,

algorithms build additional information on top of DFS.

Examples:

```
DFS

+

disc[]

↓

Tarjan
```

```
DFS

+

finish order

↓

Kosaraju
```

```
DFS

+

low[]

↓

Bridges
```

```
DFS

+

color[]

↓

Bipartite
```

The traversal remains identical.

Only the maintained invariant changes.

---

# Interview Tips

Whenever you encounter a graph problem,

ask:

> Can I solve this by performing DFS while maintaining one extra piece of information?

Surprisingly often,

the answer is **yes**.

This single question leads naturally to many advanced graph algorithms.

---

# Revision Summary

✔ DFS explores one path completely before backtracking.

✔ visited[] prevents revisiting vertices.

✔ DFS constructs a DFS tree.

✔ Discovery time and finishing time become important in advanced algorithms.

✔ Tree edges discover new vertices.

✔ Back edges connect to ancestors currently in the recursion stack.

✔ The recursion stack represents the active DFS path.

✔ DFS is not just a traversal—it is the foundation upon which many graph algorithms are built.

# 4. Breadth First Search (BFS)

Breadth First Search (BFS) is a graph traversal algorithm that explores the graph **level by level**.

Unlike DFS, which explores one path completely before backtracking, BFS explores all vertices at the current distance before moving further.

This simple property makes BFS the **shortest path algorithm for unweighted graphs**.

---

# Intuition

Imagine dropping a stone into a still pond.

The ripples spread outward in concentric circles.

```text
          Source

        Distance 0

            ●

         Distance 1

      ●    ●    ●

      Distance 2

   ●   ●   ●   ●
```

BFS behaves exactly like these ripples.

It visits vertices in increasing order of distance from the source.

---

# Example

```text
        A
      /   \
     B     C
    / \     \
   D   E     F
```

BFS traversal:

```
A

↓

B C

↓

D E F
```

Traversal order:

```
A → B → C → D → E → F
```

Notice that all vertices at distance 1 are visited before any vertex at distance 2.

---

# Why a Queue?

Suppose we visit

```text
A
```

Its neighbours become

```text
B

C
```

Which should be processed first?

The one discovered first.

That is exactly the behavior of a Queue.

```
First In

↓

First Out
```

Hence,

BFS naturally uses:

```java
Queue<Integer>
```

---

# Java Implementation

```java
Queue<Integer> queue = new LinkedList<>();

visited[source] = true;

queue.offer(source);

while (!queue.isEmpty()) {

    int u = queue.poll();

    for (int v : graph.get(u)) {

        if (!visited[v]) {

            visited[v] = true;

            queue.offer(v);

        }

    }

}
```

---

# Complexity

Every vertex is visited once.

Every edge is explored once.

Time

```
O(V + E)
```

Space

```
O(V)
```

Space includes:

- Queue
- visited[]

---

# Why visited[] is Set Before Enqueuing

This is a very common interview mistake.

Correct:

```java
visited[v] = true;

queue.offer(v);
```

Incorrect:

```java
queue.offer(v);

visited[v] = true;
```

Why?

Consider

```text
A

/ \

B  C

 \/

 D
```

If D is marked visited only when dequeued,

both B and C will enqueue D.

The queue now contains duplicates.

Marking visited **before enqueueing** guarantees each vertex enters the queue exactly once.

---

# BFS Levels

One of the most important properties of BFS.

Example

```text
        A
      /   \
     B     C
    / \
   D   E
```

Levels

```
Level 0

A

Level 1

B C

Level 2

D E
```

These levels correspond exactly to the shortest path distances in an unweighted graph.

---

# Why BFS Finds Shortest Paths

Suppose all edges have equal cost.

Every edge costs:

```
1
```

BFS first discovers all vertices:

```
1 edge away
```

Then

```
2 edges away
```

Then

```
3 edges away
```

Therefore,

the first time a vertex is visited,

the shortest path to it has already been found.

This is BFS's key invariant.

---

# Distance Array

Often,

instead of only storing visited,

we also maintain

```java
distance[]
```

Initialization

```java
distance[source] = 0;
```

Whenever

```java
u → v
```

is explored,

```java
distance[v] = distance[u] + 1;
```

---

# Parent Array

To reconstruct the actual shortest path,

maintain

```java
parent[]
```

Whenever

```java
u → v
```

is discovered,

```java
parent[v] = u;
```

After BFS,

backtrack using

```
parent[]
```

to reconstruct the path.

---

# Multi-Source BFS

Sometimes,

multiple starting vertices exist.

Example

```
🔥 Fire spreading

🏥 Multiple hospitals

🦠 Infection simulation
```

Instead of one source,

enqueue all sources initially.

Example

```java
for (int source : sources) {

    queue.offer(source);

    visited[source] = true;

}
```

The rest of the algorithm remains identical.

---

# BFS on Grids

Many interview problems are actually BFS problems disguised as matrices.

Example

```
0001

0100

0000
```

Each cell becomes a vertex.

Neighbours are generated dynamically.

Typical movement:

```java
int[] dr = {-1,1,0,0};

int[] dc = {0,0,-1,1};
```

This is an example of an **implicit graph**.

---

# BFS vs Dijkstra

One of the most important comparisons.

BFS assumes:

```
Every edge has identical cost.
```

Dijkstra assumes:

```
Edge costs may differ.

All costs are non-negative.
```

Because BFS ignores edge weights,

it may fail on weighted graphs.

Example

```text
A --100--> B

 \

  \

   1

    \

     C --1--> B
```

BFS prefers

```
A → B
```

because it has fewer edges.

Dijkstra prefers

```
A → C → B
```

because the total cost is smaller.

---

# BFS vs DFS

| BFS | DFS |
|------|------|
| Queue | Stack / Recursion |
| Level-by-level | One path at a time |
| Finds shortest path (unweighted) | Does not guarantee shortest path |
| Uses more memory on wide graphs | Uses more memory on deep graphs |
| Best for minimum number of edges | Best for exhaustive exploration |

---

# Applications

## 1. Shortest Path (Unweighted)

Classic application.

---

## 2. Level Order Traversal

Trees

Graphs

---

## 3. Connected Components

Alternative to DFS.

---

## 4. Bipartite Graph

Alternate colors level by level.

---

## 5. Multi-Source Problems

Examples

- Rotten Oranges
- Walls and Gates
- Fire Spread
- Zombie Infection

---

## 6. Minimum Moves Problems

Examples

- Knight Moves
- Snakes and Ladders
- Open Lock

---

# Interview Recognition

Think BFS when the problem asks:

- Minimum number of moves
- Minimum number of edges
- Fewest transformations
- Shortest path in an unweighted graph
- Level order traversal
- Spread over time
- Nearest source

---

# Common Interview Mistakes

❌ Using DFS for shortest path in an unweighted graph.

DFS does not guarantee minimum distance.

---

❌ Marking visited after dequeue.

Causes duplicate queue entries.

---

❌ Forgetting disconnected components.

Run BFS from every unvisited vertex if required.

---

❌ Using BFS on weighted graphs.

Switch to Dijkstra.

---

❌ Assuming BFS traversal order is unique.

Like DFS,

the neighbour ordering affects traversal order.

Only the distance guarantee remains unchanged.

---

# Personal Learning Notes

Several conceptual points from our discussions are worth remembering.

---

## 1. Why BFS Cannot Solve Weighted Shortest Paths

One of the important realizations during our sessions was:

BFS assumes

```
Every edge contributes equally.
```

It minimizes

```
Number of edges
```

not

```
Total edge weight.
```

This is why Dijkstra becomes necessary.

---

## 2. Queue Represents Increasing Distance

The queue is not chosen arbitrarily.

It guarantees:

```
Vertices are processed in increasing distance from the source.
```

This invariant is exactly why BFS finds shortest paths in unweighted graphs.

---

## 3. BFS and Graph Layers

Thinking of BFS in terms of **levels** rather than queue operations makes many interview problems easier.

Examples:

- Word Ladder
- Rotten Oranges
- Binary Matrix
- Open Lock

Each BFS layer represents one "step", "move", or "minute".

---

# How to Recognize BFS in Interviews

If the problem mentions:

- Fewest operations
- Minimum jumps
- Shortest transformation
- Least number of moves
- Spread over time
- Nearest object

Immediately ask yourself:

> "Can I model this as an unweighted graph?"

If yes,

BFS is often the correct solution.

---

# Revision Summary

✔ BFS explores the graph level by level.

✔ It uses a Queue because vertices must be processed in discovery order.

✔ The first time a vertex is visited, its shortest distance has already been determined (unweighted graphs).

✔ Mark vertices visited **before enqueueing** to avoid duplicates.

✔ BFS naturally computes levels and shortest paths in unweighted graphs.

✔ Many matrix and puzzle problems are simply BFS on an implicit graph.

✔ If edge weights differ, BFS is no longer sufficient—consider Dijkstra instead.


# 5. Connected Components

Connected Components are one of the most fundamental concepts in graph theory.

Many interview problems can be reduced to:

> "How many independent groups exist?"

or

> "Do these two vertices belong to the same group?"

Understanding connected components naturally leads to learning:

- DFS
- BFS
- Disjoint Set Union (Union-Find)

---

# Intuition

Imagine a social network.

```text
Alice ---- Bob ---- Charlie


David ---- Emma


Frank
```

Clearly,

there are three independent friend groups.

```
{Alice, Bob, Charlie}

{David, Emma}

{Frank}
```

These are the connected components.

---

# Definition

A **Connected Component** is a **maximal set of vertices** such that every vertex is reachable from every other vertex.

The word **maximal** is important.

It means:

> You cannot add another vertex to this set while preserving connectivity.

---

# Example

```text
A ---- B ---- C


D ---- E


F
```

Connected Components:

```
{A, B, C}

{D, E}

{F}
```

Number of connected components:

```
3
```

---

# Important Observation

Within one connected component,

every pair of vertices has a path.

Between two different components,

no path exists.

This observation is the basis for many interview questions.

---

# Finding Connected Components using DFS

The idea is extremely simple.

```
Pick any unvisited vertex.

↓

Run DFS.

↓

Everything visited belongs to one component.

↓

Repeat.
```

---

## Example

```text
A ---- B ---- C


D ---- E
```

Initially

```
visited = {}
```

Start DFS(A)

Visited

```
A B C
```

Component 1

Now continue scanning vertices.

D is still unvisited.

Run DFS(D)

Visited

```
D E
```

Component 2

Done.

---

# Java Implementation

```java
int components = 0;

for (int i = 0; i < V; i++) {

    if (!visited[i]) {

        dfs(i);

        components++;

    }

}
```

The same logic works with BFS.

---

# Complexity

DFS

```
O(V + E)
```

Every vertex is visited once.

Every edge is explored once.

---

# Connected Components using BFS

Exactly the same idea.

Replace

```
DFS
```

with

```
BFS
```

The complexity remains

```
O(V + E)
```

---

# Connected Components using DSU

Sometimes,

the graph is not explored through traversal.

Instead,

edges arrive one by one.

Example

```
(1,2)

(2,5)

(7,8)

(8,9)
```

Instead of repeatedly running DFS,

we perform

```
union(u,v)
```

for every edge.

Finally,

the number of distinct leaders represents the number of connected components.

This is significantly faster when connectivity changes dynamically.

---

# Comparison

| Method | Best When |
|---------|-----------|
| DFS | Static graph |
| BFS | Static graph |
| DSU | Edges added dynamically |

---

# Connected Components vs Strongly Connected Components

This distinction caused confusion for many students.

---

## Undirected Graph

Question:

```
Can every vertex reach every other vertex?
```

Since every edge works both ways,

reachability is naturally symmetric.

Connected Components are sufficient.

---

## Directed Graph

Reachability is directional.

Example

```text
A → B → C
```

A reaches C.

C cannot reach A.

Should these belong to the same component?

Not necessarily.

This leads to:

**Strongly Connected Components (SCCs)**.

---

# Typical Interview Problems

## 1. Number of Provinces

Count connected components.

---

## 2. Friend Circles

Each friend group is one component.

---

## 3. Number of Islands

Each island is one connected component.

The graph is implicit.

Vertices:

```
Land cells
```

Edges:

```
Adjacent land cells
```

---

## 4. Connecting Cities

Suppose we want to add roads.

If two cities already belong to the same connected component,

adding another road creates a cycle.

Otherwise,

the road merges two components.

This naturally leads to DSU.

---

# Recognizing Connected Component Problems

Typical phrases include:

- Number of groups
- Number of clusters
- Number of islands
- Friend circles
- Provinces
- Network groups
- Connected regions

Whenever you see these,

think:

```
Connected Components
```

---

# DFS vs DSU

Suppose someone asks

```
Are A and B connected?
```

If there is only one query,

DFS is perfectly fine.

Suppose there are

```
100,000
```

queries.

Running DFS each time becomes expensive.

DSU answers connectivity queries in nearly constant time after preprocessing.

---

# Dynamic Connectivity

Consider roads being built one by one.

Initially

```text
A   B   C
```

Road

```
A-B
```

Components

```
2
```

Road

```
B-C
```

Components

```
1
```

Road

```
A-C
```

Still

```
1
```

DSU naturally handles such updates.

DFS would require recomputation.

---

# Common Interview Mistakes

❌ Assuming the graph is connected.

Always verify.

---

❌ Running DFS only once.

Disconnected graphs require DFS/BFS from every unvisited vertex.

---

❌ Confusing Connected Components with SCCs.

Connected Components

```
Undirected
```

SCC

```
Directed
```

---

❌ Using DFS repeatedly for dynamic connectivity problems.

DSU is the better choice.

---

# Personal Learning Notes

These are observations from our discussions.

---

## 1. Counting Components using DSU

One of your answers was:

> "Number of connected components would be the number of distinct leaders after all edges have been added."

This is exactly correct.

It is one of the simplest and most elegant DSU applications.

---

## 2. Number of Islands

You immediately recognized that:

- Every land cell becomes a vertex.
- Adjacent land cells belong to the same connected component.

This is an important pattern.

Many matrix problems are simply graph problems on an implicit graph.

---

## 3. Connectivity Depends on Graph Type

One important realization during our sessions was:

For undirected graphs,

```
Connected
```

is well-defined.

For directed graphs,

the notion of connectivity depends on direction,

which naturally leads to Strongly Connected Components.

Keeping these concepts separate avoids many interview mistakes.

---

# Interview Tips

Whenever you encounter a graph problem,

ask yourself:

> "Am I trying to traverse the graph, or am I simply trying to identify groups?"

If the answer is

```
Groups
```

think:

- DFS
- BFS
- DSU

before considering more advanced algorithms.

---

# Related LeetCode Problems

### Easy

- 1971. Find if Path Exists in Graph
- 1791. Find Center of Star Graph

### Medium

- 547. Number of Provinces ⭐⭐⭐⭐⭐
- 200. Number of Islands ⭐⭐⭐⭐⭐
- 323. Number of Connected Components in an Undirected Graph (Premium)
- 1319. Number of Operations to Make Network Connected
- 947. Most Stones Removed with Same Row or Column (DSU)

### Hard

- 305. Number of Islands II (Dynamic Connectivity + DSU)

Recommended solving order:

1. Number of Provinces
2. Number of Islands
3. Number of Operations to Make Network Connected
4. Most Stones Removed with Same Row or Column
5. Number of Islands II

---

# Revision Summary

✔ A Connected Component is a maximal set of mutually reachable vertices in an **undirected** graph.

✔ Count components by running DFS/BFS from every unvisited vertex.

✔ DSU provides an efficient alternative when edges are added dynamically or when there are many connectivity queries.

✔ Connected Components and Strongly Connected Components solve different problems and should not be confused.

✔ Many interview problems involving "groups", "clusters", or "islands" are simply Connected Component problems in disguise.

# 6. Cycle Detection

Cycle detection is one of the most common graph interview topics.

However, the algorithm depends entirely on one question:

> **Is the graph directed or undirected?**

This distinction changes both the intuition and the implementation.

---

# What is a Cycle?

A cycle is a path that:

- Starts and ends at the same vertex.
- Does not repeat edges.
- (Simple cycle) does not repeat intermediate vertices.

Example:

```text
A
|\
| \
B--C
```

Cycle:

```
A → B → C → A
```

---

# Why Detect Cycles?

Cycle detection is useful in problems involving:

- Deadlocks
- Circular dependencies
- Build systems
- Course prerequisites
- Scheduling
- Graph validation
- Detecting redundant edges

---

# Undirected Graphs

## Intuition

Consider:

```text
A ----- B
```

When DFS visits B,

it naturally sees A again.

Is this a cycle?

No.

A is simply B's parent in the DFS tree.

Therefore, we must distinguish between:

- Returning to the parent
- Finding a genuine cycle

---

# Key Observation

During DFS,

if we encounter:

- an already visited vertex
- that is **not** the parent

then we have found a cycle.

---

# Algorithm

Maintain:

```java
visited[]
```

and pass

```java
parent
```

during recursion.

```java
boolean dfs(int u, int parent) {

    visited[u] = true;

    for (int v : graph.get(u)) {

        if (!visited[v]) {

            if (dfs(v, u))
                return true;

        } else if (v != parent) {

            return true;

        }

    }

    return false;

}
```

---

# Example

```text
A
|\
| \
B--C
```

DFS Tree:

```text
A

↓

B

↓

C
```

When C explores A,

A is visited,

and A is **not** C's parent.

Cycle detected.

---

# Why Parent is Necessary

Consider:

```text
A ----- B
```

DFS:

```text
A → B
```

B sees A again.

Without tracking the parent,

every undirected edge would falsely appear to be a cycle.

---

# Complexity

```
O(V + E)
```

---

# Directed Graphs

Directed graphs are different.

Parent tracking no longer works.

Example:

```text
A → B

↑   ↓

└── C
```

The edge

```
C → A
```

does not connect to the parent,

yet it forms a cycle.

Instead,

we need a different idea.

---

# The DFS Stack

While DFS runs,

some vertices are:

```
Visited
```

Some are:

```
Currently being explored
```

These are different concepts.

Example:

```
visited[]

Has this vertex ever been discovered?
```

```
recursionStack[]

Is this vertex currently in the active DFS path?
```

---

# The Key Observation

Suppose the recursion stack is:

```text
A

↓

B

↓

C
```

If C has an edge:

```text
C → A
```

then we have returned to an ancestor in the current DFS path.

That forms a directed cycle.

---

# Algorithm

Maintain:

```java
visited[]

recursionStack[]
```

Pseudo-code:

```java
boolean dfs(int u) {

    visited[u] = true;

    recursionStack[u] = true;

    for (int v : graph.get(u)) {

        if (!visited[v]) {

            if (dfs(v))
                return true;

        }

        else if (recursionStack[v]) {

            return true;

        }

    }

    recursionStack[u] = false;

    return false;

}
```

---

# Why Remove from recursionStack?

Suppose

```text
A → B → C
```

DFS finishes C.

C is still visited.

But C is **no longer in the active DFS path**.

Keeping it in recursionStack would create false cycles later.

---

# Back Edges

This leads to one of the most important DFS concepts.

A **Back Edge** is:

> An edge from a vertex to one of its ancestors currently in the DFS stack.

Example:

```text
A

↓

B

↓

C

↖
```

```
C → A
```

Back edges indicate cycles.

---

# Relationship Between DFS Edge Types

| Edge Type | Meaning |
|------------|---------|
| Tree Edge | Discovers a new vertex |
| Back Edge | Connects to an ancestor in the DFS stack |
| Forward Edge | Ancestor → Descendant (Directed graphs) |
| Cross Edge | Between different DFS branches |

For interview preparation,

Tree and Back edges are the most important.

---

# Cycle Detection using Kahn's Algorithm

For Directed Acyclic Graphs (DAGs),

another method exists.

Run Topological Sort using Kahn's Algorithm.

If:

```
Processed Vertices < Total Vertices
```

then

```
Cycle exists.
```

Reason:

Vertices in the cycle never reach in-degree zero.

This is often preferred in dependency problems.

---

# DFS vs Kahn

| DFS | Kahn |
|------|------|
| Uses recursion | Uses queue |
| Detects back edges | Detects remaining in-degree |
| General DFS approach | Topological sort based |

Both correctly detect cycles in directed graphs.

---

# DSU for Cycle Detection

Disjoint Set Union can also detect cycles,

but only for **undirected graphs**.

Algorithm:

For every edge

```
(u,v)
```

If

```
find(u) == find(v)
```

then

```
Cycle exists.
```

Otherwise,

perform

```
union(u,v)
```

---

# Choosing the Right Algorithm

| Graph Type | Algorithm |
|-------------|-----------|
| Undirected | DFS + Parent |
| Undirected | DSU |
| Directed | DFS + Recursion Stack |
| Directed | Kahn's Algorithm |

---

# Interview Recognition

Typical problem statements:

- Circular dependency
- Deadlock
- Course schedule
- Redundant connection
- Can all tasks finish?
- Infinite loop in dependency graph

Immediately think:

```
Cycle Detection
```

---

# Common Interview Mistakes

❌ Using the undirected parent trick on directed graphs.

It does **not** work.

---

❌ Confusing

```
visited[]
```

with

```
recursionStack[]
```

A vertex can remain visited long after it has left the current DFS path.

---

❌ Forgetting to remove vertices from recursionStack.

Produces false cycle detection.

---

❌ Assuming every visited neighbour indicates a cycle.

Only:

- Non-parent (undirected)
- Vertex currently in recursion stack (directed)

indicate cycles.

---

# Personal Learning Notes

Several important conceptual discussions happened during this topic.

---

## 1. Parent Trick Does Not Extend to Directed Graphs

One of the first insights we discussed was:

The parent trick works only because undirected edges are bidirectional.

Once edge direction matters,

the notion of "returning to the parent" is no longer sufficient.

This naturally motivates the recursion stack.

---

## 2. Visited vs Active Path

A key realization was:

After backtracking,

a vertex remains

```
visited
```

but leaves the active DFS path.

This distinction became crucial later in Tarjan's algorithm.

---

## 3. Back Edges

You correctly concluded that:

> A back edge connects a vertex to another vertex currently in the DFS stack.

This observation later became the foundation for understanding:

- Tarjan's Algorithm
- low[]
- Bridges
- Articulation Points

---

## 4. Cycle Detection as an Invariant

Instead of memorizing algorithms,

remember the invariant.

Undirected:

```
Visited neighbour

≠ Parent
```

Directed:

```
Visited neighbour

AND

Still in recursion stack
```

Thinking in terms of these invariants makes the implementations much easier to derive.

---

# Related LeetCode Problems

### Easy

- 141. Linked List Cycle (Conceptually similar)
- 1971. Find if Path Exists in Graph

### Medium

- 207. Course Schedule ⭐⭐⭐⭐⭐
- 210. Course Schedule II ⭐⭐⭐⭐⭐
- 684. Redundant Connection (DSU)
- 685. Redundant Connection II
- 802. Find Eventual Safe States

### Hard

- 269. Alien Dictionary (Cycle Detection + Topological Sort)

Recommended order:

1. Course Schedule
2. Course Schedule II
3. Redundant Connection
4. Find Eventual Safe States
5. Alien Dictionary

---

# Revision Summary

✔ Cycle detection depends on whether the graph is directed or undirected.

✔ Undirected graphs use **DFS + Parent** (or DSU).

✔ Directed graphs use **DFS + Recursion Stack** (or Kahn's Algorithm).

✔ A back edge indicates a cycle in directed graphs.

✔ `visited[]` and `recursionStack[]` represent different concepts and must not be confused.

✔ Understanding DFS invariants makes cycle detection easy to derive rather than memorize.


# 7. Topological Sort

Topological Sort is one of the most frequently asked graph algorithms in interviews.

Unlike DFS or BFS, it is **not a traversal algorithm**.

Instead, it produces a **valid ordering** of vertices such that every dependency is respected.

Typical interview problems include:

- Course Schedule
- Build Systems
- Task Scheduling
- Package Managers
- Compilation Order
- Dependency Resolution

---

# Motivation

Suppose you have the following prerequisites:

```text
DSA  →  System Design

Java →  Spring Boot

Spring Boot → Microservices
```

Can we study **Microservices** before learning **Spring Boot**?

No.

Dependencies impose an order.

Topological Sort computes one such valid order.

---

# Definition

A **Topological Ordering** is a linear ordering of vertices such that:

> For every directed edge

```
u → v
```

vertex

```
u
```

appears before

```
v
```

in the ordering.

---

# Important Restriction

Topological Sort exists **only for Directed Acyclic Graphs (DAGs).**

Why?

Suppose

```text
A → B → C → A
```

The ordering requires

```
A before B

B before C

C before A
```

Impossible.

Therefore,

A graph containing a cycle cannot have a valid topological ordering.

---

# Applications

Topological Sort appears whenever the problem contains:

- Prerequisites
- Dependencies
- Ordering constraints
- Scheduling
- Compilation
- Build systems
- Workflow execution

---

# Two Standard Algorithms

There are two standard approaches.

## 1. DFS Based

Uses:

- DFS
- Finishing order

---

## 2. Kahn's Algorithm

Uses:

- In-degree
- Queue

Both produce a valid topological ordering.

---

# DFS Based Topological Sort

## Intuition

Suppose

```text
A → B → C
```

Can A appear after C?

No.

Observe DFS.

```
Visit A

↓

Visit B

↓

Visit C

↓

Finish C

↓

Finish B

↓

Finish A
```

Notice something.

The finishing order is exactly the reverse of the desired answer.

Therefore,

Topological Sort can be obtained by:

```
DFS

↓

Store vertices when DFS finishes

↓

Reverse the result
```

---

# Java Skeleton

```java
void dfs(int u) {

    visited[u] = true;

    for (int v : graph.get(u)) {

        if (!visited[v])

            dfs(v);

    }

    stack.push(u);

}
```

Pop everything from the stack.

That is the topological order.

---

# Why Does It Work?

DFS guarantees:

A vertex finishes only after all its descendants have finished.

Therefore,

dependencies naturally appear before dependents after reversing.

---

# Kahn's Algorithm

This is often the preferred interview solution.

Instead of DFS,

think about prerequisites.

Suppose

```text
A → B
```

Initially,

B cannot be processed.

It still depends on A.

Only vertices with

```
in-degree = 0
```

have no remaining prerequisites.

These are immediately available.

---

# Algorithm

Step 1

Compute

```java
indegree[]
```

---

Step 2

Push every vertex with

```
indegree = 0
```

into a queue.

---

Step 3

Repeat

```
Pop vertex

↓

Add to answer

↓

Decrease indegree of neighbours

↓

If neighbour becomes zero

Push it
```

Continue until the queue becomes empty.

---

# Java Skeleton

```java
Queue<Integer> queue = new LinkedList<>();

for (int i = 0; i < V; i++) {

    if (indegree[i] == 0)

        queue.offer(i);

}

while (!queue.isEmpty()) {

    int u = queue.poll();

    answer.add(u);

    for (int v : graph.get(u)) {

        indegree[v]--;

        if (indegree[v] == 0)

            queue.offer(v);

    }

}
```

---

# Why Does Kahn's Algorithm Work?

The invariant is:

> Every vertex currently in the queue has **no unresolved dependencies**.

Whenever we remove one vertex,

some of its neighbours may now have all prerequisites satisfied.

Those neighbours become eligible.

The algorithm repeatedly removes "ready" vertices until none remain.

---

# Detecting Cycles

One beautiful property of Kahn's Algorithm.

Suppose:

```
Processed Vertices

<

Total Vertices
```

What happened?

Some vertices never reached

```
in-degree = 0
```

Why?

Because they depend on each other.

Exactly what happens in a cycle.

Therefore,

```
Processed != V

⇒ Cycle Exists
```

This is how many interview problems detect cycles.

---

# DFS vs Kahn

| DFS | Kahn |
|------|-------|
| Uses recursion | Uses queue |
| Uses finishing order | Uses in-degree |
| Reverse finishing order | Natural ordering |
| Detects cycle using recursion stack | Detects cycle using processed count |

---

# Multiple Valid Answers

Topological Sort is **not unique**.

Example

```text
A     B

 \   /

   C
```

Both are correct:

```
A B C
```

and

```
B A C
```

The only requirement is:

```
A before C

B before C
```

---

# Time Complexity

Both algorithms

```
O(V + E)
```

Every vertex processed once.

Every edge processed once.

---

# Choosing Between DFS and Kahn

| Situation | Preferred |
|-----------|-----------|
| Need explicit cycle detection | Kahn |
| Already using DFS | DFS |
| Dependency scheduling | Kahn |
| Reverse postorder reasoning | DFS |

In interviews,

either is acceptable unless specified.

---

# Relationship with DFS

Topological Sort is the first algorithm where

**backtracking** becomes useful.

Notice the progression.

DFS

```
Visit
```

Topological Sort

```
Finish
```

Kosaraju

```
Finish
```

Tarjan

```
Backtrack updates low[]
```

Bridges

```
Backtrack updates low[]
```

Articulation Points

```
Backtrack updates low[]
```

Many advanced graph algorithms derive their power from **what happens during DFS backtracking**, not during forward traversal.

---

# Common Interview Mistakes

❌ Applying Topological Sort to an undirected graph.

The concept is meaningful only for directed dependency graphs.

---

❌ Forgetting that cycles make topological ordering impossible.

---

❌ Assuming the answer is unique.

Usually,

many valid orders exist.

---

❌ Forgetting to compute initial in-degrees.

Kahn's Algorithm depends entirely on correct indegree computation.

---

# Personal Learning Notes

Several discussions during our lessons are worth remembering.

---

## 1. Why Kahn Uses In-degree

One of the most useful insights was:

A vertex with

```
in-degree = 0
```

has no remaining prerequisites.

This is why it is immediately safe to process.

Thinking in terms of "resolved dependencies" makes Kahn's Algorithm intuitive.

---

## 2. Cycle Detection Emerges Naturally

Rather than explicitly searching for cycles,

Kahn's Algorithm detects them indirectly.

If vertices remain unprocessed,

they must still depend on each other.

This is a beautiful example of solving two problems simultaneously.

---

## 3. DFS Finishing Order

A key realization was that DFS does **not** directly produce a topological ordering.

Instead,

the **reverse finishing order** satisfies all dependencies.

This idea later reappears in Kosaraju's Algorithm.

---

# Related LeetCode Problems

### Medium

- 207. Course Schedule ⭐⭐⭐⭐⭐
- 210. Course Schedule II ⭐⭐⭐⭐⭐
- 1136. Parallel Courses
- 1203. Sort Items by Groups Respecting Dependencies

### Hard

- 269. Alien Dictionary ⭐⭐⭐⭐⭐
- 444. Sequence Reconstruction

Recommended order:

1. Course Schedule
2. Course Schedule II
3. Parallel Courses
4. Alien Dictionary
5. Sequence Reconstruction

---

# Revision Summary

✔ Topological Sort applies only to **Directed Acyclic Graphs (DAGs).**

✔ It produces an ordering that respects every dependency.

✔ DFS solution uses **reverse finishing order**.

✔ Kahn's Algorithm repeatedly processes vertices with **in-degree = 0**.

✔ If Kahn processes fewer than **V** vertices, the graph contains a cycle.

✔ Multiple valid topological orderings may exist.

✔ Think "dependencies" whenever you encounter scheduling, prerequisites, or build-order problems.


# 8. Disjoint Set Union (Union-Find)

Disjoint Set Union (DSU), also known as **Union-Find**, is a data structure used to efficiently maintain **disjoint groups of elements**.

Unlike DFS or BFS, which explore a graph, DSU maintains information about **which vertices belong to the same connected component**.

It is one of the most frequently asked data structures in graph interviews.

---

# Motivation

Suppose we initially have five isolated cities.

```text
A    B    C    D    E
```

Roads are constructed one by one.

```
A - B

B - C

D - E
```

Now someone asks:

> Are A and C connected?

DFS can answer this.

But suppose there are:

- 100,000 cities
- 1,000,000 connectivity queries

Running DFS repeatedly becomes expensive.

Instead, we maintain connectivity information dynamically.

This is exactly what DSU does.

---

# Core Operations

DSU supports only two operations.

## 1. Find

```java
find(x)
```

Returns the representative (leader/root) of the set containing x.

Example

```text
A

|

B

|

C
```

```
find(A) = A

find(B) = A

find(C) = A
```

---

## 2. Union

```java
union(a, b)
```

Merges the two sets containing

```
a

and

b
```

If they already belong to the same set,

nothing changes.

---

# The Parent Representation

Internally,

every set is stored as a tree.

Initially

```text
A    B    C    D
```

Parent array

```
A → A

B → B

C → C

D → D
```

Every vertex is initially its own parent.

---

After

```
union(A,B)
```

One possible structure

```text
A

|

B
```

Parent

```
A → A

B → A
```

---

After

```
union(B,C)
```

```text
A

|

B

|

C
```

Parent

```
A → A

B → A

C → A
```

---

# Find Operation

The find operation climbs parent pointers until reaching the root.

Pseudo-code

```java
int find(int x) {

    if (parent[x] == x)

        return x;

    return find(parent[x]);

}
```

The returned root uniquely identifies the connected component.

---

# Detecting Connectivity

Two vertices belong to the same connected component iff

```java
find(u) == find(v)
```

This is the most important DSU property.

---

# Cycle Detection

Suppose we process edges one by one.

```
A-B

B-C

C-A
```

Process

```
A-B
```

Different leaders.

Union.

---

Process

```
B-C
```

Different leaders.

Union.

---

Process

```
C-A
```

Now

```
find(C) == find(A)
```

The edge connects vertices already in the same component.

Adding it creates a cycle.

This is exactly how DSU detects cycles in undirected graphs.

---

# Naive Union

Suppose

```
union(A,B)

union(B,C)

union(C,D)

union(D,E)
```

A poor implementation may create

```text
A

|

B

|

C

|

D

|

E
```

Now

```
find(E)
```

must traverse every vertex.

Complexity

```
O(N)
```

Clearly inefficient.

---

# Optimization 1 — Union by Rank

## Intuition

During our discussions, we asked:

> Which tree should become the parent?

You correctly answered:

> **Attach the smaller tree under the larger tree.**

Exactly.

The objective is to keep the overall tree height small.

Instead of always attaching arbitrarily,

attach the shallower tree beneath the deeper tree.

This optimization is called:

**Union by Rank**

(or Union by Size).

---

# Rank

Rank is an upper bound on tree height.

Example

```text
A

|

B
```

Rank

```
A = 1
```

When merging two trees,

the tree with smaller rank becomes the child.

If both ranks are equal,

choose either root

and increase its rank by one.

---

# Java Skeleton

```java
void union(int x, int y) {

    int px = find(x);

    int py = find(y);

    if (px == py)
        return;

    if (rank[px] < rank[py]) {

        parent[px] = py;

    } else if (rank[py] < rank[px]) {

        parent[py] = px;

    } else {

        parent[py] = px;

        rank[px]++;

    }

}
```

---

# Optimization 2 — Path Compression

Suppose

```text
A

|

B

|

C

|

D
```

Perform

```
find(D)
```

Without optimization

```
D

↓

C

↓

B

↓

A
```

Now imagine we update every visited node.

Result

```text
A

/ | \

B C D
```

Future finds become almost constant time.

This optimization is called

**Path Compression**.

---

# Java Implementation

```java
int find(int x) {

    if (parent[x] != x)

        parent[x] = find(parent[x]);

    return parent[x];

}
```

Notice

the recursive call updates the parent while returning.

---

# Why Union by Rank and Path Compression are Complementary

This was one of our most important conceptual discussions.

You observed:

> Union by Rank prevents trees from becoming tall during unions.

Correct.

You also observed:

> Path Compression repairs the paths discovered during find operations.

Exactly.

Think of them as solving two different problems.

### Union by Rank

Prevents bad trees from being created.

### Path Compression

Repairs whatever tall paths still exist.

Together,

they produce an almost flat tree.

---

# Complexity

Without optimizations

```
Find

O(N)
```

With both optimizations

```
Amortized

O(α(N))
```

where

```
α
```

is the inverse Ackermann function.

For every practical input,

```
α(N) ≤ 5
```

So DSU behaves almost like

```
O(1)
```

---

# Applications

## 1. Connected Components

Number of distinct leaders.

---

## 2. Cycle Detection

Undirected graphs.

---

## 3. Kruskal's Algorithm

The most famous application.

DSU efficiently determines whether adding an edge creates a cycle.

---

## 4. Dynamic Connectivity

Roads added one by one.

Friend requests.

Network connections.

---

## 5. Number of Islands II

Dynamic island creation.

---

# DFS vs DSU

| DFS | DSU |
|------|-----|
| Traverses graph | Maintains groups |
| O(V+E) traversal | Nearly O(1) operations |
| Static graph | Dynamic connectivity |
| Path discovery | Connectivity queries |

---

# Common Interview Mistakes

❌ Forgetting to call

```
find()
```

before

```
union()
```

Always merge leaders,

not arbitrary vertices.

---

❌ Forgetting path compression.

---

❌ Thinking rank equals exact height.

It is only an upper bound after path compression.

---

❌ Using DSU for directed graphs.

Standard DSU solves connectivity for **undirected graphs**.

---

# Personal Learning Notes

These are based on our discussions.

---

## 1. Union by Rank vs Path Compression

This was one of the strongest conceptual answers you gave.

Your summary was:

> Union by Rank prevents large trees from being created.

> Path Compression repairs the paths encountered during finds.

This is exactly the right mental model.

Do **not** think of them as competing optimizations.

They solve different problems.

---

## 2. Counting Connected Components

You correctly recognized that

> The number of distinct leaders after all unions equals the number of connected components.

This is one of the most elegant DSU applications.

---

## 3. Number of Islands

You immediately mapped the problem to DSU:

- Land cells become vertices.
- Adjacent land cells are unioned.
- Distinct leaders represent islands.

Recognizing implicit graphs like this is an important interview skill.

---

## 4. Detecting Redundant Edges

You correctly observed that

> If two vertices already belong to the same connected component, adding another edge between them creates a cycle.

This idea later became the foundation of Kruskal's Algorithm.

---

# Interview Recognition

Think DSU when the problem contains phrases like:

- Friend groups
- Network connectivity
- Merge groups
- Connected after operations
- Dynamic connectivity
- Redundant edge
- Number of provinces
- Number of islands (dynamic)
- Minimum Spanning Tree (Kruskal)

---

# Related LeetCode Problems

### Easy

- 1971. Find if Path Exists in Graph

### Medium

- 547. Number of Provinces ⭐⭐⭐⭐⭐
- 684. Redundant Connection ⭐⭐⭐⭐⭐
- 1319. Number of Operations to Make Network Connected ⭐⭐⭐⭐⭐
- 947. Most Stones Removed with Same Row or Column
- 721. Accounts Merge
- 990. Satisfiability of Equality Equations

### Hard

- 305. Number of Islands II ⭐⭐⭐⭐⭐
- 1579. Remove Max Number of Edges to Keep Graph Fully Traversable

Recommended order:

1. Number of Provinces
2. Redundant Connection
3. Number of Operations to Make Network Connected
4. Accounts Merge
5. Most Stones Removed
6. Number of Islands II
7. Remove Max Number of Edges...

---

# Revision Summary

✔ DSU maintains disjoint connected components efficiently.

✔ The two core operations are:

- Find
- Union

✔ Two vertices belong to the same component iff they have the same leader.

✔ Union by Rank keeps trees shallow.

✔ Path Compression flattens trees during find operations.

✔ The two optimizations are **complementary**, not interchangeable.

✔ With both optimizations, DSU operations run in nearly constant time.

✔ DSU is the standard solution for dynamic connectivity and Kruskal's Algorithm.


# 9. Dijkstra's Algorithm

Dijkstra's Algorithm solves the **Single Source Shortest Path (SSSP)** problem on graphs with **non-negative edge weights**.

Given:

- A weighted graph
- A source vertex

It computes the minimum distance from the source to every other reachable vertex.

It is one of the most important greedy algorithms in graph theory.

---

# Motivation

Suppose we have the following graph:

```text
        4
    A ------ B
    |        |
  1 |        | 2
    |        |
    C ------ D
        5
```

Question:

> What is the minimum cost to reach every vertex starting from A?

Notice that the shortest path is determined by the **sum of edge weights**, not by the number of edges.

This is why BFS is insufficient.

---

# Why BFS Fails

Consider:

```text
A --100--> B
 \
  \
   1
    \
     C --1--> B
```

BFS chooses

```
A → B
```

because it uses fewer edges.

Cost

```
100
```

The optimal path is

```
A → C → B
```

Cost

```
2
```

BFS minimizes:

```
Number of edges
```

Dijkstra minimizes:

```
Total edge weight
```

---

# The Greedy Insight

Suppose we know the current shortest distances.

```text
A = 0

B = 4

C = 1

D = 8
```

Which vertex should we process next?

Obviously,

```
C
```

because it currently has the smallest known distance.

This is the greedy choice.

---

# Core Invariant

This is the most important concept in Dijkstra.

> Once a vertex with the minimum tentative distance is removed from the Priority Queue,
>
> **its shortest distance is final.**

No future path can improve it.

This invariant is valid **only because edge weights are non-negative.**

---

# Why Negative Edges Break Dijkstra

Consider:

```text
A --2--> B

A --5--> C

C --(-4)--> B
```

Initially,

```
dist[B] = 2

dist[C] = 5
```

Dijkstra processes B first.

Later,

```
A → C → B
```

has cost

```
1
```

But B has already been finalized.

The greedy invariant is broken.

Notice:

There is **no negative cycle** here.

A **single negative edge** is sufficient to invalidate Dijkstra.

---

# Relaxation

Every shortest path algorithm relies on one operation:

**Relaxation**

Suppose

```
u → v
```

with weight

```
w
```

If

```
dist[u] + w
```

is smaller than

```
dist[v]
```

then

```
dist[v]
```

should be updated.

Formula

```java
if (dist[u] + w < dist[v]) {

    dist[v] = dist[u] + w;

}
```

This operation is called **edge relaxation**.

---

# Data Structures

During our lessons, we identified the three important data structures.

## 1. distance[]

Stores the shortest distance currently known.

---

## 2. PriorityQueue<Pair>

Stores

```
(vertex,

currentShortestDistance)
```

The queue is ordered by distance.

---

## 3. visited[]

Marks vertices whose shortest distance has already been finalized.

Some implementations omit this array and instead skip stale queue entries.

---

# Algorithm

Initialize

```
distance[source] = 0
```

All others

```
∞
```

Insert

```
(source,0)
```

into the Priority Queue.

While the queue is not empty:

1. Remove the minimum-distance vertex.
2. If already finalized, ignore it.
3. Relax every outgoing edge.
4. If a better distance is found, insert the updated pair into the Priority Queue.

---

# Java Skeleton

```java
PriorityQueue<Pair> pq =
    new PriorityQueue<>(
        Comparator.comparingInt(a -> a.distance)
    );

distance[source] = 0;

pq.offer(new Pair(source, 0));

while (!pq.isEmpty()) {

    Pair current = pq.poll();

    int u = current.vertex;

    if (visited[u])
        continue;

    visited[u] = true;

    for (Edge edge : graph.get(u)) {

        int v = edge.to;

        int weight = edge.weight;

        if (distance[u] + weight < distance[v]) {

            distance[v] = distance[u] + weight;

            pq.offer(new Pair(v, distance[v]));

        }

    }

}
```

---

# Duplicate Entries in the Priority Queue

One of the best implementation discussions we had.

Suppose

```
(B, 10)
```

already exists in the queue.

Later,

we discover

```
(B, 5)
```

Should we update the existing entry?

No.

Simply insert another one.

```
(B,10)

(B,5)
```

When

```
(B,10)
```

is eventually removed,

it is ignored because

```
visited[B]
```

is already true (or because its distance is stale).

---

# Why This Approach is Preferred

Searching for an existing element inside a heap costs

```
O(N)
```

Inserting a new element costs

```
O(log V)
```

Therefore,

allowing duplicates is both simpler and more efficient.

This is the standard implementation in interviews and production systems.

---

# Why Processing the Smallest Distance Works

Suppose

```
dist[C] = 3
```

and every edge has non-negative weight.

Any future path reaching C must first reach another vertex whose distance is at least

```
3
```

Adding a non-negative edge can only increase the total cost.

Therefore,

no shorter path to C can ever appear later.

This is exactly the greedy invariant.

---

# Complexity

Using:

- Adjacency List
- Binary Heap (PriorityQueue)

Time

```
O((V + E) log V)
```

Space

```
O(V)
```

---

# Dijkstra vs BFS

| BFS | Dijkstra |
|------|-----------|
| Unweighted graph | Weighted graph |
| Queue | Priority Queue |
| Minimizes number of edges | Minimizes total weight |
| O(V+E) | O((V+E) log V) |

---

# Dijkstra vs Bellman-Ford

| Dijkstra | Bellman-Ford |
|-----------|--------------|
| Greedy | Dynamic Programming / Relaxation |
| Non-negative weights only | Negative edges allowed |
| Faster | Slower |
| Cannot detect negative cycles | Detects negative cycles |

---

# Choosing the Next Vertex

This was one of the key intuitions from our lessons.

The Priority Queue is **not** selecting:

```
Minimum edge weight
```

It is selecting:

```
Minimum total distance from the source.
```

This distinction becomes important when comparing Dijkstra with Prim's Algorithm.

---

# Common Interview Mistakes

❌ Using Dijkstra when negative edges exist.

---

❌ Confusing

```
Edge Weight
```

with

```
Distance from Source.
```

---

❌ Trying to update an existing Priority Queue entry.

Insert another entry instead.

---

❌ Assuming BFS also works for weighted graphs.

---

❌ Forgetting to relax every outgoing edge.

---

# Personal Learning Notes

These are based on our discussions.

---

## 1. Why BFS Fails

You correctly identified:

> BFS assumes all edges are identical.

Exactly.

It optimizes

```
Number of edges
```

not

```
Total weight.
```

---

## 2. Why We Process the Smallest Distance

You reasoned:

> Processing the smallest current distance gives the best chance of reaching future vertices with the minimum total cost.

This intuition naturally leads to the greedy invariant.

---

## 3. Duplicate Priority Queue Entries

One of the strongest implementation insights you had was:

> Inserting a duplicate entry is cheaper than searching and updating an existing one.

This is the standard implementation strategy.

---

## 4. Difference Between Dijkstra and Prim

One of your best observations during our discussions was:

> Dijkstra chooses the vertex with the smallest **total distance from the source**.

> Prim chooses the edge with the smallest **weight connecting the current MST to a new vertex**.

Although both algorithms use a Priority Queue,

their greedy criteria are completely different.

---

## 5. Important Correction

Initially,

you explained Dijkstra's correctness using:

> "No negative cycles."

The more precise statement is:

> **No negative edge weights.**

A graph with one negative edge and **no negative cycle** can still break Dijkstra.

This distinction is worth remembering.

---

# Interview Recognition

Think Dijkstra when the problem mentions:

- Shortest path
- Minimum travel cost
- Minimum distance
- Cheapest route
- Weighted graph
- Non-negative weights

Immediately verify:

> Are all edge weights non-negative?

If not,

consider Bellman-Ford instead.

---

# Related LeetCode Problems

### Medium

- 743. Network Delay Time ⭐⭐⭐⭐⭐
- 1514. Path with Maximum Probability
- 1631. Path With Minimum Effort
- 1976. Number of Ways to Arrive at Destination

### Hard

- 778. Swim in Rising Water ⭐⭐⭐⭐⭐
- 882. Reachable Nodes In Subdivided Graph
- 1368. Minimum Cost to Make at Least One Valid Path in a Grid
- 2699. Modify Graph Edge Weights

Recommended order:

1. Network Delay Time
2. Path With Minimum Effort
3. Number of Ways to Arrive at Destination
4. Swim in Rising Water
5. Minimum Cost to Make at Least One Valid Path in a Grid

---

# Revision Summary

✔ Dijkstra solves the **Single Source Shortest Path** problem.

✔ It requires **non-negative edge weights**.

✔ The core operation is **edge relaxation**.

✔ The greedy invariant is:

> Once the smallest-distance vertex is processed, its distance is final.

✔ The Priority Queue stores

```
(vertex,

currentShortestDistance)
```

—not edge weights.

✔ Allow duplicate Priority Queue entries instead of updating existing ones.

✔ Dijkstra and Prim use the same data structure but optimize completely different quantities.


# 10. Bellman-Ford Algorithm

Bellman-Ford is a **Single Source Shortest Path (SSSP)** algorithm that works even when the graph contains **negative edge weights**.

Unlike Dijkstra, Bellman-Ford does **not** rely on a greedy strategy.

Instead, it repeatedly improves the current shortest paths until they converge.

It also has one major advantage over Dijkstra:

> It can detect **negative weight cycles**.

---

# Motivation

When studying Dijkstra, we proved an important invariant:

> Once the vertex with the minimum tentative distance is removed from the Priority Queue, its shortest distance is final.

This greedy property completely depends on one assumption:

> **Every edge weight is non-negative.**

If this assumption breaks,

the algorithm breaks.

---

# Why Dijkstra Fails

Consider

```text
A --2--> B

A --5--> C

C --(-4)--> B
```

Initially,

```
dist[B] = 2

dist[C] = 5
```

Dijkstra finalizes

```
B
```

first.

Later,

```
A → C → B
```

has cost

```
1
```

which is shorter.

But B has already been finalized.

The greedy invariant fails.

Notice:

There is **no negative cycle**.

A **single negative edge** is enough.

---

# The New Idea

Instead of finalizing vertices,

Bellman-Ford repeatedly asks:

> Can this edge improve the shortest path?

For every edge

```
u → v
```

perform

```java
if (dist[u] + weight < dist[v]) {

    dist[v] = dist[u] + weight;

}
```

This operation is called

**Relaxation**.

Unlike Dijkstra,

Bellman-Ford performs relaxation on **every edge repeatedly**.

---

# The Key Insight

Suppose the shortest path is

```text
A → B → C → D
```

The path contains

```
3 edges
```

Initially,

only

```
A
```

knows its correct distance.

---

After one pass

```
A → B
```

becomes correct.

---

After two passes

```
A → B → C
```

becomes correct.

---

After three passes

```
A → B → C → D
```

becomes correct.

Shortest path information propagates **one edge further** in every pass.

This is the central idea behind Bellman-Ford.

---

# Why Exactly V−1 Passes?

This is the most important correctness proof.

A shortest path never contains repeated vertices.

Otherwise,

removing the repeated cycle would produce a shorter path.

Therefore,

a shortest path is always a **simple path**.

A simple path with

```
V vertices
```

contains at most

```
V−1 edges.
```

Since each pass propagates information across one more edge,

after

```
V−1
```

passes,

every shortest path has been fully propagated.

---

# Core Invariant

After the

```
k-th
```

pass,

Bellman-Ford has correctly computed all shortest paths containing at most

```
k edges.
```

This invariant completely explains the algorithm.

---

# Algorithm

Initialize

```
dist[source] = 0
```

All others

```
∞
```

Repeat

```
V−1
```

times

```
For every edge

Relax it
```

Finally,

perform one additional pass.

If any edge can still be relaxed,

a negative cycle exists.

---

# Java Skeleton

```java
distance[source] = 0;

for (int i = 1; i <= V - 1; i++) {

    for (Edge edge : edges) {

        if (distance[edge.from] != INF &&
            distance[edge.from] + edge.weight < distance[edge.to]) {

            distance[edge.to] =
                distance[edge.from] + edge.weight;

        }

    }

}

// Negative cycle detection

for (Edge edge : edges) {

    if (distance[edge.from] != INF &&
        distance[edge.from] + edge.weight < distance[edge.to]) {

        // Negative cycle exists

    }

}
```

---

# Why Does One More Relaxation Detect a Negative Cycle?

Suppose

```
V−1
```

passes have already completed.

Every shortest simple path has already been computed.

If another relaxation still succeeds,

the new path must contain more than

```
V−1
```

edges.

Such a path must repeat a vertex.

Repeated vertices imply a cycle.

If using that cycle decreases the total distance,

the cycle must have

```
Negative Total Weight.
```

This is why the extra pass detects negative cycles.

---

# Reachable vs Unreachable Negative Cycles

Bellman-Ford only reports negative cycles that are

**reachable from the source.**

Example

```text
Component 1

A → B


Component 2

X → Y → Z → X
```

Running Bellman-Ford from

```
A
```

does not detect the cycle in

```
Component 2
```

because those vertices are never reached.

---

# Detecting Any Negative Cycle

If we need to detect a negative cycle anywhere in the graph,

a common trick is to add a

**Super Source**

connected to every vertex using zero-weight edges.

Now every component becomes reachable,

and Bellman-Ford detects any negative cycle in the graph.

---

# Bellman-Ford vs Dijkstra

| Dijkstra | Bellman-Ford |
|-----------|--------------|
| Greedy | Dynamic Programming / Relaxation |
| Non-negative edges only | Negative edges allowed |
| Faster | Slower |
| Cannot detect negative cycles | Detects negative cycles |
| Priority Queue | Edge List |

---

# Bellman-Ford vs BFS

| BFS | Bellman-Ford |
|------|--------------|
| Unweighted graphs | Weighted graphs |
| Level traversal | Edge relaxation |
| O(V+E) | O(VE) |

---

# Why Bellman-Ford Uses an Edge List

Unlike DFS or Dijkstra,

Bellman-Ford does **not** repeatedly explore neighbours.

Instead,

every iteration processes

```
Every Edge.
```

An Edge List naturally supports this operation.

---

# Complexity

Time

```
O(VE)
```

Space

```
O(V)
```

---

# Common Interview Mistakes

❌ Thinking Bellman-Ford is only for negative edges.

It also works for positive-weight graphs.

It is simply slower.

---

❌ Confusing

```
Negative Edge
```

with

```
Negative Cycle.
```

Negative edges are perfectly valid.

Negative cycles make shortest paths undefined.

---

❌ Forgetting the extra relaxation pass.

Without it,

negative cycles cannot be detected.

---

❌ Assuming Bellman-Ford detects every negative cycle.

It only detects those reachable from the chosen source.

---

# Personal Learning Notes

Several important discussions happened during this topic.

---

## 1. Why Not Stop After One Pass?

One of your observations was:

> The order of edge processing may not propagate shortest paths completely in one iteration.

Exactly.

Bellman-Ford makes **no assumptions** about the order in which edges appear.

Multiple passes guarantee complete propagation.

---

## 2. Why V−1 Passes?

You correctly reasoned that

> A shortest path contains at most V−1 edges.

The more formal invariant is:

> After the k-th pass, all shortest paths using at most k edges have been computed.

This is the proof interviewers usually expect.

---

## 3. Reachable Negative Cycles

You correctly pointed out that

> A negative cycle in another connected component should not be reported.

This is an important interview detail.

Bellman-Ford computes shortest paths **from one source**.

Unreachable vertices cannot affect those paths.

---

## 4. Why Do We Still Use Dijkstra?

One interview question we discussed was:

> If Bellman-Ford is more general, why not always use it?

The answer is **not merely because Dijkstra is faster**.

The real reason is:

Dijkstra exploits a greedy invariant that allows vertices to be finalized once.

Bellman-Ford cannot make this assumption and therefore repeatedly relaxes all edges.

---

# Interview Recognition

Think Bellman-Ford when the problem mentions:

- Negative edge weights
- Currency exchange
- Arbitrage
- Negative cycle detection
- Shortest path with negative edges

Immediately ask:

> Are negative edge weights allowed?

If yes,

Bellman-Ford is usually the first algorithm to consider.

---

# Related LeetCode Problems

### Medium

- 787. Cheapest Flights Within K Stops ⭐⭐⭐⭐ (Bellman-Ford / DP)
- 743. Network Delay Time (Compare with Dijkstra)
- 1928. Minimum Cost to Reach Destination in Time

### Hard

- 1334. Find the City With the Smallest Number of Neighbors (Compare approaches)
- Custom Bellman-Ford implementations are more common in interviews than LeetCode.

Recommended order:

1. Cheapest Flights Within K Stops
2. Minimum Cost to Reach Destination in Time
3. Compare solutions with Dijkstra on Network Delay Time

---

# Revision Summary

✔ Bellman-Ford solves the **Single Source Shortest Path** problem.

✔ It supports **negative edge weights**.

✔ The algorithm repeatedly performs **edge relaxation**.

✔ After the k-th pass, shortest paths using at most k edges are correct.

✔ **V−1** passes are sufficient because every shortest simple path contains at most V−1 edges.

✔ One additional successful relaxation implies a **negative weight cycle**.

✔ Bellman-Ford detects only **reachable** negative cycles.

✔ Unlike Dijkstra, Bellman-Ford does **not** rely on a greedy invariant.


# 11. Floyd-Warshall Algorithm

Floyd-Warshall solves the **All Pairs Shortest Path (APSP)** problem.

Unlike Dijkstra and Bellman-Ford, which answer:

> "What is the shortest path from one source to every other vertex?"

Floyd-Warshall answers:

> "What is the shortest path between every pair of vertices?"

It is also one of the earliest graph algorithms that is fundamentally based on **Dynamic Programming**.

---

# Motivation

Suppose you are building Google Maps.

Users may ask:

```
Pune → Mumbai

Delhi → Jaipur

Bangalore → Chennai
```

The source city is not fixed.

Running Dijkstra every time a user asks a query is possible, but can become expensive if many queries are expected.

Instead, compute every shortest path once.

This is exactly the purpose of Floyd-Warshall.

---

# The Naive Solution

Suppose the graph has

```
V
```

vertices.

Run Dijkstra

```
V
```

times.

Complexity

```
O(V(E log V))
```

Can we do better?

For dense graphs,

yes.

---

# The Dynamic Programming Insight

Forget graphs for a moment.

Suppose we want the shortest path

```
A → D
```

Possible paths are:

```
A → D

A → B → D

A → C → D

A → B → C → D
```

Notice something.

Every shortest path is composed of **smaller shortest paths**.

This is exactly the property Dynamic Programming exploits.

---

# DP State

Define

```java
dist[i][j]
```

Meaning

> Current shortest distance from vertex

```
i
```

to

```
j
```

Initially

- Direct edge → edge weight
- No edge → ∞
- Same vertex → 0

Example

```text
      A   B   C

A     0   5   ∞

B     ∞   0   2

C     1   ∞   0
```

This matrix is the DP table.

---

# The Core Idea

Suppose we ask:

Can the shortest path

```
A → C
```

be improved by passing through

```
B
```

Two possibilities exist.

Without B

```
A → C
```

With B

```
A → B → C
```

Choose the better one.

Transition

```java
dist[A][C] = Math.min(
    dist[A][C],
    dist[A][B] + dist[B][C]
);
```

This is the heart of Floyd-Warshall.

---

# General DP Transition

Generalizing,

allow every vertex

```
k
```

to become an intermediate vertex.

Transition

```java
dist[i][j] = Math.min(
    dist[i][j],
    dist[i][k] + dist[k][j]
);
```

Every shortest path either:

- does not use

```
k
```

or

- uses

```
k
```

exactly once as the highest-numbered allowed intermediate.

---

# The DP State Interpretation

This is the conceptual understanding we developed during our lessons.

Think of the DP state as:

> **Shortest distance from i to j using only the first k vertices as intermediate vertices.**

Initially

```
k = -1
```

No intermediate vertices allowed.

Only direct edges.

Then

```
k = 0
```

Vertex 0 may now appear in the path.

Then

```
k = 1
```

Vertices

```
0,1
```

may appear.

Eventually,

all vertices become available as intermediates.

---

# Why Must k Be the Outermost Loop?

This was one of the most important conceptual discussions.

The invariant is:

> After iteration

```
k
```

every

```
dist[i][j]
```

is correct using only vertices

```
{0...k}
```

as intermediate vertices.

If

```
k
```

were not the outermost loop,

this invariant would be violated because partially updated states would mix together.

This is a classic Dynamic Programming dependency ordering.

---

# Why Does the Transition Work?

Suppose the optimal path uses

```
k
```

Then the path naturally splits into:

```
i → k
```

and

```
k → j
```

Both of these are themselves shortest paths using only the previous intermediate vertices.

Therefore,

all possible paths such as

```
i → a → b → k → c → d → j
```

are already summarized by

```
dist[i][k]
```

and

```
dist[k][j]
```

This is the optimal substructure property.

---

# Algorithm

```java
for (int k = 0; k < V; k++) {

    for (int i = 0; i < V; i++) {

        for (int j = 0; j < V; j++) {

            if (dist[i][k] != INF &&
                dist[k][j] != INF) {

                dist[i][j] = Math.min(
                    dist[i][j],
                    dist[i][k] + dist[k][j]
                );

            }

        }

    }

}
```

Notice the

```
INF
```

checks.

Without them,

adding

```
INF + weight
```

may overflow.

---

# Negative Edge Weights

Floyd-Warshall supports

```
Negative Edge Weights
```

just like Bellman-Ford.

However,

negative cycles still make shortest paths undefined.

---

# Detecting Negative Cycles

After the algorithm finishes,

check

```java
dist[i][i]
```

If

```
dist[i][i] < 0
```

then

vertex

```
i
```

lies on (or can return through) a negative cycle.

Why?

A shortest path from a vertex to itself should always cost

```
0
```

A negative value means the path can repeatedly reduce its own cost.

---

# Complexity

Three nested loops.

Time

```
O(V³)
```

Space

```
O(V²)
```

---

# Why Floyd-Warshall Uses an Adjacency Matrix

Unlike Dijkstra,

the algorithm repeatedly updates

```
Every Pair
```

of vertices.

A matrix naturally supports constant-time access to

```
dist[i][j]
```

An adjacency list would make these updates inefficient.

---

# Floyd-Warshall vs Bellman-Ford

| Floyd-Warshall | Bellman-Ford |
|----------------|--------------|
| All-pairs shortest path | Single-source shortest path |
| Dynamic Programming | Edge Relaxation |
| O(V³) | O(VE) |
| Matrix | Edge List |

---

# Floyd-Warshall vs Dijkstra

| Floyd-Warshall | Dijkstra |
|----------------|-----------|
| All-pairs | Single-source |
| Matrix | Priority Queue |
| O(V³) | O((V+E)logV) |
| Supports negative edges | Requires non-negative edges |

---

# Dense vs Sparse Graphs

Suppose

```
V = 10,000

E = 20,000
```

The graph is sparse.

Running Floyd-Warshall

```
O(V³)
```

is completely impractical.

Repeated Dijkstra is far more efficient.

Conversely,

for dense graphs,

Floyd-Warshall becomes competitive.

---

# Common Interview Mistakes

❌ Forgetting that Floyd-Warshall is a Dynamic Programming algorithm.

---

❌ Changing the loop order.

The outermost loop **must** be

```
k
```

---

❌ Forgetting

```
dist[i][i] = 0
```

during initialization.

---

❌ Forgetting

```
INF
```

checks before addition.

---

❌ Using Floyd-Warshall on extremely sparse graphs.

Repeated Dijkstra is often better.

---

# Personal Learning Notes

These are based on our discussions.

---

## 1. Dynamic Programming Perspective

One of the biggest conceptual shifts during this lesson was realizing that Floyd-Warshall is **not** a graph traversal algorithm.

It is a Dynamic Programming algorithm operating on graph distances.

---

## 2. Why k Must Be the Outermost Loop

You correctly reasoned that

```
k
```

represents the set of vertices currently allowed as intermediates.

This is the DP state.

Keeping

```
k
```

outermost preserves the correctness of state transitions.

---

## 3. Negative Cycle Detection

You correctly explained that

> If

```
dist[i][i] < 0
```

then reaching the same vertex has negative cost,

which is only possible through a negative cycle.

---

## 4. Sparse Graphs

When asked whether to use Floyd-Warshall for

```
10,000 vertices

20,000 edges
```

you correctly chose repeated Dijkstra.

This demonstrates an important interview skill:

Choosing algorithms based on graph density.

---

# Interview Recognition

Think Floyd-Warshall when the problem asks:

- Shortest path between every pair
- Distance matrix
- Multiple shortest-path queries
- Dense weighted graph

Immediately ask:

> Do I need distances between **all pairs** of vertices?

If yes,

Floyd-Warshall becomes a strong candidate.

---

# Related LeetCode Problems

Although Floyd-Warshall appears less frequently than Dijkstra, the following problems are excellent practice.

### Medium

- 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance ⭐⭐⭐⭐⭐
- 1462. Course Schedule IV (Transitive Closure variant)

### Hard

- 2976. Minimum Cost to Convert String I (Floyd-Warshall)
- 2642. Design Graph With Shortest Path Calculator (Compare approaches)

Recommended order:

1. Find the City With the Smallest Number of Neighbors
2. Course Schedule IV
3. Minimum Cost to Convert String I

---

# Revision Summary

✔ Floyd-Warshall solves the **All Pairs Shortest Path** problem.

✔ It is fundamentally a **Dynamic Programming** algorithm.

✔ DP State:

> Shortest distance from

```
i
```

to

```
j
```

using only the first

```
k
```

vertices as intermediates.

✔ Transition:

```java
dist[i][j] = Math.min(
    dist[i][j],
    dist[i][k] + dist[k][j]
);
```

✔ The outermost loop must iterate over

```
k
```

to preserve DP correctness.

✔ Supports negative edge weights.

✔ Detects negative cycles using

```
dist[i][i] < 0
```

✔ Best suited for **all-pairs shortest path** problems, especially on dense graphs.


# 12. Minimum Spanning Trees (MST)

A **Minimum Spanning Tree (MST)** connects every vertex in a **connected, undirected, weighted graph** while minimizing the **total weight of the selected edges**.

Unlike shortest path algorithms, MST algorithms are **not concerned with the distance between any two particular vertices**.

Instead, they optimize the cost of connecting the entire graph.

This section covers:

- Minimum Spanning Tree intuition
- Kruskal's Algorithm
- Prim's Algorithm
- Cut Property
- Correctness
- Comparison with Shortest Path algorithms

---

# Motivation

Suppose a telecom company wants to connect cities using optical fiber.

Possible connections:

```text
      4
A -------- B
| \         |
|  \        |2
3   1       |
|    \      |
C-----D-----E
     5
```

Question:

> How can every city be connected using the **minimum total cable length**?

Notice that we are **not** asking:

- Shortest route between two cities.
- Cheapest path from one city.

We simply want **every city to become connected as cheaply as possible.**

---

# What is a Spanning Tree?

A spanning tree is a subgraph that:

✔ Includes every vertex.

✔ Is connected.

✔ Contains **no cycles**.

---

## Properties

If a graph contains

```
N vertices
```

then every spanning tree contains exactly

```
N - 1 edges.
```

This is one of the most important interview facts.

---

# Why Exactly N−1 Edges?

A tree satisfies:

- Connected
- No cycles

Suppose

```
Edges < N−1
```

The graph cannot be connected.

Suppose

```
Edges > N−1
```

A cycle must exist.

Therefore,

every spanning tree contains exactly

```
N−1
```

edges.

---

# Minimum Spanning Tree

Among all possible spanning trees,

choose the one having the **minimum total edge weight**.

Example

```text
      4
A -------- B
| \         |
|  \        |2
3   1       |
|    \      |
C-----D-----E
     5
```

One spanning tree

```
Weight = 15
```

Another

```
Weight = 11
```

The lighter one is the MST.

---

# Properties of MST

✔ Connects every vertex.

✔ Contains no cycles.

✔ Uses exactly

```
N−1
```

edges.

✔ Has minimum possible total weight.

---

# Important Observation

An MST is **not necessarily unique**.

If multiple edges have equal weights,

multiple valid MSTs may exist.

However,

their total weight is always the same.

---

# The Cut Property

This is the single most important theorem behind MST algorithms.

---

## Definition of a Cut

Imagine dividing the graph into two groups.

```text
A  B

---------

C  D  E
```

Every edge crossing this partition belongs to the cut.

---

## Cut Property

> For any cut,
>
> the **minimum-weight edge crossing the cut is always safe to include in the MST.**

This theorem is the foundation of both:

- Kruskal's Algorithm
- Prim's Algorithm

---

# Why Does the Cut Property Work?

Suppose the smallest edge crossing the cut is **not** included.

Then some heavier edge must connect those two components.

Replacing that heavier edge with the lighter one:

- keeps the graph connected,
- does not create a cycle,
- reduces the total weight.

Contradiction.

Therefore,

the lightest edge crossing any cut must belong to **at least one** MST.

---

# Kruskal's Algorithm

## Intuition

Instead of growing one connected tree,

Kruskal grows **many small trees simultaneously**.

Initially,

every vertex is its own connected component.

```text
A   B   C   D
```

Repeatedly choose the smallest edge.

If it connects two different components,

accept it.

Otherwise,

discard it.

Eventually,

all components merge into one MST.

---

# Algorithm

1. Sort all edges in ascending order.
2. Process edges from smallest to largest.
3. If the endpoints belong to different DSU components:
   - Add the edge to the MST.
   - Union the components.
4. Otherwise,
   skip the edge.
5. Stop after selecting

```
N−1
```

edges.

---

# Java Skeleton

```java
Collections.sort(edges);

DSU dsu = new DSU(V);

int mstWeight = 0;

for (Edge edge : edges) {

    if (dsu.find(edge.u) != dsu.find(edge.v)) {

        dsu.union(edge.u, edge.v);

        mstWeight += edge.weight;

    }

}
```

---

# Why DSU?

Suppose we choose an edge.

How do we know whether it creates a cycle?

Exactly the same way we discussed during DSU.

If

```java
find(u) == find(v)
```

both vertices already belong to the same connected component.

Adding the edge creates a cycle.

Otherwise,

the edge safely connects two different components.

---

# Complexity

Sorting

```
O(E log E)
```

DSU Operations

```
O(E α(V))
```

Overall

```
O(E log E)
```

Sorting dominates.

---

# Prim's Algorithm

## Intuition

Prim grows **one tree**.

Initially,

only one vertex belongs to the MST.

```text
A
```

Repeatedly choose the **minimum-weight edge** that connects

```
Current MST

↓

Outside Vertex
```

This continues until every vertex has been included.

---

# Data Structures

One of the implementation discussions we had.

Maintain:

```java
PriorityQueue<Pair>

key[]

inMST[]
```

where

```
key[v]
```

stores

> Minimum edge weight currently known to connect vertex

```
v
```

to the MST.

---

# Algorithm

Choose any starting vertex.

Initialize

```
key[start] = 0
```

Repeatedly:

1. Remove the vertex with the smallest key.
2. Mark it as part of the MST.
3. Relax every outgoing edge.

If

```
edgeWeight < key[v]
```

update

```
key[v]
```

and push a new Priority Queue entry.

---

# Java Skeleton

```java
PriorityQueue<Pair> pq = new PriorityQueue<>();

key[start] = 0;

pq.offer(new Pair(start, 0));

while (!pq.isEmpty()) {

    Pair current = pq.poll();

    int u = current.vertex;

    if (inMST[u])
        continue;

    inMST[u] = true;

    for (Edge edge : graph.get(u)) {

        int v = edge.to;

        if (!inMST[v] &&
            edge.weight < key[v]) {

            key[v] = edge.weight;

            pq.offer(new Pair(v, key[v]));

        }

    }

}
```

---

# Why Prim Works

Prim repeatedly applies the **Cut Property**.

At every step,

the current MST defines a cut:

```
Vertices Inside MST

↓

Vertices Outside MST
```

The smallest edge crossing that cut is always safe.

Therefore,

every greedy choice preserves optimality.

---

# Why Duplicate Priority Queue Entries?

Exactly the same implementation trick as Dijkstra.

Instead of updating an existing queue entry,

simply insert another.

When an outdated entry is removed,

ignore it because

```
inMST[u]
```

is already true.

Searching inside a heap would be slower.

---

# Prim vs Kruskal

| Prim | Kruskal |
|-------|----------|
| Grows one tree | Grows many components |
| Priority Queue | Sorting + DSU |
| Chooses smallest connecting edge | Chooses globally smallest edge |
| Best for dense graphs | Best for sparse graphs |

---

# Prim vs Dijkstra

This was one of the biggest conceptual discussions during our lessons.

Although both algorithms use:

```java
PriorityQueue<Pair>
```

they optimize completely different quantities.

---

## Dijkstra

Priority Queue stores

```
(vertex,

shortestDistanceFromSource)
```

The greedy choice minimizes

```
Total path cost.
```

---

## Prim

Priority Queue stores

```
(vertex,

minimumEdgeWeight)
```

The greedy choice minimizes

```
Edge weight connecting the current MST.
```

The data structure is identical.

The invariant is completely different.

---

# Choosing Between Prim and Kruskal

Suppose

```
Graph A

V = 1,000

E = 1,100
```

Almost a tree.

Sorting is inexpensive.

Kruskal is often preferable.

---

Suppose

```
Graph B

V = 1,000

E = 450,000
```

Very dense.

Prim avoids globally sorting every edge and usually performs better.

---

# Common Interview Mistakes

❌ Confusing MST with shortest path.

---

❌ Forgetting that MST is defined only for connected, undirected graphs.

---

❌ Thinking Prim minimizes path cost.

It minimizes the connecting edge.

---

❌ Thinking Kruskal needs adjacency lists.

It naturally operates on an edge list.

---

❌ Updating Priority Queue entries instead of inserting duplicates.

---

# Personal Learning Notes

These points came directly from our discussions.

---

## 1. Conditions of a Spanning Tree

One of your earliest summaries was:

> A spanning tree must:
>
> - connect every vertex,
> - contain exactly N−1 edges,
> - contain no cycles.

This is an excellent checklist and should become automatic during interviews.

---

## 2. Kruskal's Algorithm

You summarized Kruskal perfectly:

> Sort the edges.

> Process from smallest to largest.

> Use DSU to determine whether adding the edge creates a cycle.

This is the algorithm in one sentence.

---

## 3. Prim vs Dijkstra

One of your strongest conceptual observations was:

> Dijkstra chooses the vertex minimizing the **total distance from the source**.

> Prim chooses the edge minimizing the **cost of expanding the MST**.

This distinction is far more important than memorizing code.

---

## 4. Priority Queue Implementation

You questioned whether using only an array would require a linear search.

Exactly.

Using a Priority Queue avoids repeatedly searching for the minimum key,

reducing the complexity from

```
O(V²)
```

to

```
O((V+E) log V)
```

---

## 5. Choosing Prim vs Kruskal

When comparing sparse and dense graphs,

you correctly reasoned:

- Sparse graphs → Kruskal
- Dense graphs → Prim

This is precisely the trade-off expected in interviews.

---

# Interview Recognition

Think MST when the problem asks:

- Connect all cities
- Minimum cable cost
- Cheapest network
- Water supply
- Power grid
- Minimum infrastructure cost

Notice the wording.

The objective is usually:

> **Connect everything as cheaply as possible.**

Not

> Find the shortest route.

---

# Related LeetCode Problems

### Medium

- 1135. Connecting Cities With Minimum Cost ⭐⭐⭐⭐⭐
- 1584. Min Cost to Connect All Points ⭐⭐⭐⭐⭐
- 1168. Optimize Water Distribution in a Village
- 1489. Find Critical and Pseudo-Critical Edges in MST

### Hard

- 1579. Remove Max Number of Edges to Keep Graph Fully Traversable

Recommended order:

1. Min Cost to Connect All Points
2. Connecting Cities With Minimum Cost
3. Optimize Water Distribution in a Village
4. Find Critical and Pseudo-Critical Edges
5. Remove Max Number of Edges...

---

# Revision Summary

✔ An MST connects every vertex with the minimum possible total edge weight.

✔ Every MST has exactly

```
N−1
```

edges and contains no cycles.

✔ The **Cut Property** is the fundamental theorem behind MST algorithms.

✔ Kruskal grows multiple components using **sorting + DSU**.

✔ Prim grows one tree using a **Priority Queue**.

✔ Prim and Dijkstra use the same data structure but maintain different invariants.

✔ Kruskal is generally preferred for sparse graphs, while Prim is often better for dense graphs.

✔ MST minimizes the **total cost of connecting the graph**, not the shortest path between vertices.


# 13. Strongly Connected Components (SCC)

Strongly Connected Components (SCCs) are one of the most important concepts in directed graphs.

Unlike connected components in undirected graphs, connectivity in directed graphs depends on **edge direction**.

Understanding SCCs naturally leads to:

- Kosaraju's Algorithm
- Tarjan's Algorithm
- Condensation Graphs
- 2-SAT
- Compiler optimizations

---

# Motivation

Consider the graph:

```text
A → B → C
↑       ↓
└───────┘

D → E
```

Question:

Can every vertex reach every other vertex?

For

```
A, B, C
```

Yes.

For

```
D
```

No.

Therefore,

```
{A,B,C}
```

forms one SCC,

while

```
{D}
```

and

```
{E}
```

form separate SCCs.

---

# Definition

A **Strongly Connected Component** is a **maximal set of vertices** such that:

> Every vertex can reach every other vertex.

Notice the word **maximal** again.

You cannot add another vertex while preserving this property.

---

# Connected Components vs SCC

## Undirected Graph

```text
A ----- B ----- C
```

Reachability is naturally bidirectional.

Connected Components are sufficient.

---

## Directed Graph

```text
A → B → C
```

A reaches C.

C cannot reach A.

Therefore,

connectivity depends on direction.

We need SCCs instead.

---

# Important Observation

If there exists a directed cycle between two SCCs,

they are actually **one SCC**.

Therefore,

after compressing every SCC into a single node,

the resulting graph is always a

**Directed Acyclic Graph (DAG).**

This graph is called the

**Condensation Graph**.

---

# Why SCCs Matter

Many problems become easier after compressing SCCs.

Instead of working on

```
100,000 vertices
```

you may only have

```
500 SCCs.
```

The condensed graph is always a DAG,

allowing algorithms like Topological Sort.

---

# Kosaraju's Algorithm

Kosaraju is a beautiful two-pass DFS algorithm.

It answers:

> Which vertices belong to the same SCC?

---

# Core Intuition

Suppose we have

```text
SCC1 → SCC2
```

Notice something.

DFS starting inside

```
SCC1
```

can visit

```
SCC2.
```

But DFS starting in

```
SCC2
```

cannot return.

Therefore,

the order in which DFS finishes becomes important.

---

# Why Finishing Time?

During our lessons, this was one of the biggest conceptual discussions.

Suppose

```text
SCC1 → SCC2
```

Forward DFS:

```
Visit SCC1

↓

Visit SCC2

↓

Finish SCC2

↓

Finish SCC1
```

The source SCC finishes **last**.

This is exactly the ordering Kosaraju needs.

---

# Step 1

Run DFS on the original graph.

Store vertices in **decreasing finishing time**.

Usually implemented using a stack.

---

# Step 2

Reverse every edge.

```text
A → B
```

becomes

```text
B → A
```

This creates the **transpose graph**.

---

# Step 3

Process vertices in decreasing finishing order.

Run DFS on the reversed graph.

Each DFS discovers exactly one SCC.

---

# Why Reverse the Graph?

This was one of the most important intuitions we developed.

Suppose

```text
SCC1 → SCC2
```

Original graph.

Reverse it.

```text
SCC2 → SCC1
```

Now,

starting DFS from the SCC that finished last,

there is **no outgoing edge to an unprocessed SCC**.

The DFS becomes trapped inside one SCC.

That is exactly what we want.

---

# Why Does It Work?

Suppose

```
SCC(A)
```

finishes last.

If another SCC could reach

```
SCC(A)
```

in the reversed graph,

then in the original graph,

```
SCC(A)
```

could reach that SCC.

Those SCCs would have finished later,

contradicting the finishing order.

Therefore,

the first DFS on the reversed graph always discovers exactly one SCC.

---

# Algorithm

1. DFS on original graph.
2. Store finishing order.
3. Reverse graph.
4. DFS in reverse finishing order.
5. Every DFS is one SCC.

---

# Complexity

Original DFS

```
O(V+E)
```

Reverse graph

```
O(V+E)
```

Second DFS

```
O(V+E)
```

Overall

```
O(V+E)
```

---

# Java Skeleton

```java
// Pass 1

dfsOriginal()

stack.push(vertex)

// Reverse graph

// Pass 2

while (!stack.isEmpty()) {

    int v = stack.pop();

    if (!visited[v])

        dfsReverse(v);

}
```

---

# Tarjan vs Kosaraju

Kosaraju uses

```
Two DFS
```

Tarjan uses

```
One DFS
```

Both compute SCCs in

```
O(V+E)
```

Tarjan is more elegant,

but significantly harder to derive.

---

# Condensation Graph

Compress every SCC into a single vertex.

Example

```text
(A,B,C)

↓

SCC1
```

```text
(D,E)

↓

SCC2
```

Edges become

```text
SCC1 → SCC2
```

This graph is always acyclic.

Many advanced graph problems are solved on this condensed graph instead of the original graph.

---

# Common Interview Mistakes

❌ Confusing Connected Components with SCCs.

---

❌ Forgetting to reverse the graph.

---

❌ Processing vertices in arbitrary order during the second DFS.

The order **must** be decreasing finishing time.

---

❌ Thinking SCCs can have cycles between them.

If two SCCs formed a directed cycle,

they would actually merge into one SCC.

---

# Personal Learning Notes

These are based on our discussions.

---

## 1. Connectivity Depends on Direction

One of your earliest observations was:

> Connectivity in directed graphs depends on the starting and ending vertex.

Exactly.

This is the motivation behind SCCs.

---

## 2. Cycles Between SCCs

You correctly reasoned:

> If there is a directed cycle between two SCCs, they are actually one SCC.

This is one of the most important theoretical properties.

It immediately implies that the condensation graph is always a DAG.

---

## 3. Why Reverse the Graph?

Initially,

you suggested:

> "It would be easier to just reverse the graph and perform DFS."

This led us to derive the real reason.

Reversing alone is **not sufficient**.

The second DFS must also process vertices in **decreasing finishing order**.

Only then is each DFS guaranteed to remain inside one SCC.

---

## 4. Why Decreasing Finishing Order?

You reasoned that

> Starting with the vertex that finishes last in the original graph prevents the DFS in the reversed graph from escaping into another SCC.

This is exactly the intuition behind Kosaraju's correctness proof.

---

## 5. SCC Intersection

When discussing why SCCs cannot overlap,

you correctly answered:

> Their intersection.

If two SCCs share even one vertex,

every vertex in one becomes reachable from every vertex in the other,

meaning they should merge into a single SCC.

---

# Interview Recognition

Think SCC when the problem mentions:

- Mutual reachability
- Circular dependencies
- Groups where everyone can reach everyone
- Compress graph
- Condensation graph
- Directed connectivity

Immediately ask:

> Is reachability required in **both directions**?

If yes,

SCCs are likely involved.

---

# Related LeetCode Problems

### Medium

- 1192. Critical Connections in a Network *(Bridge problem using related DFS concepts)*
- 1557. Minimum Number of Vertices to Reach All Nodes *(Condensation graph intuition)*
- 802. Find Eventual Safe States *(Reverse graph intuition)*

### Hard

- 1568. Minimum Number of Days to Disconnect Island *(Related low-link concepts)*
- UVA 247 - Calling Circles *(Classic SCC)*
- CSES - Planets and Kingdoms ⭐⭐⭐⭐⭐ *(Excellent Kosaraju practice)*

> **Note:** Pure SCC problems are less common on LeetCode than in interviews and competitive programming. CSES and UVA contain some of the best practice problems.

Recommended order:

1. Find Eventual Safe States
2. CSES - Planets and Kingdoms
3. UVA - Calling Circles
4. Minimum Number of Vertices to Reach All Nodes

---

# Revision Summary

✔ SCCs apply only to **directed graphs**.

✔ Every vertex inside an SCC can reach every other vertex.

✔ SCCs are maximal and cannot overlap.

✔ Compressing SCCs produces a **Directed Acyclic Graph (Condensation Graph).**

✔ Kosaraju uses:

1. DFS on original graph.
2. Record finishing order.
3. Reverse the graph.
4. DFS in decreasing finishing order.

✔ Reversing the graph alone is **not enough**—the processing order is essential.

✔ Tarjan computes the same result using a single DFS and low-link values.


# 14. Tarjan's Algorithm (Strongly Connected Components)

Tarjan's Algorithm computes **Strongly Connected Components (SCCs)** in a **single DFS traversal**.

Unlike Kosaraju, it does **not** require:

- Reversing the graph
- A second DFS

Instead, Tarjan identifies SCCs **during backtracking** using two powerful concepts:

- **Discovery Time (`disc[]`)**
- **Low-Link Value (`low[]`)**

Among all graph algorithms, Tarjan is one of the most elegant because the entire algorithm emerges naturally from one invariant.

---

# Motivation

Kosaraju required:

1. DFS
2. Reverse Graph
3. Another DFS

Question:

> Can we identify SCCs while performing the very first DFS?

Tarjan answers:

**Yes.**

---

# Prerequisites

Before understanding Tarjan, you should already know:

- DFS Tree
- Tree Edges
- Back Edges
- Discovery Time
- DFS Backtracking

These concepts are the building blocks of the algorithm.

---

# The DFS Tree

Consider

```text
A → B → C
     ↑   |
     └───┘
```

DFS Tree

```text
A

↓

B

↓

C
```

Tree edges:

```
A → B

B → C
```

Back edge

```
C → B
```

Back edges are the key to identifying SCCs.

---

# Discovery Time (disc[])

Every vertex receives a timestamp when it is first visited.

Example

```text
A = 1

B = 2

C = 3

D = 4
```

Stored in

```java
disc[]
```

Discovery time never changes.

It simply records when a vertex entered DFS.

---

# Why Discovery Time Alone Isn't Enough

Suppose

```text
A → B → C

↑       |

└───────┘
```

Discovery times

```
A = 1

B = 2

C = 3
```

Can we identify the SCC using only

```
disc[]
```

No.

We also need to know:

> How far back can this vertex reach?

That leads to the most important concept.

---

# Low-Link Value (low[])

Definition:

```
low[u]
```

=

> The **smallest discovery time reachable from u**, including:

- u itself
- Tree edges
- At most one back edge

This definition is the heart of Tarjan.

---

# Intuition

Suppose

```text
A → B → C

↑       |

└───────┘
```

Discovery

```
A = 1

B = 2

C = 3
```

C has a back edge to

```
A
```

Therefore

```
low[C] = 1
```

B can reach C.

Therefore

```
low[B] = 1
```

A obviously reaches itself.

```
low[A] = 1
```

Notice

all three vertices now share

```
low = 1
```

This strongly suggests they belong together.

---

# Initial Values

When a vertex is first discovered

```java
disc[u] = timer;

low[u] = timer;
```

Initially,

every vertex can only reach itself.

Backtracking gradually improves

```
low[]
```

---

# Maintaining the DFS Stack

Unlike ordinary DFS,

Tarjan keeps a stack containing the

**currently active SCC**.

Example

```
Top

C

B

A
```

Notice

This stack is **not** the JVM recursion stack.

It is an explicit stack maintained by the algorithm.

---

# Why Do We Need Another Stack?

Consider

```text
A → B → C
```

DFS finishes

```
C
```

C remains

```
visited
```

but is no longer in the recursion stack.

Should later back edges be allowed to update

```
low[]
```

using C?

No.

Only vertices that still belong to the **current unfinished SCC** should participate.

Hence,

Tarjan maintains

```java
inStack[]
```

instead of relying on

```
visited[]
```

---

# Tree Edge Update

Suppose

```
u → v
```

is a tree edge.

DFS first computes

```
low[v]
```

Then,

during backtracking,

```java
low[u] = Math.min(low[u], low[v]);
```

Reason:

Anything reachable from

```
v
```

is also reachable from

```
u
```

---

# Back Edge Update

Suppose

```
u → ancestor
```

where the ancestor is still inside the Tarjan stack.

Update

```java
low[u] = Math.min(low[u], disc[ancestor]);
```

Notice carefully.

We use

```
disc[]
```

Not

```
low[]
```

Reason:

The back edge directly reaches the ancestor.

It does **not** automatically inherit everything reachable from that ancestor.

This distinction is extremely important.

---

# Why Ignore Edges to Vertices Not in the Stack?

Suppose

```text
A → B

↓

C
```

C has already finished.

Later,

another edge points to C.

Should

```
low[]
```

be updated?

No.

C belongs to a completed SCC.

Allowing such updates would incorrectly merge two SCCs.

Therefore,

Tarjan only considers back edges to vertices currently in

```
inStack[]
```

---

# Detecting the Root of an SCC

This is the most beautiful invariant.

Suppose

```java
disc[u] == low[u]
```

What does it mean?

It means:

No descendant of

```
u
```

can reach any ancestor of

```
u
```

Therefore,

```
u
```

is the root of an SCC.

---

# Extracting the SCC

When

```java
disc[u] == low[u]
```

Pop vertices from the stack until

```
u
```

is removed.

Those popped vertices form exactly one SCC.

Example

```
Stack

D

C

B

A
```

Suppose

```
disc[B] == low[B]
```

Pop

```
D

C

B
```

This becomes one SCC.

A remains.

---

# Complete Algorithm

For every vertex:

1. Assign

```
disc[]

low[]
```

2. Push onto stack.

3. Mark

```
inStack = true
```

4. DFS neighbours.

5. Tree edge

```
low[parent] = min(low[parent], low[child])
```

6. Back edge

```
low[current] = min(low[current], disc[ancestor])
```

7. If

```
disc == low
```

pop one SCC.

---

# Java Skeleton

```java
dfs(u) {

    disc[u] = low[u] = timer++;

    stack.push(u);

    inStack[u] = true;

    for (Edge edge : graph.get(u)) {

        int v = edge.to;

        if (disc[v] == -1) {

            dfs(v);

            low[u] = Math.min(low[u], low[v]);

        }

        else if (inStack[v]) {

            low[u] = Math.min(low[u], disc[v]);

        }

    }

    if (disc[u] == low[u]) {

        while (true) {

            int x = stack.pop();

            inStack[x] = false;

            if (x == u)
                break;

        }

    }

}
```

---

# Why Tarjan Works

The algorithm maintains one fundamental invariant:

> Every vertex currently in the Tarjan stack belongs to the same **unfinished SCC**.

Tree edges propagate

```
low[]
```

upwards.

Back edges connect descendants to ancestors.

When

```
disc == low
```

no path exists to an earlier ancestor.

Therefore,

the SCC is complete and can safely be removed.

---

# Complexity

Time

```
O(V + E)
```

Space

```
O(V)
```

---

# Tarjan vs Kosaraju

| Tarjan | Kosaraju |
|---------|----------|
| One DFS | Two DFS |
| No graph reversal | Reverse graph required |
| Uses low[] | Uses finishing order |
| Harder to derive | Easier to understand |

---

# Common Interview Mistakes

❌ Updating

```
low[u]
```

using

```
low[v]
```

for every visited neighbour.

Correct only for **tree edges**.

---

❌ Using

```
low[v]
```

instead of

```
disc[v]
```

for back edges.

This is one of the most common mistakes.

---

❌ Using

```
visited[]
```

instead of

```
inStack[]
```

A vertex may be visited but already belong to a completed SCC.

---

❌ Forgetting to remove vertices from

```
inStack[]
```

after popping an SCC.

---

# Personal Learning Notes

These points came directly from our discussions.

---

## 1. Tree Edges vs Back Edges

This was one of the biggest conceptual breakthroughs.

You correctly distinguished:

- Tree edges discover new vertices.
- Back edges connect to ancestors currently in the DFS stack.

Understanding this made Tarjan much easier.

---

## 2. Why `inStack[]` Instead of `visited[]`

Initially,

this was the main conceptual hurdle.

You later summarized it perfectly:

> A vertex remains visited after backtracking but is no longer part of the active DFS path.

Exactly.

That is why Tarjan requires

```
inStack[]
```

---

## 3. Understanding `low[]`

During the dry runs,

you correctly computed:

```
A = 1

B = 1

C = 1

D = 4
```

and later recognized that vertices sharing the same reachable ancestor naturally belong to one SCC.

---

## 4. `disc == low`

One of the nicest observations you made was:

> Nodes with the same low values form an SCC.

This is almost correct.

The precise rule is:

> An SCC is identified when its **root** satisfies

```
disc[root] == low[root]
```

The subsequent stack pop determines exactly which vertices belong to that SCC.

---

## 5. Backtracking Perspective

One major shift during this lesson was realizing that Tarjan performs almost all of its important work **while backtracking**, not while moving forward.

This same pattern appears later in:

- Bridges
- Articulation Points

---

# Interview Recognition

Think Tarjan when the problem asks:

- Strongly Connected Components
- Compress a directed graph
- Find mutually reachable groups
- One-pass SCC algorithm

---

# Related LeetCode Problems

Pure Tarjan problems are relatively uncommon on LeetCode.

The following are the best practice problems.

### Medium

- 1192. Critical Connections in a Network *(shares low-link concepts)*
- 802. Find Eventual Safe States

### Hard

- CSES - Planets and Kingdoms ⭐⭐⭐⭐⭐
- UVA 247 - Calling Circles ⭐⭐⭐⭐⭐
- SPOJ - Submerging Islands

> **Recommendation:** Master Tarjan through CSES/UVA rather than relying only on LeetCode.

---

# Revision Summary

✔ Tarjan computes SCCs using a **single DFS**.

✔ Every vertex stores:

- `disc[]`
- `low[]`

✔ `low[u]` is the earliest discovery time reachable from `u`.

✔ Tree edges update using:

```java
low[parent] = min(low[parent], low[child])
```

✔ Back edges update using:

```java
low[current] = min(low[current], disc[ancestor])
```

✔ Only vertices currently in `inStack[]` participate in SCC formation.

✔ When

```java
disc[u] == low[u]
```

`u` is the root of an SCC, and vertices are popped until `u` is removed.

✔ Tarjan is one of the cleanest examples of deriving an algorithm from a carefully maintained invariant.


# 15. Bridges (Critical Edges)

A **Bridge** (also called a **Critical Edge** or **Cut Edge**) is an edge whose removal increases the number of connected components in an **undirected graph**.

In simpler terms:

> Removing a bridge disconnects part of the graph.

Bridges are one of the most elegant applications of DFS, backtracking, and **low-link values**.

---

# Motivation

Suppose cities are connected by roads.

```text
A ----- B ----- C
```

If road

```
B-C
```

is destroyed,

city

```
C
```

becomes unreachable.

Therefore,

```
B-C
```

is a bridge.

---

Now consider

```text
      A
     / \
    B---C
```

Remove any edge.

The graph remains connected.

No edge is a bridge.

Why?

Because there is always an alternative path.

---

# Definition

A **Bridge** is an edge whose removal increases the number of connected components.

Bridges exist **only in undirected graphs**.

---

# Intuition

Suppose DFS discovers

```text
A

↓

B

↓

C

↓

D
```

Question:

If we remove

```
C-D
```

can D still reach A?

If yes,

then another path exists.

Not a bridge.

If no,

then D's entire subtree becomes disconnected.

It is a bridge.

Everything depends on one question:

> Can the child's subtree reach an ancestor without using the parent edge?

This is exactly what

```
low[]
```

tells us.

---

# Reusing Tarjan's Concepts

Bridges use the same arrays we learned in Tarjan.

```java
disc[]

low[]
```

The interpretation changes slightly.

---

## disc[]

When was the vertex discovered?

---

## low[]

Earliest discovery time reachable from this vertex using:

- Tree edges
- At most one back edge

Exactly the same definition as before.

---

# The Bridge Condition

Suppose

```
u → v
```

is a DFS tree edge.

If

```java
low[v] > disc[u]
```

then

```
u-v
```

is a bridge.

This is one of the most important interview conditions.

---

# Why Does It Work?

Suppose

```
low[v] > disc[u]
```

This means:

The subtree rooted at

```
v
```

cannot reach

```
u
```

or any ancestor of

```
u
```

using a back edge.

Therefore,

the **only** connection between the subtree and the rest of the graph is

```
u-v
```

Removing it disconnects the graph.

Hence,

it is a bridge.

---

# Example 1

```text
A ----- B ----- C
```

Discovery

```
A = 1

B = 2

C = 3
```

Low

```
A = 1

B = 2

C = 3
```

Check

```
low[C] > disc[B]

3 > 2

True
```

Bridge

```
B-C
```

Similarly

```
low[B] > disc[A]

2 > 1

True
```

Bridge

```
A-B
```

---

# Example 2

```text
      A
     / \
    B---C
```

Discovery

```
A = 1

B = 2

C = 3
```

Back edge

```
C → A
```

Low

```
A = 1

B = 1

C = 1
```

Check

```
low[C] > disc[B]

1 > 2

False
```

No bridge.

Exactly what we expect.

---

# Algorithm

DFS.

For every tree edge

```
u → v
```

1. DFS(v)

2. Update

```java
low[u] = Math.min(low[u], low[v]);
```

3. Check

```java
if (low[v] > disc[u])
```

Bridge found.

---

# Java Skeleton

```java
dfs(u, parent) {

    visited[u] = true;

    disc[u] = low[u] = timer++;

    for (int v : graph.get(u)) {

        if (v == parent)
            continue;

        if (!visited[v]) {

            dfs(v, u);

            low[u] = Math.min(low[u], low[v]);

            if (low[v] > disc[u]) {

                // Bridge

            }

        }

        else {

            low[u] = Math.min(low[u], disc[v]);

        }

    }

}
```

Notice

Visited neighbours update using

```
disc[]
```

Tree edges update using

```
low[]
```

Exactly like Tarjan.

---

# Why Strictly Greater (>)

This was one of the key discussions during our lessons.

Why not

```
>=
```

Suppose

```
low[v] == disc[u]
```

This means:

The subtree rooted at

```
v
```

can still reach

```
u
```

using a back edge.

Removing

```
u-v
```

does **not** disconnect the graph.

Therefore,

the edge is **not** a bridge.

Hence,

the condition must be

```java
low[v] > disc[u]
```

---

# Relationship with Cycles

A bridge can **never** belong to a cycle.

Why?

Because every cycle provides an alternate route.

Removing one edge from the cycle still leaves another path.

Conversely,

every edge not belonging to any cycle is a bridge.

---

# Complexity

DFS

```
O(V + E)
```

Space

```
O(V)
```

---

# Bridges vs Tarjan SCC

| Tarjan SCC | Bridges |
|-------------|----------|
| Directed Graph | Undirected Graph |
| Uses stack | No stack needed |
| Finds SCCs | Finds critical edges |
| Condition: disc == low | Condition: low[child] > disc[parent] |

---

# Bridges vs Articulation Points

Bridges remove

```
Edges
```

Articulation Points remove

```
Vertices
```

Both rely on

```
disc[]

low[]
```

The only difference is the comparison.

---

# Common Interview Mistakes

❌ Using

```
>=
```

instead of

```
>
```

---

❌ Forgetting to ignore the parent edge.

---

❌ Updating visited neighbours using

```
low[]
```

instead of

```
disc[]
```

---

❌ Applying the algorithm directly to directed graphs.

Bridge theory is defined for **undirected graphs**.

---

# Personal Learning Notes

These points came directly from our discussions.

---

## 1. Bridge Condition

When asked for the bridge condition,

you immediately answered:

```java
low[v] > disc[u]
```

Exactly correct.

This became one of your strongest recall points.

---

## 2. Why `>` Instead of `>=`

We spent extra time understanding this.

The key insight was:

```
low[v] == disc[u]
```

means the child's subtree can still reach

```
u
```

Therefore,

an alternate route exists.

The graph remains connected.

Hence,

the edge is **not** a bridge.

---

## 3. Thinking in Terms of Reachability

One conceptual shift during this topic was:

Instead of asking

> "Does this edge create a cycle?"

ask

> "Can the child's subtree still reach an ancestor without this edge?"

This interpretation makes the bridge condition almost obvious.

---

## 4. Backtracking Is Where the Work Happens

Just like Tarjan,

the important work is done while returning from recursion.

Only after completely exploring the child's subtree do we know whether the connecting edge is critical.

---

# Interview Recognition

Think Bridges when the problem asks:

- Critical roads
- Critical connections
- Removing one road disconnects cities
- Network reliability
- Weak links
- Single point of failure (edge)

---

# Related LeetCode Problems

### Medium

- 1192. Critical Connections in a Network ⭐⭐⭐⭐⭐

### Hard

- CSES - Necessary Roads ⭐⭐⭐⭐⭐
- UVA - Critical Links

Recommended order:

1. Critical Connections in a Network
2. CSES - Necessary Roads
3. UVA - Critical Links

---

# Revision Summary

✔ Bridges exist only in **undirected graphs**.

✔ A bridge is an edge whose removal disconnects the graph.

✔ Bridges use the same

```
disc[]

low[]
```

concepts as Tarjan.

✔ Tree edges update using

```java
low[parent] = min(low[parent], low[child])
```

✔ Back edges update using

```java
low[current] = min(low[current], disc[ancestor])
```

✔ A tree edge

```
u-v
```

is a bridge iff

```java
low[v] > disc[u]
```

✔ The strict inequality (`>`) is essential.

✔ Every bridge lies outside all cycles, and every edge outside every cycle is a bridge.


# 16. Articulation Points (Cut Vertices)

An **Articulation Point** (also called a **Cut Vertex**) is a vertex whose removal increases the number of connected components in an **undirected graph**.

In simple terms:

> Removing this vertex disconnects the graph.

Articulation Points are the vertex counterpart of **Bridges**.

Like Bridges, they are derived entirely from:

- DFS Tree
- Discovery Time (`disc[]`)
- Low-Link Value (`low[]`)
- DFS Backtracking

---

# Motivation

Suppose a communication network is

```text
A ----- B ----- C
```

If server

```
B
```

fails,

A can no longer reach C.

Therefore,

```
B
```

is an articulation point.

---

Now consider

```text
      A
     / \
    B---C
```

Remove any vertex.

The remaining graph remains connected.

There are **no articulation points**.

Again,

cycles provide alternate paths.

---

# Definition

An **Articulation Point** is a vertex whose removal disconnects the graph.

Like Bridges,

Articulation Points are defined for **undirected graphs**.

---

# Intuition

Suppose DFS produces

```text
A

↓

B

↓

C

↓

D
```

Question:

If we remove

```
B
```

can

```
C
```

(or any vertex in C's subtree)

still reach

```
A
```

without passing through

```
B
```

If yes,

B is **not** critical.

If no,

B disconnects the graph.

Again,

everything depends on

```
low[]
```

---

# Reusing Tarjan's Concepts

Exactly like Bridges,

we maintain

```java
disc[]

low[]
```

---

## disc[]

Discovery time of each vertex.

---

## low[]

Earliest discovery time reachable using:

- Tree edges
- At most one back edge

---

# The General Condition

Suppose

```
u → v
```

is a DFS tree edge.

If

```java
low[v] >= disc[u]
```

then

```
u
```

is an articulation point.

Notice something carefully.

For Bridges we used

```
>
```

Now we use

```
>=
```

This small difference is one of the most frequently asked interview questions.

---

# Why Greater Than or Equal (>=)?

Suppose

```
low[v] > disc[u]
```

Easy.

The child's subtree cannot reach

```
u
```

or any ancestor.

Removing

```
u
```

disconnects the subtree.

Clearly an articulation point.

---

Now consider

```
low[v] == disc[u]
```

The child's subtree can reach

```
u
```

itself,

but **cannot bypass u**.

If

```
u
```

is removed,

that back edge disappears too.

Therefore,

the subtree still becomes disconnected.

Hence,

```
>=
```

is correct.

This is the crucial difference from Bridges.

---

# Root is a Special Case

The DFS root has no parent.

Therefore,

the previous condition cannot be applied directly.

Instead,

Root is an articulation point **iff**

it has **more than one DFS child**.

---

# Why?

Suppose the root has only one child.

```text
A

↓

B

↓

C
```

Removing

```
A
```

does not separate multiple DFS subtrees.

Everything remaining stays connected.

---

Now suppose

```text
      A
     / \
    B   C
```

Removing

```
A
```

disconnects

```
B

and

C
```

Therefore,

Root is an articulation point only when

```
children > 1
```

---

# Example 1

```text
A ----- B ----- C
```

Discovery

```
A = 1

B = 2

C = 3
```

Low

```
A = 1

B = 2

C = 3
```

Check

```
low[C] >= disc[B]

3 >= 2

True
```

Articulation Point

```
B
```

---

# Example 2

```text
      A
     / \
    B---C
```

Discovery

```
A = 1

B = 2

C = 3
```

Back edge

```
C → A
```

Low

```
A = 1

B = 1

C = 1
```

Check

```
low[C] >= disc[B]

1 >= 2

False
```

B is not an articulation point.

Correct.

---

# Example 3 (Equality Case)

```text
A

↓

B

↓

C

↑

└────
```

Suppose

```
disc[B] = 2

low[C] = 2
```

Notice

```
low[C] == disc[B]
```

Bridge?

No.

Articulation Point?

Yes.

Removing

```
B
```

disconnects

```
C
```

from

```
A
```

even though

```
C
```

can reach

```
B
```

This example explains why articulation points use

```
>=
```

instead of

```
>
```

---

# Algorithm

DFS.

For every tree edge

```
u → v
```

1.

DFS(v)

2.

Update

```java
low[u] = Math.min(low[u], low[v]);
```

3.

If

```java
parent != -1 &&
low[v] >= disc[u]
```

then

```
u
```

is an articulation point.

Handle root separately.

---

# Java Skeleton

```java
dfs(u, parent) {

    visited[u] = true;

    disc[u] = low[u] = timer++;

    int children = 0;

    for (int v : graph.get(u)) {

        if (v == parent)
            continue;

        if (!visited[v]) {

            children++;

            dfs(v, u);

            low[u] = Math.min(low[u], low[v]);

            if (parent != -1 &&
                low[v] >= disc[u]) {

                articulation[u] = true;

            }

        }

        else {

            low[u] = Math.min(low[u], disc[v]);

        }

    }

    if (parent == -1 &&
        children > 1)

        articulation[u] = true;

}
```

---

# Complexity

Time

```
O(V + E)
```

Space

```
O(V)
```

---

# Bridges vs Articulation Points

| Bridges | Articulation Points |
|----------|---------------------|
| Remove edge | Remove vertex |
| `low[child] > disc[parent]` | `low[child] >= disc[parent]` |
| Root has no special case | Root handled separately |

---

# Why Root Is Different

The root has no parent.

Therefore,

the question

> "Can the child's subtree reach an ancestor?"

does not make sense.

Instead,

we ask:

> "Does removing the root disconnect two different DFS subtrees?"

Hence,

```
children > 1
```

---

# Common Interview Mistakes

❌ Using

```
>
```

instead of

```
>=
```

---

❌ Forgetting the root special case.

---

❌ Forgetting to ignore the parent edge.

---

❌ Updating visited neighbours using

```
low[]
```

instead of

```
disc[]
```

---

❌ Applying the algorithm directly to directed graphs.

---

# Personal Learning Notes

These observations came directly from our discussions.

---

## 1. Bridge vs Articulation Condition

One of your best questions was:

> Does the equality (`=`) correspond to the starting vertex of an SCC?

This led us to derive the real intuition.

Equality means:

The subtree can reach the current vertex,

but **cannot bypass it**.

That is sufficient for the vertex to be critical,

but **not** sufficient for the connecting edge to be non-critical.

This explains the difference between:

```
>

and

>=
```

---

## 2. Bridges and Articulation Points

You summarized them nicely:

> Bridges are cut edges.

> Articulation points are cut vertices.

Exactly.

Keeping this analogy in mind makes both algorithms easier to remember.

---

## 3. Root Rule

Initially,

the root condition felt like a special exception.

The deeper intuition is:

Removing the root only disconnects the graph if it separates **multiple DFS branches**.

That naturally leads to the

```
children > 1
```

condition.

---

## 4. Low-Link Interpretation

One important shift was thinking of

```
low[]
```

not as a formula,

but as answering:

> Can this subtree escape to an earlier ancestor without passing through the parent?

Once viewed this way,

both Bridges and Articulation Points become almost identical algorithms.

---

# Interview Recognition

Think Articulation Points when the problem asks:

- Critical cities
- Critical servers
- Single point of failure
- Removing one vertex disconnects the network
- Vulnerable junctions

---

# Related LeetCode Problems

### Medium

- 1192. Critical Connections in a Network *(Bridge problem using the same low-link concepts)*
- CSES - Necessary Cities ⭐⭐⭐⭐⭐

### Hard

- UVA 315 - Network ⭐⭐⭐⭐⭐
- SPOJ - Submerging Islands ⭐⭐⭐⭐⭐

> **Note:** Pure articulation point problems are rare on LeetCode. CSES, UVA, and SPOJ provide much better practice.

Recommended order:

1. CSES - Necessary Cities
2. UVA - Network
3. SPOJ - Submerging Islands

---

# Revision Summary

✔ Articulation Points are **critical vertices** in an undirected graph.

✔ They use the same

```
disc[]

low[]
```

arrays as Bridges and Tarjan.

✔ General condition:

```java
low[child] >= disc[parent]
```

✔ Root condition:

```
DFS Children > 1
```

✔ The equality (`=`) matters because reaching the current vertex is **not enough**—the subtree must be able to bypass it.

✔ Bridges remove **edges**.

✔ Articulation Points remove **vertices**.

✔ Both algorithms are elegant applications of DFS backtracking and low-link values.


# 17. Bipartite Graphs

A **Bipartite Graph** is a graph whose vertices can be divided into **two disjoint sets** such that **every edge connects a vertex from one set to the other**.

Equivalently,

> **A graph is bipartite if and only if it can be colored using two colors such that no adjacent vertices have the same color.**

This is one of the most elegant graph properties because a seemingly complex structural property reduces to a simple graph-coloring problem.

---

# Motivation

Suppose we have:

- Students
- Clubs

Every edge represents:

> A student belongs to a club.

```text
Students          Clubs

A  -----------  X

B  -----------  X

B  -----------  Y

C  -----------  Y
```

Notice:

- Student → Club
- Club → Student

There are **no Student-Student** edges and **no Club-Club** edges.

This naturally forms a bipartite graph.

---

# Definition

A graph is **bipartite** if its vertices can be partitioned into two disjoint sets:

```
Set 1

Set 2
```

such that

> Every edge goes from one set to the other.

No edge connects two vertices inside the same set.

---

# Graph Coloring Interpretation

Instead of maintaining two sets,

think of assigning colors.

Example

```text
Red        Blue

A  ------  B

 \        /

  \      /

    C
```

One possible coloring

```
A : Red

B : Blue

C : Red
```

Every edge joins opposite colors.

The graph is bipartite.

---

# BFS Intuition

During our discussions, one important insight emerged.

Imagine BFS levels.

```text
Level 0

A

↓

Level 1

B C

↓

Level 2

D E
```

Assign colors

```
Level 0 → Red

Level 1 → Blue

Level 2 → Red

Level 3 → Blue
```

Notice:

Every BFS edge naturally connects opposite levels.

This immediately suggests a BFS coloring algorithm.

---

# Algorithm (BFS)

Maintain

```java
color[]
```

Possible values

```
-1

0

1
```

Initially

```
All vertices

↓

-1
```

Choose any uncolored vertex.

Assign

```
0
```

Perform BFS.

Whenever visiting a neighbour

```
v
```

Assign

```java
color[v] = 1 - color[u];
```

If

```
color[v] == color[u]
```

the graph is **not bipartite**.

---

# Java Skeleton (BFS)

```java
Queue<Integer> queue = new LinkedList<>();

color[start] = 0;

queue.offer(start);

while (!queue.isEmpty()) {

    int u = queue.poll();

    for (int v : graph.get(u)) {

        if (color[v] == -1) {

            color[v] = 1 - color[u];

            queue.offer(v);

        }

        else if (color[v] == color[u]) {

            return false;

        }

    }

}

return true;
```

---

# DFS Implementation

Exactly the same idea.

Replace the queue with recursion.

```java
boolean dfs(int u, int currentColor) {

    color[u] = currentColor;

    for (int v : graph.get(u)) {

        if (color[v] == -1) {

            if (!dfs(v, 1 - currentColor))
                return false;

        }

        else if (color[v] == currentColor) {

            return false;

        }

    }

    return true;

}
```

---

# Disconnected Graphs

Just like DFS and BFS,

the graph may have multiple connected components.

Therefore,

run BFS/DFS from every uncolored vertex.

```java
for (int i = 0; i < V; i++) {

    if (color[i] == -1) {

        if (!bfs(i))
            return false;

    }

}
```

---

# The Most Important Theorem

A graph is bipartite

**if and only if**

it contains **no odd-length cycle.**

This theorem appears frequently in interviews.

---

# Why Do Odd Cycles Fail?

Consider

```text
A

/ \

B---C
```

Cycle length

```
3
```

Try coloring

```
A → Red

B → Blue

C → Red
```

Problem

```
A

and

C
```

are adjacent.

Same color.

Impossible.

No matter where we start,

the contradiction always appears.

Therefore,

odd cycles cannot be bipartite.

---

# Why Even Cycles Work

Example

```text
A

/   \

B     D

 \   /

   C
```

Cycle length

```
4
```

Coloring

```
A → Red

B → Blue

C → Red

D → Blue
```

Everything works perfectly.

Hence,

even cycles are bipartite.

---

# Trees are Always Bipartite

One of your strongest observations during our lessons.

Trees contain

```
No Cycles
```

Therefore,

they certainly contain

```
No Odd Cycles.
```

Hence,

every tree is bipartite.

This is one of the simplest applications of the theorem.

---

# Why BFS Naturally Works

BFS visits vertices level by level.

Every edge in a bipartite graph connects:

```
Level k

↓

Level k+1
```

Alternating colors level by level satisfies the bipartite property.

If an edge ever connects two vertices on the same level (or equivalently, two vertices with the same color),

an odd cycle exists.

---

# Complexity

Using either BFS or DFS

Time

```
O(V + E)
```

Space

```
O(V)
```

---

# Applications

## 1. Matching Problems

Examples:

- Students ↔ Projects
- Workers ↔ Jobs
- Drivers ↔ Passengers

Many advanced matching algorithms assume the graph is bipartite.

---

## 2. Scheduling Problems

Tasks divided into two independent groups.

---

## 3. Constraint Satisfaction

Two mutually exclusive categories.

---

## 4. Network Design

Partitioning systems into compatible groups.

---

# Relationship with Cycles

| Graph | Bipartite? |
|---------|------------|
| Tree | ✅ Always |
| Even Cycle | ✅ Yes |
| Odd Cycle | ❌ No |

This table alone answers many interview questions.

---

# Common Interview Mistakes

❌ Thinking every cycle breaks bipartiteness.

Only **odd** cycles do.

---

❌ Forgetting disconnected components.

---

❌ Forgetting to color newly discovered vertices immediately.

---

❌ Assuming DFS and BFS behave differently.

Both implement exactly the same coloring invariant.

---

# Personal Learning Notes

These came directly from our discussions.

---

## 1. Trees Are Bipartite

One of your first answers was:

> Trees are bipartite because they contain no cycles, let alone odd cycles.

Exactly correct.

This is the cleanest proof.

---

## 2. Even Cycle

When given an even cycle,

you immediately recognized that it remains bipartite.

Correct.

Alternating colors never conflict.

---

## 3. Odd Cycle

You correctly identified that

> An odd cycle makes the graph non-bipartite.

This is the defining theorem.

---

## 4. Why BFS?

One of your best intuitions was:

> BFS proceeds level by level, so alternate levels naturally correspond to alternate colors.

This is precisely why BFS is the most common implementation.

---

## 5. Disconnected Graphs

You also correctly noted that

> A single non-bipartite connected component makes the entire graph non-bipartite.

Therefore,

every connected component must be checked.

---

# Interview Recognition

Think Bipartite Graph when the problem mentions:

- Two groups
- Two teams
- Two colors
- Alternate assignments
- No conflicts within a group
- Matching problems

Immediately ask:

> Can I color adjacent vertices using only two colors?

If yes,

a bipartite graph is likely involved.

---

# Related LeetCode Problems

### Medium

- 785. Is Graph Bipartite? ⭐⭐⭐⭐⭐
- 886. Possible Bipartition ⭐⭐⭐⭐⭐
- 1042. Flower Planting With No Adjacent *(Related graph coloring intuition)*
- 886. Possible Bipartition

### Hard

- 2127. Maximum Employees to Be Invited to a Meeting *(Uses graph structure insights)*
- Hungarian Algorithm and Hopcroft-Karp (advanced bipartite matching; typically outside standard interview scope)

Recommended order:

1. Is Graph Bipartite?
2. Possible Bipartition
3. Flower Planting With No Adjacent
4. Explore Hopcroft-Karp after mastering graph fundamentals.

---

# Revision Summary

✔ A bipartite graph can be partitioned into **two disjoint sets**.

✔ Equivalently, it can be colored using **two colors**.

✔ BFS and DFS both solve the problem using graph coloring.

✔ A graph is bipartite **if and only if it contains no odd-length cycle**.

✔ Trees are always bipartite because they contain no cycles.

✔ Even cycles are bipartite.

✔ Odd cycles are never bipartite.

✔ Always process every connected component independently.


# 18. Eulerian Paths, Eulerian Circuits & Hierholzer's Algorithm

Eulerian graphs solve a very different problem from shortest paths or spanning trees.

Instead of asking:

- How do we reach a vertex cheaply?
- How do we connect all vertices?

they ask:

> **Can we traverse every edge exactly once?**

Notice the emphasis:

**Edges**, not vertices.

This distinction is the source of many interview mistakes.

---

# Motivation

Imagine a postman delivering letters.

He must travel through every street.

The objective is:

- Every street (edge) should be used exactly once.
- Revisiting intersections (vertices) is perfectly acceptable.

This is the classic **Chinese Postman** intuition.

---

# Eulerian Path vs Eulerian Circuit

These two terms are often confused.

## Eulerian Path

A path that visits **every edge exactly once**.

The start and end vertices **may be different**.

---

## Eulerian Circuit

A circuit that visits **every edge exactly once** and returns to the starting vertex.

The start and end vertices are the same.

Every Eulerian Circuit is also an Eulerian Path.

The reverse is **not** true.

---

# Important Observation

Unlike Hamiltonian problems,

Eulerian problems care about

```
Edges
```

not

```
Vertices.
```

Vertices may be visited multiple times.

Edges may **never** be reused.

---

# Example

```text
A ----- B ----- C
```

Eulerian Path

```
A → B → C
```

Every edge used exactly once.

No edge repeated.

---

Now consider

```text
      A
     / \
    B---C
```

Eulerian Circuit

```
A → B → C → A
```

Again,

every edge is used exactly once.

---

# Why Degree Matters

This was the biggest conceptual discussion during our lessons.

Suppose you arrive at a vertex.

```
↓

Vertex

↓

Leave
```

Every time you enter,

you must also leave.

Therefore,

except for the start/end of a path,

edges naturally come in pairs.

One edge enters.

One edge exits.

This immediately explains why **degree parity** becomes important.

---

# The Degree Theorem

## Eulerian Circuit

An undirected graph has an Eulerian Circuit **iff**

1. Every non-isolated vertex belongs to one connected component.
2. Every vertex has **even degree**.

---

## Eulerian Path

An undirected graph has an Eulerian Path **iff**

1. Every non-isolated vertex belongs to one connected component.
2. Exactly **0 or 2** vertices have odd degree.

---

# Why Even Degree Gives a Circuit

Suppose every vertex has even degree.

Whenever you enter a vertex,

there is always another unused edge available to leave.

Eventually,

you return to where you started.

No vertex gets "stuck."

---

# Why Exactly Two Odd Vertices Give a Path

Suppose only

```
A

and

D
```

have odd degree.

One of them must consume one extra outgoing edge.

The other consumes one extra incoming edge.

Therefore,

the path naturally starts at one odd vertex

and finishes at the other.

Every other vertex still pairs:

```
Enter

↓

Leave
```

---

# Summary of Degree Conditions

| Odd Degree Vertices | Result |
|---------------------|--------|
| 0 | Eulerian Circuit |
| 2 | Eulerian Path |
| >2 | Impossible |

This is one of the most frequently asked interview facts.

---

# Why DFS Is Not Enough

This was one of the most important questions we discussed.

Suppose

```text
      B
     / \
A---C---D
```

A careless DFS may choose

```
C → D
```

too early.

Later,

unused edges remain disconnected from the current traversal.

The traversal gets stuck,

even though an Eulerian Circuit exists.

The issue is **not** reachability.

The issue is consuming edges in the wrong order.

---

# The Key Insight Behind Hierholzer

Suppose we begin walking.

Rule:

> Always take **any unused edge**.

Eventually,

something interesting happens.

If every vertex has even degree,

you **must** return to the starting vertex.

Why?

Because you can never get trapped at another vertex.

Every arrival guarantees another unused exit.

Therefore,

the first walk always forms a **cycle**.

---

# But What If Edges Remain?

Example

```text
      D
      |
A------B
|      |
C------E
```

Suppose the first cycle is

```
A → B → E → C → A
```

The edge

```
B → D
```

was never used.

We are **not finished**.

Instead,

notice that

```
B
```

already belongs to the existing cycle.

Start another walk from

```
B
```

using only unused edges.

A second cycle appears.

Now simply **splice** the new cycle into the old one.

This is the central idea of Hierholzer's Algorithm.

---

# Hierholzer's Algorithm

The algorithm repeatedly builds cycles

and merges them into one larger Eulerian traversal.

---

# Recursive Intuition

Suppose we stand at a vertex.

If an unused edge exists,

take it immediately.

Continue recursively.

When a vertex has **no unused edges left**,

add it to the answer.

Notice:

Vertices are added during **backtracking**,

not while moving forward.

This is remarkably similar to:

- Topological Sort
- Tarjan
- Bridges
- Articulation Points

---

# Stack-Based Algorithm

Maintain:

- Stack
- Current vertex
- Adjacency list with unused edges

Algorithm:

```
Push start vertex.

↓

While stack not empty

↓

If current vertex has unused edge

Take one

Push neighbour

↓

Else

Pop vertex

Append to answer
```

Finally,

reverse the answer (or append during popping).

---

# Java Skeleton

```java
Stack<Integer> stack = new Stack<>();

List<Integer> circuit = new ArrayList<>();

stack.push(start);

while (!stack.isEmpty()) {

    int u = stack.peek();

    if (!adj.get(u).isEmpty()) {

        int v = removeUnusedEdge(u);

        stack.push(v);

    }

    else {

        circuit.add(stack.pop());

    }

}

Collections.reverse(circuit);
```

---

# Why Does It Work?

The crucial invariant is:

> A vertex is removed from the stack **only after all of its incident edges have been exhausted.**

Therefore,

once added to the answer,

that vertex never needs to be revisited.

Backtracking naturally constructs the Eulerian traversal in reverse order.

---

# Circuit vs Cycle

This was one of your best questions.

A **cycle** is simply any closed walk satisfying the cycle definition.

A **Eulerian circuit** is much stronger.

It must:

- Visit **every edge**
- Visit every edge **exactly once**

Hierholzer may temporarily construct **small cycles**,

but after repeated splicing,

the final result becomes **one Eulerian circuit**.

---

# Why Don't We Get Stuck?

Another excellent question you asked.

The answer comes directly from the degree theorem.

Every intermediate vertex satisfies

```
Enter

↓

Leave
```

Therefore,

before the traversal is complete,

there is always another unused edge available.

The only place where the walk can terminate is:

- the starting vertex (Eulerian circuit), or
- the second odd-degree vertex (Eulerian path).

We do **not** rely on luck.

The theorem guarantees this.

---

# Starting Vertex

## Eulerian Circuit

Start anywhere.

---

## Eulerian Path

Start from one of the two odd-degree vertices.

This guarantees the traversal ends at the other odd-degree vertex.

---

# Complexity

Every edge is processed exactly once.

Time

```
O(V + E)
```

Space

```
O(E)
```

---

# Common Interview Mistakes

❌ Confusing Eulerian and Hamiltonian problems.

Eulerian:

```
Edges
```

Hamiltonian:

```
Vertices
```

---

❌ Forgetting the connectivity condition.

Degree conditions alone are insufficient.

All non-isolated vertices must belong to one connected component.

---

❌ Thinking DFS automatically finds an Eulerian circuit.

DFS does not control edge consumption correctly.

---

❌ Thinking the first discovered cycle is the final answer.

Hierholzer repeatedly merges multiple cycles.

---

# Personal Learning Notes

These observations came directly from our discussions.

---

## 1. Why Degree Matters

One of your earliest explanations was:

> Every non-starting vertex has an exit path because of the degree condition.

Exactly.

This is the fundamental intuition behind Eulerian graphs.

Think in terms of **pairing**:

```
Enter

↓

Leave
```

---

## 2. Why Vertices Are Added During Backtracking

You correctly observed:

> A vertex is popped only after it has no unused edges left.

Exactly.

Once popped,

its work is permanently finished.

---

## 3. DFS Similarity

You also noticed:

> Hierholzer feels like DFS with a stack variant.

Very good observation.

The forward traversal resembles DFS,

but the correctness comes entirely from **when vertices are added to the answer**.

---

## 4. Circuit vs Cycle

You asked one of the most insightful questions:

> How do we ensure that we obtain a circuit rather than merely a cycle?

The answer is:

The algorithm does **not** stop after the first cycle.

It repeatedly discovers additional cycles and **splices** them together until **every edge** has been consumed.

---

## 5. Starting Vertex

Another important observation from our discussion:

For an Eulerian Path,

the algorithm should begin at **one of the odd-degree vertices**.

Otherwise,

the traversal may terminate prematurely.

---

## 6. Corrected Example

During our discussion,

you correctly noticed an error where an example reused the same edge twice.

That highlighted an important invariant:

> Every edge must be consumed **exactly once**.

This is an excellent interview habit—always verify edge usage explicitly.

---

# Interview Recognition

Think Eulerian Graphs when the problem asks:

- Traverse every road exactly once
- Visit every flight exactly once
- Reconstruct itinerary
- Postman problem
- Edge traversal

Immediately ask:

> Is the objective to visit **every edge exactly once?**

If yes,

consider Eulerian Path/Circuit and Hierholzer.

---

# Related LeetCode Problems

### Medium

- 332. Reconstruct Itinerary ⭐⭐⭐⭐⭐ *(Hierholzer with lexical ordering)*
- 2097. Valid Arrangement of Pairs ⭐⭐⭐⭐⭐ *(Eulerian Path in directed graph)*

### Hard

- 753. Cracking the Safe *(De Bruijn Graph + Eulerian Circuit)*

### Excellent External Practice

- CSES – Mail Delivery ⭐⭐⭐⭐⭐
- CSES – Teleporters Path ⭐⭐⭐⭐⭐

Recommended order:

1. Reconstruct Itinerary
2. Valid Arrangement of Pairs
3. CSES – Mail Delivery
4. CSES – Teleporters Path
5. Cracking the Safe

---

# Revision Summary

✔ Eulerian problems are about **edges**, not vertices.

✔ An Eulerian Path visits every edge exactly once.

✔ An Eulerian Circuit is an Eulerian Path that starts and ends at the same vertex.

✔ Degree conditions:

- **0 odd-degree vertices → Eulerian Circuit**
- **2 odd-degree vertices → Eulerian Path**
- **More than 2 odd-degree vertices → Impossible**

✔ Connectivity of all non-isolated vertices is also required.

✔ Hierholzer's Algorithm repeatedly builds and merges cycles until every edge has been used.

✔ Vertices are added to the answer during **backtracking**, after all incident edges have been exhausted.

✔ The correctness of the algorithm follows directly from the degree theorem and the invariant that every edge is consumed exactly once.


# 19. Choosing the Right Graph Algorithm (Interview Decision Guide)

One of the hardest parts of graph interviews is **not implementing an algorithm**.

It is recognizing **which algorithm to use**.

Many graph problems look different on the surface but reduce to the same underlying pattern.

This section serves as a decision guide to help map problem statements to the correct algorithm.

---

# Step 1 — Is It a Graph Problem?

Sometimes the graph is explicit.

```text
Cities

Roads
```

Sometimes it is hidden.

Examples:

- Matrix cells
- Words
- Flights
- Courses
- Accounts
- Computers
- People
- Strings

Ask yourself:

> **Can I model entities as vertices and relationships as edges?**

If yes,

it is probably a graph problem.

---

# Decision Tree

```text
                    GRAPH PROBLEM
                          │
         ┌────────────────┴────────────────┐
         │                                 │
     Traversal?                    Optimization?
         │                                 │
   DFS / BFS                    Shortest Path / MST
```

---

# Traversal Problems

Ask:

> "Do I simply need to explore the graph?"

Examples:

- Is there a path?
- Count islands
- Count provinces
- Traverse components

Use:

- DFS
- BFS

---

# DFS vs BFS

```text
Need shortest path
in an unweighted graph?
        │
      Yes
        │
       BFS
```

Otherwise

```text
Need exhaustive exploration?

Need recursion?

Need backtracking?

Need subtree information?

↓

DFS
```

---

## Use DFS For

- Connected Components
- Cycle Detection
- Topological Sort (DFS)
- Bridges
- Articulation Points
- Tarjan
- Kosaraju
- Tree DP
- Backtracking

---

## Use BFS For

- Minimum number of moves
- Shortest path (unweighted)
- Level order traversal
- Multi-source spread
- Bipartite checking
- Grid shortest path

---

# Shortest Path Problems

Ask:

> "What exactly is being minimized?"

---

## Unweighted Graph

```text
Minimum number of edges

↓

BFS
```

---

## Weighted Graph

Ask:

```
Negative edge?
```

---

### No Negative Edge

```
↓

Dijkstra
```

---

### Negative Edge Exists

```
↓

Bellman-Ford
```

---

### Need Shortest Path Between Every Pair?

```
↓

Floyd-Warshall
```

---

# Shortest Path Decision Tree

```text
Shortest Path?
        │
        │
Weighted?
   │        │
 No       Yes
 │          │
BFS   Negative Edge?
             │
        ┌────┴────┐
        │         │
       Yes       No
        │         │
 Bellman     Dijkstra
   Ford
        │
Need all-pairs?
        │
      Floyd-Warshall
```

---

# Minimum Spanning Tree

Ask:

> "Do I need to connect everything with minimum total cost?"

Examples:

- Connect cities
- Lay cables
- Water distribution
- Power grid

↓

Minimum Spanning Tree

---

## Sparse Graph

```
↓

Kruskal
```

---

## Dense Graph

```
↓

Prim
```

---

## Prim vs Kruskal

| Prim | Kruskal |
|------|----------|
| Dense graph | Sparse graph |
| Priority Queue | Sorting + DSU |
| Grows one tree | Grows many components |

---

# Connectivity Problems

Ask:

> "Am I only trying to identify groups?"

↓

Connected Components

Use

- DFS
- BFS

---

Need repeated connectivity queries?

↓

DSU

---

Edges added dynamically?

↓

DSU

---

# Cycle Detection

First question:

```text
Directed?

or

Undirected?
```

---

## Undirected

Use

```
DFS + Parent

or

DSU
```

---

## Directed

Use

```
DFS + Recursion Stack

or

Kahn's Algorithm
```

---

# Dependency Problems

Typical wording

- Prerequisites
- Build order
- Compilation
- Scheduling
- Course order

↓

Topological Sort

Choose:

- DFS
- Kahn

---

Need cycle detection too?

↓

Kahn is usually cleaner.

---

# Strong Connectivity

Ask

> "Can every vertex reach every other vertex?"

↓

SCC

---

Need easiest implementation?

↓

Kosaraju

---

Need one DFS?

↓

Tarjan

---

# Critical Network Problems

Typical wording

- Critical roads
- Critical connections
- Critical servers
- Single point of failure

---

Removing

```
Edge
```

↓

Bridge

---

Removing

```
Vertex
```

↓

Articulation Point

---

# Two-Group Problems

Typical wording

- Two teams
- Two colors
- Possible bipartition
- No conflicts

↓

Bipartite Graph

Use:

- BFS Coloring
- DFS Coloring

---

# Edge Traversal Problems

Typical wording

- Visit every road
- Traverse every edge
- Reconstruct itinerary

↓

Eulerian Graph

↓

Hierholzer

---

# Dynamic Connectivity

Suppose roads are continuously added.

Need connectivity queries.

↓

DSU

Not DFS.

---

# Matrix Problems

Many matrix problems secretly become graph problems.

---

## Number of Islands

↓

Connected Components

DFS/BFS

---

## Rotten Oranges

↓

Multi-source BFS

---

## Shortest Path in Binary Matrix

↓

BFS

---

## Minimum Effort Path

↓

Dijkstra

---

# Recognition Patterns

| Problem Statement | Algorithm |
|-------------------|-----------|
| Reachability | DFS / BFS |
| Count Groups | DFS / BFS / DSU |
| Shortest Path (Unweighted) | BFS |
| Shortest Path (Weighted) | Dijkstra |
| Negative Edge | Bellman-Ford |
| All Pairs Shortest Path | Floyd-Warshall |
| Dependency Ordering | Topological Sort |
| Strong Connectivity | Kosaraju / Tarjan |
| Connect Everything Cheaply | MST |
| Dynamic Connectivity | DSU |
| Critical Roads | Bridges |
| Critical Cities | Articulation Points |
| Two Groups | Bipartite |
| Traverse Every Edge | Hierholzer |

---

# Time Complexity Cheat Sheet

| Algorithm | Complexity |
|-----------|------------|
| DFS | O(V+E) |
| BFS | O(V+E) |
| Connected Components | O(V+E) |
| Cycle Detection | O(V+E) |
| Topological Sort | O(V+E) |
| Dijkstra | O((V+E) log V) |
| Bellman-Ford | O(VE) |
| Floyd-Warshall | O(V³) |
| Kruskal | O(E log E) |
| Prim | O((V+E) log V) |
| DSU | O(α(N)) amortized |
| Kosaraju | O(V+E) |
| Tarjan | O(V+E) |
| Bridges | O(V+E) |
| Articulation Points | O(V+E) |
| Bipartite | O(V+E) |
| Hierholzer | O(V+E) |

---

# Data Structure Cheat Sheet

| Algorithm | Primary Data Structure |
|-----------|------------------------|
| DFS | Stack / Recursion |
| BFS | Queue |
| Dijkstra | Priority Queue |
| Prim | Priority Queue |
| Kruskal | Edge List + DSU |
| Bellman-Ford | Edge List |
| Floyd-Warshall | Matrix |
| Kahn | Queue + In-degree |
| Tarjan | Stack |
| Hierholzer | Stack |

---

# Common Interview Confusions

| Question | Correct Choice |
|----------|----------------|
| Shortest path vs Minimum Spanning Tree | Dijkstra ≠ Prim |
| Weighted vs Unweighted | BFS vs Dijkstra |
| Connected vs Strongly Connected | CC vs SCC |
| Bridge vs Articulation | Edge vs Vertex |
| Eulerian vs Hamiltonian | Edges vs Vertices |
| DFS vs BFS | Deep exploration vs Level exploration |
| Kosaraju vs Tarjan | Two DFS vs One DFS |

---

# Personal Learning Notes

These observations summarize your learning journey across the Graph module.

---

## 1. You Prefer Understanding Invariants

Rather than memorizing algorithms, you repeatedly asked **why** each greedy choice or DFS update was correct.

Examples include:

- Why Dijkstra finalizes a vertex.
- Why Prim minimizes edge weight instead of path cost.
- Why `low[]` works.
- Why Hierholzer cannot get stuck.

This is exactly the right approach for interview-level understanding.

---

## 2. Your Strongest Conceptual Distinction

One of the clearest distinctions you made was:

| Algorithm | Greedy Choice |
|-----------|---------------|
| Dijkstra | Minimum **total distance from source** |
| Prim | Minimum **edge connecting the MST** |

This is a comparison many candidates struggle with.

---

## 3. Backtracking Became the Common Theme

As the module progressed, you recognized that several advanced algorithms derive their power from **what happens while returning from DFS**, not while exploring forward.

This unifies:

- Topological Sort
- Tarjan
- Bridges
- Articulation Points
- Hierholzer (stack backtracking)

Recognizing this pattern is a major milestone.

---

## 4. Interview Strategy

Before thinking about implementation, ask these questions in order:

1. **What is the graph?** (Explicit or implicit?)
2. **What is the objective?**
   - Traverse?
   - Optimize?
   - Group?
   - Order?
3. **Is the graph weighted?**
4. **Is it directed?**
5. **Is the graph static or dynamic?**
6. **What exactly is being optimized?**
   - Distance
   - Total weight
   - Reachability
   - Connectivity
   - Edge traversal

These six questions usually narrow the solution to one or two algorithms.

---

# Final Recognition Flow

```text
Need shortest path?
    │
    ├── Unweighted → BFS
    ├── Weighted, non-negative → Dijkstra
    ├── Negative edges → Bellman-Ford
    └── All pairs → Floyd-Warshall

Need to connect everything cheaply?
    │
    ├── Sparse → Kruskal
    └── Dense → Prim

Need dependency ordering?
    │
    └── Topological Sort

Need groups?
    │
    ├── Static → DFS / BFS
    └── Dynamic → DSU

Need mutual reachability?
    │
    ├── Two-pass → Kosaraju
    └── One-pass → Tarjan

Need critical roads?
    │
    └── Bridges

Need critical cities?
    │
    └── Articulation Points

Need two-coloring?
    │
    └── Bipartite

Need every edge exactly once?
    │
    └── Hierholzer
```

---

# Revision Summary

✔ Always identify the **problem objective** before choosing an algorithm.

✔ The same graph can require completely different algorithms depending on whether you're optimizing **distance**, **total connection cost**, **reachability**, **ordering**, or **edge traversal**.

✔ Interview success often depends more on **algorithm recognition** than on implementation.

✔ Use the recognition patterns and decision trees in this section as your first step whenever solving a new graph problem.


# 20. Personal Learning Notes & Interview Pitfalls

This section is unique to **your learning journey**.

Instead of summarizing the algorithms themselves, it records:

- Concepts that initially caused confusion.
- Questions that led to deeper understanding.
- Mental models that worked particularly well.
- Common interview traps to avoid.

Unlike generic notes, these are tailored to the way **you think** and should be revisited before interviews.

---

# Overall Assessment

## Current Graphs Proficiency

Overall understanding:

```
9 / 10
```

Your strength is **conceptual reasoning** rather than memorization.

Throughout the Graph module, you consistently tried to derive algorithms from first principles instead of recalling formulas.

This is exactly the approach expected in senior software engineering interviews.

---

# Your Strengths

## 1. You Think in Invariants

One recurring pattern throughout our sessions was that you preferred understanding:

> **Why is this algorithm always correct?**

instead of

> **How do I implement it?**

Examples include:

- Why Dijkstra can finalize a vertex.
- Why Prim's greedy choice is safe.
- Why Bellman-Ford needs V−1 passes.
- Why Kosaraju requires reverse finishing order.
- Why Tarjan uses `disc[]` for back edges.
- Why Hierholzer cannot get stuck.

This habit will help significantly in system design and senior-level interviews.

---

## 2. You Naturally Compare Algorithms

Rather than learning algorithms independently, you repeatedly asked questions like:

- Prim vs Dijkstra
- Kruskal vs Prim
- DFS vs BFS
- Bellman-Ford vs Dijkstra
- Kosaraju vs Tarjan

This comparative approach is much more effective than studying algorithms in isolation.

---

## 3. You Focus on "Why"

Many of your questions were of the form:

- Why does this theorem hold?
- Why is the condition `>` instead of `>=`?
- Why do we reverse the graph?
- Why is `disc[]` used instead of `low[]`?

These are exactly the kinds of follow-up questions interviewers ask after a candidate writes a correct solution.

---

## 4. You Build Mental Models

You rarely memorized formulas directly.

Instead, you preferred intuitive models such as:

- Pairing **enter → leave** for Eulerian graphs.
- Thinking of BFS as expanding "ripples."
- Viewing `low[]` as "how far back can this subtree escape?"
- Viewing the Priority Queue as selecting the "best current candidate."

These models make long-term retention much easier.

---

# Topics That Required Extra Attention

These concepts initially required additional discussion before the intuition became clear.

---

## 1. Directed vs Undirected Cycle Detection

### Initial misunderstanding

Trying to extend the parent-tracking technique from undirected graphs to directed graphs.

### Final understanding

Undirected graphs:

```
Visited neighbour

≠ Parent
```

Directed graphs:

```
Visited neighbour

AND

Currently in recursion stack
```

---

## 2. Dijkstra's Correctness

### Initial statement

> Dijkstra works because there are no negative cycles.

### Correct understanding

Dijkstra requires:

> **No negative edge weights.**

Even one negative edge (without a cycle) invalidates the greedy invariant.

---

## 3. Prim vs Dijkstra

This became one of your strongest conceptual improvements.

Final mental model:

| Dijkstra | Prim |
|-----------|------|
| Minimize total distance from the source | Minimize edge weight connecting the MST |
| Shortest Path | Minimum Spanning Tree |

Although both use a Priority Queue, they optimize different quantities.

---

## 4. Tarjan's `low[]`

Initially,

the purpose of `low[]` felt mechanical.

Later,

you began thinking of it as answering:

> **"How far back can this subtree escape?"**

This interpretation makes Tarjan, Bridges, and Articulation Points much easier to derive.

---

## 5. Bridge vs Articulation Point

One of your best questions was:

> Why do Bridges use `>` while Articulation Points use `>=`?

Final understanding:

### Bridges

```
low[child] > disc[parent]
```

The subtree cannot even reach the parent.

The edge is critical.

---

### Articulation Points

```
low[child] >= disc[parent]
```

Even if the subtree reaches the parent,

it cannot bypass it.

Removing the parent still disconnects the graph.

---

## 6. Hierholzer's Algorithm

This topic generated some of the deepest discussions.

Questions included:

- Why degree parity works.
- Why DFS alone is insufficient.
- How cycles become one Eulerian circuit.
- Why the traversal cannot get stuck.
- Why vertices are added during backtracking.

This is now one of your strongest conceptual topics.

---

# Questions That Demonstrated Deep Understanding

The following questions stood out because they explored correctness rather than implementation.

---

### Priority Queue in Prim

> Wouldn't using only an array require a linear search?

Excellent observation.

This naturally led to comparing:

```
O(V²)

vs

O((V+E)logV)
```

---

### Duplicate Priority Queue Entries

You proposed:

> Inserting another entry should be sufficient.

Correct.

This is exactly how Dijkstra and Prim are implemented in practice.

---

### Choosing Prim vs Kruskal

You reasoned using graph density rather than memorizing rules.

This is the expected interview-level approach.

---

### Why Reverse the Graph in Kosaraju?

Instead of accepting the algorithm,

you questioned:

> Why does reversing actually help?

Understanding this intuition is more valuable than memorizing the steps.

---

### Circuit vs Cycle in Hierholzer

You asked:

> How do we ensure we obtain a circuit rather than merely a cycle?

This is one of the most insightful questions in the entire module.

---

### Incorrect Example Detection

You noticed that an earlier Eulerian example reused the same edge twice.

This attention to invariants is an excellent habit.

---

# Common Interview Traps

These are worth revisiting before interviews.

---

## Trap 1

Shortest Path

≠

Minimum Spanning Tree

---

## Trap 2

Connected Components

≠

Strongly Connected Components

---

## Trap 3

BFS

≠

Dijkstra

BFS minimizes:

```
Number of edges.
```

Dijkstra minimizes:

```
Total edge weight.
```

---

## Trap 4

Bridge

≠

Articulation Point

Edge

vs

Vertex

---

## Trap 5

Eulerian

≠

Hamiltonian

Eulerian

↓

Edges

Hamiltonian

↓

Vertices

---

## Trap 6

Directed

≠

Undirected algorithms

Always determine graph type before choosing an algorithm.

---

# Areas to Revisit Before Interviews

These topics deserve a quick revision before interviews because they rely on subtle invariants.

- Tarjan (`disc[]` vs `low[]`)
- Bridges (`>` condition)
- Articulation Points (`>=` condition + root case)
- Hierholzer's cycle splicing intuition
- Floyd-Warshall DP state
- Kosaraju correctness proof
- Bellman-Ford correctness proof

---

# Suggested Revision Strategy

Rather than rereading every algorithm,

focus on answering these questions from memory:

1. **What invariant makes the algorithm correct?**
2. **Why is the greedy choice safe (if any)?**
3. **Why does the update rule use `disc[]` or `low[]`?**
4. **Why is the complexity what it is?**
5. **When would I choose this over a similar algorithm?**

If you can answer these five questions, you understand the algorithm—not just its implementation.

---

# Overall Readiness

## Conceptual Understanding

⭐⭐⭐⭐⭐ Excellent

---

## Algorithm Recognition

⭐⭐⭐⭐⭐ Excellent

---

## Correctness Proofs

⭐⭐⭐⭐☆ Very Good

Continue revising:

- Tarjan
- Bridges
- Articulation Points

---

## Implementation Readiness

⭐⭐⭐⭐☆ Very Good

The only remaining work is solving enough problems to make the implementations automatic.

---

# Final Advice for Interviews

Your natural tendency is to understand deeply before coding.

Keep that habit.

However, during interviews:

1. Spend **1–2 minutes identifying the algorithm.**
2. State the key invariant out loud.
3. Explain why the chosen algorithm fits.
4. Then write the implementation.

Interviewers usually care as much about your reasoning as your code.

If you continue solving problems with this mindset, Graphs should become one of your strongest DSA topics.