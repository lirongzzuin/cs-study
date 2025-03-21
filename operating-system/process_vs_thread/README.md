# 프로세스 vs 스레드

## 1. 프로세스(Process)란?
프로세스는 실행 중인 프로그램을 의미하며, 운영체제에서 독립적으로 실행된다. 
각 프로세스는 자체 메모리 공간(코드, 데이터, 힙, 스택 영역)을 가지며, 다른 프로세스와 메모리를 공유하지 않는다.

### 🔹 프로세스의 주요 특징
- 독립적인 실행 단위이며, 운영체제에서 개별적으로 관리됨
- 각 프로세스는 자신만의 메모리 공간을 가짐 (주소 공간 분리)
- 프로세스 간 데이터 교환은 **IPC(Inter Process Communication)** 기법을 사용해야 함
- 운영체제의 스케줄러에 의해 CPU 할당을 받아 실행됨

### 🔹 프로세스의 메모리 구조
1. **코드(Code) 영역**: 실행할 프로그램 코드가 저장됨
2. **데이터(Data) 영역**: 전역 변수, 정적 변수 등이 저장됨
3. **힙(Heap) 영역**: 동적으로 할당된 메모리가 저장됨
4. **스택(Stack) 영역**: 함수 호출 및 지역 변수가 저장됨

## 2. 스레드(Thread)란?
스레드는 프로세스 내에서 실행되는 실행 단위로, 하나의 프로세스는 여러 개의 스레드를 가질 수 있다.
스레드는 같은 프로세스 내에서 **코드, 데이터, 힙 영역을 공유**하지만, 개별적인 **스택**을 가진다.

### 🔹 스레드의 주요 특징
- 같은 프로세스 내에서 실행되며, 메모리를 공유함
- 독립적인 스택을 가지지만, 코드, 데이터, 힙 영역은 공유됨
- 컨텍스트 스위칭 비용이 낮아 성능이 향상됨
- 멀티스레딩을 통해 병렬 처리가 가능함

## 3. 프로세스와 스레드의 차이점
| 구분 | 프로세스 | 스레드 |
|------|---------|--------|
| 실행 단위 | 독립적인 실행 단위 | 프로세스 내의 실행 단위 |
| 메모리 공간 | 독립적 | 공유 (코드, 데이터, 힙) |
| 데이터 공유 | 불가능 (IPC 필요) | 가능 (단, 스택은 독립적) |
| 생성 속도 | 느림 (새로운 메모리 공간 필요) | 빠름 (메모리 공유로 인해 가벼움) |
| 문맥 전환 비용 | 높음 | 낮음 |

## 4. 언제 프로세스를 사용하고, 언제 스레드를 사용할까?
- **프로세스 사용 사례**
  - 독립적인 실행 환경이 필요한 경우 (예: 웹 브라우저의 여러 탭을 각각 별도 프로세스로 실행)
  - 강한 격리가 필요한 경우 (예: 보안이 중요한 애플리케이션)

- **스레드 사용 사례**
  - 같은 프로세스 내에서 빠른 실행이 필요한 경우 (예: 웹 서버의 다중 요청 처리)
  - 멀티코어 프로세서의 성능을 극대화할 때 (예: 병렬 계산 작업)

## 5. 코드 예제
### 🔹 멀티프로세스 예제 (Java)
```java
class ProcessExample {
    public static void main(String[] args) throws Exception {
        ProcessBuilder processBuilder = new ProcessBuilder("notepad.exe");
        Process process = processBuilder.start();
        System.out.println("새 프로세스 생성됨: " + process.pid());
    }
}
```

### 🔹 멀티스레드 예제 (Java)
```java
class ThreadExample extends Thread {
    public void run() {
        System.out.println("스레드 실행 중: " + Thread.currentThread().getName());
    }
    public static void main(String[] args) {
        ThreadExample t1 = new ThreadExample();
        t1.start();
    }
}
```

### 🔹 멀티프로세스 예제 (JavaScript)
```javascript
const { exec } = require('child_process');
exec('notepad.exe', (error, stdout, stderr) => {
    if (error) console.error(`실패: ${error.message}`);
    else console.log("새 프로세스 생성됨");
});
```

### 🔹 멀티스레드 예제 (JavaScript)
```javascript
function worker() {
    console.log(`스레드 실행 중: ${process.pid}`);
}
setTimeout(worker, 1000);
```

### 🔹 멀티프로세스 예제 (Python)
```python
import os

def child_process():
    print(f"자식 프로세스 실행 중, PID: {os.getpid()}")

if __name__ == "__main__":
    pid = os.fork()
    if pid == 0:
        child_process()
    else:
        print(f"부모 프로세스 실행 중, PID: {os.getpid()}, 자식 PID: {pid}")
```

### 🔹 멀티스레드 예제 (Python)
```python
import threading

def worker():
    print(f"스레드 실행 중: {threading.current_thread().name}")

threads = []
for _ in range(3):
    t = threading.Thread(target=worker)
    threads.append(t)
    t.start()

for t in threads:
    t.join()
```

## 6. 정리
- **프로세스**는 독립적인 실행 단위로, 각 프로세스는 자체 메모리 공간을 가짐.
- **스레드**는 같은 프로세스 내에서 실행되며, 메모리를 공유하여 더 가볍고 빠름.
- 상황에 따라 적절한 실행 방식을 선택하는 것이 중요함 (독립성 vs 성능 최적화 고려).

