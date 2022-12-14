# Web-Base

# HTTP란?
### HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
## 클라이언트 → 서버
### 요청(Requests)
## 클라이언트 ← 서버
### 응답(Responses)

## 클라이언트: 사용자 에이전트
### 사용자를 대신해 동작하는 모든 도구, 주로 브라우저에 의해 수행됨
### 브라우저는 항상 요청을 보내는 개체이므로, 결코 서버가 될 수 없음
#### 웹 페이지 표시를 위해, 브라우저는 페이지의 HTML 문서를 가져오기 위한 요청을 전송한 뒤, 파일을 구문 분석하여 실행해야 할 스크립트 그리고 페이지 내 포함된 하위 리소스들을 잘 표시하기 위한 레이아웃 정보(CSS)에 대응하는 추가적인 요청들을 가져옴

## 웹 서버
### 클라이언트에 의한 요청에 대한 문서를 제공

## 프록시
### 애플리케이션 계층에서 동작하는 것들
#### 웹 브라우저와 서버 사이에 수많은 컴퓨터와 머신이 HTTP 메시지를 이어 받고 전달하는 과정, HTTP 계층에서는 이들이 어떻게 동작하는지 보이지 않음.
### 프록시의 기능
#### 캐싱 (브라우저 캐시 등)
#### 필터링 (바이러스 백신 스캔, 유해 컨텐츠 차단)
#### 로드 밸런싱(여러 서버가 서로 다른 요청을 처리하도록 허용)
#### 인증(다양한 리소스에 대한 접근제어)
#### 로깅(이력 정보를 저장)

## HTTP의 기초 측면
### HTTP는 간단하다.
### HTTP는 확장이 가능하다.
#### HTTP 헤더는 HTTP를 확장하고 실험하기 쉽게 만듦. 클라이언트와 서버가 새로운 헤더의 시맨틱에 대해 합의만 한다면 언제든 새로운 기능 추가 가능
### HTTP는 상태가 없으나, 세션은 존재
#### HTTP는 상태를 저장하지 않는 Stateless. 동일 연결 상 연속 전달된 두 개의 요청 사이에는 연결고리가 없다. 다만 HTTP 쿠키는 상태가 있는 세션을 만들도록 허용
#### 헤더의 확장성을 사용해, 동일한 컨텍스트 또는 동일한 상태를 공유하고자 쿠키가 추가됨.

## HTTP와의 연결
#### 연결은 전송 계층의 영역, 다만 신뢰할 수 있거나 메시지 손실이 없는 연결을 요구
#### 가장 일반적인 두 개의 전송 프로토콜 중 TCP는 신뢰 가능, UDP는 그렇지 않음 때문에 TCP 표준에 의존

## HTTP로 제어할 수 있는 것
### 캐시
#### 문서가 캐시되는 방식을 제어할 수 있음. 서버는 캐시 대상과 기간을 프록시와 클라이언트에 지시하고 클라이언트는 저장된 문서를 무시하라고 중간 캐시 프록시에게 지시 가능
### origin
#### 제약사항 완화를 위해 스누핑과 다른 프라이버시 침해 예방을 위해 엄격한 분리를 강제
### 프록시와 터널링
#### 서버 혹은 클라이언트 또는 둘 모두 인트라넷에 종종 위치하며 실제 주소를 숨기기도함
#### HTTP 요청은 프록시를 통해 나가지만, 모든 프록시가 HTTP인것은 아님.

## HTTP의 흐름
### (1) TCP 연결 열기
#### TCP 연결은 요청을 보내거나 응답을 받는데 사용. 클라이언트는 새로운 연결을 열거나, 기존 연결을 재사용하거나 서버에 대한 여러 TCP 연결을 열 수 있음
### (2) HTTP 메시지 전송
#### 간단한 메시지가 프레임 속으로 캡슐화 되어 가시성은 없으나 원칙은 동일
### (3) 서버에 의해 전송된 응답을 읽어들이기
### (4) 연결을 닫거나 다른 요청들을 위해 재사용

