# 트랜잭션(Transaction)

## 1. 트랜잭션이란?
트랜잭션(Transaction)은 **데이터베이스에서 하나의 논리적 작업 단위를 구성하는 연산 집합**이다. 여러 개의 SQL 작업이 하나의 트랜잭션으로 묶여 실행되며, **일부 작업만 실행되는 것을 방지하고, 전체 작업이 성공하거나 실패하도록 보장**한다.

### 🔹 트랜잭션의 주요 특징 (ACID 원칙)
| 원칙 | 설명 |
|------|------|
| **Atomicity (원자성)** | 모든 연산이 완전히 수행되거나 전혀 수행되지 않아야 함 |
| **Consistency (일관성)** | 트랜잭션이 실행되기 전과 후의 데이터 일관성이 유지되어야 함 |
| **Isolation (고립성)** | 동시에 여러 트랜잭션이 실행되더라도 서로 영향을 미치지 않아야 함 |
| **Durability (지속성)** | 트랜잭션이 성공적으로 완료되면 그 결과가 영구적으로 저장되어야 함 |

---

## 2. 트랜잭션 명령어
| 명령어 | 설명 |
|--------|------|
| `BEGIN TRANSACTION` | 트랜잭션 시작 |
| `COMMIT` | 트랜잭션 정상 종료 및 변경 사항 저장 |
| `ROLLBACK` | 트랜잭션 오류 발생 시 변경 사항 취소 |
| `SAVEPOINT` | 특정 시점에서 되돌릴 수 있도록 저장 |

---

## 3. 트랜잭션 코드 예제
### 🔹 SQL에서 트랜잭션 사용
##### Java (JDBC - 트랜잭션 적용)
```java
import java.sql.*;

public class TransactionExample {
    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password")) {
            conn.setAutoCommit(false);
            try (Statement stmt = conn.createStatement()) {
                stmt.executeUpdate("INSERT INTO accounts (id, balance) VALUES (1, 1000)");
                stmt.executeUpdate("UPDATE accounts SET balance = balance - 500 WHERE id = 1");
                conn.commit();
                System.out.println("트랜잭션 완료");
            } catch (SQLException e) {
                conn.rollback();
                System.out.println("롤백 수행");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

##### JavaScript (MySQL - 트랜잭션 적용)
```javascript
const mysql = require('mysql2/promise');
(async () => {
    const conn = await mysql.createConnection({host: 'localhost', user: 'root', database: 'mydb'});
    try {
        await conn.beginTransaction();
        await conn.query("INSERT INTO accounts (id, balance) VALUES (1, 1000)");
        await conn.query("UPDATE accounts SET balance = balance - 500 WHERE id = 1");
        await conn.commit();
        console.log("트랜잭션 완료");
    } catch (err) {
        await conn.rollback();
        console.log("롤백 수행");
    } finally {
        await conn.end();
    }
})();
```

##### Python (SQLite - 트랜잭션 적용)
```python
import sqlite3
conn = sqlite3.connect("mydb.db")
cursor = conn.cursor()
try:
    cursor.execute("BEGIN TRANSACTION")
    cursor.execute("INSERT INTO accounts (id, balance) VALUES (1, 1000)")
    cursor.execute("UPDATE accounts SET balance = balance - 500 WHERE id = 1")
    conn.commit()
    print("트랜잭션 완료")
except Exception as e:
    conn.rollback()
    print("롤백 수행")
finally:
    conn.close()
```

---

## 4. 트랜잭션 격리 수준
트랜잭션이 동시에 실행될 때 **격리 수준(Isolation Level)** 에 따라 데이터 일관성을 보장할 수 있다.

| 격리 수준 | 설명 | 발생할 수 있는 문제 |
|----------|------|----------------|
| **READ UNCOMMITTED** | 다른 트랜잭션이 커밋하지 않은 데이터도 읽을 수 있음 | Dirty Read |
| **READ COMMITTED** | 커밋된 데이터만 읽을 수 있음 | Non-Repeatable Read |
| **REPEATABLE READ** | 한 트랜잭션 내에서 동일한 데이터를 여러 번 조회하면 항상 같은 결과 반환 | Phantom Read |
| **SERIALIZABLE** | 가장 엄격한 격리 수준, 모든 트랜잭션이 순차적으로 실행됨 | 성능 저하 |

---

## 5. 트랜잭션 사용 시 고려할 점
- **트랜잭션 크기 최소화**: 트랜잭션이 오래 지속되면 데이터베이스 성능 저하 가능
- **적절한 격리 수준 선택**: 애플리케이션 특성에 맞게 적절한 격리 수준 설정
- **예외 처리 필수**: 오류 발생 시 `ROLLBACK`을 수행하도록 예외 처리 필요
- **트랜잭션 로그 관리**: 장애 발생 시 데이터 복구를 위한 로그 유지 필요

---

## 6. 면접 질문 예시
1. 트랜잭션이란 무엇이며, 왜 중요한가?
2. ACID 원칙에서 가장 중요한 요소는 무엇인가?
3. 트랜잭션 격리 수준별 차이점과 발생할 수 있는 문제는?
4. 트랜잭션이 너무 길어질 경우 어떤 문제가 발생할 수 있는가?
5. NoSQL 데이터베이스에서 트랜잭션을 어떻게 처리하는가?

---