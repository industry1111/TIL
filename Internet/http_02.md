# HTTP 메시지 구조
HTTP는 요청 메시지와 응답 메시지 구조가 다르다.


<img width="60%" src="https://velog.velcdn.com/images/industry1111/post/0de27cf0-5c6a-4cae-b53a-a5ba7a7447bc/image.png">

<img width="60%" src = "https://velog.velcdn.com/images/industry1111/post/b2a80f13-7eee-4f68-97bf-4e153a22445a/image.png">


HTTP 메시지는 start-line , header, message body로 이루어져 있다.


## HTTP start-line

시작라인은 요청/응답에 따라 request-line/status-line으로 불린다.

### reqeust-line
request-line = method SP(공백) request-target SP(공백) HTTP-version CRLF(엔터) 로 구성되어 있다.

<img width="60%" src="https://velog.velcdn.com/images/industry1111/post/92da2a01-0048-4c91-b8c6-5e06cb752143/image.png">

- **HTTP method** : GET, POST, PUT/PATCH, DELETE 등 서버가 수행해야 할 동작 지정
- **요청대상** : "/"로 시작하는 절대경로 ? 쿼리스트링
- **HTTP Version**

### status-line
status-line = HTTP-version SP status-code SP reason-phrase CRLF 로 구성되어 있다.

<img width="60%" src="https://velog.velcdn.com/images/industry1111/post/a15d06ec-ed09-452b-894b-e53311df64e7/image.png">

- **HTTP Version**
- **HTTP 상태 코드** : 요청 성공, 실패를 나타냄(1XX,2XX,3XX,4XX,5XX)
- **이유 문구** : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

## HTTP Header

header-field = field-name":" OWS field-value OWS (OWS : 띄어쓰기 허용)로 이루어져 있고, field-name의 경우 대소문자 구분이 없다.

- HTTP 전송에 필요한 모든 부가 정보가 담겨져 있다.(메시지 바디 크기, 압축,인증, 클라이언트(브라우저)정보 등
- 필요시 임의의 헤더 추가 가능

## HTTP Message Body

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON, 등등 byte로 표현할 수 있는 모든 데이터 전송 가능


# HTTP Method

API URI 설계시 가장 중요한 것은`리소스`를 식별하는 것이다.

- 회원 목록 조회
- 회원 조회
- 회원 등록
- 회원 수정
- 회원 삭제

회원을 등록하고 수정하고 조회하는게 리소스가 아니라 `회원이라는 개념 자체가 바로 리소스`이다.
URI는 리소스만 식별하고 행위는 **HTTP Method**를 이용하여 구분해야한다.

- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제

기타
- HEAD : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS : 대상 리소스에 대한 통신 가능 옵션을 설명
- CONNECT : 대상 리소스로 식별되는 서버에 대한 터널을 설정
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

## GET
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는곳이 많아서 권장하지 않음

## POST
- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
    - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

## PUT
- 리소스를 대체
    - 리소스가 있으면 대체, 없으면 생성
- 클라이언특가 리소스를 식별
    - 클라이언트가 리소스 위치를 알고 URI 지정 (PUT/members/100)
    - POST와 차이점

## PATCH
- 리소스 부분 변경

## DELETE
- 리소스 제거


## HTTP 메서드 속성
- 안전(Safe Methods)
  호출해도 리소스를 변경하지 않는다.
- 멱등(Idempotent Methods)
  한 번 호출 하든 몇 번을 호출하든 결과가 똑같다.
- 캐시가능(Cacheable Methods)
  응답 결과를 리소스를 캐시해서 사용해도 되는지 여부

<img width="80%" src="https://velog.velcdn.com/images/industry1111/post/e36be76e-cd17-4614-9da5-27065321cd23/image.png">


출처

[링크](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)