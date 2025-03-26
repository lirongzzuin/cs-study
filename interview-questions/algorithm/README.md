# 📚 Algorithm Interview Questions

## 1. 알고리즘 개요
**알고리즘(Algorithm)**은 문제를 해결하기 위한 절차 또는 연산 과정이다. 효율적인 알고리즘을 설계하는 것은 성능 최적화와 직접적인 연관이 있으며, 면접에서는 알고리즘의 **시간 복잡도, 공간 복잡도, 실무 적용 사례** 등에 대한 이해를 평가한다.

---

## 2. 주요 알고리즘 및 비교

| 알고리즘 | 설명 | 평균 시간 복잡도 |
|------|------|------|
| **정렬(Sorting)** | 데이터를 일정한 순서로 정렬 | O(n log n) (퀵 정렬, 병합 정렬) |
| **탐색(Search)** | 특정 값을 찾는 과정 | O(log n) (이진 탐색) |
| **재귀(Recursion)** | 함수가 자기 자신을 호출 | 문제에 따라 다름 |
| **동적 계획법(DP)** | 부분 문제를 해결하고 결과를 저장하여 중복 계산 방지 | O(n) ~ O(n²) |
| **탐욕 알고리즘(Greedy)** | 매 순간 최적의 선택을 하는 방식 | O(n log n) |
| **분할 정복(Divide & Conquer)** | 문제를 작은 부분으로 나누어 해결 | O(n log n) |
| **그래프 알고리즘(Graph Algorithm)** | 그래프 탐색 및 최단 경로 탐색 | O(V+E) (BFS, DFS) |

---

## 3. 면접 질문 및 답변

### 1️⃣ 정렬 알고리즘의 종류와 차이점은?
- **버블 정렬(Bubble Sort)**: O(n²), 단순하지만 비효율적
- **선택 정렬(Selection Sort)**: O(n²), 최소값을 반복적으로 선택하여 정렬
- **삽입 정렬(Insertion Sort)**: O(n²), 이미 정렬된 데이터에 적합
- **퀵 정렬(Quick Sort)**: O(n log n), 분할 정복 기반의 정렬
- **병합 정렬(Merge Sort)**: O(n log n), 안정 정렬(Stable Sort) 지원

### 2️⃣ 이진 탐색(Binary Search)이란?
- **정렬된 배열에서** 특정 값을 찾기 위한 탐색 알고리즘
- O(log n)의 시간 복잡도를 가짐

### 3️⃣ 동적 계획법(Dynamic Programming)이란?
- **부분 문제를 해결하고 그 결과를 저장하여 중복 계산을 방지하는 기법**
- 예제: 피보나치 수열, 배낭 문제, 최장 공통 부분 수열(LCS)

### 4️⃣ 탐욕 알고리즘(Greedy Algorithm)이란?
- **매 순간 최적의 선택을 하는 방식으로 최적해를 구하는 알고리즘**
- 예제: 다익스트라 알고리즘, 최소 신장 트리(Kruskal, Prim)

### 5️⃣ DFS(깊이 우선 탐색)와 BFS(너비 우선 탐색)의 차이점은?
- **DFS(Depth-First Search)**: 스택(Stack) 또는 재귀를 사용하여 깊이 우선 탐색
- **BFS(Breadth-First Search)**: 큐(Queue)를 사용하여 너비 우선 탐색

---

## 4. 코드 예제

### 🔹 **이진 탐색(Binary Search) 구현**

#### 📌 Java (Binary Search)
```java
public class BinarySearch {
    public static int search(int[] arr, int target) {
        int left = 0, right = arr.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) return mid;
            if (arr[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }
}
```

#### 📌 Python (Binary Search)
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

---

## 5. 실무에서 고려할 점

✅ **알고리즘의 시간 복잡도 및 공간 복잡도 분석**  
✅ **대량 데이터 처리 시 최적화 적용 (정렬, 탐색 알고리즘 활용)**  
✅ **재귀 호출 시 스택 오버플로우 방지 (메모이제이션, DP 활용)**  
✅ **그래프 탐색 시 BFS, DFS 선택 (최단 경로, 사이클 탐색 등 고려)**  
✅ **실시간 데이터 처리 시 탐욕 알고리즘과 DP 조합 활용**  

---

## 6. 결론

✅ **알고리즘은 문제 해결의 핵심이며, 성능 최적화의 필수 요소**  
✅ **면접에서는 알고리즘의 개념, 시간 복잡도, 코드 구현 능력을 평가**  
✅ **단순 개념 암기보다 실제 구현 및 최적화 경험이 중요**  
