# TCP vs UDP

## 1. TCP와 UDP란?
TCP(Transmission Control Protocol)와 UDP(User Datagram Protocol)는 **인터넷에서 데이터를 전송하는 주요 프로토콜**이다. 각각의 특성과 차이를 이해하면 네트워크 프로그래밍과 시스템 설계에서 적절한 선택을 할 수 있다.

### 🔹 TCP (Transmission Control Protocol)
- 연결 지향형(서버-클라이언트 간 **연결을 설정**한 후 데이터 전송)
- 신뢰성 보장(패킷 손실 시 재전송, 흐름 제어, 순서 보장)
- 속도가 느리지만 안정적인 데이터 전송
- **사용 사례**: 웹 브라우징(HTTP, HTTPS), 이메일(SMTP, IMAP), 파일 전송(FTP)

### 🔹 UDP (User Datagram Protocol)
- 비연결형(데이터를 보내기만 하고, 받는 쪽이 확인하지 않음)
- 신뢰성이 낮지만 속도가 빠름
- 패킷 손실 가능성 존재(재전송 기능 없음)
- **사용 사례**: 실시간 스트리밍, 온라인 게임, VoIP(음성 통화)

---

## 2. TCP vs UDP 비교
| 특징 | TCP | UDP |
|------|-----|-----|
| 연결 방식 | 연결 지향(Connection-oriented) | 비연결(Connectionless) |
| 신뢰성 | 높음(패킷 손실 시 재전송) | 낮음(손실된 패킷 무시) |
| 데이터 순서 보장 | O | X |
| 속도 | 상대적으로 느림 | 빠름 |
| 사용 사례 | HTTP, 이메일, FTP | 스트리밍, 게임, VoIP |

---

## 3. TCP와 UDP의 동작 방식
### 🔹 TCP 3-Way Handshake (연결 설정 과정)
TCP는 데이터 전송 전에 **3-Way Handshake**를 통해 클라이언트와 서버 간 **연결을 설정**한다.
1. **SYN**: 클라이언트가 서버에 연결 요청
2. **SYN-ACK**: 서버가 요청을 승인
3. **ACK**: 클라이언트가 응답을 보내고 연결 확립

### 🔹 UDP 데이터 전송 방식
UDP는 연결을 설정하지 않고 바로 데이터를 전송한다. 별도의 흐름 제어나 오류 복구 기능이 없기 때문에 빠른 속도가 보장되지만 신뢰성은 떨어진다.

---

## 4. 코드 예제
### 🔹 TCP 통신 예제
##### Java (TCP 서버 & 클라이언트)
```java
// TCP 서버
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(5000);
        System.out.println("서버 대기 중...");
        Socket socket = serverSocket.accept();
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        System.out.println("클라이언트 메시지: " + in.readLine());
        socket.close();
    }
}
```

```java
// TCP 클라이언트
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 5000);
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        out.println("안녕하세요, 서버!");
        socket.close();
    }
}
```

### 🔹 UDP 통신 예제
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

```javascript
// UDP 클라이언트
const dgram = require('dgram');
const client = dgram.createSocket('udp4');
const message = Buffer.from("안녕하세요, 서버!");
client.send(message, 5000, 'localhost');
```

##### Python (UDP 서버 & 클라이언트)
```python
# UDP 서버
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server.bind(("localhost", 5000))
print("서버 대기 중...")
while True:
    data, addr = server.recvfrom(1024)
    print(f"클라이언트 메시지: {data.decode()}")
```

```python
# UDP 클라이언트
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
client.sendto(b"안녕하세요, 서버!", ("localhost", 5000))
```

---

## 5. 정리
- **TCP는 신뢰성을 보장하지만 속도가 느리며, UDP는 속도가 빠르지만 신뢰성이 낮음**
- **TCP는 연결 설정(3-Way Handshake)이 필요하지만, UDP는 바로 데이터 전송 가능**
- **사용 사례에 따라 적절한 프로토콜을 선택하는 것이 중요**

이제 TCP와 UDP의 차이점을 명확히 이해할 수 있으며, 실무에서 어떤 경우에 사용할지 고민해 볼 수 있다!
