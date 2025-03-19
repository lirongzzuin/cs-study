# 운영체제 면접 질문 정리 (Operating System Interview Questions)

## 1. 운영체제 개요
운영체제(OS, Operating System)는 **컴퓨터 하드웨어와 소프트웨어를 관리하는 시스템 소프트웨어**이다. 다양한 기능을 제공하며, 효율적인 자원 관리를 통해 애플리케이션 실행을 지원한다.

### 🔹 운영체제의 주요 역할
- **프로세스 관리(Process Management)**: 프로그램 실행 및 스케줄링 관리
- **메모리 관리(Memory Management)**: RAM 할당 및 가상 메모리 관리
- **파일 시스템 관리(File System Management)**: 저장 장치의 파일 및 디렉터리 관리
- **장치 관리(Device Management)**: 하드웨어 장치와의 인터페이스 제공
- **보안 및 접근 제어(Security & Access Control)**: 사용자 인증 및 권한 관리

---

## 2. 운영체제 면접 질문 및 답변

### 1️⃣ 프로세스와 스레드의 차이점은?
- **프로세스(Process)**: 실행 중인 프로그램의 인스턴스로, 독립적인 메모리 공간을 가짐
- **스레드(Thread)**: 프로세스 내에서 실행되는 작은 실행 단위로, 같은 메모리 공간을 공유함

### 2️⃣ 멀티스레딩(Multithreading)의 장점은?
- 응답성(Response Time) 향상
- 자원 공유를 통한 메모리 절약
- 병렬 실행을 통한 성능 개선

### 3️⃣ 운영체제의 CPU 스케줄링 알고리즘 종류는?
| 알고리즘 | 설명 |
|---------|------|
| **FCFS (First Come First Serve)** | 먼저 도착한 프로세스부터 실행 |
| **SJF (Shortest Job First)** | 실행 시간이 가장 짧은 프로세스부터 실행 |
| **Round Robin** | 시간 할당량(Time Quantum) 기반으로 프로세스를 순환 실행 |
| **Priority Scheduling** | 우선순위가 높은 프로세스를 먼저 실행 |
| **Multilevel Queue** | 여러 개의 대기열을 사용하여 프로세스를 분류하고 실행 |

### 4️⃣ 가상 메모리(Virtual Memory)란?
- 물리적 메모리보다 더 많은 메모리를 사용할 수 있도록 **디스크 공간을 활용하는 메모리 관리 기법**
- **페이지 교체 알고리즘**을 통해 사용되지 않는 페이지를 스왑 아웃하여 메모리를 최적화함

### 5️⃣ 페이지 교체 알고리즘(Page Replacement Algorithms) 종류는?
| 알고리즘 | 설명 |
|---------|------|
| **FIFO (First In First Out)** | 가장 먼저 들어온 페이지를 먼저 교체 |
| **LRU (Least Recently Used)** | 가장 오랫동안 사용되지 않은 페이지를 교체 |
| **Optimal (OPT)** | 앞으로 가장 사용되지 않을 페이지를 교체 (이론적 최적) |

### 6️⃣ 동기화 문제(Synchronization Problem)와 해결 방법은?
- **동기화 문제**: 여러 프로세스/스레드가 동일한 자원을 동시에 접근할 때 발생하는 문제
- **해결 방법**: 세마포어(Semaphore), 뮤텍스(Mutex), 모니터(Monitor) 등을 사용하여 **경쟁 조건(Race Condition)을 방지**

### 7️⃣ 교착 상태(Deadlock)의 조건과 해결 방법은?
#### 🔹 교착 상태 발생 조건 (Coffman 조건)
1. **상호 배제(Mutual Exclusion)**: 한 번에 한 프로세스만 자원을 사용할 수 있음
2. **점유와 대기(Hold and Wait)**: 자원을 점유한 상태에서 다른 자원을 요청
3. **비선점(Non-preemptive)**: 강제적으로 자원을 빼앗을 수 없음
4. **순환 대기(Circular Wait)**: 프로세스 간 순환적인 자원 대기 상태 발생

#### 🔹 해결 방법
- **교착 상태 예방(Deadlock Prevention)**: Coffman 조건 중 하나 이상을 제거
- **교착 상태 회피(Deadlock Avoidance)**: 자원 할당 그래프, 은행가 알고리즘(Banker's Algorithm) 활용
- **교착 상태 탐지(Deadlock Detection) 및 복구(Recovery)**: 발생 시 프로세스 종료 또는 자원 회수

---

## 3. 코드 예제
### 🔹 뮤텍스를 활용한 스레드 동기화 예제
##### Java (Mutex 사용)
```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class SharedResource {
    private int count = 0;
    private final Lock lock = new ReentrantLock();
    
    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }

    public int getCount() {
        return count;
    }
}
```

##### Python (뮤텍스 사용)
```python
import threading

class SharedResource:
    def __init__(self):
        self.count = 0
        self.lock = threading.Lock()

    def increment(self):
        with self.lock:
            self.count += 1
```

---

## 4. 운영체제 사용 시 고려할 점
- **멀티태스킹 환경에서의 자원 관리**
- **병렬 프로세스 및 스레드 동기화 문제**
- **CPU 및 메모리 사용 최적화 기법**
- **보안 및 접근 제어 정책 고려**

---

## 5. 결론
운영체제는 **컴퓨터 시스템의 핵심 요소**로, 프로세스 관리, 메모리 관리, 파일 시스템, 보안 등의 다양한 기능을 제공한다. 면접에서는 **운영체제 개념과 관련된 알고리즘 및 코드 구현 능력을 평가**하므로, 개념을 정확히 이해하고 적용할 수 있도록 준비해야 한다.

---