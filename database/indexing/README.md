# 인덱싱(Indexing)

## 1. 인덱싱이란?
인덱싱(Indexing)은 **데이터베이스에서 검색 성능을 향상시키기 위해 사용되는 기법**이다. 대량의 데이터가 저장된 테이블에서 원하는 데이터를 빠르게 찾기 위해 인덱스를 생성하며, 인덱스는 특정 열(Column)에 대한 정렬된 데이터 구조를 유지한다.

### 🔹 인덱싱의 주요 특징
- **검색 속도 향상**: 테이블 전체를 조회하는 `Full Table Scan`을 줄이고, 검색 성능을 개선
- **데이터 정렬 유지**: 인덱스를 기반으로 데이터를 정렬하여 빠른 접근 가능
- **쓰기 성능 저하 가능**: 인덱스가 많아질수록 `INSERT`, `UPDATE`, `DELETE` 작업이 느려질 수 있음
- **디스크 공간 사용 증가**: 인덱스를 저장하기 위한 추가적인 공간 필요

---

## 2. 인덱스의 종류
| 인덱스 유형 | 설명 |
|-------------|------|
| **Primary Index (기본 키 인덱스)** | 기본 키(Primary Key)가 자동으로 생성하는 인덱스 |
| **Unique Index (고유 인덱스)** | 중복되지 않는 값만 저장할 수 있는 인덱스 |
| **Clustered Index (클러스터형 인덱스)** | 데이터 자체가 인덱스 구조로 저장되는 방식 |
| **Non-clustered Index (비클러스터형 인덱스)** | 인덱스와 데이터가 별도로 저장됨, 일반적인 인덱스 |
| **Full-text Index (전문 검색 인덱스)** | 텍스트 검색 최적화용 인덱스 |
| **Composite Index (복합 인덱스)** | 여러 개의 열(Column)을 결합한 인덱스 |

---

## 3. 인덱스의 동작 방식
### 🔹 B-Tree 인덱스
- 대부분의 관계형 데이터베이스에서 사용하는 인덱스 구조
- 균형 트리(Balanced Tree) 구조로, 검색, 삽입, 삭제가 O(log N) 복잡도를 가짐
- **사용 예시**: MySQL, PostgreSQL, SQL Server 등

### 🔹 Hash 인덱스
- 해시 함수를 사용하여 데이터의 위치를 찾음
- 특정 값에 대한 빠른 검색 가능하지만, 범위 검색이 어려움
- **사용 예시**: NoSQL 데이터베이스, 메모리 기반 인덱싱

---

## 4. 코드 예제
### 🔹 SQL에서 인덱스 생성 및 조회
##### Java (JDBC - MySQL 인덱스 조회)
```java
import java.sql.*;

public class IndexExample {
    public static void main(String[] args) throws Exception {
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password");
        Statement stmt = conn.createStatement();
        stmt.execute("CREATE INDEX idx_name ON users(name)");
        ResultSet rs = stmt.executeQuery("SHOW INDEX FROM users");
        while (rs.next()) {
            System.out.println("Index: " + rs.getString("Key_name"));
        }
        rs.close();
        stmt.close();
        conn.close();
    }
}
```

##### JavaScript (MySQL - 인덱스 생성 및 조회)
```javascript
const mysql = require('mysql');
const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'mydb'
});
connection.connect();
connection.query('CREATE INDEX idx_name ON users(name)');
connection.query('SHOW INDEX FROM users', (error, results) => {
    if (error) throw error;
    console.log(results);
});
connection.end();
```

##### Python (SQLite - 인덱스 생성 및 조회)
```python
import sqlite3
conn = sqlite3.connect("mydb.db")
cursor = conn.cursor()
cursor.execute("CREATE INDEX idx_name ON users(name)")
cursor.execute("PRAGMA index_list('users')")
print(cursor.fetchall())
conn.close()
```

---

## 5. 인덱스를 사용할 때 고려할 점
- **읽기 성능 향상**: `SELECT` 속도가 빨라짐
- **쓰기 성능 저하 가능성**: `INSERT`, `UPDATE`, `DELETE` 성능이 느려질 수 있음
- **적절한 컬럼 선택 필요**: 자주 조회하는 열에 인덱스를 생성해야 함
- **인덱스 오버헤드 발생 가능**: 너무 많은 인덱스는 오히려 성능 저하를 유발할 수 있음

---

## 6. 면접 질문 예시
1. 인덱스란 무엇이며, 어떤 역할을 하는가?
2. 클러스터형 인덱스와 비클러스터형 인덱스의 차이점은?
3. 인덱스가 많은 경우 성능 저하가 발생할 수 있는 이유는?
4. B-Tree 인덱스와 Hash 인덱스의 차이점은?
5. 인덱스를 최적화하는 방법은 무엇인가?

---
