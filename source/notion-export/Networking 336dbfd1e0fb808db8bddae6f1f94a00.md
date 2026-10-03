# Networking

속성: Infra

#### Networking Concepts

- DNS - 🟢 Easy
- IP Address - 🟢 Easy
- Ports - 🟢 Easy
- HTTP - 🟢 Easy
- TCP / UDP - 🟡 Easy–Medium
- Subnets - 🟡 Easy–Medium
- NAT - 🟡 Easy–Medium
- Firewall - 🟡 Easy–Medium
- Routing - 🟡 Easy–Medium
- ARP - 🟡 Easy–Medium
- Load Balancer - 🟠 Medium
- Reverse Proxy - 🟠 Medium
- CDN - 🟠 Medium
- VPC - 🟠 Medium
- VPN - 🟠 Medium
- TLS - 🔴 Hard
- HTTPS (internals) - 🔴 Hard
- TLS - 🔴 Hard
- DNS Internals - 🔴 Hard
- BGP - 🔴 Hard
- MTU / Fragmentation - 🔴 Hard

#### 아무도 컴퓨터 네트워킹을 이렇게 설명하지 않아

- 인터넷 = 네트워크들이 서로 대화하는 것
- IP 주소 = 당신 기기의 신분증
- DNS = 인터넷의 전화번호부
- TCP 대 UDP = 신뢰성 대 속도
- 라우터 = 교통 통제자
- 방화벽 = 보안 게이트
- 지연 = 거리 + 지체

네트워킹은 암기가 아니야. 데이터가 어떻게 이동하는지 이해하는 거지.

#### Targeted Ports by Hackers

🔒 Port 21 (FTP)

🚪 Port 22 (SSH)

💻 Port 23 (Telnet)

📧 Port 25 (SMTP)

🌐 Port 53 (DNS)

🌐 Port 80 (HTTP)

🔒 Port 443 (HTTPS)

🎮 Port 3074 (Xbox Live)

📲 Port 5060 (SIP)

🎲 Port 8080 (Proxy)

📁 Port 135 (RPC)

🖥️ Port 139 (NetBIOS)

🔓 Port 1433 (MSSQL)

🎲 Port 1521 (Oracle)

🔓 Port 1723 (PPTP)

📤 Port 1900 (UPnP)

🎮 Port 2302 (DayZ)

🖨️ Port 3389 (RDP)

🔒 Port 3306 (MySQL)

🕸️ Port 4000 (Elasticsearch)

📂 Port 4444 (Metasploit)

📤 Port 5000 (Python Flask)

🎮 Port 5555 (Android Debug Bridge)

📤 Port 5900 (VNC)

🖥️ Port 6667 (IRC)

📧 Port 6697 (IRC SSL)

📂 Port 8000 (HTTP Alt)

🖥️ Port 8081 (HTTP Proxy)

🔓 Port 9100 (Printer)

📂 Port 27017 (MongoDB)

🌐 Port 28017 (MongoDB HTTP Interface)

📂 Port 9090 (Web Debugging)

📁 Port 445 (SMB)

💻 Ports 5985/5986 (WinRM)

🔄 Port 6379 (Redis)

📂 Port 6666 (IRC)

📧 Port 993 (IMAP SSL)

🔒 Port 995 (POP3 SSL)

🎲 Port 1434 (Microsoft SQL Monitor)

#### Network Protocols

https://x.com/i/status/2047835811958382792

![image.png](image%2014.png)

#### 대부분의 사람들은 자신의 앱이 사용자를 처리한다고 생각합니다.

그렇지 않습니다. Nginx가 처리합니다.

사용자 → Nginx → 당신의 앱

- 웹사이트를 빠르게 제공합니다
- 요청을 백엔드로 전송합니다
- 서버 간 트래픽을 균형 있게 분산합니다
- 속도를 위해 응답을 캐시합니다

가볍습니다. 빠릅니다. 대규모 트래픽을 처리합니다.

대부분의 앱은 사용자를 직접 상대하지 않습니다. Nginx가 합니다.

당신의 설정에서 Nginx를 사용해 보셨나요?

![image.png](image%2015.png)

#### 카페 wi-fi 는 방화벽을 카페에 설치 안해두면 위험하겠다 생각이 든게

지금은 없어진 집근처 카x베네 wi-fi 라우터가 악성코드 감염되어 있어서 비보안(http) 통신은 중간에서 가로채 도박 사이트 배너 띄우고 그랬음.

보안(https) 통신은 문제가 없었음. 그래서 https가 왜 중요한지 그때 다시 상기시켜줬지

http는 모든 구간에서 그 내용을 들여다보고 변경할 수 있는 평문 전송입니다. 그래서 라우터도 이걸 변경해서 다른 정보를 보여줄 수 있죠

https는 양 끝 단에서만 해석이 가능한 보안 통신입니다. 그래서 라우터가 악성코드 감염되어도 멀쩡한 정보를 받을 수 있죠

#### SSH 터널 심층 탐구 - 원격 포트 포워딩

![image.png](image%2016.png)

### 1. 기본 명령어 구조

SSH 원격 포트 포워딩을 설정하는 기본 명령어 구문은 다음과 같습니다.

```jsx
$ ssh -R [remote_addr:]remote_port:local_addr:local_port [user@]sshsrv_addr
```

이미지에서 제시된 예시 명령어는 작성 방식에 따라 두 가지로 나뉩니다.

