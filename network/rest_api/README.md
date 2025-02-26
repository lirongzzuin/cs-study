# REST API

## 1. REST API란?
REST(Representational State Transfer) API는 **웹에서 클라이언트와 서버 간의 데이터를 주고받기 위한 아키텍처 스타일**이다. HTTP 프로토콜을 기반으로 동작하며, 리소스를 자원(Resource)으로 정의하고, HTTP 메서드를 활용하여 CRUD(Create, Read, Update, Delete) 작업을 수행한다.

### 🔹 REST의 특징
- **클라이언트-서버 구조**: 클라이언트와 서버가 독립적으로 동작
- **무상태(Stateless)**: 요청 간에 클라이언트 상태를 저장하지 않음
- **캐시(Cacheable)**: 응답을 캐싱하여 성능 최적화 가능
- **계층화(Layered System)**: 여러 계층으로 시스템 구성 가능
- **일관된 인터페이스(Uniform Interface)**: 표준화된 방식으로 자원에 접근

---

## 2. HTTP 메서드와 REST API 매핑
| HTTP 메서드 | 동작 | 설명 |
|------------|------|------|
| `GET` | 조회(Read) | 특정 리소스 조회 |
| `POST` | 생성(Create) | 새로운 리소스 생성 |
| `PUT` | 수정(Update) | 기존 리소스 전체 업데이트 |
| `PATCH` | 부분 수정 | 리소스의 일부 업데이트 |
| `DELETE` | 삭제(Delete) | 특정 리소스 삭제 |

---

## 3. REST API의 엔드포인트 설계 예시
### 🔹 사용자 관리 API 예시
| 기능 | 엔드포인트 | HTTP 메서드 |
|------|------------|-------------|
| 사용자 목록 조회 | `/users` | `GET` |
| 사용자 상세 조회 | `/users/{id}` | `GET` |
| 사용자 생성 | `/users` | `POST` |
| 사용자 정보 수정 | `/users/{id}` | `PUT` |
| 사용자 부분 수정 | `/users/{id}` | `PATCH` |
| 사용자 삭제 | `/users/{id}` | `DELETE` |

---

## 4. 코드 예제
### 🔹 REST API 요청 예제
##### Java (Spring Boot - REST 컨트롤러)
```java
import org.springframework.web.bind.annotation.*;
import java.util.*;

@RestController
@RequestMapping("/users")
public class UserController {
    private Map<Integer, String> users = new HashMap<>();
    
    @GetMapping
    public Map<Integer, String> getUsers() {
        return users;
    }
    
    @PostMapping
    public String addUser(@RequestParam String name) {
        int id = users.size() + 1;
        users.put(id, name);
        return "User added: " + name;
    }
}
```

##### JavaScript (Fetch API)
```javascript
fetch('https://api.example.com/users', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'John Doe' })
})
.then(response => response.json())
.then(data => console.log(data));
```

##### Python (Flask - REST API 서버)
```python
from flask import Flask, request, jsonify

app = Flask(__name__)
users = {}

@app.route('/users', methods=['GET'])
def get_users():
    return jsonify(users)

@app.route('/users', methods=['POST'])
def add_user():
    user_id = len(users) + 1
    name = request.json.get('name')
    users[user_id] = name
    return jsonify({"message": "User added", "user": name})

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 5. REST API 설계 원칙
- **리소스 중심의 URL**: 동사 대신 명사 사용 (`/getUsers ❌` → `/users ✅`)
- **일관된 상태 코드 반환**
  - `200 OK`: 요청 성공
  - `201 Created`: 리소스 생성됨
  - `400 Bad Request`: 잘못된 요청
  - `404 Not Found`: 리소스 없음
  - `500 Internal Server Error`: 서버 오류
- **HATEOAS 적용 가능**: API 응답에 관련 리소스 링크 포함 가능

---

## 6. REST API와 RESTful의 차이
- **REST API**는 REST 원칙을 따르는 API를 의미
- **RESTful API**는 REST의 원칙을 철저하게 준수하여 설계된 API
- 모든 REST API가 RESTful한 것은 아님 (예: URL에 동사가 포함되거나 상태 유지하는 API)

---

## 7. REST API의 한계 및 고려사항
- **과도한 요청 수 증가**: 클라이언트가 여러 요청을 보내야 할 수도 있음 → GraphQL 활용 고려
- **보안 문제**: 인증 및 권한 관리 필요 → JWT, OAuth2 적용
- **버전 관리 필요**: `/v1/users`와 같은 방식으로 API 버전 관리 적용

---

## 8. REST API와 관련된 면접 질문 예시
1. RESTful API란 무엇인가?
2. REST API와 SOAP의 차이점은?
3. REST API에서 PUT과 PATCH의 차이점은?
4. RESTful한 API를 설계할 때 고려해야 할 사항은?
5. REST API의 인증 방식에는 어떤 것이 있는가?

---
