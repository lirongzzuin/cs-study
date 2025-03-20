# 네트워크 면접 질문 정리 (Network Interview Questions)

## 1. 네트워크 개요
네트워크(Network)는 **두 개 이상의 컴퓨터 또는 장치가 서로 연결되어 데이터를 주고받는 시스템**이다. 네트워크는 LAN(Local Area Network), WAN(Wide Area Network) 등으로 분류되며, 다양한 프로토콜과 기술을 기반으로 통신이 이루어진다.

### 🔹 네트워크의 주요 역할
- **데이터 전송**: 패킷을 이용한 정보 교환
- **자원 공유**: 파일, 프린터, 인터넷 등의 자원 공유
- **보안 및 접근 제어**: 방화벽, 암호화, 인증 기술 활용
- **인터넷 서비스 제공**: 웹, 이메일, 클라우드 등의 서비스 지원

---

## 2. 네트워크 면접 질문 및 답변

### 1️⃣ OSI 7 계층이란?
OSI 7 계층(Open Systems Interconnection Model)은 네트워크 통신을 7개의 계층으로 나누어 설명하는 모델이다.

| 계층 | 역할 |
|------|------|
| **7. 응용 계층(Application Layer)** | 사용자와 네트워크 간 인터페이스 제공 (HTTP, FTP) |
| **6. 표현 계층(Presentation Layer)** | 데이터 형식 변환 및 암호화 (JPEG, SSL/TLS) |
| **5. 세션 계층(Session Layer)** | 세션 연결 및 관리 (RPC, NetBIOS) |
| **4. 전송 계층(Transport Layer)** | 신뢰성 있는 데이터 전송 (TCP, UDP) |
| **3. 네트워크 계층(Network Layer)** | IP 주소를 통한 경로 설정 (IP, ICMP) |
| **2. 데이터 링크 계층(Data Link Layer)** | MAC 주소 기반 데이터 전송 (Ethernet, Switch) |
| **1. 물리 계층(Physical Layer)** | 물리적 신호 전송 (케이블, Wi-Fi) |

### 2️⃣ TCP와 UDP의 차이점은?
| 특징 | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|------|---------------------------------|---------------------------------|
| 연결 방식 | 연결 지향 (Connection-oriented) | 비연결형 (Connectionless) |
| 신뢰성 | 높음 (패킷 손실 시 재전송) | 낮음 (패킷 손실 시 재전송 없음) |
| 속도 | 상대적으로 느림 | 빠름 |
| 사용 사례 | HTTP, FTP, 이메일 | VoIP, 스트리밍, 온라인 게임 |

### 3️⃣ HTTP와 HTTPS의 차이점은?
- **HTTP(HyperText Transfer Protocol)**: 데이터를 암호화하지 않고 전송
- **HTTPS(HyperText Transfer Protocol Secure)**: SSL/TLS 암호화를 적용하여 보안 강화

### 4️⃣ 3-Way Handshake 과정은?
TCP 연결을 설정하는 과정으로, 다음 3단계를 거친다:
1. **SYN(Synchronize)**: 클라이언트가 서버에 연결 요청
2. **SYN-ACK(Synchronize-Acknowledge)**: 서버가 요청을 승인하고 응답
3. **ACK(Acknowledge)**: 클라이언트가 확인 응답 후 연결 확립

### 5️⃣ NAT(Network Address Translation)란?
- 사설 IP 주소를 공인 IP 주소로 변환하는 기술
- IPv4 주소 부족 문제를 해결하기 위해 사용됨
- **종류**: 정적 NAT, 동적 NAT, 포트 주소 변환(PAT)

### 6️⃣ VPN(Virtual Private Network)이란?
- 공용 네트워크를 이용하여 **보안성이 높은 사설 네트워크를 구축**하는 기술
- 원격 접속 및 데이터 보호에 사용됨
- **터널링 프로토콜**: PPTP, L2TP, OpenVPN, WireGuard

### 7️⃣ DNS(Domain Name System)의 역할은?
- **도메인 이름을 IP 주소로 변환하는 서비스**
- DNS 서버가 계층적으로 동작 (Root → TLD → Authoritative DNS)
- **예제**: `www.google.com` → `142.250.74.68`

---

## 3. 코드 예제
### 🔹 TCP와 UDP 소켓 통신 예제
##### Java (TCP 서버 & 클라이언트)
```java
// TCP 서버
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(5000);
        Socket socket = serverSocket.accept();
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        System.out.println("클라이언트 메시지: " + in.readLine());
        socket.close();
    }
}
```

##### JavaScript (UDP 서버 & 클라이언트)
```javascript
// UDP 서버
const dgram = require('dgram');
const server = dgram.createSocket('udp4');
server.on('message', (msg, rinfo) => {
    console.log(`클라이언트 메시지: ${msg}`);
});
server.bind(5000);
```

##### Python (TCP 서버 & 클라이언트)
```python
import socket

# TCP 서버
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("0.0.0.0", 5000))
server.listen(1)
client_socket, addr = server.accept()
print("클라이언트 메시지:", client_socket.recv(1024).decode())
client_socket.close()
```

---

## 4. 네트워크 사용 시 고려할 점
- **보안 문제**: 데이터 암호화(HTTPS), 방화벽(Firewall) 설정 필요
- **네트워크 속도 및 대역폭 관리**: 부하 분산 및 QoS(Quality of Service) 적용
- **IP 주소 관리**: 공인 IP와 사설 IP의 구분 및 NAT 적용 필요
- **서버 부하 분산**: 로드 밸런서를 활용한 트래픽 관리

---

## 5. 결론
네트워크는 **인터넷과 시스템 간 통신의 핵심 요소**이며, 면접에서는 OSI 7 계층, TCP/UDP, DNS, NAT, VPN 등 기본 개념을 정확히 이해하고 응용할 수 있는 능력이 중요하다. 다양한 네트워크 기술과 보안 개념을 학습하여 실무 적용 능력을 키워야 한다.

---
