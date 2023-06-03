# application.properties
- 스프링 부트에서는 application.properties 파일을 통해 설정을 관리한다.
- 이 파일은 src/main/resources 디렉토리에 위치한다.
- application.properties 파일에 설정을 추가하면 스프링 부트가 자동으로 설정을 읽어들인다.


### spring.jpa.show-sql=true
- JPA가 생성하는 SQL을 출력한다.

### spring.jpa.hibernate.ddl-auto=none
- create : 기존 테이블 삭제후 다시 생성 (DROP + CREATE)
- create-drop : create와 같으나 종료시점에 테이블 DROP
- update : 변경분만 반영
- validate : 엔티티와 테이블이 정상 매핑되었는지만 확인
- none : 사용하지 않음

### spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
- JPA가 사용할 SQL dialect를 설정한다.
- MySQL5Dialect : MySQL 5에 맞게 SQL을 생성한다.
- Oracle10gDialect : Oracle 10g에 맞게 SQL을 생성한다.
- Hibernate는 특정 데이터베이스에 종속적이지 않은 SQL을 생성한다.

