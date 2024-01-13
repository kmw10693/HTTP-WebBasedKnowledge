# 섹션 2 URI와 웹 브라우저 요청 흐름

- URI
- 웹 브라우저 요청 흐름

---

### URI(Uniform Resource Identifier)

URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다.

URI: **URL(Resource Locator), URN(Resource Name)**

**URI 단어 뜻**

- Uniform: 리소스 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier: 다른 항목과 구분하는데 필요한 정보

**URL, URN 단어 뜻**

- URL - Locator: 리소스가 있는 위치를 지정
- URN - Name: 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다.

### URL 전체 문법

**scheme**

- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
- http는 80포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

**path**

- 리소스 경로(path), 계층적 구조
- /home/file1.jpg
- /members
- /members/100, /items/iphone12

**query**

- key=value 형태
- ?로 시작, &로 추가 가능
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

---

### 웹 브라우저 요청 흐름

https://www.google.com:443/search?q=hello&hl=ko

1. DNS 조회 (HTTPS PORT 생략, 443)
2. HTTP 요청 메시지 생성
3. TCP/IP 패킷 감싸음
4. 요청 패킷 도착 
5. HTTP 응답 메시지
6. 응답 패킷 전달
7. 웹 브라우저 HTML 렌더링