## 요청(Requests)
### HTTP 메서드
#### 클라이언트가 수행하고자 하는 동작을 정의한 GET, POST 같은 동사나 OPTIONS, HEAD와 같은 명사
#### 클라이언트가 리소르를 가져오거나(GET 사용) HTML 폼의 데이터를 전송(POST 사용)하지만, 다른 경우엔 다른 동작 요구
#### 예를 들면 프로토콜 같은 리소스 경로, 도메인, 또는 TCP 포트인 요소들을 제거한 리소스의 URL

## 응답(Responses)
### HTTP 프로토콜 버전
### 상태 코드
### 상태 메시지
### 요청 헤더와 비슷한 HTTP 헤더들
### 리소스가 포함된 본문

## HTTP 기반 API
#### 일반적인 API는 user agent와 서버간 데이터를 교환하는데 사용하는 XMLHttpRequest API

## Requests Message
#### Request Header
#### GET /1.html HTTP/1.1                    => 요청행
#### Host: localhost:8080                       => 네트워크의 컴퓨터 식별하는 이름
#### ...
#### ...
#### User-Agent : ...                        => 유저 컴퓨터, 웹브라우저 정보
#### ...
#### ...
#### Accept-Encoding : gzip, deflate, br     => 데이터 양이 많으면 압축해서 전송하는데, 어떤 압축방식을 지원하는지 설명
#### ...
#### ...
#### If-Modified-Since: Tue, ...             => 마지막으로 페이지를 다운받은게 언제인지 확인하여 다시 다운받을지 결정
#### blank line>                                    => 블랭크로 헤더와 바디 구분
#### Request Message Body

## HTTP Response Format
### 1xx codes : 정보를 주기 위한 응답
### 2xx codes : 통신 성공
### 3xx codes : 리다이렉션
### 4xx codes : 클라이언트 에러
### 5xx codes : 서버 에러

# Domain
## DNS 서버의 원리
### 도메인 네임 시스템 서버
#### IP 주소를 기억하여 가시성이 좋은 문자열을 변환했을 때 IP를 반환해 웹 접속이 가능하게 함

### blog.example.com
#### blog는 sub, example은 second-level, com은 top-level로 구분
#### 상위가 하위를 알고 있어야 함
#### sub <- second-level <- top-level <- root

## 질의
#### root-name-server에게 먼저 물어봄(com이 전담하는 ip 주소들을 알려줌)
#### top-level 네임 서버를 전담하는 ip를 알려줌
#### second-level 도 마찬가지로 sub로 이동
#### sub에서 원하는 도메인에 대한 ip 주소를 알 수 있게 됨

# nslookup
#### 도메인 주소(example.com)를 던지면
#### 도메인에 대한 IP를 반환해주는 명령어
## nslookup -type=ns (도메인 주소)
#### 네임서버를 반환
## nslookup example.com nameserver
#### DNS 주소 기반 IP를 반환

# DNS record & CNAME
## A 레코드
#### A 레코드의 장점은 한번의 요청으로 찾아갈 서버의 IP 주소를 한번에 알 수 있다는 점이다. 
#### 반면 단점은 IP 주소가 자주 바뀌는 환경에서는 조금 번거로울 수 있다는 점이다. 
#### 예를 들어, 172.17.0.2 서버에서 plusblog.co.kr, dev.plusblog.co.kr, travel.plusblog.co.kr 등 
#### 여러개의 서브 도메인들을 처리하고 있다고하자. 각 서브 도메인들을 A 레코드로만 매핑시켰다면, 172.17.0.2라는 
#### IP 주소가 172.17.0.3이라는 주소로 변경되었다면 모든 A 레코드를 찾아서 변경해야 한다. 

## CNAME 레코드
#### CNAME 레코드의 장점은 IP 주소가 자주 변경되는 환경에서 유연하게 대응할 수 있다는 점이다. 
#### 예를 들어, dev.plusblog.co.kr, travel.plusblog.co.kr 도메인 정보를 plusblog.co.kr이라는 주소로 매핑시키는 CNAME 레코드로 저장하고, 
#### plusblog.co.kr이라는 주소를 172.17.0.2 라는 IP 주소로 매핑시키는 A 레코드로 저장해 놨다면, 
#### 서버의 IP 주소가 바뀌었을 때 plusblog.co.kr의 A 레코드 정보만 변경시키면 된다.