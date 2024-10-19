# HTTP in Action

1. [인터넷네트워크](./1_인터넷_네트워크/README.md)
2. [URI와 웹 브라우저 요청 흐름](./2_URI와_웹_브라우저_요청_흐름/README.md)
3. [HTTP 기본](./3_HTTP_기본/README.md)
4. [HTTP 메서드](./4_HTTP_메서드/README.md)
5. [HTTP 메서드 활용](./5_HTTP_메서드_활용/README.md)

# 모든 개발자를 위한 HTTP 웹 기본 지식

- HTTP의 전체 흐름 이해
- 실무에 꼭 필요한 핵심 내용

최근 스터디에서 '멱등성'을 주제로 대화를 나눴다. 자주 사용하는 HTTP 프로토콜이지만 나만의 정의가 없었다. 만약 정의가 되어있었다면 기준과 개념에 대해 대화를 나눌 수 있지 않았을까?
이렇게 웹 개발자가 되고 싶다면 HTTP는 한번쯤 고민하는 주제다. 웹 프레임워크는 HTTP위에서 동작한다. 따라서 사용자가 'HTTP를 당연히 이해하고 있다'라고 가정한다.
나만의 기준이 없다면 "API를 어떻게 설계할 것인가?", "상태코드는 어떻게 설정할 것인가?" 이런 고민을 나눌 수 없다. 언젠가 마주하고 정의해야 하는 주제라면 지금이 적기다.
지식 공유자는 본인의 기준을 제안한다. 네트워크부터 시작해서 실무에서 활용되는 HTTP 개념까지 함께 알아보자.

# 1. 인터넷 네트워크

- 인터넷 통신
- IP(Internet Protocol)
- TCP, UDP
- PORT
- DNS

## 인터넷 통신

"HTTP를 배우고 싶어요. 그런데 왜 인터넷 네트워크를 알아야 하나요?"

HTTP와 웹은 인터넷 네트워크 위에서 동작한다. 클라이언트와 서버가 통신할 때 인터넷 네트워크를 사용한다. 그렇다. 우리는 지금 이 순간에도 인터넷을 사용하고 있다.
그렇다면 어떤 규칙으로 안전하게 통신할 수 있는 걸까?

## IP(Internet Protocol)

IP(Internet Protocol)란 인터넷이 통신하는 네트워크에서 정보를 송신, 수신할 때 사용하는 규약이다. IP는 '지정한 주소(IP Address)로 정보를 전송한다'는 규칙을 가진다.
이때 정보를 전송하는 단위는 '패킷(Packet)'이라한다. 데이터를 전송할 때는 매번 다른 길(Node)을 사용할 수 있다.

IP도 한계점이 명확하다. 대표적으로 이야기하는 한계점은 비연결성, 비신뢰성, 프로그램 구분이다.

**1. 비연결성**

"나는 몰라요. 갑니다~"

비연결성이란 수신자의 상태가 확인되지 않아도 전송 가능하다는 뜻이다. 상대방의 의사와 상태는 확인하지 않는다.

**2. 비신뢰성**

"내가 생각했던 건 이게 아닌데..."

비신뢰성이란 2가지를 이야기한다. 순서대로 도착하지 않고, 중간에 소실될 수 있다. 그렇다면 왜 그럴까? 패킷이 크면 나눠서 전송한다.
적절한 예시는 인터넷 방송이다. 네트워크가 혼잡하고 과부하에 걸리면 패킷이 손실된다. 방송에 버퍼링이 생기고 끊기는 이유는 네트워크의 과부하, 패킷의 손실과 관련 있다.

**3. 프로그램 구분**

"음악도 듣고 게임도 하고 멀티플레이어"

우리는 동시에 여러 프로그램을 실행한다. 예를 들어 Lo-Fi를 들으며 코딩한다. 그렇다면 같은 IP를 어떻게 구분할까?

IP는 다음과 같은 한계점이 있다. 상호보완하기 위해 함께 사용되는 기술은 TCP, UDP다.

## TCP, UDP

TCP, UDP 재수강

## PORT

"한 번에 여러 곳에 연결해야 한다면? 너희 집 몇 동 몇 호야?"

PORT는 같은 IP 내에서 프로세스를 구분한다. 자주 사용하는 PORT는 사용하지 않는다. 예를 들어 파일을 전송할 때 21번, 웹 서핑을 할 때는 80번이 있다.

## 도메인 이름 시스템(Domain Name System, DNS)

