# [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#)

## IP (인터넷 프로토콜)

- 인터넷의 고유 주소인 아이피를 각자 가지고 있다.
- 아이피끼리 통신일 때에는 패킷을 만들어서 통신한다.
- 패킷에는 출발IP, 도착IP 를 가지고 있고, 전달할 내용도 포함한다.
- 특징
  - 비연결성
    - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
  - 비신뢰성
    - 중간에 패킷이 사라질 수 있다.
    - 패킷이 보낸 순서대로 전달이 되지 않을 수 있다.
  - 프로그램 구분
    - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

### 패킷

- 패키지 + 버킷 합성어

## TCP / UDP

### TCP

인터넷 프로토콜 스택의 4계층
- 애플리케이션 계층 - HTTP, FTP
- 전송계층 - TCP, UDP
- 인터넷 계층 - IP
- 네트워크 인터페이스 계층

![프로토콜계층](./protocol.png)

#### TCP 특징

> 전송 제어 프로토콜(Transmission Control Protocol)

- 연결지향 - TCP 3 way handshake (가상연결)
  1. SYN (클라이언트)
  2. SYN + ACK (서버)
  3. ACK + 데이터 (클라이언트)
   - SYN: 접속 요청
   - ACK: 요청 수락
     - 요청을 보내고, 연결 확인을 받으면 그 후에 데이터를 전송한다. (3번 통신이 이루어짐)
- 데이터 전달 보증
  - 데이터를 받으면 제대로 받았다고 응답을 보낸다.
- 순서 보장
  - 1, 3, 2 순으로 데이터가 잘못 전달되었을 경우 2번부터 다시 보내라고 서버가 클라이언트에게 요청한다.
- 신뢰할 수 있는 프로토콜
- 현재 대부분 TCP 사용  

#### UDP 특징

> 사용자 데이터그램 프로토콜(User Datagram Protocol)

- 하얀 도화지와 같다. (기능이 거의 없음)
- 연결지향 X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠르다.
- 정리
  - IP 와 거의 같다.
    - PORT 추가
    - 체크섬 추가
  - 애플리케이션에서 추가 작업 필요

### PORT

> 항구

- 포트로 인해 한 아이피 주소 내에서 여러 애플리케이션을 실행하여 응답 / 요청이 가능해진다.

#### TCP/IP 패킷 정보

- 출발지 IP / PORT
- 목적지 IP / PORT
- 전송 데이터

#### IP / PORT

- 예시
  - IP: 아파트
  - PORT: 호수

#### PORT

- 0 ~ 65535: 할당 가능
- 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋다.
  - FTP - 20, 21
  - TELNET - 23
  - HTTP - 80
  - HTTPS - 443

### DNS

- 아이피는 기본적으로 외우기 어렵다. (100.234.50.31..?)
- 아이피는 변경이 될 수 있다.
- DNS 서버에서 도메인 주소를 구매해서 사용할 수 있다.
  - ex) google.com
  - DNS 서버에 도메인명을 찾아서 IP 주소를 응답받아 해당 IP 로 접속할 수 있게 된다.


## URI 와 웹 브라우저 요청 흐릅

### URI (Uniform Resource Identifier)

> 리소스 식별자

- URI는 URL, URN 을 포함하는 개념이다.
- 보통 URN 은 보기도 어렵고, 이해하기 쉽지 않기 때문에 URL 을 거의 사용한다.
![uri](uri.png)
![url](urlurn.png)

### URI 단어 뜻

- Uniform: 리소스 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것 (제한 없음)
- Identifier: 다른 항목과 구분하는데 필요한 정보
  
### URL, URN 단어 뜻

- URL: Uniform Resource Locator
  - Locator: 리소스가 있는 위치를 지정
- URN: Uniform Resource Name
  - Name: 리소스에 이름을 부여

추가 설명
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- urn:isb:8960777331 (어떤 책의 isbn URN)
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않는다.

### URL 알아보기

- scheme://[userinfo@]host[:prot][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko

#### scheme

- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속된 규칙, 규약
  - 예) http, https, ftp 등

#### USERINFO

- URL 에 사용자 정보를 포함해서 인증
- 거의 사용하지 않는다.

#### HOST
- 호스트명
- 도메인명 또는 IP 주소를 직접 사용 가능

#### PORT

- 접속 포트
- http 는 80포트, https 는 443 포트를 주로 사용, 해당 포트는 생략이 가능하다.

#### PATH

- 리소스 경로, 계층적 구조
- 예시
  - /home/file1.jpg
  - members

#### QUERY

- key=value 형태
- ? 로 시작
- &로 이어서 여러 개를 붙일 수 있음.
  - keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불린다.

#### FRAGMENT
- html 내부 북마크 등에서 사용된다.
- 서버에 전송하는 정보가 아니다.

### 웹 브라우저 요청 흐름

> https://www.google.com:443/search?q=hello&hl=ko

1. DNS 에 조회하여 IP 주소를 찾는다.
2. HTTP 요청 메세지 생성
> GET /search?q=hello&hl=ko HTTP/1.1  
Host: www.google.com
3. SOCKET 라이브러리를 통해 전달.
   - A: TCP/IP 연결 (IP, PORT)
   - B: 데이터 전달
