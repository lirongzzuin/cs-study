# 메모리 관리 (Memory Management)

## 1. 메모리 관리란?
메모리 관리는 운영체제가 프로세스에 메모리를 할당하고, 효율적으로 사용할 수 있도록 관리하는 기법이다. 효율적인 메모리 관리는 시스템 성능에 직접적인 영향을 미친다.

### 🔹 메모리 관리의 주요 목표
- **효율적인 메모리 사용**: 메모리 낭비를 줄이고 최적화된 방식으로 활용
- **프로세스 간 메모리 보호**: 프로세스가 다른 프로세스의 메모리에 접근하지 못하도록 보호
- **가용 메모리 최대화**: 다수의 프로세스가 동시에 실행될 수 있도록 관리

## 2. 메모리 관리 기법
운영체제는 다양한 방식으로 메모리를 관리하며, 대표적인 기법은 다음과 같다.

### 🔹 단순 메모리 관리 (Single Contiguous Allocation)
- 하나의 프로그램만 실행되는 구조
- 메모리 전체를 하나의 프로세스에 할당
- **장점**: 구현이 간단하고 관리가 용이함
- **단점**: 멀티태스킹 불가능, 메모리 낭비 발생

### 🔹 고정 분할 (Fixed Partitioning)
- 메모리를 미리 정해진 크기의 고정된 블록으로 나눠서 관리
- **장점**: 관리가 비교적 단순함
- **단점**: 내부 단편화(Internal Fragmentation) 발생 가능

### 🔹 동적 분할 (Dynamic Partitioning)
- 프로세스가 필요할 때마다 필요한 크기만큼 메모리를 할당
- **장점**: 고정 분할 방식보다 유연함, 내부 단편화 문제 감소
- **단점**: 외부 단편화(External Fragmentation) 발생 가능

### 🔹 가상 메모리 (Virtual Memory)
- 실제 물리적 메모리(RAM)보다 더 큰 메모리를 사용할 수 있도록 하는 기술
- 디스크의 일부를 가상 메모리(스왑 영역)로 활용하여 실행 가능
- **장점**: 여러 개의 프로세스를 실행할 수 있으며, 큰 프로그램도 실행 가능
- **단점**: 디스크 I/O가 많아지면 속도 저하 발생 (페이지 폴트 문제)

## 3. 페이징과 세그멘테이션

### 🔹 페이징 (Paging)
- 물리 메모리를 일정 크기(페이지 프레임)로 나누고, 프로세스의 메모리를 동일한 크기(페이지)로 분할하여 관리
- **장점**: 외부 단편화 문제 해결, 효율적인 메모리 활용
- **단점**: 페이지 테이블 관리 비용 발생

### 🔹 세그멘테이션 (Segmentation)
- 프로그램을 논리적인 단위(코드, 데이터, 스택 등)로 나누어 메모리에 배치
- **장점**: 프로세스 구조에 맞게 메모리를 배치할 수 있음
- **단점**: 외부 단편화 문제 발생 가능

## 4. 메모리 단편화와 해결 방법
메모리 관리에서는 **단편화(Fragmentation)** 문제가 발생할 수 있으며, 크게 두 가지 유형이 있다.

### 🔹 내부 단편화 (Internal Fragmentation)
- 고정 분할 방식에서 프로세스가 필요한 메모리보다 더 큰 블록을 할당받아 발생
- **해결 방법**: 동적 분할 방식 사용, 메모리 블록 크기 조정

### 🔹 외부 단편화 (External Fragmentation)
- 동적 분할 방식에서 작은 빈 공간이 많이 생겨서 메모리를 효율적으로 사용하지 못하는 문제
- **해결 방법**: 압축(Compaction) 기법, 페이징 기법 사용

## 5. 코드 예제
### 🔹 메모리 관리 기법 예제 (Java)
```java
class MemoryBlock {
    int size;
    boolean allocated;
    
    public MemoryBlock(int size) {
        this.size = size;
        this.allocated = false;
    }
}

class MemoryManager {
    MemoryBlock[] memory;
    
    public MemoryManager(int totalMemory) {
        memory = new MemoryBlock[totalMemory / 100];
        for (int i = 0; i < memory.length; i++) {
            memory[i] = new MemoryBlock(100);
        }
    }
    
    public MemoryBlock allocate(int processSize) {
        for (MemoryBlock block : memory) {
            if (!block.allocated && block.size >= processSize) {
                block.allocated = true;
                System.out.println("메모리 " + block.size + "KB 할당됨");
                return block;
            }
        }
        System.out.println("메모리 부족");
        return null;
    }
    
    public void deallocate(MemoryBlock block) {
        block.allocated = false;
        System.out.println("메모리 " + block.size + "KB 해제됨");
    }
}
```

### 🔹 메모리 관리 기법 예제 (JavaScript)
```javascript
class MemoryBlock {
    constructor(size) {
        this.size = size;
        this.allocated = false;
    }
}

class MemoryManager {
    constructor(totalMemory) {
        this.memory = Array.from({ length: totalMemory / 100 }, () => new MemoryBlock(100));
    }
    
    allocate(processSize) {
        for (let block of this.memory) {
            if (!block.allocated && block.size >= processSize) {
                block.allocated = true;
                console.log(`메모리 ${block.size}KB 할당됨`);
                return block;
            }
        }
        console.log("메모리 부족");
        return null;
    }
    
    deallocate(block) {
        block.allocated = false;
        console.log(`메모리 ${block.size}KB 해제됨`);
    }
}
```

### 🔹 메모리 관리 기법 예제 (Python)
```python
class MemoryBlock:
    def __init__(self, size):
        self.size = size
        self.allocated = False

class MemoryManager:
    def __init__(self, total_memory):
        self.memory = [MemoryBlock(100) for _ in range(total_memory // 100)]
    
    def allocate(self, process_size):
        for block in self.memory:
            if not block.allocated and block.size >= process_size:
                block.allocated = True
                print(f"메모리 {block.size}KB 할당됨")
                return block
        print("메모리 부족")
        return None
    
    def deallocate(self, block):
        block.allocated = False
        print(f"메모리 {block.size}KB 해제됨")
```

## 6. 정리
이제 메모리 관리의 기본 개념과 기법을 이해할 수 있게 되었다. 실제로 운영체제에서 어떻게 동작하는지 더 깊이 연구해보면 좋을 것 같다!
