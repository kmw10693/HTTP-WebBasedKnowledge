# 섹션 6 - HTTP 상태코드

클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1XX (Informational): 요청이 수신되어 처리중
- 2xx (Successful): 요청 정상 처리
- 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요
- 4xx (Client Error): 클라 오류, 잘못된 문법등으로 서버가 요청을 수행 x
- 5xx (Server Error): 서버 오류, 서버가 정상요청 처리 x

---

### 2xx - 성공

- 200 OK
- 201 Created : 요청 성공해서 새로운 리소스가 생성됨
- 202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
- 204 No Content : 서버가 요청을 성공적 수행, 응답 페이로드 본문에 보낼 데이터 x

---

### 3xx - 리다이렉션

요청을 완료하기 위해 유저 에이전트의 추가 조치 필요

웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면 ,Location 위치로 자동 이동

```java
1. 요청 GET /event HTTP/1.1
Host: localhost:8080

2. 응답 HTTP/1.1 301 Moved Permanently
Location: /new-event
3. 자동 리다이렉트
4. 요청 GET /new-event HTTP/1.1
Host: localhost:8080
5. 응답

```

- 영구 리다이렉션 - 특정 리소스의 URI가 영구적 이동
- 예) /members → /users
- 일시 리다이렉션 - 일시적 변경
- 특수 리다이렉션
- 결과 대신 캐시 사용

301 Moved Permanently

- 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거 될 수 있음

308 Permanent Redirect

- 301과 기능은 같음
- 리다이렉트시 요청 메서드와 본문 유지

**일시적인 리다이렉션**

302, 307, 303

- 리소스의 URI가 일시적으로 변경
- 따라서 검색 엔진 등에서 URL을 변경하면 안됨
- 302 FOUND
- 307 Temporary Redirect
- **303 See Other(GET으로 변경)**

**PRG: Post/Redirect/Get**

일시적인 리다이렉션 - 예시

- POST로 주문후에 웹 브라우저를 새로고침하면?
- 새로고침은 다시 요청
- 중복 주문이 될 수 있다.

- POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트
- 중복 주문 대신에 결과 화면만 GET으로 다시 요청

**4xx (Client Error)**

**클라이언트 오류**

- 클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 오류의 원인이 클라이언트에 있음
- 중요! 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함

**400 Bad Request**

**클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음**

- 요청 구문, 메시지 등등 오류
- 클라이언트는 요청 내용을 다시 검토하고, 보내야함

**401 Unauthorized**

- 인증 되지 않음
- 인증(Authentication): 본인이 누구인지 확인, (로그인)
- 인가(Authrorization): 권한부여
- 오류 메시지가 Unauthorized 이지만 인증 되지 않음 (이름이 아쉬움)

**403 Forbidden**

- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우

**404 Not Found**

요청 리소스를 찾을 수 없음

- 요청 리소스가 서버에 없음
- 도는 클라이언트가 권한이 부족한 리소스에 접근할 떄 해당 리소스를 숨기고 싶을 때

**5xx (Server Error)**

**서버 오류**

- 서버 문제로 오류 발생

**503 Service Unavailable**

- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리 할 수 없음
- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수 도 있음