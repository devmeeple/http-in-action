# 2. URI와 웹 브라우저 요청 흐름
웹 브라우저에 요청하면 HTTP 메시지가 어떤식으로 만들어지며 어떻게 동작하게 되는지 흐름을 알아보자.

## URI
> URI(Uniform Resource Identifier)는 리소스를  식별하는 통합된 방법을 의미한다.

### URI, URL, URN
- URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다.
	- URI가 가장 상위 개념이고 하위 개념에 URL과 URN이 포함된다.
	- 로케이터(locator)는 위치를 의미한다. 따라서 URL은 리소스의 위치다.
	- URN은 리소스의 이름이다.
	- 우리가 흔히 적는 방식은 URL이다. `devemeeple.tistory.com/post/33`
	- URN은 이름을 부여하는 것인데 이런 것이 있다 정도만 인지해도 충분하다.
- 위치는 변경가능하지만 이름은 변경되지 않는다.
- URN만으로 리소스를 식별하는 방법은 보편화되지 않았다.
- 따라서 URI를 URL과 같은 의미로 이야기 한다.

### URL
> scheme://[userinfo@]host[:port][/path][?query][#fragment]
> https://www.google.com:443/search?q=hello&hl=ko

- scheme
	- 주로 프로토콜 사용
	- 프로토콜은 자원을 접근하는 방법들을 담은 규칙 세트이다.
		- 예) http, https, ftp 등
- userinfo
	- 거의 사용하지 않음
- host
	- 호스트명으로 지칭한다.
	- 도메인 명, IP 주소를 입력한다.
- port
	- 접속포트를 의미한다.
	- 생략가능하다. (특정 서버에 따로 접근을 해야하는 경우 작성한다.)
	- 일반적으로 생략한다. 생략시 http는 80, https는 443을 의미한다.
- path
	- 리소스의 경로를 의미한다.
	- 계층적 구조를 가진다.
	- 예)
		- /members
		- /members/3
- query
	- query parameter, query string으로 부른다.
	- key = value 형태를 가진다.
	- ?로 시작하여 &로 연결한다. 예) `?search?q=hello&hl=ko`
- fragment
	- html 내부 북마크에 사용된다.
	- 서버에 전송하는 정보가 아니다.
## 정리: 웹 브라우저 요청 흐름
> https://www.google.com/search?q=hello&hl=ko

다음과 같은 요청을 보내면 DNS서버에서 다음과 같이 동작한다.
1. 도메인서버에서 `google.com` 에 해당하는 IP를 얻는다. (포트 생략시 다음 예제에서는 443)
2. HTTP 요청 메시지를 생성한다. (다음 예시는 간략화되어있다. 실제로는 부가정보도 있다.)

	```text
	GET/ search?q=hello&hl=ko HTTP/1.1
	Host: www.google.com
	```

3. 메시지가 전송된다.
	- 생성된 메시지는 SOCKET 라이브러리를 통해 전달되고 패킷 생성 과정을 거친다.
4. 노드를 거쳐 도착한 메시지를 확인한다.
	- 패킷(포장)을 버리고 메시지를 분석한다. (hello와 관련된 한국어 데이터를 요청하는 것을 이해한다.)
5. 응답메시지를 전송한다.
	```text
	HTTP/1.1 200 OK
	Content-Type: text/html;charset=UTF-8
	Content-Length: 3423
	```
6. 응답메시지가 도착하면 다시 분석을 거쳐 결과를 출력한다.
