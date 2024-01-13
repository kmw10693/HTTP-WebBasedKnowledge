# 섹션 1 인터넷 통신

### 인터넷에서 컴퓨터 둘은 어떻게 통신할까?

클라이언트 ↔ 인터넷 ↔ 서버

**IP(인터넷 프로토콜)**

- 지정한 IP 주소(IP Address)에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 전달

출발: 200.200.200.2

목적: 100.100.100.1 OK

---

### IP 프로토콜의 한계

- 패킷을 받을 대상이 없거나 서비스 불능 상태에도 패킷 전송

**비신뢰성**

- 중간에 패킷이 사라지면?
- 패킷이 순서대로 안오면?

**프로그램 구분**

- 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

**패킷 전달 순서 문제 발생**

---

### TCP & UDP

- 인터넷 프로토콜 스택의 4계층

애플리케이션 계층 - HTTP, FTP

전송 계층 - TCP, UDP

인터넷 계층 - IP

네트워크 인터페이스 계층

### 프로토콜 계층

1. 프로그램이 Hello, world! 메시지 생성
2. SOCKET 라이브러리를 통해 전달
3. TCP 정보 생성, 메시지 데이터 포함
4. IP 패킷 생성, TCP 데이터 포함

---

### TCP/IP 패킷 정보

**IP 패킷**: 출발지 IP, 목적지 IP, 기타

**TCP 세그먼트**: 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보

### TCP 특징

전송 제어 프로토콜(Transmission Control Protocol)

- 연결 지향 - TCP 3 way handshake (가상 연결)
- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜

### TCP 3 way handshake

클라이언트 ↔ 서버

1. SYN: 접속 요청
2. SYN+ACK : 접속 요청 & 요청 수락
3. ACK
4. 데이터 전송

### 1. 데이터 전달 보증

### 2. 순서 보장

1. 패킷1, 패킷2, 패킷3 순서로 전송
2. 패킷1, 패킷3, 패킷2 순서로 도착
3. 패킷2부터 다시 보내

### 3. UDP 특징

- IP와 거의 같다 + PORT + 체크섬 정도만 추가

---

## PORT

### 한번에 둘 이상 연결해야 하면?

서버 안에서 돌아가는 애플리케이션 구분: 포트

**PORT - 같은 IP 내에서 프로세스 구분**

0 ~65535 할당 가능

0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음

- ftp - 20, 21
- TELNET - 23
- HTTP - 80
- HTTPS - 443

---

# DNS

### IP는 기억하기 어렵다.

**DNS 도메인 네임 시스템(Domain Name System)**

- 전화번호부
- 도메인 명을 IP 주소로 변환

1. 도메인 명 google.com
2. 응답: 200.200.200.2
3. 접속: 200.200.200.2