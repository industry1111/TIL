# JPA 사용시 고려할 점
- JPA를 사용하면 엔티티 객체를 중심으로 개발
- 검색을 할 때도 `테이블이 아닌 엔티티 객체를 대상으로 검색`
- 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요

## JPQL (Java Persistence Query Language)
- SQL과 유사한 문법을 가지고 있지만, 객체와 속성을 기반으로 쿼리를 작성
- 객체 그래프 탐색과 같은 객체 지향적인 기능을 활용
- JPQL을 사용하여 JPA를 통해 데이터베이스에 쿼리를 수행하면, 데이터베이스 액세스 작업을 더 간편하게 수행할 수 있고, 객체 지향적인 개발을 지향
- 객체 지향 SQL
```java
String sql = "select m from Member m where m.name like '%industry'";

List<Member> resultList = em.createQuery(sql, Member.class).getResultList();
```
 실행된 SQL
```sql
SELECT m.id,
       m.email,
       m.name
  FROM MEMBER m
 WHERE 1=1
   AND m.name like '%hello'
```

### 결과 조회
```java

```
