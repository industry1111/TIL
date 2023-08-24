# HTTP 상태 코드란
클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx (Informational): 요청이 수신되어 처리중, 거의 사용하지 않음
- 2xx (Successful): 요청 정상 처리
- 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요
- 4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함

클라인언트가 인식할 수 없는 상태코드를 서버가 반환하면 클라이언트는 상위 상태코드로 해석해서 처리
- 299(???) -> 2XX
- 451(???) -> 4XX
- 599(???) -> 5XX

## 2XX (Successful)
- 200 OK
    - 요청이 성공적으로 수행
- 201 Created
    - 요청 성공해서 새로운 리소스가 생성됨, 응답 헤더 부분에 Location 생성
- 202 Accepted
    - 요청이 접수되었으나 처리가 완료되지 않았음, 배치 처리 같은 곳에서 사용
- 204 NoContent
    - 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음

## 3XX (Redirection)

요청을 완료하기 위해 유저 에이전트의 추가 조치 필요

### 영구 리다이렉션
- 301 Moved permanently
    - 영구 리다이렉션으로 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 308 Permanent Redirect
    - 301과 기능은 같음
    - 리다이렉트시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)


### 일시적인 리다이렉션
- 302 Found
    - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될수 있음(MAY)
- 303 See Other
    - 302와 기능은 같음
    - 리다이렉트시 요청 메서드가 GET으로 변경
- 307 Temporary Redirect
    - 302와 기능은 같음
    - 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)

#### 예시
POST로 주문후에 웹부라우저를 새로고침하면 중복 주문이 될 수있다.
해당 문제를 해결하기 위해 PRG : **Post/Redirect/Get**을 사용

![](https://velog.velcdn.com/images/industry1111/post/17d8911b-06b3-47ef-9104-e2c1623ef9a9/image.png) PRG 적용전 |![](https://velog.velcdn.com/images/industry1111/post/c353530e-eeaa-42e8-9d23-f71036f894df/image.png) PRG 적용 후
---|---|

### 기타 리다이렉션
- 300 Multiple Choices
    - 사용하지 않음
- 304 Not Modified
    - 캐시를 목적으로 사용
    - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬PC에 저장된 캐시를 재사용한다. ( 캐시로 리다이렉트 한다.)
    - 응답에 메시지 바디를 포함하면 안된다(로컬 캐시를사용해야 하므로)

> **Redirection**
웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)<br/>
**종류**
- 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
    - 예) /event -> /new-event
    - 예) /members -> /users
- 일시 리다이렉션 - 일시적인 변경
    - 주문 완료 후 주문 내역 화면으로 이동
    - PRG: Post/Redirect/Get
- 특수 리다이렉션
    - 결과 대신 캐시를 사용


## 4XX (Client Error)

클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음, 오류의 원인이 클라이언트에 있음

- 401 Bad Request
    - 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
    - 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때
- 401 Unauthorized
    - 클라이언트가 해당 리소스에 대한 인증이 필요함
- 403 Forbidden
    - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
    - 예) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우
- 404 Not Found
    - 요청 리소스를 찾을 수 없음


> **인증(Authentication) 과 인가(Authorization)**
인증 : 본인이 누구인지 확인
인가 : 권한부여(ADMIN 권한 처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)

## 5XX (Server Error)

서버 문제로 오류 발생, 서버에 문젝가 있기 떄문에 재시도하면 성공할 수도 있음

- 500 Internal Server Error
    - 서버 내부 문제로 오류 발생
    - 애매하면 500 오류

- 503 Service Unavailable
    - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
    - Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음


출처

[링크](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)