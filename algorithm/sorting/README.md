# 정렬 알고리즘 (Sorting Algorithms)

## 1. 정렬 알고리즘이란?
정렬(Sorting)은 **데이터를 일정한 순서대로 정렬하는 과정**을 의미한다. 다양한 정렬 알고리즘이 존재하며, 데이터의 크기, 정렬 조건, 시간 복잡도 등을 고려하여 적절한 알고리즘을 선택해야 한다.

### 🔹 정렬 알고리즘의 주요 목표
- **데이터 정렬을 통해 검색, 탐색 등의 연산을 최적화**
- **정렬된 데이터를 이용하여 빠른 이진 탐색(Binary Search) 수행 가능**
- **알고리즘의 효율성을 고려하여 적절한 방법 선택 필요**

---

## 2. 정렬 알고리즘 비교
| 정렬 알고리즘 | 시간 복잡도 (평균) | 공간 복잡도 | 특징 |
|--------------|-----------------|------------|------|
| **버블 정렬 (Bubble Sort)** | O(n²) | O(1) | 인접한 요소를 비교하며 정렬 |
| **선택 정렬 (Selection Sort)** | O(n²) | O(1) | 가장 작은 요소를 찾아 정렬 |
| **삽입 정렬 (Insertion Sort)** | O(n²) | O(1) | 이미 정렬된 부분에 삽입 |
| **병합 정렬 (Merge Sort)** | O(n log n) | O(n) | 분할 정복 방식, 안정 정렬 |
| **퀵 정렬 (Quick Sort)** | O(n log n) | O(log n) | 피벗을 기준으로 정렬, 빠름 |
| **힙 정렬 (Heap Sort)** | O(n log n) | O(1) | 힙(Heap) 자료구조 사용 |
| **계수 정렬 (Counting Sort)** | O(n + k) | O(k) | 정수 데이터에 적합 |
| **기수 정렬 (Radix Sort)** | O(nk) | O(n + k) | 숫자 기반 정렬 |

---

## 3. 코드 예제
### 🔹 정렬 알고리즘 구현
##### Java (퀵 정렬 & 병합 정렬)
```java
import java.util.Arrays;

public class SortingExample {
    public static void quickSort(int[] arr, int left, int right) {
        if (left < right) {
            int pivot = partition(arr, left, right);
            quickSort(arr, left, pivot - 1);
            quickSort(arr, pivot + 1, right);
        }
    }

    private static int partition(int[] arr, int left, int right) {
        int pivot = arr[right];
        int i = left - 1;
        for (int j = left; j < right; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, right);
        return i + 1;
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};
        quickSort(arr, 0, arr.length - 1);
        System.out.println("퀵 정렬 결과: " + Arrays.toString(arr));
    }
}
```

##### JavaScript (버블 정렬 & 삽입 정렬)
```javascript
function bubbleSort(arr) {
    let n = arr.length;
    for (let i = 0; i < n - 1; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    return arr;
}

let arr = [5, 3, 8, 4, 2];
console.log("버블 정렬 결과:", bubbleSort(arr));
```

##### Python (병합 정렬 & 힙 정렬)
```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]
        merge_sort(left_half)
        merge_sort(right_half)
        
        i = j = k = 0
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1
        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1
        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1

arr = [5, 3, 8, 4, 2]
merge_sort(arr)
print("병합 정렬 결과:", arr)
```

---

## 4. 정렬 알고리즘 사용 시 고려할 점
- **데이터 크기**: 작은 데이터셋은 단순 정렬(O(n²) 알고리즘)도 유용할 수 있음
- **메모리 사용량**: 병합 정렬은 추가 메모리를 필요로 하지만, 퀵 정렬은 적은 메모리를 사용
- **데이터의 정렬 상태**: 데이터가 이미 정렬되어 있다면 삽입 정렬이 효율적
- **안정 정렬 여부**: 동일한 값의 순서를 유지해야 하는 경우 안정 정렬 사용 필요 (병합 정렬, 삽입 정렬 등)

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 정렬 알고리즘을 선택할 때 고려해야 할 요소는?
데이터 크기, 메모리 사용량, 정렬 상태, 안정 정렬 여부 등을 고려해야 한다.

### 2️⃣ 퀵 정렬과 병합 정렬의 차이점은?
퀵 정렬은 **피벗을 중심으로 분할 정복 방식**을 사용하며 평균적으로 O(n log n) 성능을 가진다. 반면 병합 정렬은 항상 O(n log n) 시간이 걸리며, 추가 메모리가 필요하다.

### 3️⃣ 안정 정렬이란 무엇인가?
정렬 후에도 **같은 값이 입력된 순서를 유지하는 정렬 알고리즘**을 의미한다. 예: 병합 정렬, 삽입 정렬

### 4️⃣ 힙 정렬의 특징은?
힙 자료구조를 기반으로 동작하며, **최대 힙 또는 최소 힙을 사용하여 정렬**한다. 최악의 경우에도 O(n log n) 성능을 유지한다.

### 5️⃣ O(n²) 정렬 알고리즘이 언제 유용할 수 있는가?
데이터 크기가 작은 경우(예: 100개 이하)에는 버블 정렬, 삽입 정렬 등이 더 빠를 수도 있다.

### 6️⃣ 계수 정렬(Counting Sort)의 제한점은?
데이터 값의 범위가 크면 많은 메모리가 필요하므로, **정수 데이터에만 적합**하다.

### 7️⃣ 가장 효율적인 정렬 알고리즘은 무엇인가?
대부분의 경우 퀵 정렬이 빠르지만, 데이터 특성에 따라 병합 정렬, 힙 정렬, 계수 정렬 등이 더 적합할 수 있다.

---