IP 주소는 외우기 어렵고 변경될 수 있다. 이러한 문제를 해결하기 위해 도메인 이름 시스템(Domain Name System)을 사용한다. 예를들어 흔히 구글, 네이버와 같은 사이트에 주소를 몰라도 들어갈
수 있는 이유는 도메인 이름 시스템 덕분이다.

## 마무리

HTTP는 IP를 사용해서 인터넷 네트워크위에서 동작한다. 자주 사용하는 IP는 장점도 있지만 도 명확한 단점[^1]이 있다. 이를 보완하기 위해 TCP, UDP, PORT, DNS를 사용한다.

# 2. URI와 웹 브라우저 요청 흐름

URI는 통합 자원 식별자를 의미한다. 하위 개념으로 URL, URN이 포함되는데 주로 사용되는 건 URL이다. 결국 오늘날에는 URI, URL을 같은 맥락으로 사용한다.
클라이언트는 입력한 URL을 DNS을 조회해서 IP 주소를 알아낸다. 이어서 HTTP 요청 메시지를 만든다. 서버는 요청 메시지를 읽고 응답 메시지를 만들어서 다시 전송한다.
결국 우리가 브라우저를 사용해 보는 화면은 이런 과정을 거쳐 만들어진다.

## URI(Uniform Resource Identifier)

- URL 문법

URI는 통합 자원 식별자 라고한다. URI에 URL과 URN이 포함된다. URL, URN은 자원을 식별하는 방법에 따라 분류된다. 이때 URL은 위치, URN은 이름으로 식별한다. 하지만 URN은 보편적으로
사용하기엔 어려워서 사용하지 않는다. 따라서 지금은 URI와 URL을 같은 맥락으로 사용한다.

## 웹 브라우저 요청 흐름

웹 브라우저(클라이언트)는 DNS를 먼저 조회해서 도착지를 확인한다. HTTP 요청 메시지는 socket 라이브러리를 통해 만들어진다. 이때 TCP/IP 패킷이 포함된다. 서버는 도착한 메시지를 확인하고
응답 타입, 길이등 응답 메시지를 전송한다. 클라이언트는 응답 메시지를 확인해서 브라우저에 렌더링 된다.

# 3. HTTP 기본

"HTTP로 모든 것을 할 수 있다" 이야기하는 게 과장이 아닐 정도로 다양한 분야에 HTTP를 사용한다. 다양한 분야에 사용될 만큼 거대해진 HTTP를 배울 때 HTTP/1.1을 강조한다. 이후 나온 버전들도
물론 필요하지만 핵심기능은 HTTP/1.1에 개발됐다. 이러한 HTTP는 클라이언트 서버 구조, 무상태 프로토콜과 같은 특징을 가진다. 또한 메시지도 알아야 한다. 그렇다. 지금은 HTTP 시대다.

## 모든 것이 HTTP

HTTP의 시작은 미약했다. 간단한 HTML(HyperText Markup Language) 전송을 위해 등장했다. 하지만 현재는 '모든 것을 HTTP로 할 수 있다'라고 해도 과장이 아니다. 예를 들어 서버 간의
통신, 이미지, 동영상 등 다양한 데이터를 전송할 때 사용한다. 이렇게 HTTP는 계속 진화했다. 현재는 HTTP/2, 3 버전도 사용되지만 핵심기능은 HTTP/1.1에서 개발됐다.
따라서 HTTP/1.1을 먼저 알아보자. 여러 특징 중 핵심적인 특징[^2]을 다룬다.

## 클라이언트 서버 구조

HTTP는 클라이언트 서버 구조를 가진다. 클라이언트는 요청(Request)을 서버는 응답(Response)한다. 간단한 구조지만 신경 쓸 필요가 있다. 과거에는 클라이언트와 서버의 구분이 애매했다.
하지만 지금은 클라이언트와 서버를 분리해서 독립적인 발전을 실현한다. 클라이언트는 UI/UX에 집중하고, 서버는 비즈니스 로직과 데이터에 집중한다.

## Stateful, Stateless

> 재수강이 필요하다. Stateful vs Stateless 적절한 예시추가, 한계

무상태 프로토콜(Stateless Protocol)은 서버가 클라이언트 상태를 보존하지 않는다. 수평확장(Scale-out)이 유리하지만, 클라이언트가 추가 데이터를 제공해야 한다는 단점이 있다.

## 비연결성(Connectionless)

