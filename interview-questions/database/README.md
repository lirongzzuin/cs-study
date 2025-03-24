# 데이터베이스 면접 질문 정리 (Database Interview Questions)

## 1. 데이터베이스 개요
데이터베이스(Database)는 **데이터를 구조적으로 저장하고, 효율적으로 조회·추가·수정·삭제할 수 있도록 지원하는 시스템**이다. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)로 나뉘며, 각각의 특성과 장단점이 있다.

### 🔹 데이터베이스의 주요 기능
- **데이터 저장 및 관리**
- **동시성 제어 및 트랜잭션 처리**
- **데이터 무결성과 보안 보장**
- **효율적인 쿼리(Query) 지원**

---

## 2. 데이터베이스 면접 질문 및 답변

### 1️⃣ RDBMS와 NoSQL의 차이점은?
| 항목 | RDBMS | NoSQL |
|------|-------|--------|
| 데이터 모델 | 테이블 기반 (정형 데이터) | 문서, 키-값, 그래프 등 유연한 모델 |
| 스키마 | 고정 스키마 | 동적 스키마 |
| 확장성 | 수직 확장 | 수평 확장 |
| 사용 사례 | 금융, ERP, 전자상거래 | 빅데이터, 실시간 서비스, IoT

### 2️⃣ 정규화(Normalization)란?
- **중복을 최소화하고 데이터 무결성을 보장하기 위한 과정**
- 여러 단계(1NF, 2NF, 3NF 등)를 거치며 테이블을 분해함

### 3️⃣ 트랜잭션(Transaction)이란?
- 하나의 논리적 작업 단위로, **모두 성공하거나 모두 실패해야 함**
- **ACID 원칙** 적용:
  - Atomicity(원자성), Consistency(일관성), Isolation(고립성), Durability(지속성)

### 4️⃣ 인덱스(Index)의 역할은?
- **쿼리 성능 향상을 위한 자료구조로, 특정 컬럼의 값을 빠르게 찾기 위해 사용**
- 검색 속도는 빨라지지만 **쓰기 성능은 낮아지고 저장 공간이 추가로 필요**함

### 5️⃣ 조인(Join)의 종류와 차이점은?
| 조인 종류 | 설명 |
|-----------|------|
| **INNER JOIN** | 양쪽 테이블에 모두 존재하는 레코드만 반환 |
| **LEFT JOIN** | 왼쪽 테이블의 모든 레코드 + 오른쪽 일치 레코드 |
| **RIGHT JOIN** | 오른쪽 테이블의 모든 레코드 + 왼쪽 일치 레코드 |
| **FULL OUTER JOIN** | 양쪽 모든 레코드 포함, 일치하지 않으면 NULL 반환 |

### 6️⃣ View(뷰)란?
- **하나 이상의 테이블을 조합한 가상의 테이블**
- 실제 데이터는 저장되지 않고 쿼리 결과를 보여줌
- 복잡한 쿼리를 단순하게 재사용 가능

### 7️⃣ 트랜잭션 격리 수준(Isolation Level)과 발생 가능한 문제는?
| 격리 수준 | 설명 | 발생 가능한 문제 |
|-----------|------|------------------|
| READ UNCOMMITTED | 커밋되지 않은 데이터 읽기 허용 | Dirty Read |
| READ COMMITTED | 커밋된 데이터만 읽기 허용 | Non-Repeatable Read |
| REPEATABLE READ | 트랜잭션 내 동일한 쿼리 결과 보장 | Phantom Read |
| SERIALIZABLE | 완전한 직렬 실행 보장 | 성능 저하 가능 |

---

## 3. 코드 예제
### 🔹 SQL 트랜잭션 예제 (INSERT + ROLLBACK)
##### Java (JDBC 트랜잭션 처리)
```java
Connection conn = DriverManager.getConnection(DB_URL, USER, PASS);
try {
    conn.setAutoCommit(false);
    Statement stmt = conn.createStatement();
    stmt.executeUpdate("INSERT INTO users (name) VALUES ('Alice')");
    conn.rollback(); // 롤백으로 인해 저장되지 않음
} catch (SQLException e) {
    conn.rollback();
} finally {
    conn.close();
}
```

##### JavaScript (Node.js - MySQL 트랜잭션 처리)
```javascript
const mysql = require('mysql2/promise');
const conn = await mysql.createConnection(config);
try {
    await conn.beginTransaction();
    await conn.query("INSERT INTO users (name) VALUES ('Alice')");
    await conn.rollback();
} catch (err) {
    await conn.rollback();
}
```

##### Python (SQLite 트랜잭션 처리)
```python
import sqlite3
conn = sqlite3.connect('mydb.db')
cursor = conn.cursor()
try:
    cursor.execute("BEGIN TRANSACTION")
    cursor.execute("INSERT INTO users (name) VALUES ('Alice')")
    conn.rollback()
finally:
    conn.close()
```

---

## 4. 데이터베이스 사용 시 고려할 점
- **정규화와 성능 간의 균형**: 데이터 무결성과 성능을 동시에 고려해야 함
- **인덱스는 필요한 곳에만 생성**: 과도한 인덱스는 성능 저하 유발
- **트랜잭션 처리 철저**: 예외 발생 시 롤백 고려
- **조인 및 서브쿼리 최적화**: 복잡한 쿼리는 실행 계획(Explain Plan) 분석
- **보안 고려**: 권한 관리, SQL Injection 방지

---

## 5. 결론
데이터베이스는 백엔드 시스템의 핵심 요소 중 하나로, 면접에서는 **트랜잭션, 인덱스, 정규화, 조인, 트랜잭션 격리 수준** 등 핵심 개념을 얼마나 명확하게 이해하고, 이를 실무에 어떻게 적용할 수 있는지를 중점적으로 평가한다. 단순한 용어 암기보다는 **쿼리 작성 경험, 성능 최적화 경험, 트러블슈팅 사례 중심의 정리**가 필요하다.

---
