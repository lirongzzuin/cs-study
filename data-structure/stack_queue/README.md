# 스택(Stack) vs 큐(Queue)

## 1. 스택과 큐란?
스택(Stack)과 큐(Queue)는 **선형 자료구조**로, 데이터의 삽입 및 삭제 방식이 다르다. 각각의 특성과 차이를 이해하면 상황에 따라 적절한 자료구조를 선택할 수 있다.

### 🔹 스택(Stack)
- **후입선출(LIFO, Last In First Out)** 구조
- **가장 마지막에 삽입된 데이터가 가장 먼저 제거됨**
- **예제**: 재귀 호출, 실행 취소(Undo), 괄호 검사

### 🔹 큐(Queue)
- **선입선출(FIFO, First In First Out)** 구조
- **가장 먼저 삽입된 데이터가 가장 먼저 제거됨**
- **예제**: 프린터 작업 대기열, 프로세스 스케줄링, 네트워크 요청 처리

---

## 2. 스택 vs 큐 비교
| 특징 | 스택(Stack) | 큐(Queue) |
|------|------------|----------|
| **데이터 구조** | LIFO (후입선출) | FIFO (선입선출) |
| **삽입 위치** | top(맨 위) | rear(맨 뒤) |
| **삭제 위치** | top(맨 위) | front(맨 앞) |
| **사용 사례** | 함수 호출 스택, 되돌리기(Undo) | 작업 대기열, 메시지 큐 |

---

## 3. 코드 예제
### 🔹 스택과 큐 구현
##### Java (스택과 큐 구현)
```java
import java.util.*;

public class StackQueueExample {
    public static void main(String[] args) {
        // 스택(Stack) 구현
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        System.out.println("스택 팝: " + stack.pop());
        
        // 큐(Queue) 구현
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(1);
        queue.offer(2);
        queue.offer(3);
        System.out.println("큐 디큐: " + queue.poll());
    }
}
```

##### JavaScript (스택과 큐 구현)
```javascript
// 스택(Stack) 구현
class Stack {
    constructor() {
        this.items = [];
    }
    push(element) { this.items.push(element); }
    pop() { return this.items.pop(); }
}

// 큐(Queue) 구현
class Queue {
    constructor() {
        this.items = [];
    }
    enqueue(element) { this.items.push(element); }
    dequeue() { return this.items.shift(); }
}

const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);
console.log("스택 팝:", stack.pop());

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);
console.log("큐 디큐:", queue.dequeue());
```

##### Python (스택과 큐 구현)
```python
from collections import deque

# 스택(Stack) 구현
stack = []
stack.append(1)
stack.append(2)
stack.append(3)
print("스택 팝:", stack.pop())

# 큐(Queue) 구현
queue = deque()
queue.append(1)
queue.append(2)
queue.append(3)
print("큐 디큐:", queue.popleft())
```

---

## 4. 스택과 큐 사용 시 고려할 점
- **스택은 후입선출 방식이므로, 가장 마지막에 추가된 데이터를 먼저 처리할 때 적합**
- **큐는 선입선출 방식이므로, 순차적으로 데이터를 처리해야 할 때 적합**
- **연결 리스트를 사용하면 동적 크기 조정이 가능하지만, 배열을 사용하면 접근 속도가 빠름**
- **우선순위가 있는 경우, `Priority Queue` 사용 가능**

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 스택과 큐의 차이점은?
스택은 **후입선출(LIFO)** 구조를 가지며, 큐는 **선입선출(FIFO)** 구조를 가진다. 스택은 가장 마지막에 추가된 요소가 먼저 제거되며, 큐는 가장 먼저 추가된 요소가 먼저 제거된다.

### 2️⃣ 스택과 큐의 시간 복잡도는?
- **스택**: `push()`와 `pop()` 연산이 O(1)
- **큐**: `enqueue()`와 `dequeue()` 연산이 O(1)

### 3️⃣ 큐의 변형된 형태로는 어떤 것들이 있는가?
- **원형 큐(Circular Queue)**: 큐의 크기를 고정하여 메모리를 효율적으로 사용
- **우선순위 큐(Priority Queue)**: 우선순위가 높은 요소가 먼저 처리됨
- **이중 끝 큐(Deque, Double-Ended Queue)**: 양쪽에서 삽입 및 삭제 가능

### 4️⃣ 스택을 이용하여 큐를 구현할 수 있는가?
네, **두 개의 스택을 사용하여 큐를 구현 가능**하다. 하나의 스택을 입력 용도로 사용하고, 다른 하나를 출력 용도로 사용하여 데이터를 유지한다.

### 5️⃣ 큐를 이용하여 스택을 구현할 수 있는가?
네, **두 개의 큐를 사용하여 스택을 구현 가능**하다. 한 큐를 주 큐로 사용하고, 다른 큐를 보조 큐로 활용하여 스택 연산을 수행할 수 있다.

### 6️⃣ 재귀 함수에서 스택이 활용되는 방식은?
재귀 호출은 내부적으로 **함수 호출 스택을 사용**하여 실행된다. 각 함수 호출은 스택 프레임에 저장되며, 함수가 종료될 때 역순으로 스택에서 제거된다.

### 7️⃣ 큐를 사용하면 발생할 수 있는 문제점과 해결 방법은?
- **메모리 낭비**: 일반 큐에서 요소를 제거하면 앞쪽 공간이 비어도 사용되지 않음 → **원형 큐(Circular Queue)** 사용
- **느린 처리 속도**: 우선순위가 필요한 경우 일반 큐는 비효율적 → **우선순위 큐(Priority Queue)** 활용

---
