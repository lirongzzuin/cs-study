# 📚 Data Structure Interview Questions

## 1. 데이터 구조 개요
**데이터 구조(Data Structure)**는 데이터를 **효율적으로 저장하고 관리하는 방식**을 의미하며, 성능 최적화를 위해 적절한 데이터 구조를 선택하는 것이 중요하다. 면접에서는 다양한 자료구조의 **특징, 시간 복잡도, 실무 적용 사례** 등에 대한 이해를 평가한다.

---

## 2. 주요 데이터 구조 및 비교

| 자료구조 | 설명 | 평균 시간 복잡도 |
|------|------|------|
| **배열(Array)** | 연속된 메모리 공간에 요소를 저장 | 검색 O(1), 삽입/삭제 O(n) |
| **연결 리스트(Linked List)** | 노드와 포인터로 연결된 동적 구조 | 검색 O(n), 삽입/삭제 O(1) |
| **스택(Stack)** | LIFO(Last In First Out) 방식 | 삽입/삭제 O(1), 검색 O(n) |
| **큐(Queue)** | FIFO(First In First Out) 방식 | 삽입/삭제 O(1), 검색 O(n) |
| **해시 테이블(Hash Table)** | 키-값 기반의 해싱 구조 | 검색/삽입/삭제 O(1) |
| **힙(Heap)** | 우선순위 기반의 이진 트리 | 삽입/삭제 O(log n), 검색 O(1) |
| **트리(Tree)** | 계층적 구조, 부모-자식 관계 | 검색/삽입/삭제 O(log n) |
| **그래프(Graph)** | 노드와 간선으로 이루어진 비선형 구조 | 탐색 O(V+E) |

---

## 3. 면접 질문 및 답변

### 1️⃣ 배열과 연결 리스트의 차이점은?
- **배열(Array)**: 연속된 메모리 공간을 사용하여 **빠른 랜덤 접근(O(1))**이 가능하지만 **삽입/삭제가 느림(O(n))**
- **연결 리스트(Linked List)**: 노드가 포인터로 연결된 구조로, **삽입/삭제가 빠름(O(1))**이지만 **랜덤 접근이 불가능(O(n))**

### 2️⃣ 스택(Stack)과 큐(Queue)의 차이점은?
- **스택(Stack)**: **LIFO(Last In First Out)** 방식으로, **재귀 호출, 실행 취소(Undo) 기능** 등에 활용
- **큐(Queue)**: **FIFO(First In First Out)** 방식으로, **작업 대기열, 네트워크 패킷 처리** 등에 사용

### 3️⃣ 해시 테이블(Hash Table)의 원리와 충돌 해결 방법은?
- **해시 테이블**: 해시 함수를 이용하여 **키를 인덱스로 변환하여 값을 저장**하는 자료구조
- **충돌 해결 방법**:
  - **체이닝(Chaining)**: 같은 인덱스에 여러 개의 값을 리스트로 연결
  - **오픈 어드레싱(Open Addressing)**: 충돌 시 다른 빈 공간을 찾아 저장

### 4️⃣ 트리(Tree)와 그래프(Graph)의 차이점은?
- **트리(Tree)**: 부모-자식 관계를 가지며 **사이클이 없는 계층적 구조**
- **그래프(Graph)**: 노드 간 **연결 관계가 자유로우며, 사이클이 존재할 수 있음**

### 5️⃣ 이진 탐색 트리(Binary Search Tree, BST)의 특징과 문제점은?
- **BST 특징**:
  - 왼쪽 서브트리는 **부모보다 작은 값**, 오른쪽 서브트리는 **부모보다 큰 값** 저장
  - **이진 탐색(O(log n))을 이용하여 빠른 검색 가능**
- **BST 문제점**:
  - **불균형 트리(Skewed Tree)**가 되면 성능이 O(n)까지 저하될 수 있음
  - **해결 방법**: **AVL 트리, 레드-블랙 트리(Red-Black Tree) 같은 균형 트리 사용**

### 6️⃣ 힙(Heap)의 개념과 사용 사례는?
- **힙(Heap)**은 **최댓값 또는 최솟값을 빠르게 찾기 위한 완전 이진 트리**
- **사용 사례**:
  - **우선순위 큐(Priority Queue)**: 작업 스케줄링, 네트워크 패킷 처리
  - **힙 정렬(Heap Sort)**: O(n log n) 복잡도로 정렬 가능

### 7️⃣ 그래프 탐색 알고리즘(BFS vs DFS)의 차이점은?
- **너비 우선 탐색(BFS)**:
  - 큐(Queue)를 사용하며 **최단 경로 탐색**에 유리
  - 시간 복잡도: O(V+E)
- **깊이 우선 탐색(DFS)**:
  - 스택(Stack) 또는 재귀를 사용하며 **백트래킹 문제 해결**에 유리
  - 시간 복잡도: O(V+E)

---

## 4. 코드 예제

### 🔹 스택 & 큐 구현

#### 📌 Java (Stack & Queue)
```java
import java.util.*;

public class StackQueueExample {
    public static void main(String[] args) {
        // 스택(Stack) 사용
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        System.out.println("스택 팝: " + stack.pop());

        // 큐(Queue) 사용
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(1);
        queue.offer(2);
        System.out.println("큐 디큐: " + queue.poll());
    }
}
```

#### 📌 Python (Stack & Queue)
```python
from collections import deque

# 스택(Stack) 사용
stack = []
stack.append(1)
stack.append(2)
print("스택 팝:", stack.pop())

# 큐(Queue) 사용
queue = deque()
queue.append(1)
queue.append(2)
print("큐 디큐:", queue.popleft())
```

---

## 5. 실무에서 고려할 점

✅ **데이터 크기 및 구조에 따라 적절한 자료구조 선택**  
✅ **시간 복잡도 분석을 통해 최적의 성능 확보**  
✅ **대규모 데이터 처리 시 해시 테이블, 트리, 힙 등을 활용한 최적화**  
✅ **멀티스레딩 환경에서 동기화 문제 고려 (Concurrent 자료구조 사용)**  
✅ **분산 환경에서 일관성 및 가용성 고려 (CAP 이론 적용)**  

---

## 6. 결론

✅ **자료구조는 알고리즘의 기본이며, 문제 해결의 핵심 요소**  
✅ **면접에서는 자료구조의 개념, 시간 복잡도, 실무 활용 사례, 코드 구현 능력을 평가**  
✅ **단순 개념 암기보다 실제 구현 및 최적화 경험이 중요**  

