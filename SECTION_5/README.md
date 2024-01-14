# 섹션5 HTTP 메서드 활용

- 쿼리 파라미터를 통한 데이터 전송
    - GET
    - 주로 정렬 필터(검색어)
- 메시지 바디를 통한 데이터 전송
    - POST, PUT, PATCH
    - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경
    

정적 데이터 조회

**쿼리 파라미터 미사용**

- 이미지, 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로 단순히 조회 가능

동적 데이터 조회

**쿼리 파라미터 사용**

- 주로 검색, 게시판 목록에서 정렬 필터(검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터 전달

**HTML Form 데이터 전송**

POST 전송 - 저장

**HTML Form 데이터 전송**

multipart/form-data

- HTML Form submit시 POST 전송
- 예) 회원 가입, 상품 주문, 데이터 변경
- Content-Type: application/x-www-form-urlencoded 사용
    - form의 내용을 메시지 바디를 통해서 전송
    - 전송 데이터를 url encoding 처리
    

HTTP API 데이터 전송

```java
POST /members HTTP/1.1
Content-Type: application/json
{
	"username": "young",
	"age" : 20
}
```

정리

- 서버 to 서버
- 앱 클라이언트
- 웹 클라이언트
- HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용
- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달

---

HTTP API 설계 예시

- 회원 목록 /members → GET
- 회원 등록 /members → POST
- 회원 조회 /members/{id} → GET
- 회원 수정 /members/{id} → PATCH, PUT, POST
- 회원 삭제 /members/{id} → DELETE

POST - 신규 자원 등록 특징

- 클라이언트는 등록될 리소스의 URI를 모른다
- 서버가 새로 등록된 리소스 URI를 생성해준다.

**파일 관리 시스템**

**API 설계 - PUT 기반 등록**

- 파일 목록 /files → GET
- 파일 조회 /files/{filename} → GET
- 파일 등록 /files/{filename} → PUT
- 파일 삭제 /files/{filename} → DELETE
- 파일 대량 등록 /files → POST

- 클라이언트가 리소스 URI를 모두 알고 있어야 함
- 클라이언트가 직접 리소스의 URI를 지정

**스토어**

- 클라이언트가 관리하는 리소스 저장소
- 클라이언트가 리소스의 URI를 알고 관리

문서(document)

- 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
- 예) /members/100, /files/star.jpg

컬렉션(collection)

- 서버가 관리하는 리소스 디렉터리
- 서버가 리소스의 URI를 생성하고 관리
- /members

스토어(store)

- 클라이언트가 관리하는 자원 저장소

- 컨트롤러(controller), 컨트롤 uri
- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
- 동사를 직접 사용
- /members/{id}/delete