# JPA Annotation

### `@Entity`

### `@Id`
- PK 매핑

### `@GeneratedValue`
- PK의 생성 방법을 매핑하는 애노테이션
  - strategy = GenerationType.AUTO : 방언에 따라 자동 지정, 기본
  - IDENTITY : 데이터베이스에 위임
  - SEQUENCE : 데이터베이스 시퀀스 오브젝트 사용 , ORACLE @SequenceGenerator 필요
  - TABLE :

### `@Column`
- 컬럼매핑
- name = ""(default): 매핑할 테이블의 컬럼이름(객체의 필드이름),
- insertable/updatable : 등록 변경 가능여부 (TRUE) - DB에 컬럼 반영여부
- nullable(DDL) : null 값 허용 여부(TRUE)  false 설정 시 NOT NULL 제약조건 생성
- unique(DDL) : @Table(uniqueConstrains와 같음 )
- columnDefinition(DDL) : 데이터베이스 컬럼 정보를 직접 줄 수 있다.
- length(DDL) :  문자길이 제약 조건 String  타입에만 서용 (255)
- precision/scale : BigDecimal/BigInteger 타입에서 사용 precision 은 소수점 포함 전체자릿수, scale 은 소수점 자릿수
       
### `@Temporal`
- 날짜타입 매핑
- LocalDate, LocalDateTime 사용할 때는 생략 가능

### `@Enumerated`
- enum 타입 매핑
### `@Lob`
- BLOB,CLOB 매핑
### `@Transient` 
- 특정 필드를 컬럼에 매핑하지 않음 (매핑 무시)
