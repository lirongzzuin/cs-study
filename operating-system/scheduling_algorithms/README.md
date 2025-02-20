# CPU 스케줄링 알고리즘 (Scheduling Algorithms)

## 1. 스케줄링이란?
운영체제에서 CPU는 여러 프로세스를 동시에 실행해야 하므로, **어떤 프로세스에게 CPU를 할당할 것인지 결정하는 과정**이 필요하다. 이를 **CPU 스케줄링**이라 하며, 다양한 스케줄링 알고리즘이 존재한다.

### 🔹 스케줄링의 주요 목표
- **공정성(Fairness)**: 모든 프로세스가 공정하게 CPU를 사용할 수 있도록 보장
- **CPU 이용률 최대화(CPU Utilization)**: CPU가 최대한 효율적으로 사용되도록 함
- **처리량(Throughput) 증가**: 일정 시간 동안 처리할 수 있는 프로세스 개수를 증가
- **응답 시간(Response Time) 최소화**: 사용자에게 빠른 응답 제공
- **대기 시간(Waiting Time) 및 반환 시간(Turnaround Time) 최소화**

---

## 2. CPU 스케줄링 알고리즘 종류
CPU 스케줄링 알고리즘은 **비선점(Non-Preemptive)과 선점(Preemptive) 방식**으로 나뉜다.

| 구분 | 설명 |
|------|------|
| **비선점(Non-Preemptive) 스케줄링** | 프로세스가 CPU를 할당받으면 끝날 때까지 유지 |
| **선점(Preemptive) 스케줄링** | 더 높은 우선순위의 프로세스가 오면 CPU를 양보 |

### 🔹 1️⃣ FCFS (First Come First Served, 선착순)
- 먼저 도착한 프로세스부터 순차적으로 실행
- **비선점 방식**
- **장점**: 구현이 간단함
- **단점**: **Convoy Effect (호위 효과)** 발생 가능 (긴 작업이 짧은 작업을 지연시킴)

#### 예제 코드
##### Java
```java
import java.util.Arrays;

class FCFS {
    static void findWaitingTime(int processes[], int n, int bt[], int wt[]) {
        wt[0] = 0;
        for (int i = 1; i < n; i++) {
            wt[i] = bt[i - 1] + wt[i - 1];
        }
    }

    static void findTurnAroundTime(int processes[], int n, int bt[], int wt[], int tat[]) {
        for (int i = 0; i < n; i++) {
            tat[i] = bt[i] + wt[i];
        }
    }

    public static void main(String[] args) {
        int processes[] = {1, 2, 3};
        int n = processes.length;
        int burst_time[] = {10, 5, 8};
        int waiting_time[] = new int[n];
        int turn_around_time[] = new int[n];

        findWaitingTime(processes, n, burst_time, waiting_time);
        findTurnAroundTime(processes, n, burst_time, waiting_time, turn_around_time);

        System.out.println("Processes Burst time Waiting time Turnaround time");
        for (int i = 0; i < n; i++) {
            System.out.println(processes[i] + "\t" + burst_time[i] + "\t\t" + waiting_time[i] + "\t\t" + turn_around_time[i]);
        }
    }
}
```

##### JavaScript
```javascript
function fcfs(burstTimes) {
    let waitingTime = [0];
    let turnAroundTime = [burstTimes[0]];
    
    for (let i = 1; i < burstTimes.length; i++) {
        waitingTime[i] = waitingTime[i - 1] + burstTimes[i - 1];
        turnAroundTime[i] = waitingTime[i] + burstTimes[i];
    }
    
    return { waitingTime, turnAroundTime };
}

const burstTimes = [10, 5, 8];
console.log(fcfs(burstTimes));
```

##### Python
```python
def fcfs(burst_times):
    waiting_time = [0]
    turnaround_time = [burst_times[0]]
    
    for i in range(1, len(burst_times)):
        waiting_time.append(waiting_time[i - 1] + burst_times[i - 1])
        turnaround_time.append(waiting_time[i] + burst_times[i])
    
    return waiting_time, turnaround_time

burst_times = [10, 5, 8]
print(fcfs(burst_times))
```

---

### 🔹 2️⃣ SJF (Shortest Job First, 최단 작업 우선)
- 실행 시간이 가장 짧은 프로세스를 우선 실행
- **비선점/선점 방식 가능**
- **장점**: 평균 대기 시간 최소화 가능
- **단점**: **Starvation(기아 현상)** 발생 가능 (긴 작업이 계속 뒤로 밀림)

### 🔹 3️⃣ Round Robin (라운드 로빈)
- **선점 방식**, 모든 프로세스가 **일정한 시간(Time Quantum, 시간 할당량) 동안 CPU를 사용**
- **장점**: 모든 프로세스가 공정하게 CPU를 사용할 수 있음
- **단점**: 적절한 Time Quantum 설정이 중요

### 🔹 4️⃣ Priority Scheduling (우선순위 스케줄링)
- 각 프로세스에 **우선순위(priority)**를 부여하여 높은 우선순위부터 실행
- **비선점/선점 방식 가능**
- **단점**: 낮은 우선순위의 프로세스가 무한정 기다릴 가능성 (Aging 기법으로 해결 가능)

---

## 3. 정리
- **FCFS**: 단순하지만 긴 작업이 짧은 작업을 지연시킬 수 있음
- **SJF**: 평균 대기 시간 최소화, 하지만 기아 현상 가능
- **Round Robin**: 공정성 보장, 하지만 Time Quantum 조정이 중요
- **Priority Scheduling**: 중요한 작업을 우선 처리 가능, 하지만 낮은 우선순위 작업의 기아 현상 해결 필요

각 알고리즘은 상황에 맞게 선택해야 하며, **운영체제 및 응용 프로그램의 특성에 따라 적절한 방식이 적용**된다.
