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

### spring.h2.console.enabled=true
- 스프링 부트 애플리케이션이 실행될 때 H2 데이터베이스의 웹 콘솔에 접근가능하다.
- 
### spring.datasource.url=jdbc:h2:mem:testdb
- 데이터베이스를 사용하기 위한 데이터베이스 URL 설정한다.
- h2데이터베이스 경우
  - jdbc:h2:mem:testdb
    -In-memory DB다. DB를 연결하고 닫으면 해당 DB는 사라진다.
  - jdbc:h2:~/dbname
    - Local DB다. 직접 로컬에서 홈디렉토리로 가보면 db들이 생성되있는 것을 확인할 수 있다.
    해당 DB는 저장되며 계속 사용할 수 있다.