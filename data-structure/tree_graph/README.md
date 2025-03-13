# 트리(Tree) vs 그래프(Graph)

## 1. 트리와 그래프란?
트리(Tree)와 그래프(Graph)는 **비선형 자료구조**로, 데이터 간의 관계를 표현하는 데 사용된다. 각각의 특성과 차이를 이해하면 적절한 자료구조를 선택하는 데 도움이 된다.

### 🔹 트리(Tree)
- **계층적 구조**를 가지며, 부모-자식 관계로 연결됨
- **사이클이 없는 연결 그래프**
- **한 개의 루트 노드(root node)에서 시작**하여 여러 개의 자식 노드(child node)로 확장됨
- **예제**: 파일 시스템, 조직도, 이진 탐색 트리(BST)

### 🔹 그래프(Graph)
- **노드(Node)와 간선(Edge)으로 이루어진 자료구조**
- **방향성(Directed) 또는 비방향성(Undirected)을 가질 수 있음**
- **사이클이 존재할 수도 있음**
- **예제**: 도로망, 소셜 네트워크, 웹 페이지 링크 구조

---

## 2. 트리 vs 그래프 비교
| 특징 | 트리(Tree) | 그래프(Graph) |
|------|-----------|--------------|
| **구조** | 계층적 (Hierarchical) | 네트워크형 (Networked) |
| **노드 간 관계** | 부모-자식 관계 | 노드 간 자유로운 연결 |
| **사이클 여부** | 없음 (비순환) | 있을 수도 있음 (순환 가능) |
| **경로 존재** | 루트에서 특정 노드까지 유일한 경로 존재 | 경로가 여러 개일 수 있음 |
| **사용 사례** | 이진 탐색 트리(BST), 힙(Heap) | 소셜 네트워크, 지도 내 최단 경로 |

---

## 3. 코드 예제
### 🔹 트리 및 그래프 구현
##### Java (트리 및 그래프 구현)
```java
import java.util.*;

class TreeNode {
    int value;
    List<TreeNode> children;
    
    TreeNode(int value) {
        this.value = value;
        this.children = new ArrayList<>();
    }
}

class Graph {
    Map<Integer, List<Integer>> adjList = new HashMap<>();
    
    void addEdge(int u, int v) {
        adjList.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
        adjList.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
    }
}
```

##### JavaScript (트리 및 그래프 구현)
```javascript
class TreeNode {
    constructor(value) {
        this.value = value;
        this.children = [];
    }
}

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
}
```

##### Python (트리 및 그래프 구현)
```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []

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
```

---

## 4. 트리와 그래프 사용 시 고려할 점
- **트리는 특정 계층적 관계를 표현할 때 적합** (예: 조직도, 파일 시스템)
- **그래프는 복잡한 관계를 표현할 때 적합** (예: 소셜 네트워크, 경로 탐색)
- **트리는 부모-자식 관계가 명확하지만, 그래프는 자유로운 연결 가능**
- **그래프에서 특정 경로 탐색이 필요할 경우 DFS, BFS 알고리즘 활용**

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 트리와 그래프의 차이점은?
트리는 **계층적 구조**를 가지며 **사이클이 없는 연결 그래프**이다. 반면, 그래프는 **노드 간 자유롭게 연결될 수 있으며, 사이클이 존재할 수도 있다**.

### 2️⃣ 트리에서 이진 탐색 트리(BST)의 특징은?
이진 탐색 트리는 **왼쪽 자식 노드는 부모보다 작은 값, 오른쪽 자식 노드는 부모보다 큰 값**을 가지는 특성을 지닌다. 이를 통해 효율적인 검색(O(log n))이 가능하다.

### 3️⃣ DFS(깊이 우선 탐색)와 BFS(너비 우선 탐색)의 차이는?
- **DFS(Depth First Search)**: 스택(Stack) 기반 탐색, 깊은 경로를 먼저 탐색
- **BFS(Breadth First Search)**: 큐(Queue) 기반 탐색, 가까운 노드를 먼저 탐색

### 4️⃣ 그래프에서 최단 경로를 찾는 알고리즘은?
- **다익스트라 알고리즘**: 가중치 그래프에서 한 정점에서 모든 정점까지의 최단 경로 탐색
- **플로이드-워셜 알고리즘**: 모든 정점에서 모든 정점까지의 최단 경로 탐색

### 5️⃣ 그래프에서 사이클이 존재하는지 확인하는 방법은?
- **DFS를 활용하여 백 엣지(Back Edge) 탐색**
- **유니온 파인드(Union-Find) 알고리즘 적용**

### 6️⃣ 트리의 균형을 유지하는 기법은?
- **AVL 트리**: 각 노드의 균형 인수를 유지하며 자동으로 균형 조정
- **레드-블랙 트리**: 균형을 보장하며, 삽입 및 삭제 시 재조정 수행

### 7️⃣ 그래프를 인접 행렬과 인접 리스트로 표현하는 차이는?
- **인접 행렬(Adjacency Matrix)**: 노드 간의 연결을 2차원 배열로 표현 (공간 복잡도 O(V²))
- **인접 리스트(Adjacency List)**: 연결된 노드만 리스트로 저장 (공간 복잡도 O(V+E))

---