- **Long Form**
    
    ```jsx
    ssh -R 0.0.0.0:8080:localhost:80 user@pub-ssh-server
    ```
    
- **Short Form**
    
    ```jsx
    ssh -R 8080:localhost:80 user@pub-ssh-server
    ```
    

### 2. 명령어 구성 요소 분석

- **`R`**: SSH 클라이언트에게 원격 포트 포워딩 설정을 지시합니다.
- **`0.0.0.0:8080` (원격 주소 및 포트)**: 원격 SSH 서버가 수신(Listen)을 대기할 주소와 포트입니다. 서버 설정(GatewayPorts)이 허용될 경우 모든 네트워크 인터페이스(`0.0.0.0`)에서 포트 `8080`으로 들어오는 트래픽을 수신합니다.
- **`localhost:80` (로컬 주소 및 포트)**: 원격 서버에서 받은 트래픽이 최종적으로 전달될 SSH 클라이언트 측의 주소와 포트입니다. 해당 예시에서는 클라이언트 기기(James의 머신)의 `localhost:80`으로 트래픽을 보냅니다.
- **`user@pub-ssh-server`**: 터널을 생성하기 위해 접속할 대상 퍼블릭 SSH 서버의 계정과 주소입니다.

### 3. 핵심 주의 사항: 서버의 `GatewayPorts` 설정

원격 포트 포워딩이 외부망에서 정상적으로 작동하기 위해서는 SSH 서버 측의 설정 확인이 필수적입니다.

- **기본 동작의 한계:** 기본적으로 `R` 옵션을 사용하면 원격 SSH 서버는 보안상 루프백 인터페이스(`127.0.0.1`)에서만 수신 대기합니다. 즉, 외부 IP(예: `10.2.0.2` 등)를 명시적으로 지정해도 서버 외부에서는 접근할 수 없습니다.
- **설정 파일 위치:** 이 동작은 서버의 `sshd_config` 파일 내 `GatewayPorts` 설정에 의해 제어되며 기본값은 `no`입니다.
- **해결 및 변경 방법:**
    - **`GatewayPorts yes`**: 서버가 포워딩된 포트에 대해 모든 인터페이스에서 수신을 허용합니다. 이 설정을 켜면 명령어에서 `0.0.0.0`을 생략(Short Form)하더라도 서버가 자동으로 모든 인터페이스에서 수신 대기합니다.
    - **`GatewayPorts clientspecified`**: 클라이언트가 `R` 명령어에서 명시한 바인드 주소(Bind Address)를 서버가 그대로 존중하여 동작하게 합니다.

### 4. 동작 원리 및 트래픽 흐름 모델링

**[네트워크 참여 요소]**

1. **James (로컬 측 / 내부 네트워크):** 방화벽/NAT 뒤에 위치한 SSH 클라이언트이며, 내부적으로 웹 서버(`localhost:80`)를 구동 중입니다.
2. **Public SSH Server (퍼블릭 서버):** 공인 IP를 가져 외부 통신이 가능한 중간 서버입니다.
3. **Kay (원격 측 / 외부 네트워크):** James의 내부 웹 서버에 접근하고자 하는 외부 사용자입니다.

**[포워딩 및 통신 프로세스]**

1. **터널 생성:** James가 자신의 환경에서 퍼블릭 SSH 서버로 `ssh -R` 명령어를 실행하여 **SSH 터널을 확립**합니다.
2. **요청 발생:** 외부 사용자 Kay가 퍼블릭 SSH 서버의 노출된 포트로 접근을 시도합니다.
    - 실행 명령어: `$ curl public-ssh-server:8080`
3. **트래픽 전달:** 퍼블릭 SSH 서버는 `8080` 포트로 들어온 요청을 앞서 생성된 **SSH 터널을 통해 James의 머신으로 포워딩**합니다.
4. **최종 응답:** 트래픽을 넘겨받은 James의 SSH 클라이언트는 이를 자신이 구동 중인 로컬 웹 서버(`localhost:80`)로 라우팅하여 Kay에게 응답을 반환합니다.

#### HTTPS .local 도메인

localhost에서 "연결이 비공개가 아닙니다" 오류에 지쳤나요? 몇 초 만에 로컬 프로젝트를 위한 신뢰할 수 있는 HTTPS .local 도메인을 설정하세요.

https://www.tecmint.com/setup-https-local-domain-linux/

로컬 개발할 때 브라우저 보안 경고 때문에 쿠키나 세션 꼬여서 고생해본 사람들은 무조건 챙겨둘 자료임. 리눅스 환경에서 .local 도메인으로 HTTPS 인증 간단하게 붙이는 가이드인데, 설정 한 번 해두면 테스트할 때마다 터지는 귀찮은 예외 상황에서 해방임. 실무랑 똑같은 보안 환경 미리 맞추는 게 나중에 삽질 비용 줄이는 답임.

#### 초보자가 알아야 할 10가지 네트워킹 도구

- Ping – 연결성 테스트
- Traceroute – 패킷 경로 추적
- Netstat – 네트워크 연결 검사
- Wireshark – 패킷 분석
- Nslookup – DNS 문제 해결
- Curl – API 및 엔드포인트 테스트
- SSH – 서버 안전 접근
- IPConfig / IFConfig – 네트워크 설정 검사
- Speedtest – 대역폭 측정
- Nmap – 네트워크 및 포트 스캔