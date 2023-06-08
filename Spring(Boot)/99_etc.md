## 우선 정리만 해두는 공간 

### Spring 웹 계층
- Web Layer
  - 흔히 사용하는 컨트롤러(@Controller)와 JSP/Freemarker 등의 뷰 템플릿 영역

- Service Layer
  - @Service에 사용되는 서비스 영역
  - Transactional이 사용되어야 하는 영역
- Repository Layer
  - Database와 같이 데이터 저장소에 접근하는 영역 (= DAO 영역)

- Dtos
  - DTO(Data Transfer Object)들의 영역을 말함
  
- Domain Model
 - 도메인이라 불리는 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 잇고 공유할 수 있도록 단순화 시킨 것

- @MappedSuperclass
  - JPA Entity 클래스들이 BaaseTimeEntity를 상속할 경우 필드들도 칼럼으로 인식하도록함.

- @EntityListeners(AuditingEntityListener.clas)
  - BaseTimeEntity 클래스에 Auditing 기능을 포함시킴.



### OAuth(Open Authorization)
- 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준이다.
- 페이스북, 구글, 카카오 등에서 제공하는 인증 서비스를 사용하여 인증을 수행

#### Google OAuth
- [api-client-library](https://developers.google.com/api-client-library/java/google-oauth-java-client/oauth2?hl=ko)

<img src="img/google_oauth.png" alt="대체_텍스트" width="300" height="200">

