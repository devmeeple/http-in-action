# HTTP in Action

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

1. [인터넷네트워크](./1_인터넷_네트워크/README.md)
2. [URI와 웹 브라우저 요청 흐름](./2_URI와_웹_브라우저_요청_흐름/README.md)
3. [HTTP 기본](./3_HTTP_기본/README.md)
4. [HTTP 메서드](./)
5. [HTTP 메서드 활용](./5_HTTP_메서드_활용/README.md)

**<참고 자료>**

- [김영한 '모든 개발자를 위한 HTTP 웹 기본 지식'](https://inf.run/8ZEU8)

[^1]: 비연결성, 비신뢰성, 프로그램 구분
