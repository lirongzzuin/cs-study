# SQL vs NoSQL

## 1. SQL과 NoSQL 개요
SQL(Structured Query Language)과 NoSQL(Not Only SQL)은 **데이터를 저장하고 관리하는 데이터베이스 유형**이다. 각각의 특징과 사용 사례를 이해하면, 프로젝트에 적합한 데이터베이스를 선택할 수 있다.

### 🔹 SQL (관계형 데이터베이스, RDBMS)
- **구조화된 데이터 저장** (테이블, 행, 열)
- **스키마 기반** (명확한 데이터 모델 필요)
- **ACID(원자성, 일관성, 고립성, 지속성) 보장**
- **사용 사례**: 금융 시스템, ERP, CRM, 전자상거래

### 🔹 NoSQL (비관계형 데이터베이스)
- **유연한 데이터 모델** (키-값, 문서, 컬럼, 그래프 등)
- **스키마가 없거나 동적** (JSON, BSON 등 사용)
- **수평 확장 용이** (분산 시스템 기반)
- **사용 사례**: 소셜 미디어, 빅데이터, 실시간 애플리케이션

---

## 2. SQL vs NoSQL 비교
| 특징 | SQL (RDBMS) | NoSQL |
|------|------------|-------|
| 데이터 모델 | 테이블 기반 (정형 데이터) | 다양한 모델 (문서, 키-값, 그래프 등) |
| 스키마 | 고정 스키마 | 동적 스키마 |
| 확장성 | 수직 확장 (Scale-Up) | 수평 확장 (Scale-Out) |
| 트랜잭션 | ACID 보장 | BASE (Eventually Consistent) 모델 적용 |
| 사용 사례 | 금융, ERP, 전자상거래 | 실시간 데이터, 소셜 네트워크, IoT |

---

## 3. SQL과 NoSQL의 활용 사례
### 🔹 SQL 데이터베이스 활용 사례
- **은행 시스템**: 일관성이 중요한 금융 거래 관리
- **전자상거래**: 주문 처리 및 관계형 데이터 유지
- **기업 애플리케이션**: ERP, CRM 시스템

### 🔹 NoSQL 데이터베이스 활용 사례
- **소셜 미디어**: 빠른 읽기/쓰기 처리 (예: Facebook, Twitter)
- **빅데이터 분석**: 분산 저장 구조를 활용한 데이터 처리
- **IoT 시스템**: 다양한 센서 데이터 처리

---

## 4. 코드 예제
### 🔹 SQL 예제 (MySQL)
##### Java (JDBC - SQL 데이터 조회)
```java
import java.sql.*;

public class SQLExample {
    public static void main(String[] args) throws Exception {
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password");
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        while (rs.next()) {
            System.out.println("User: " + rs.getString("name"));
        }
        rs.close();
        stmt.close();
        conn.close();
    }
}
```

##### JavaScript (MySQL 연결 - Node.js)
```javascript
const mysql = require('mysql');
const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'mydb'
});
connection.connect();
connection.query('SELECT * FROM users', (error, results) => {
    if (error) throw error;
    console.log(results);
});
connection.end();
```

##### Python (SQLite - SQL 데이터 조회)
```python
import sqlite3
conn = sqlite3.connect("mydb.db")
cursor = conn.cursor()
cursor.execute("SELECT * FROM users")
for row in cursor.fetchall():
    print("User:", row[0])
conn.close()
```

### 🔹 NoSQL 예제 (MongoDB)
##### Java (MongoDB 연결)
```java
import com.mongodb.client.*;
import org.bson.Document;

public class NoSQLExample {
    public static void main(String[] args) {
        MongoClient mongoClient = MongoClients.create("mongodb://localhost:27017");
        MongoDatabase database = mongoClient.getDatabase("mydb");
        MongoCollection<Document> collection = database.getCollection("users");
        for (Document doc : collection.find()) {
            System.out.println(doc.toJson());
        }
        mongoClient.close();
    }
}
```

##### JavaScript (MongoDB 연결 - Node.js)
```javascript
const { MongoClient } = require('mongodb');
const client = new MongoClient("mongodb://localhost:27017");
async function run() {
    await client.connect();
    const db = client.db("mydb");
    const users = await db.collection("users").find().toArray();
    console.log(users);
    await client.close();
}
run();
```

##### Python (MongoDB - 데이터 조회)
```python
from pymongo import MongoClient
client = MongoClient("mongodb://localhost:27017")
db = client["mydb"]
users = db["users"].find()
for user in users:
    print(user)
```

---

## 5. SQL vs NoSQL 선택 기준
- **데이터 정합성이 중요하다** → SQL
- **대량의 데이터를 빠르게 처리해야 한다** → NoSQL
- **트랜잭션이 필수적이다** → SQL
- **수평 확장이 필요하다** → NoSQL
- **데이터 구조가 자주 변경된다** → NoSQL

---

## 6. 면접 질문 예시
1. SQL과 NoSQL의 차이점은?
2. SQL에서 JOIN 연산이 중요한 이유는?
3. NoSQL은 어떤 상황에서 사용하는 것이 적절한가?
4. SQL과 NoSQL 중 어떤 것이 성능적으로 더 유리한가?
5. CAP 이론과 NoSQL의 관계는?

---
