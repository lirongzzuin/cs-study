# 로드 밸런싱 (Load Balancing)

## 1. 로드 밸런싱이란?
로드 밸런싱(Load Balancing)은 **여러 서버에 트래픽을 분산하여 성능을 최적화하고 가용성을 높이는 기술**이다. 서버 부하를 균등하게 배분하여 응답 시간을 줄이고 시스템의 장애를 방지하는 역할을 한다.

### 🔹 로드 밸런싱의 주요 목표
- **트래픽 분산**: 서버 간 부하를 균등하게 배분
- **성능 최적화**: 응답 시간 감소 및 처리량(Throughput) 증가
- **고가용성(High Availability)**: 일부 서버 장애 발생 시 서비스 지속 가능
- **확장성(Scalability)**: 트래픽 증가 시 서버 확장이 용이

---

## 2. 로드 밸런싱의 유형
### 🔹 L4 로드 밸런싱 (네트워크 계층, Layer 4)
- **TCP/UDP 프로토콜 기반**으로 요청을 분산
- 패킷을 기반으로 목적지 서버를 결정
- **예제**: AWS ELB(Network Load Balancer), Nginx Stream Module

### 🔹 L7 로드 밸런싱 (애플리케이션 계층, Layer 7)
- **HTTP/HTTPS 기반**으로 요청을 분석하여 특정 서버로 라우팅
- 쿠키, 헤더, URL 패턴 등을 활용한 라우팅 가능
- **예제**: AWS ELB(Application Load Balancer), Nginx Reverse Proxy

---

## 3. 로드 밸런싱 알고리즘
| 알고리즘 | 설명 |
|-----------|------|
| **라운드 로빈(Round Robin)** | 순차적으로 각 서버에 요청을 배분 |
| **가중치 라운드 로빈(Weighted Round Robin)** | 각 서버에 가중치를 부여하여 요청을 배분 |
| **최소 연결(Least Connections)** | 현재 연결된 세션 수가 가장 적은 서버로 분배 |
| **IP 해시(IP Hashing)** | 클라이언트 IP를 해싱하여 특정 서버로 고정 라우팅 |
| **랜덤(Random)** | 무작위로 서버를 선택하여 요청을 배분 |

---

## 4. 코드 예제
### 🔹 Nginx를 이용한 로드 밸런싱 설정
##### Java (Spring Boot 애플리케이션)
```java
@RestController
public class LoadBalanceController {
    @GetMapping("/")
    public String home() {
        return "서버 응답: " + UUID.randomUUID();
    }
}
```

##### Nginx (Reverse Proxy - Round Robin 방식)
```nginx
http {
    upstream backend_servers {
        server server1.example.com;
        server server2.example.com;
    }

    server {
        listen 80;
        location / {
            proxy_pass http://backend_servers;
        }
    }
}
```

##### JavaScript (Node.js - 클라이언트 요청 분산)
```javascript
const http = require('http');
const servers = ['http://server1.example.com', 'http://server2.example.com'];
let current = 0;

const server = http.createServer((req, res) => {
    const target = servers[current];
    current = (current + 1) % servers.length;
    http.get(target, (proxyRes) => {
        proxyRes.pipe(res);
    });
});

server.listen(8080);
```

##### Python (Flask - 로드 밸런서 구현)
```python
from flask import Flask
import random

app = Flask(__name__)
servers = ["http://server1.example.com", "http://server2.example.com"]

@app.route('/')
def load_balance():
    return f"Redirecting to: {random.choice(servers)}"

if __name__ == '__main__':
    app.run(port=8080)
```

---

## 5. 로드 밸런싱 사용 시 고려 사항
- **세션 유지(Session Persistence)**: 특정 사용자의 요청이 항상 같은 서버로 전달될 필요가 있는 경우 쿠키 기반 세션 유지 적용
- **Failover 설정**: 서버 장애 시 자동으로 다른 서버로 요청을 전달하도록 설정 필요
- **SSL 종료(SSL Termination)**: 로드 밸런서에서 SSL을 해제하여 백엔드 서버의 부하를 줄일 수 있음
- **Health Check**: 주기적으로 백엔드 서버의 상태를 확인하여 정상적인 서버로만 요청을 전달

---

## 6. 면접 질문 예시 및 답변
### 1️⃣ 로드 밸런싱이란 무엇이며, 왜 필요한가?
로드 밸런싱은 여러 서버에 트래픽을 분산하여 부하를 조절하고, 성능을 최적화하는 기술이다. 이를 통해 서비스 가용성을 높이고 장애를 방지할 수 있다.

### 2️⃣ L4와 L7 로드 밸런싱의 차이점은?
- **L4 로드 밸런싱**: 네트워크 계층(TCP/UDP)에서 패킷을 기반으로 트래픽을 분산.
- **L7 로드 밸런싱**: 애플리케이션 계층(HTTP/HTTPS)에서 요청의 내용을 분석하여 트래픽을 분산.

### 3️⃣ 로드 밸런싱 알고리즘 중 라운드 로빈과 최소 연결 방식의 차이점은?
- **라운드 로빈**: 순차적으로 각 서버에 요청을 배분.
- **최소 연결**: 현재 연결된 세션 수가 가장 적은 서버로 요청을 배분하여 부하를 최소화.

### 4️⃣ 로드 밸런싱 설정 시 세션 관리는 어떻게 해결할 수 있는가?
- **세션 스티키니스(Sticky Session)**: 특정 사용자의 요청을 동일한 서버로 전달.
- **세션을 중앙 저장소에 저장**: Redis 또는 데이터베이스를 활용하여 세션을 공유.

### 5️⃣ 클라우드 환경에서 로드 밸런서를 구성할 때 고려해야 할 점은?
- **Auto Scaling과 연계 가능성**
- **Failover 및 Health Check 설정**
- **SSL/TLS 오프로드 지원 여부**
- **CDN과의 연계 가능성**

### 6️⃣ 로드 밸런서를 활용한 장애 복구(Failover) 방식은?
- 주기적으로 백엔드 서버의 상태를 확인하여 비정상 서버를 제외하고 요청을 전달하는 **Health Check** 기법을 적용.
- DNS 기반 로드 밸런싱을 활용하여 장애 발생 시 다른 데이터센터로 트래픽을 분산.

### 7️⃣ 로드 밸런싱이 적용된 시스템에서 발생할 수 있는 문제점과 해결 방법은?
- **지나치게 많은 서버 추가로 인해 비용 증가** → 적절한 Auto Scaling 정책 적용.
- **잘못된 알고리즘 선택으로 인해 특정 서버에 부하 집중** → 부하 테스트를 통해 적절한 알고리즘 선택.
- **네트워크 병목 현상 발생** → CDN과 결합하여 트래픽을 최적화.

---