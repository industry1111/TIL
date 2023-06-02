# JPA 소개
****
## 1. SQL을 직접 다룰 때 발생하는 문제점

### 1.1 반복, 지루한 코드

* CRUD 작업의 반복
    - 애플리케이션에서 데이터의 생성(Create), 조회(Read), 수정(Update), 삭제(Delete) 작업은 반복적으로 수행된다.

```java
public class Member {
    
    private Long id;
    private String name;
    ...
    
}
```
``` java
// 1.회원 조회용 SQL 작성
String sql = "SELECT * FROM MEMBER WHERE NAME = ?";

// 2. SQL 실행 코드 작성
PreparedStatement preparedStatement = connection.prepareStatement(sql);
preparedStatement.setString(1, name);
ResultSet resultSet = preparedStatement.executeQuery();

// 3. SQL 실행 결과를 객체로 변환
Member member = new Member();
member.setId(resultSet.getLong("ID"));
member.setName(resultSet.getString("NAME"));
...
```
등록, 수정, 삭제도  SQL을 작성하고 JDBC API를 사용하는 비슷한 일을 밥복해야 할 것이다

### 1.2 SQL에 의존적인 개발

* 갑자기 회원정보에 연락처도 함께 저장해달라는 요구사항이 추가되었다고 한다면?
    * Member 객체에 연락처 필드를 추가해야하며, 기존에 작성한 **모든 SQL과 JDBC API 코드를 수정해야 한다.**
    * SQL에 의존적인 개발을 피하기 어렵다.

```java
public class Member {
        
        private Long id;
        private String name;
        private String phoneNumber; // 추가된 필드
        ...
        
}
```

### 2. 패러다임의 불일 

### 2.1 상속
* 객체는 상속이라는 기능을 가지고 있지만 테이블은 상속기능이 없다.
* 슈퍼타입과 서브타입 관계를 이용하여 객체 상속과 가장 유사하게 테이블 설계를 할 수 있다.
  * DTYPE 컬럼을 이용

![01_object inheritance relationship.png](img%2F01_object%20inheritance%20relationship.png)



### 2.2 연관관계
* 객체는 참조를 사용하여 연관관계를 가지고 있지만 테이블은 외래 키를 사용하여 연관관계를 가지고 있다.
* 객체의 참조와 테이블의 외래 키를 매핑하는 것은 불가능하다.
* 객체를 테이블에 맞추어 모델링하면, 협력 관계를 만들 수 없다.
  * 객체의 참조와 테이블의 외래 키를 매핑할 수 없기 때문에 객체의 참조를 테이블에 맞추어 모델링하면 협력 관계를 만들 수 없다.
* 