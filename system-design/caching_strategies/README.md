# 캐싱 전략 (Caching Strategies)

## 1. 캐싱이란?
캐싱(Caching)은 **자주 사용하는 데이터를 빠르게 제공하기 위해 임시 저장소에 데이터를 저장하는 기술**이다. 이를 통해 **시스템 성능을 향상**시키고, 데이터베이스 또는 원격 API 요청을 줄여 응답 속도를 개선할 수 있다.

### 🔹 캐싱의 주요 목적
- **응답 속도 향상**: 데이터베이스 조회 없이 빠르게 데이터 제공
- **서버 부하 감소**: 요청 수 감소로 인해 서버의 처리 부담 완화
- **네트워크 비용 절감**: 원격 요청을 줄여 데이터 전송 비용 절약
- **시스템 확장성 개선**: 캐싱을 활용하여 많은 요청을 효율적으로 처리 가능

---

## 2. 캐싱 전략 종류

| 전략 | 설명 |
|------|------|
| **Write-Through** | 데이터를 캐시에 저장한 후 데이터베이스에도 즉시 반영 |
| **Write-Back (Write-Behind)** | 데이터를 먼저 캐시에 저장하고, 일정 시간이 지난 후 데이터베이스에 반영 |
| **Write-Around** | 데이터베이스에 직접 저장하고, 캐시에 반영하지 않음 |
| **Read-Through** | 캐시에서 데이터를 가져오고, 없으면 데이터베이스에서 읽어 캐시에 저장 |
| **Cache-Aside (Lazy Loading)** | 애플리케이션이 직접 캐시를 관리하며, 필요할 때 데이터베이스에서 가져와 캐시에 저장 |
| **Distributed Caching** | 여러 서버에서 캐시를 공유하여 확장성과 가용성을 높임 |

---

## 3. 코드 예제
### 🔹 캐싱 구현 예제
##### Java (Spring Boot - Redis Cache 적용)
```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Cacheable(value = "users", key = "#userId")
    public String getUserById(Long userId) {
        simulateSlowService();
        return "User-" + userId;
    }

    private void simulateSlowService() {
        try { Thread.sleep(3000); } catch (InterruptedException e) { }
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

async function setUser(userId, userData) {
    client.setex(`user:${userId}`, 3600, JSON.stringify(userData));
}
```

##### Python (Flask - Redis 캐싱 적용)
```python
import redis
import time

cache = redis.Redis(host='localhost', port=6379)

def get_user(user_id):
    user = cache.get(f'user:{user_id}')
    if user:
        return user.decode('utf-8')
    else:
        time.sleep(3)  # 가짜 지연 시간
        user = f"User-{user_id}"
        cache.setex(f'user:{user_id}', 3600, user)
        return user
```

---

## 4. 캐싱 사용 시 고려할 점
- **데이터 일관성 유지**: 캐시와 데이터베이스 간 동기화 필요
- **적절한 만료 시간 설정**: 캐시가 너무 자주 갱신되면 효과가 떨어질 수 있음
- **캐시 무효화(Invalidation) 전략 적용**: 데이터 변경 시 캐시 갱신 방법 고려
- **메모리 관리 최적화**: 너무 많은 데이터를 캐시에 저장하면 오히려 성능이 저하될 수 있음

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 캐싱이란 무엇이며, 왜 필요한가?
캐싱은 자주 사용하는 데이터를 빠르게 제공하기 위해 메모리 또는 저장소에 임시로 저장하는 기술이다. 이를 통해 응답 속도를 향상시키고 서버 부하를 줄일 수 있다.

### 2️⃣ 캐싱을 사용할 때 발생할 수 있는 문제점은?
- **데이터 불일치(Inconsistency)**: 원본 데이터가 변경되었을 때 캐시가 최신 상태를 유지하지 못할 가능성이 있음.
- **캐시 폭발(Cache Stampede)**: 많은 요청이 한 번에 몰려 캐시가 비어 있는 상태에서 데이터베이스에 부하가 집중됨.
- **메모리 관리 이슈**: 너무 많은 데이터를 캐시에 저장하면 메모리 부족 문제가 발생할 수 있음.

### 3️⃣ 캐싱 전략 중 Write-Through와 Write-Back의 차이는?
- **Write-Through**: 데이터를 캐시에 저장한 후, 즉시 데이터베이스에도 반영.
- **Write-Back**: 데이터를 먼저 캐시에 저장하고, 일정 시간이 지난 후 데이터베이스에 반영하여 쓰기 성능을 최적화.

### 4️⃣ Cache-Aside와 Read-Through 방식의 차이는?
- **Cache-Aside**: 애플리케이션이 직접 캐시를 관리하며, 필요할 때 데이터베이스에서 가져와 캐시에 저장.
- **Read-Through**: 캐시가 데이터베이스를 조회하고, 없으면 데이터베이스에서 가져와 자동으로 캐시에 저장.

### 5️⃣ LRU(Least Recently Used) 캐싱 알고리즘이란?
LRU는 가장 오래 사용되지 않은 데이터를 제거하는 캐싱 알고리즘이다. 제한된 캐시 공간을 효율적으로 사용하기 위해 활용된다.

### 6️⃣ 분산 캐싱(Distributed Caching)이 필요한 이유는?
- 단일 서버의 메모리 한계를 극복하고 확장성을 높이기 위해 여러 서버에서 캐시를 공유하여 사용.
- 여러 개의 서버에서 동일한 캐시를 사용할 수 있어 부하 분산이 가능.

### 7️⃣ 캐싱을 적용할 때 보안적으로 고려해야 할 사항은?
- **민감한 데이터 캐싱 방지**: 사용자 정보, 비밀번호 등의 캐싱을 피해야 함.
- **캐시 무효화 정책 명확화**: 오래된 데이터가 노출되지 않도록 TTL(Time-To-Live) 설정 필요.
- **인증된 사용자만 캐시 데이터에 접근 가능하도록 권한 관리** 적용.

---
