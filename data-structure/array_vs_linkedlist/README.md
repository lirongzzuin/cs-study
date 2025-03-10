# 배열(Array) vs 연결 리스트(Linked List)

## 1. 배열과 연결 리스트란?
배열(Array)과 연결 리스트(Linked List)는 **데이터를 저장하는 선형 자료구조**이다. 각각의 특성과 차이를 이해하면 상황에 따라 적절한 자료구조를 선택할 수 있다.

### 🔹 배열(Array)
- **연속된 메모리 공간에 요소를 저장**하는 자료구조
- **고정된 크기**를 가지며, 선언 시 크기를 지정해야 함
- **인덱스를 사용한 O(1) 랜덤 접근 가능**

### 🔹 연결 리스트(Linked List)
- **노드(Node)와 포인터로 구성된 동적 자료구조**
- **크기가 가변적이며 동적으로 메모리 할당 가능**
- **연속된 메모리 공간이 필요하지 않음**

---

## 2. 배열 vs 연결 리스트 비교
| 특징 | 배열(Array) | 연결 리스트(Linked List) |
|------|------------|--------------------------|
| **메모리 구조** | 연속된 메모리 공간 | 노드와 포인터로 연결 |
| **삽입/삭제** | 느림 (O(n), 중간 요소 추가/삭제 시 이동 필요) | 빠름 (O(1) 또는 O(n), 포인터만 변경) |
| **검색 속도** | 빠름 (O(1), 인덱스로 접근 가능) | 느림 (O(n), 순차 탐색 필요) |
| **메모리 사용량** | 효율적 (추가 메모리 필요 없음) | 비효율적 (포인터 저장 공간 필요) |
| **크기 조정** | 고정 크기 (재할당 필요) | 동적 크기 조정 가능 |

---

## 3. 코드 예제
### 🔹 배열 vs 연결 리스트 구현
##### Java (배열과 연결 리스트 구현)
```java
import java.util.LinkedList;
import java.util.Arrays;

public class ArrayVsLinkedList {
    public static void main(String[] args) {
        // 배열 사용
        int[] array = {1, 2, 3, 4, 5};
        System.out.println("배열: " + Arrays.toString(array));
        
        // 연결 리스트 사용
        LinkedList<Integer> linkedList = new LinkedList<>();
        linkedList.add(1);
        linkedList.add(2);
        linkedList.add(3);
        System.out.println("연결 리스트: " + linkedList);
    }
}
```

##### JavaScript (배열과 연결 리스트 구현)
```javascript
class ListNode {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
    }
    add(value) {
        const newNode = new ListNode(value);
        if (!this.head) this.head = newNode;
        else {
            let current = this.head;
            while (current.next) current = current.next;
            current.next = newNode;
        }
    }
}

const array = [1, 2, 3, 4, 5];
console.log("배열:", array);

const linkedList = new LinkedList();
linkedList.add(1);
linkedList.add(2);
linkedList.add(3);
console.log("연결 리스트:", JSON.stringify(linkedList));
```

##### Python (배열과 연결 리스트 구현)
```python
class ListNode:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def add(self, value):
        if not self.head:
            self.head = ListNode(value)
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = ListNode(value)

# 배열 사용
array = [1, 2, 3, 4, 5]
print("배열:", array)

# 연결 리스트 사용
linked_list = LinkedList()
linked_list.add(1)
linked_list.add(2)
linked_list.add(3)
print("연결 리스트:", linked_list.head.value, "->", linked_list.head.next.value, "->", linked_list.head.next.next.value)
```

---

## 4. 배열과 연결 리스트 사용 시 고려할 점
- **배열은 랜덤 접근이 필요할 때 유리** (O(1) 접근 속도)
- **연결 리스트는 삽입/삭제가 빈번할 때 유리** (O(1) 삽입/삭제 속도)
- **메모리 사용량 고려**: 연결 리스트는 추가적인 포인터 공간이 필요하여 메모리 사용량이 많음
- **연속된 메모리 할당이 어려운 경우 연결 리스트가 적합**

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 배열과 연결 리스트의 차이점은?
배열은 **연속된 메모리 공간**에 데이터를 저장하는 반면, 연결 리스트는 **노드와 포인터를 이용하여 동적으로 메모리를 할당**하는 자료구조이다.

### 2️⃣ 배열에서 특정 요소를 삭제할 때 시간 복잡도는?
배열에서 특정 요소를 삭제하려면 **삭제 후 나머지 요소를 이동해야 하므로 O(n)의 시간 복잡도**가 발생한다.

### 3️⃣ 연결 리스트에서 특정 요소를 검색할 때 시간 복잡도는?
연결 리스트는 순차 탐색을 해야 하므로 평균적으로 **O(n)의 시간 복잡도**가 소요된다.

### 4️⃣ 연결 리스트가 배열보다 유리한 경우는?
삽입과 삭제가 빈번하게 발생하는 경우 연결 리스트가 더 효율적이다. 특히, **중간 위치에서 데이터를 자주 추가/삭제해야 할 경우** 적합하다.

### 5️⃣ 배열이 연결 리스트보다 유리한 경우는?
랜덤 접근이 필요한 경우 배열이 더 적합하다. **인덱스를 이용한 O(1) 접근 속도** 덕분에 데이터를 빠르게 검색할 수 있다.

### 6️⃣ 연결 리스트에서 메모리 사용량이 증가하는 이유는?
연결 리스트는 각 노드가 **데이터뿐만 아니라 다음 노드를 가리키는 포인터도 저장해야 하기 때문**에 배열보다 메모리를 더 많이 사용한다.

### 7️⃣ 연결 리스트의 단점은 무엇인가?
- 메모리 사용량 증가 (포인터를 저장해야 함)
- 랜덤 접근이 불가능 (순차 탐색 필요, O(n) 속도)
- 캐시 효율성이 낮음 (메모리의 비연속적 할당으로 인해 CPU 캐시 활용이 어려움)

---
