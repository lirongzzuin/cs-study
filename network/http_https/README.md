# HTTP vs HTTPS

## 1. HTTP와 HTTPS란?
HTTP(HyperText Transfer Protocol)와 HTTPS(HyperText Transfer Protocol Secure)는 **웹에서 데이터를 주고받는 프로토콜**이다. 차이점을 이해하면 보안이 중요한 웹 서비스에서 어떤 방식을 선택해야 하는지 판단할 수 있다.

### 🔹 HTTP (HyperText Transfer Protocol)
- **기본적인 웹 통신 프로토콜**
- 데이터를 암호화하지 않고 전송
- 속도가 빠르지만 보안 취약점 존재
- **사용 사례**: 공공 웹사이트, 블로그, 뉴스 사이트

### 🔹 HTTPS (HyperText Transfer Protocol Secure)
- **SSL/TLS 암호화를 적용한 HTTP**
- 데이터를 암호화하여 보안성을 높임
- 신뢰할 수 있는 인증서를 사용하여 피싱 및 중간자 공격 방지
- **사용 사례**: 금융 서비스, 전자상거래, 로그인 페이지

---

## 2. HTTP vs HTTPS 비교
| 특징 | HTTP | HTTPS |
|------|------|------|
| 보안 | 암호화 없음 | SSL/TLS 암호화 적용 |
| 데이터 무결성 | 데이터 변조 가능성 있음 | 데이터 무결성 보장 |
| 신뢰성 | 피싱 공격에 취약 | 인증서를 통한 신뢰성 확보 |
| 속도 | HTTPS보다 빠름 | 암호화 과정으로 인해 약간 느림 |
| 사용 사례 | 일반 정보 제공 사이트 | 로그인, 결제 등 보안이 필요한 서비스 |

---

## 3. HTTPS의 동작 방식
### 🔹 HTTPS 연결 과정 (SSL/TLS Handshake)
1. **클라이언트(브라우저)가 서버에 접속** (https:// 로 시작하는 URL 요청)
2. **서버가 SSL/TLS 인증서를 제공** (공개키 포함)
3. **클라이언트가 서버 인증서를 검증** (인증서 유효성 체크)
4. **보안 키 교환 후 암호화된 데이터 전송**
5. **클라이언트와 서버 간 안전한 통신 진행**

---

## 4. 코드 예제
### 🔹 HTTP 요청 예제
##### JavaScript (Fetch API)
```javascript
fetch('http://example.com')
  .then(response => response.text())
  .then(data => console.log(data));
```

##### Python (requests 라이브러리)
```python
import requests
response = requests.get("http://example.com")
print(response.text)
```

### 🔹 HTTPS 요청 예제
##### Java (HttpURLConnection)
```java
import java.io.*;
import java.net.*;

public class HttpsExample {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://example.com");
        HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
        BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String inputLine;
        while ((inputLine = in.readLine()) != null) {
            System.out.println(inputLine);
        }
        in.close();
    }
}
```

---

## 5. HTTPS 적용 방법
1. **SSL/TLS 인증서 구매 또는 무료 인증서 사용 (Let's Encrypt 추천)**
2. **웹 서버 설정 (Nginx, Apache 등)에서 HTTPS 적용**
3. **HSTS(HTTP Strict Transport Security) 적용으로 강제 HTTPS 전환**
4. **인증서 자동 갱신 설정 (Certbot 등 활용)**

---

## 6. 정리
- **HTTP는 보안이 없지만 속도가 빠르며, HTTPS는 보안성이 뛰어나지만 약간의 속도 저하가 있음**
- **HTTPS는 데이터 암호화와 무결성을 제공하며, 신뢰할 수 있는 웹사이트 운영을 위한 필수 요소**
- **SSL/TLS 인증서를 적용하여 보안 강화를 추천**

이제 HTTP와 HTTPS의 차이점을 명확히 이해할 수 있으며, 보안이 중요한 웹 서비스에서 HTTPS를 반드시 사용해야 하는 이유도 확인할 수 있다!