비연결성은 연결을 유지하지 않는다. 덕분에 서버자원을 효율적으로 사용할 수 있다. 물론 비연결성도 한계가 명확하다. 매번 TCP/IP 연결이 필요해서 3-Way Handshake 시간이 추가된다.
이러한 문제는 지속 연결(Persistent Connections)을 통해 극복한다. 또한 HTTP/2, HTTP/3에서 최적화 중이다.

특정 시간에 발생하는 이벤트[^3]는 대용량 트래픽이 요구된다. 문제를 해결하기 위해서는 무상태(Stateless) 설계가 중요하다. 이는 서버 개발자의 업무 중 어려운 편에 속한다.
하지만 우리는 어떻게 이 문제를 해결할 것인지 고뇌가 필요하다. 예를 들어 신청페이지와 소개페이지를 분리하는 방법으로 분리한다.

## HTTP 메시지

HTTP 메시지는 요청과 응답에 따라 내용이 다르다. 하지만 크게 보면 다음과 같은 구조를 가진다. 시작, 헤더, 공백라인(CRLF)', '메시지

# 4. HTTP 메서드

## HTTP API를 만들어보자

"API URI를 설계하세요" 처음 맡겨진 과제다. 어떻게 API를 설계하면 좋을지 고민에 빠진다. API URI 설계에서 강조하는 점은 '자원(Resource)'다. 무엇을 의미할까.
"음식을 먹는다", "음식을 포장한다" 이와 같은 요구사항에 API를 설계할 때 직역해서 `/eat-food`, `/pack-food`와 비슷하게 설계할 수 있다. 하지만 앞서 이야기했듯 자원을 기준으로 설계한다.
동작은 HTTP 메서드[^4]가 표현한다. 돌아보면 중요한 자원은 음식이다. "음식을 먹는다"를 `POST /food`와 같이 설계한다. 이러한 원칙과 함께 API를 설계했을 때 직관적이고 일관성을 얻을 수 있다.

계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장(member -> members)

## HTTP 메서드 - GET, POST

HTTP 메서드는 다양하다. 자주 사용되는 메서드는 `GET`, `POST`, `PUT`, `PATCH`, `DELETE`다. 간단하게 알아보면 다음과 같다.

- GET: 데이터를 조회한다.
- POST: 등록한다.
- PUT: 리소스를 대체한다. 없으면 새로 만든다. 디렉터리와 유사하다.
- PATCH: 부분 변경한다.
- DELETE: 삭제한다.

이 외에도 `HEAD`, `OPTIONS`, `CONNECT`, `TRACE`등 다양하다. 자세한 설명은 문서를 참고하자.

앞서 다뤘듯 GET은 데이터를 조회할 때 많이 사용한다. HTTP 메시지 바디에 내용을 담을 수 있지만 지원하지 않는 서버도 있어서 담지 않는 것이 일반적이다. POST가 가장 많이 사용되는 건 등록이다.
하지만 POST는 등록뿐만 아니라 다른 방법으로도 사용된다. 데이터 처리등 애매하면 POST로 문제를 해결할 수 있다.

그렇다면 활용도가 높은 POST는 치트키일까. 아니다. 메서드는 각 용도가 있다. 가능하면 용도에 맞게 사용하고 어쩔 수 없는 상황에만 POST로 처리하자.

## HTTP 메서드 - PUT, PATCH, DELETE

PUT은 자원을 완전 대체, 덮어쓴다. 간단하게 파일 시스템과 `git commit --amend` 명령과 비슷하다.
PUT 메서드로 요청을 보낼 때 이전에 입력한 부분을 작성하지 않았다면 이전 입력은 사라진다. POST와 가장 큰 차이점은 클라이언트가 요청을 식별하는 여부다. POST는 클라이언트가 서버에서 어떤 경로를
수정, 추가하는지 지정하지 않다. 하지만 PUT은 명확하게 경로를 지정한다.

PATCH는 부분 변경으로 수정에 주로 사용한다. 예를 들어 글 제목만 수정하고 싶은 경우에 사용한다. 만약 서버에서 PATCH를 지원하지 않는다면 POST로 문제를 해결한다.

DELETE는 자원을 삭제할 때 사용한다.

## HTTP 메서드의 속성

HTTP 메서드 속성은 안전, 멱등, 캐시가능이 있다. 각 속성은 중요한 점이 있다.

