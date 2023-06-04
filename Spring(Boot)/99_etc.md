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


