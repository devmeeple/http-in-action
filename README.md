# HTTP in Action

# 모든 개발자를 위한 HTTP 웹 기본 지식

- HTTP의 전체 흐름 이해
- 실무에 꼭 필요한 핵심 내용

최근 스터디에서 '멱등성'을 주제로 대화를 나눴다. 자주 사용하는 HTTP 프로토콜이지만 나만의 정의가 없었다. 만약 정의가 되어있었다면 기준과 개념에 대해 대화를 나눌 수 있지 않았을까?
이렇게 웹 개발자가 되고 싶다면 HTTP는 한번쯤 고민하는 주제다. 웹 프레임워크는 HTTP위에서 동작한다. 따라서 사용자가 'HTTP를 당연히 이해하고 있다'라고 가정한다.
나만의 기준이 없다면 "API를 어떻게 설계할 것인가?", "상태코드는 어떻게 설정할 것인가?" 이런 고민을 나눌 수 없다. 언젠가 마주하고 정의해야 하는 주제라면 지금이 적기다.
지식 공유자는 본인의 기준을 제안한다. 네트워크부터 시작해서 실무에서 활용되는 HTTP 개념까지 함께 알아보자.

## 1. 인터넷 네트워크

- 인터넷 통신
- IP(Internet Protocol)
- TCP, UDP
- PORT
- DNS

"HTTP를 배우고 싶어요. 그런데 왜 인터넷 네트워크를 알아야 하나요?"

HTTP와 웹은 인터넷 네트워크 위에서 동작한다. 클라이언트와 서버가 통신할 때 인터넷 네트워크를 사용한다. 그렇다. 우리는 지금 이 순간에도 인터넷을 사용하고 있다.
그렇다면 어떤 규칙으로 안전하게 통신할 수 있는 걸까?

1. [인터넷네트워크](./1_인터넷_네트워크/README.md)
2. [URI와 웹 브라우저 요청 흐름](./2_URI와_웹_브라우저_요청_흐름/README.md)
3. [HTTP 기본](./3_HTTP_기본/README.md)
4. [HTTP 메서드](./)
5. [HTTP 메서드 활용](./5_HTTP_메서드_활용/README.md)

**<참고 자료>**

- [김영한 '모든 개발자를 위한 HTTP 웹 기본 지식'](https://inf.run/8ZEU8)