4. TCP/IP 패킷 생성, HTTP 메시지 포함
5. 데이터를 서버에 전달.
6. TCP/IP 패킷을 버리고, HTTP 메시지를 열어서 확인.
7. HTTP 응답 메시지 생성
8. 응답 메시지 전달
9. 브라우저에서 해당 응답 메시지를 확인 후 렌더링

## 모든 것이 HTTP

### HTTP (HyperText Transfer Protocol)

> HTTP 메시지에 모든 것을 전송

- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML (API)
- 거의 모든 형태의 데이터 전송 가능
- 서버 간 데이터를 주고 받을 때에도 대부분 HTTP 사용
- 현재 기준으로 HTTP 시대

#### HTTP 역사

- HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
- HTTP/1.0 1996년: 메서드, 헤더 추가
- `HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전`
  - RFC2068 (1997) -> RFC2616 (1999) -> RFC7230 ~ 7235 (2014)
- HTTP/2 2015년: 성능개선
- HTTP/3 진행중: TCP 대신 UDP 사용, 성능개선

#### 기반 프로토콜

- TCP: HTTP/1.1, HTTP/2
- UDP: HTTP/3
- 현재 주로 HTTP/1.1 사용
  - HTTP/2, HTTP/3 도 증가하는 추세

### HTTP 특징

- 클라이언트 서버 구조
- 무상태 프로토콜 (스테이스리스), 비연결성
- HTTP 메시지
- 단순함, 확장 가능

#### 클라이언트 서버 구조

- Request / Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

#### Stateful, Stateless

무상태 프로토콜 스테이스리스(Stateless)

- 서버가 클라이언트의 상태를 보존하지 않는다.
- 장점: 서버 확장성이 높다. (스케일 아웃)
- 단점: 클라이언트가 추가 데이터 전송
  
Stateful, Stateless 차이
- Stateful (상태 유지): 중간에 다른 서버로 변경되면 안된다.
  - 중간에 다른 서버로 변경되면 상태 정보를 다른 서버에 미리 알려줘야 된다.
- Stateful (무상태): 중간에 다른 서버로 변경이 되어도 된다.
  - 접속이 갑자기 증가하면 여러 서버를 새로 투입하여도 문제가 되지 않는다.
- 무상태는 응답 서버를 쉽게 변경할 수 있다. -> 무한한 서버 증설이 가능하다.

무상태 실무 한계

- 로그인이 필요없는 단순한 서비스 소개 화면은 무상태로 설계해도 장애 발생 가능성이 적다.
- 로그인이 필요한 서비스 경우 사용자의 로그인 정보를 서버에서 유지를 해주어야 하는 문제점이 있다.
  - 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태를 유지한다.
  - 상태 유지는 최소한만 사용한다.

#### 비 연결성(connectionless)

특징

- 요청 / 응답 후에 연결을 끊어버린다.
- 계속 연결되어 있지 않는 상태이기 때문에 서버 자원을 매우 효율적으로 사용할 수 있다.

한계와 극복
- TCP/IP 연결을 새로 맺어야 한다. - 3way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTTP 뿐만 아니라 자바스크립트, css, 추가 이미지 등  
  수 많은 자원이 함께 다운로드 된다.
- 지금은 HTTP 지속 연결(Persistent Connections) 로 문제 해결
- HTTP/2, HTTP3 에서 더 많은 최적화

#### HTTP 메시지

![HTTP메시지](http_message.png)

`시작라인`

- 요청 메시지는 request-line
  - method SP(공백) request-target SP HTTP-version CRLF(엔터)
- 응답 메시지는 status-line
  - HTTP-version SP status-code SP reason-phrase CRLF

  
- method: GET, POST, PUT, DELETE
- request-target: 예시) /search?q=hello&hl=ko
- HTTP-version: HTTP/1.1
- status-code: 요청 성공, 실패를 나타냄.
  - 200 (성공), 400 (클라이언트 요청 오류), 500 (서버 내부 오류)
- reason-phrase: 사람이 이해할 수 있는 짧은 상태 코드 설명 글

`헤더`

- header-field = filed-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)

- 요청 메시지
  - `Host: www.google.com`
- 응답 메시지
  - Context-Type: text/html;charset=UTF-8
  - Context-Length: 3423
- 필드네임과 ":"은 붙여야 한다.
  
  
- HTTP 전송에 필요한 모든 부가 정보를 표시한다.
  - 메시지 바디의 내용, 메시지 바디의 크기, 압축 여부, 인증 정보, 요청 클라이언트(브라우저) 정보, 캐시 관리정보 ...
- 표준 헤더가 너무 많다.
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
- 필요 시 임의의 헤더 정보 추가를 할 수 있다.
  - 하지만, 이렇게 되면 약속된 클라이언트와만 통신이 가능하다.

`HTTP 메시지 바디`

- 실제 전송할 데이터
  - HTML 문서, 이미지, 영상, JSON 등등 byte 로 표현할 수 있는 모든 데이터 전송이 가능

## HTTP 메서드

### 리소스와 행위를 분리하자.

> 가장 주요한 것은 리소스를 식별하는 것

- `URI` 는 `리소스`만 식별하자!
- `리소스`와 해당 리소스를 대상으로 하는 `행위`를 분리
  - 리소스: 회원
  - 행위: 조회, 등록, 수정, 삭제
- 리소스는 명사, 행위는 동사
  - 예시) 회원을 조회하라.