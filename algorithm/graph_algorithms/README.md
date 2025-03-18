# 그래프 알고리즘 (Graph Algorithms)

## 1. 그래프 알고리즘이란?
그래프(Graph)는 **노드(Node)와 간선(Edge)으로 이루어진 자료구조**로, 다양한 알고리즘을 통해 탐색 및 최단 경로 문제를 해결할 수 있다. 그래프는 **방향성(Directed) 여부와 가중치(Weighted) 여부**에 따라 다양한 유형으로 나뉜다.

### 🔹 그래프의 주요 특징
- **노드(Node, Vertex)**: 데이터가 저장되는 기본 단위
- **간선(Edge)**: 노드를 연결하는 경로
- **방향 그래프(Directed Graph)** vs **무방향 그래프(Undirected Graph)**
- **가중 그래프(Weighted Graph)** vs **비가중 그래프(Unweighted Graph)**

---

## 2. 그래프 탐색 알고리즘
| 알고리즘 | 설명 | 시간 복잡도 |
|----------|------|------------|
| **너비 우선 탐색 (BFS, Breadth-First Search)** | 큐(Queue)를 사용하여 레벨별 탐색 | O(V + E) |
| **깊이 우선 탐색 (DFS, Depth-First Search)** | 스택(Stack) 또는 재귀를 사용하여 탐색 | O(V + E) |
| **다익스트라 알고리즘 (Dijkstra’s Algorithm)** | 가중 그래프에서 최단 경로 탐색 | O((V + E) log V) |
| **벨만-포드 알고리즘 (Bellman-Ford Algorithm)** | 음수 가중치를 포함한 최단 경로 탐색 | O(VE) |
| **플로이드-워셜 알고리즘 (Floyd-Warshall Algorithm)** | 모든 노드 간 최단 경로 탐색 | O(V³) |
| **크루스칼 알고리즘 (Kruskal’s Algorithm)** | 최소 신장 트리(MST) 탐색 | O(E log E) |
| **프림 알고리즘 (Prim’s Algorithm)** | 최소 신장 트리(MST) 탐색 | O(E log V) |

---

## 3. 코드 예제
### 🔹 BFS와 DFS 구현
##### Java (BFS & DFS)
```java
import java.util.*;

class Graph {
    private Map<Integer, List<Integer>> adjList = new HashMap<>();
    
    void addEdge(int u, int v) {
        adjList.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
        adjList.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
    }
    
    void bfs(int start) {
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(start);
        visited.add(start);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            for (int neighbor : adjList.getOrDefault(node, new ArrayList<>())) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.add(neighbor);
                }
            }
        }
    }
}
```

##### JavaScript (BFS & DFS)
```javascript
class Graph {
    constructor() {
        this.adjList = new Map();
    }
    addEdge(u, v) {
        if (!this.adjList.has(u)) this.adjList.set(u, []);
        if (!this.adjList.has(v)) this.adjList.set(v, []);
        this.adjList.get(u).push(v);
        this.adjList.get(v).push(u);
    }
    bfs(start) {
        let queue = [start], visited = new Set([start]);
        while (queue.length) {
            let node = queue.shift();
            console.log(node);
            this.adjList.get(node).forEach(neighbor => {
                if (!visited.has(neighbor)) {
                    visited.add(neighbor);
                    queue.push(neighbor);
                }
            });
        }
    }
}
```

##### Python (BFS & DFS)
```python
from collections import deque

class Graph:
    def __init__(self):
        self.adj_list = {}

    def add_edge(self, u, v):
        if u not in self.adj_list:
            self.adj_list[u] = []
        if v not in self.adj_list:
            self.adj_list[v] = []
        self.adj_list[u].append(v)
        self.adj_list[v].append(u)

    def bfs(self, start):
        queue = deque([start])
        visited = set([start])
        while queue:
            node = queue.popleft()
            print(node, end=" ")
            for neighbor in self.adj_list.get(node, []):
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
```

---

## 4. 그래프 알고리즘 사용 시 고려할 점
- **그래프의 방향성 여부**: 방향 그래프인지 무방향 그래프인지 확인 필요
- **가중치 유무**: 최단 경로 알고리즘 선택 시 중요 (예: 다익스트라 vs BFS)
- **음수 가중치 여부**: 음수 가중치가 존재하면 벨만-포드 알고리즘 고려 필요
- **탐색 목적**: 연결 여부 탐색이면 DFS/BFS, 최단 경로 탐색이면 다익스트라/플로이드-워셜 고려

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ BFS와 DFS의 차이점은?
- **BFS**는 큐(Queue)를 사용하여 너비 우선 탐색을 수행하며, **최단 경로 탐색에 유리**하다.
- **DFS**는 스택(Stack) 또는 재귀를 사용하여 깊이 우선 탐색을 수행하며, **백트래킹 문제 해결에 유리**하다.

### 2️⃣ 다익스트라 알고리즘과 벨만-포드 알고리즘의 차이점은?
- **다익스트라 알고리즘**: 양수 가중치 그래프에서 최단 경로 탐색, O((V + E) log V) 시간 복잡도
- **벨만-포드 알고리즘**: 음수 가중치 그래프에서도 최단 경로 탐색 가능, O(VE) 시간 복잡도

### 3️⃣ 플로이드-워셜 알고리즘이란?
모든 노드 간의 최단 경로를 구하는 알고리즘으로, 동적 프로그래밍을 활용하여 **O(V³) 시간 복잡도**를 가진다.

### 4️⃣ 크루스칼 알고리즘과 프림 알고리즘의 차이점은?
- **크루스칼 알고리즘**: 간선을 가중치 기준으로 정렬 후 최소 신장 트리(MST)를 구성 (O(E log E))
- **프림 알고리즘**: 하나의 정점에서 시작하여 최소 신장 트리를 확장하는 방식 (O(E log V))

### 5️⃣ 위상 정렬(Topological Sorting)이란?
방향 그래프에서 **노드의 선후 관계를 유지하면서 정렬하는 기법**으로, 주로 작업 스케줄링에 사용된다.

### 6️⃣ 유니온-파인드(Union-Find) 알고리즘이란?
서로소 집합(Disjoint Set)을 관리하는 알고리즘으로, **그래프에서 사이클 판별 및 MST(크루스칼 알고리즘) 등에 활용**된다.

### 7️⃣ 그래프의 최적 탐색 방법을 선택하는 기준은?
그래프의 크기, 가중치 여부, 방향성 여부, 최단 경로 탐색 여부 등을 고려하여 BFS, DFS, 다익스트라, 벨만-포드 등을 선택한다.

---