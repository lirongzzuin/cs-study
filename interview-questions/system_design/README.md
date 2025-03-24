# 시스템 설계 면접 질문 정리 (System Design Interview Questions)

## 1. 시스템 설계 개요
시스템 설계(System Design)는 **대규모 애플리케이션을 구축하는 과정에서 아키텍처, 데이터 관리, 확장성, 성능 최적화 등을 고려하는 설계 기법**이다. 면접에서는 트래픽 처리, 데이터 저장, 서비스 확장성 등 **실제 시스템 구축에서 직면할 문제를 해결하는 능력**을 평가한다.

### 🔹 시스템 설계의 핵심 요소
- **확장성(Scalability)**: 트래픽 증가 시 시스템이 원활하게 동작하도록 설계
- **가용성(Availability)**: 장애 발생 시에도 서비스를 지속적으로 제공
- **일관성(Consistency)**: 데이터 정합성을 유지하는 구조 설계
- **내결함성(Fault Tolerance)**: 장애 발생 시 빠른 복구 가능하도록 구성
- **보안(Security)**: 데이터 보호 및 접근 제어 전략 적용

---

## 2. 시스템 설계 면접 질문 및 답변

### 1️⃣ 확장성을 고려한 시스템 설계 방법은?
- **수직 확장(Scale-Up)**: 서버 성능을 향상 (CPU, RAM 증가)
- **수평 확장(Scale-Out)**: 여러 대의 서버를 추가하여 부하 분산 (로드 밸런싱 활용)
- **캐싱(Caching) 활용**: Redis, Memcached 등을 사용하여 빠른 응답 제공
- **데이터베이스 샤딩(Sharding)**: 데이터를 여러 개의 DB 인스턴스로 분할하여 성능 최적화

### 2️⃣ 로드 밸런싱이란?
- 트래픽을 여러 서버로 분산하여 성능을 개선하는 기술
- **L4(네트워크 계층) 로드 밸런싱**: TCP/UDP 기반으로 부하 분산
- **L7(애플리케이션 계층) 로드 밸런싱**: HTTP 기반으로 요청을 분산 (예: URL 패턴 기반 분배)

### 3️⃣ 데이터베이스 확장 전략은?
| 확장 방식 | 설명 |
|----------|------|
| **레플리케이션(Replication)** | 데이터를 여러 개의 복제본으로 유지하여 읽기 성능 향상 |
| **샤딩(Sharding)** | 데이터를 여러 개의 DB 인스턴스에 분산 저장하여 쓰기 성능 향상 |
| **캐싱(Caching)** | 자주 조회하는 데이터를 Redis, Memcached와 같은 캐시 시스템에 저장 |

### 4️⃣ 메시지 큐(Message Queue)란?
- **비동기 처리 및 이벤트 기반 아키텍처** 구현에 사용됨
- 대표적인 MQ 시스템: RabbitMQ, Kafka, AWS SQS
- **사용 사례**: 주문 처리 시스템, 비동기 이메일 전송, 로그 수집

### 5️⃣ REST API와 GraphQL의 차이점은?
| 항목 | REST API | GraphQL |
|------|----------|---------|
| 데이터 요청 방식 | 엔드포인트별 고정된 응답 | 클라이언트가 필요한 데이터만 요청 |
| 오버페칭 문제 | 발생 가능 | 해결 가능 |
| 언더페칭 문제 | 해결 어려움 | 원하는 데이터만 가져옴 |
| 복잡성 | 상대적으로 단순 | 클라이언트가 유연한 요청 가능 |

### 6️⃣ CDN(Content Delivery Network)이란?
- 전 세계 여러 지역에 **캐시 서버를 배치**하여 콘텐츠를 빠르게 제공하는 기술
- **장점**:
  - 웹사이트 로딩 속도 개선
  - 서버 부하 감소
  - DDoS 공격 방어

### 7️⃣ CAP 이론이란?
- **일관성(Consistency), 가용성(Availability), 네트워크 파티션 허용(Partition Tolerance)** 중 **동시에 두 가지만 보장 가능**
- **CP 시스템**: 일관성과 네트워크 파티션을 보장 (예: Zookeeper)
- **AP 시스템**: 가용성과 네트워크 파티션을 보장 (예: Cassandra, DynamoDB)

---

## 3. 코드 예제
### 🔹 로드 밸런싱과 캐싱 적용 예제
##### Java (Spring Boot - Redis 캐싱 적용)
```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Cacheable(value = "users", key = "#userId")
    public String getUserById(Long userId) {
        return "User-" + userId;
    }
}
```

##### JavaScript (Node.js - Redis 캐싱 적용)
```javascript
const redis = require("redis");
const client = redis.createClient();

async function getUser(userId) {
    return new Promise((resolve, reject) => {
        client.get(`user:${userId}`, (err, data) => {
            if (data) resolve(JSON.parse(data));
            else reject("Cache miss");
        });
    });
}
```

##### Python (Flask - Redis 캐싱 적용)
```python
import redis
cache = redis.Redis(host='localhost', port=6379)

def get_user(user_id):
    user = cache.get(f'user:{user_id}')
    if user:
        return user.decode('utf-8')
    else:
        return "User not found"
```

---

## 4. 시스템 설계 시 고려할 점
- **트래픽 증가에 대비한 확장성 확보** (로드 밸런싱, 샤딩, 캐싱 활용)
- **데이터 일관성과 가용성 간의 균형 조정** (CAP 이론 고려)
- **비동기 처리를 통한 성능 최적화** (메시지 큐, 이벤트 기반 아키텍처)
- **보안 및 장애 대응 시스템 구축** (DDoS 방어, 모니터링, 로깅 시스템 활용)

---

## 5. 결론
시스템 설계는 **트래픽 처리, 데이터 저장, 서비스 확장성, 성능 최적화, 보안** 등을 고려하여 아키텍처를 결정하는 과정이다. 면접에서는 특정 요구사항에 맞춰 **확장성, 가용성, 일관성 간의 트레이드오프를 고려하는 능력**이 중요하다. 단순 개념 암기보다 **실제 시스템 구축 경험과 다양한 설계 패턴에 대한 이해가 핵심**이다.

---
