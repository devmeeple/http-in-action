# 5. HTTP 메서드 활용

- 클라이언트 -> 서버 데이터 전송
- HTTP API 설계 예시

## 클라이언트에서 서버로 데이터 전송

데이터 전달 방식은 크게 2가지이다.

1. 쿼리파라미터를 사용한 데이터 전송
    - GET
    - 주로 정렬 필터(검색어)

2. 메시지 바디를 사용한 데이터 전송
    - POST, PUH, PATCH
    - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

### 상황

조회는 GET을 사용한다. (1, 2)

1. 정적 데이터 조회
    - 이미지,정적 텍스트 문서
    - 쿼리 파라미터 없이 리소스 경로로 단순조회 가능
2. 동적 데이터 조회
    - 주로 검색,게시판 목록에서 정렬 필터(검색어)
    - 조회 조건을 줄여주는 필터(검색어), 조회 결과를 정렬하는 정렬 조건에 주로 사용
    - 쿼리 파라미터를 사용해서 데이터를 전달
3. HTML Form을 통한 데이터 전송
    - HTML Form submit시 POST 전송
        - 예)회원 가입, 상품 주문, 데이터 변경
    - Content-Type: application/x-www-form-urlencoded 사용
        - form 내용을 메시지 바디에 담아서 전송(key=value 쿼리 파라미터 형식)
        - 전송 데이터를 url encoding 처리
    - GET으로도 전송이 가능하지만 권장하지 않음
    - Content-Type: multipart/form-data
        - 파일 업로드 같은 바이너리 데이터 전송 시 사용
        - 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능
    - **HTML Form 전송은 GET, POST만 지원**

4. HTTP API를 통한 데이터 전송
    - 회원 가입, 상품 주문, 데이터 변경
    - 서버 -> 서버(시스템 통신), 앱 클라이언트, 웹 클라이언트(Ajax)
    - POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
    - GET: 조회, 쿼리 파라미터를 사용해 전달
    - Content-Type: application/json을 주로 사용(사실상 표준)
        - TEXT, XML, JSON 등등

## API 설계

HTTP API를 어떤식으로 설계하는지 알아보자. POST 기반, PUT 기반의 차이를 이해한다.

> 대부분 POST 기반으로 설계한다. PUT도 사용하지만 비중이 적다.

- HTTP API - 컬렉션
    - POST 기반 등록
    - 예) 회원 관리 API 제공
- HTTP API- 스토어
    - PUT 기반 등록
    - 예) 정적 컨텐츠 관리, 원격 파일 관리
- HTTP Form 사용
    - 웹 페이지 회원 관리
    - GET, POST만 지원

### 회원 관리 시스템

API 설계 - POST 기반 등록

```text
회원 목록 GET /members
회원 등록 POST /members
회원 조회 GET /members/{id}
회원 수정 PATCH, PUT, POST /members/{id}
회원 삭제 DELETE /members/{id}
```

POST - 신규 자원 등록 특징

- 클라이언트는 등록될 리소스의 URI를 모른다.
    - 회원 등록 POST /members
    - POST /members
- 서버가 새로 등록된 리소스 URI을 생성해준다.
    - ```text
      HTTP/1.1 201 Created
      Location: /members/100
      ```
- 컬렉션(Collection)
    - 서버가 관리하는 리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리
    - 여기서 컬렉션은 /members

### 파일 관리 시스템

API 설계 - PUT 기반 등록

```text
파일 목록 GET /files
파일 등록 PUT /files/{filename}
파일 조회 GET /files/{filename}
파일 삭제 DELETE /files/{filename}
파일 대량 등록 POST /files
```

PUT - 신규 자원 등록 특징

- 클라이언트가 리소스 URI를 알고 있어야 한다.
    - 파일 등록 PUT /files/{filename}
    - PUT /files/star.jpg
- 클라이언트가 직접 리소스의 URI를 지정한다.
- 스토어(Store)
    - 클라이언트가 관리하는 리소스 저장소
    - 클라이언트가 리소스의 URI을 알고 관리
    - 여기서 스토어는 /files

HTML Form 사용

순수 HTML, HTML Form을 기준으로 이야기 한다.

- HTML Form은 GET, POST만 지원한다.
- GET, POST만 지원하므로 제약이 있다.
    - Ajax 같은 기술을 사용해서 해결 가능하다.

```text
회원 목록 GET /members
회원 등록 폼 GET /members/new
회원 등록 POST /members/new, /members
회원 조회 GET /members/{id}
회원 수정 폼 GET /members/{id}/edit
회원 수정 POST /members/{id}/edit, /members/{id}
회원 삭제 POST /members/{id}/delete
```

- HTML Form은 GET, POST만 지원하기 때문에 제약이 많은 것을 볼 수 있다.
- 컨트롤 URI를 사용해야 한다.
    - 제약을 해결하기 위해 동사로 된 리소스 경로 사용
    - POST의 /new, /edit, /delete가 컨트롤 URI
    - HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)

> 이상적으로 해결하면 좋겠지만 실무는 애매한 경우가 많다. 컨트롤 URI도 많이 사용된다.
> 하지만 명심해야 할 것은 리소스로 설계를 우선 진행하고 대체제로 컨트롤 URI를 사용해야 한다.

## 정리

- HTTP API - 컬렉션
    - POST 기반 등록
    - 서버가 리소스 URI 결정
- HTTP API - 스토어
    - PUT 기반 등록
    - 클라이언트가 리소스 URI 결정
- HTML Form 사용
    - 순수 HTML + HTML Form 사용
    - GET, POST만 지원

### 참고하면 좋은 URI 설계

[REST API URI Naming Conventions](https://restfulapi.net/resource-naming/)

- 문서(document)
    - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
    - /members/100, /files/star.jpg
- ✅ 컬렉션(collection)
    - 서버가 관리하는 리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리
    - 예) /members
- 스토어(store)
    - 클라이언트가 관리하는 자원 저장소
    - 클라이언트가 리소스의 URI를 알고 관리
    - 예) /files
- 컨트롤러(controller), 컨트롤 URI
    - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 작업
    - 동사를 직접 사용
    - 예) /members/{id}/delete