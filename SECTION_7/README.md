# 섹션 7 - HTTP 헤더1

용도

- HTTP 전송에 필요한 모든 부가정보

HTTP BODY

- 메시지 본문(message body)은 엔티티 본문(entity body)을 전달하는데 사용
- 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
- 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공

- 메시지 본문(message body)을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- **표현**은 요청이나 응답에서 전달할 실제 데이터
- **표현 헤더**는 표현 데이터를 해석할 수 있는 정보 제공

### 표현

- Content-Type: 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language: 표현 데이터의 자연 언어
- Content-Length: 표현 데이터의 길이
- 표현 헤더는 전송, 응답 둘다 사용

**Content-Type**

**표현 데이터의 형식 설명**

- 미디어 타입, 문자 인코딩
- 예)
- text/html; charset=utf-8
- application/json
- image/png

**협상(콘텐츠 네고시에이션)**

**클라이언트가 선호하는 표현 요청**

- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 자연언어

협상 헤더는 요청시에만 사용

```java
GET /event
Accept-Language: ko
-> 

<-

```

협상과 우선순위1

- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko

협상과 우선순위2

Quality Values(q)

- 구체적인 것이 우선한다.
- Accept: text/*, text/plain, text/plain;format=flowed, *
    1. text/plain;format=flowed
    2. text
    3. text/*
    
    ---
    

### 전송 방식 설명

- 단순 전송

Content-Length

- 압축 전송

Content-Encoding

- 분할 전송

Transfer-Encoding

- 범위 전송

Range, Content-Range

### Referer

이전 웹 페이지 주소

### User-Agent

유저 에이전트 애플리케이션 정보

### **Server**

요청을 처리하는 ORIGIN 서버의 소프트웨어 정보

- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

### HOST

요청한 호스트 정보(도메인)

### Location

페이지 리다이렉션

### 인증

- Authorization: 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 질의

### 쿠키

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, 요청시 서버로 전달

- HTTP는 무상태(Stateless) 프로토콜이다
- 클라이언트와 서버는 서로 상태를 유지 X
- 모든 요청에 쿠키 정보 자동 포함

예) set-cookie: sessionId=abcde123; expires= ; path=/, domain=google.com; Secure

- 사용처
    - 사용자 로그인 세션 관리
    - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
    - 네트워크 트래픽 추가 유발
    - 최소한의 정보만 사용
    

쿠키 - 생명주기

- 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시까지만
- 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

명시: 명시한 문서 기준 도메인 + 서브 도메인 포함

- domain=example.org를 지정해서 쿠키 생성

쿠키 - 보안

Secure, HttpOnly, SameSite

- Secure
    - 쿠키는 http, https를 구분하지 않고 전송
    - Secure를 적용하면 https의 경우에만 전송
- HttpOnly
    - XSS 공격 방지
    - 자바 스크립트에서 접근 불가
    - HTTP 전송에만 사용
- SameSite
    - XSRF 공격 방지
    - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송