- 안전: 자원의 변경
- 멱등: 똑같은 요청을 보내도 결과가 같은지
- 캐시가능: 캐시 가능한가(저장할 수 있는가)

### 안전(Safe Methods)

안전은 여러 번 호출해도 자원을 변경하지 않는 특징이 있다. 중요한 점은 '자원의 변경여부'다. 조회에 사용되는 GET은 여러 번 호출해도 자원이 변하지 않는다. 반면 GET 이외에 메서드[^5]는 자원을 변경하는데
사용한다. 따라서 안전하지 않다. 그렇다면 다음과 같은 질문을 할 수 있다. "조회를 많이 하면 로그가 쌓이고 부하가 걸리지 않나요?" 앞서 말했듯이 핵심은 자원이다.
서버에 영향은 갈 수 있지만 자원이 변하지 않으므로 상관 쓰지 않는다. 안전성의 핵심은 자원의 변경여부다.

### 멱등(Idempotent Methods)

"넌 맨날 그런 식이야."

멱등은 1번 호출과 100번 호출의 결과가 같음을 의미한다. 중요한 점은 '똑같은 요청'이다. 결제에도 사용되는 POST는 멱등하지 않다. 판매 중인 상품을 구매했다.
상품은 판매완료되어 더 이상 상품을 구매할 수없다. 같은 경로로 요청을 보내지만 결과가 다르다. 따라서 멱등하지 않다.

POST 외에 GET, PUT, PATCH, DELETE는 멱등하다. 조회, 수정, 삭제는 같은 경로로 요청을 보내도 결과가 같다. 그렇다면 다음과 같은 질문을 할 수 있다.

"중간에 게시글을 삭제하면 조회에도 영향이 가지 않나요?" 똑같은 요청을 강조한다.

똑같은 요청이란 중간에 외부요인을 신경 쓰지 않는다. 자주 사용하지 않는 단어인 멱등을 어떻게 사용할 수 있을까. 자동복구에 사용한다. 서버에 문제가 생겼을 때 멱등한 부분을 복구한다.

### 캐시가능(Cacheable Methods)

"자주 사용하는 이미지 보관 가능할까요?"

캐시가능은 '캐시', 저장 가능한지 여부를 의미한다. 응답결과를 저장할 수 있는 메서드는 `GET`, `HEAD` `POST`, `PATCH`가 있다. 하지만 `GET`, `HEAD`에 주로 사용한다.
`POST`, `PATCH`에 캐시가 가능하게 구현하기 어렵기 때문이다.

> 강의에서 제공하는 정보는 PATCH가 cacheable 하다고 설명한다. 하지만 현재 위키백과에서는 cacheable 하지 않다고 설명한다. MDN 문서를 확인한 결과, PATCH는 freshness와
> 같은 특정 조건이 포함된 경우에만 cacheable 하다고 이야기한다.

# 5. HTTP 메서드 활용

## 클라이언트에서 서버로 데이터 전송

클라이언트에서 서버로 데이터를 전송하는 방법은 크게 2가지다. 쿼리 파라미터(Query Parameter)로 데이터를 전송하거나 메시지 바디(Message Body)를 통해 데이터를 전송한다.
쿼리 파라미터는 `GET` 메서드로 사용한다. 예를 들어 이미지를 불러오거나, 검색 조건 필터링에 사용한다. 메시지 바디는 `POST`, `PUT`, `PATCH`에 사용한다. 회원가입, 주문 등
다양하게 사용할 수 있다. 이외에도 HTML `<form>` 태그로 데이터를 전송할 때, HTTP API 데이터 전송[^6]에도 사용한다.

## 참고 자료

- [김영한 '모든 개발자를 위한 HTTP 웹 기본 지식'](https://inf.run/8ZEU8)
- [김정환 '판교 퇴근길 밋업 with 인프런 #08 HTTP'](https://inf.run/R44jf)
- [IETF 'RFC 3986'](https://datatracker.ietf.org/doc/html/rfc3986)
- [위키백과 'HTTP'](https://ko.wikipedia.org/wiki/HTTP)

[^1]: 비연결성, 비신뢰성, 프로그램 구분
[^2]: 클라이언트/서버구조, 무상태 프로토콜(Stateless Protocol)과 비연결성, HTTP 메시지
[^3]: 티켓팅, 수강신청
[^4]: GET, POST, DELETE, PUT, PATCH 등
[^5]: POST, PUT, PATCH, DELETE
[^6]: 주로 서버와 서버끼리 통신한다.
