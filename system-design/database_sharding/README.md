# 데이터베이스 샤딩 (Database Sharding)

## 1. 데이터베이스 샤딩이란?
데이터베이스 샤딩(Database Sharding)은 **데이터를 여러 개의 작은 데이터베이스(샤드, Shard)로 분할하여 저장하는 수평 확장(Scale-Out) 기술**이다. 이는 데이터베이스의 성능과 확장성을 높이는 데 사용된다.

### 🔹 데이터베이스 샤딩의 주요 목적
- **데이터베이스 성능 개선**: 단일 데이터베이스의 부하를 줄이고 트래픽을 분산
- **확장성 확보**: 수평 확장(Scale-Out)을 통해 대량의 데이터를 처리 가능
- **고가용성(High Availability) 보장**: 특정 샤드 장애 발생 시 전체 서비스 중단 방지

---

## 2. 샤딩 방식
| 샤딩 방식 | 설명 |
|-----------|------|
| **범위 기반 샤딩 (Range-Based Sharding)** | 특정 범위의 데이터를 하나의 샤드에 저장 (예: ID 1~1000, 1001~2000) |
| **해시 기반 샤딩 (Hash-Based Sharding)** | 특정 키(예: 사용자 ID)를 해시 함수로 변환하여 샤드 결정 |
| **디렉터리 기반 샤딩 (Directory-Based Sharding)** | 샤드 정보를 저장하는 중앙 디렉터리를 통해 특정 샤드에 데이터를 저장 |
| **지리적 샤딩 (Geographical Sharding)** | 지역별 데이터를 해당 지역의 샤드에 저장 |

---

## 3. 코드 예제
### 🔹 데이터 샤딩 구현 예제
##### Java (Spring Boot - 샤딩 적용)
```java
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Service;

@Service
public class ShardingService {
    private final JdbcTemplate db1;
    private final JdbcTemplate db2;

    public ShardingService(JdbcTemplate db1, JdbcTemplate db2) {
        this.db1 = db1;
        this.db2 = db2;
    }

    public void saveUser(int userId, String name) {
        JdbcTemplate selectedDb = (userId % 2 == 0) ? db1 : db2;
        selectedDb.update("INSERT INTO users (id, name) VALUES (?, ?)", userId, name);
    }
}
```

##### JavaScript (Node.js - 해시 기반 샤딩 적용)
```javascript
const mysql = require('mysql2/promise');
const db1 = mysql.createPool({ host: 'db1.example.com', user: 'user', database: 'shard1' });
const db2 = mysql.createPool({ host: 'db2.example.com', user: 'user', database: 'shard2' });

async function saveUser(userId, name) {
    const db = userId % 2 === 0 ? db1 : db2;
    await db.query("INSERT INTO users (id, name) VALUES (?, ?)", [userId, name]);
}
```

##### Python (Flask - 범위 기반 샤딩 적용)
```python
import sqlite3

def get_db(user_id):
    if user_id <= 1000:
        return sqlite3.connect("shard1.db")
    else:
        return sqlite3.connect("shard2.db")

def save_user(user_id, name):
    db = get_db(user_id)
    cursor = db.cursor()
    cursor.execute("INSERT INTO users (id, name) VALUES (?, ?)", (user_id, name))
    db.commit()
    db.close()
```

---

## 4. 데이터베이스 샤딩 사용 시 고려할 점
- **샤드 간 조인(Join) 불가능**: 여러 샤드에 걸쳐 있는 데이터의 조인이 어려움
- **샤딩 키(Sharding Key) 선정 중요**: 균형 잡힌 샤드 분배를 위해 해시 기반 또는 적절한 범위 기준 설정 필요
- **샤드 추가 시 마이그레이션 문제**: 샤드를 추가할 경우 기존 데이터를 재분배해야 하는 어려움 존재
- **트랜잭션 관리 어려움**: 샤드 간 일관성을 유지하기 위해 분산 트랜잭션이 필요할 수 있음

---

## 5. 면접 질문 예시 및 답변

### 1️⃣ 데이터베이스 샤딩이란 무엇이며, 왜 필요한가?
데이터베이스 샤딩은 데이터를 여러 개의 작은 데이터베이스(샤드)로 나누어 저장하는 기술이다. 대량의 데이터를 효율적으로 처리하고, 데이터베이스의 확장성을 높이는 데 필요하다.

### 2️⃣ 범위 기반 샤딩과 해시 기반 샤딩의 차이는?
- **범위 기반 샤딩**: 특정 범위의 데이터를 하나의 샤드에 저장. 데이터의 분포가 불균형할 수 있음.
- **해시 기반 샤딩**: 해시 함수를 사용하여 샤드를 결정. 데이터가 균등하게 분배되지만, 샤드를 추가할 경우 기존 데이터의 재배치가 필요할 수 있음.

### 3️⃣ 샤딩을 적용할 때 샤딩 키를 어떻게 선택해야 하는가?
샤딩 키는 데이터가 고르게 분포되도록 선택해야 한다. 특정 값(예: 날짜) 기반 샤딩은 특정 샤드에 부하가 집중될 수 있으므로 해시 기반 샤딩이 더 나은 선택일 수 있다.

### 4️⃣ 샤딩 환경에서 트랜잭션을 어떻게 관리할 수 있는가?
- 샤드 내에서 트랜잭션을 유지하는 것이 가장 간단한 방법.
- 분산 트랜잭션(Distributed Transactions) 또는 2PC(Two-Phase Commit)를 사용할 수도 있지만, 성능 오버헤드가 있을 수 있음.

### 5️⃣ 샤딩을 적용한 시스템에서 장애가 발생하면 어떻게 복구할 수 있는가?
- 개별 샤드에 대한 백업 및 복구 전략이 필요함.
- 샤드 간 데이터 복제를 활용하여 장애 시 다른 샤드로 트래픽을 리디렉션할 수 있음.

### 6️⃣ 샤딩과 레플리케이션(Replication)의 차이점은?
- **샤딩**: 데이터를 수평으로 분할하여 여러 데이터베이스에 저장하는 방식.
- **레플리케이션**: 동일한 데이터를 여러 개의 서버에 복제하여 가용성과 읽기 성능을 향상시키는 방식.

### 7️⃣ 샤딩을 적용했을 때 발생할 수 있는 문제점과 해결 방법은?
- **데이터 불균형** → 샤딩 키를 최적화하여 균등한 데이터 분배 필요.
- **샤드 간 조인 불가능** → 애플리케이션 단에서 조인 로직을 처리하거나 NoSQL을 고려.
- **샤드 추가 시 데이터 이동 문제** → 가상 샤딩(Virtual Sharding) 기법을 활용하여 데이터 마이그레이션 최소화.

---