---
layout: post
title: Graph Theory
description: Graph Theory
permalink: /graph_theory
toc: False
comments: True
---

## Part 1
### How might I represent a weighted graph?
- Using an adjaceny list: each node points to a list of (neigbor, weight) pairs
~~~
Map<Integer, List<Pair<Integer, Integer>>> adjList = new HashMap<>();
~~~
- Using a Vertex and Edge Set
~~~
Set<Integer> vertices = new HashSet<>();

class Edge {
    int from;
    int to;
    int weight;

    Edge(int from, int to, int weight) {
        this.from = from;
        this.to = to;
        this.weight = weight;
    }
}

Set<Edge> edges = new HashSet<>();

~~~
- How might I represent a directed graph?
~~~
Map<Integer, List<Integer>> adjList = new HashMap<>();
~~~
~~~
Set<Integer> vertices = new HashSet<>();

class Edge {
    int from;
    int to;

    Edge(int from, int to) {
        this.from = from;
        this.to = to;
    }
}

Set<Edge> edges = new HashSet<>();

~~~

## Part 2
-  addNode
~~~
public void addNode(int node) {
    if (node >= adjacencyList.length) {
        // Optionally resize or throw an error depending on implementation
    } else {
        if (adjacencyList[node] == null) {
            adjacencyList[node] = new LinkedList<>();
        }
    }
}
~~~
- removeEdge

~~~
public void removeEdge(int source, int destination) {
    if (source < adjacencyList.length && adjacencyList[source] != null) {
        adjacencyList[source].remove(Integer.valueOf(destination));
    }
}
~~~


## Search Algorithms & Cycle Handling
- BFS (Breadth-First Search)
~~~
public void bfs(int start, int target) {
    Queue<Integer> queue = new LinkedList<>();
    Map<Integer, Integer> parent = new HashMap<>();
    Set<Integer> visited = new HashSet<>();

    queue.add(start);
    parent.put(start, -1);
    visited.add(start);

    while (!queue.isEmpty()) {
        int current = queue.poll();
        System.out.println("Visiting: " + current);

        if (current == target) {
            System.out.println("Target " + target + " found!");
            printPath(parent, target);
            return;
        }

        for (int neighbor : adjacencyList[current]) {
            if (!visited.contains(neighbor)) {
                parent.put(neighbor, current);
                queue.add(neighbor);
                visited.add(neighbor);
            }
        }
    }
    System.out.println("Target " + target + " not found.");
}
~~~
- DFS (Depth-First Search)
~~~
public void dfs(int start, int target) {
    Map<Integer, Integer> parent = new HashMap<>();
    Set<Integer> visited = new HashSet<>();
    dfsHelper(start, target, parent, visited);
}

private boolean dfsHelper(int current, int target, Map<Integer, Integer> parent, Set<Integer> visited) {
    System.out.println("Visiting: " + current);
    visited.add(current);

    if (current == target) {
        System.out.println("Target " + target + " found!");
        printPath(parent, target);
        return true;
    }

    for (int neighbor : adjacencyList[current]) {
        if (!visited.contains(neighbor)) {
            parent.put(neighbor, current);
            if (dfsHelper(neighbor, target, parent, visited)) {
                return true;
            }
        }
    }
    return false;
}
~~~
- BONUS: Traveling Salesman Problem (TSP) (Cursed Edition)
~~~
public List<Integer> cursedTSP(int start, int end, int n, List<List<Integer>> adjList) {
    List<Integer> bestPath = new ArrayList<>();
    boolean[] visited = new boolean[n];
    List<Integer> currentPath = new ArrayList<>();
    currentPath.add(start);
    visited[start] = true;
    tspHelper(start, end, n, adjList, visited, currentPath, bestPath);
    return bestPath;
}

private void tspHelper(int current, int end, int n, List<List<Integer>> adjList, boolean[] visited,
                       List<Integer> currentPath, List<Integer> bestPath) {
    if (currentPath.size() == n) {
        if (current == end) {
            if (bestPath.isEmpty() || currentPath.size() < bestPath.size()) {
                bestPath.clear();
                bestPath.addAll(new ArrayList<>(currentPath));
            }
        }
        return;
    }

    for (int neighbor : adjList.get(current)) {
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            currentPath.add(neighbor);

            tspHelper(neighbor, end, n, adjList, visited, currentPath, bestPath);

            visited[neighbor] = false;
            currentPath.remove(currentPath.size() - 1);
        }
    }
}
~~~
