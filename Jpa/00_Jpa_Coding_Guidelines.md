### setter 메소드를 만들지 않는다.
- setter 메소드를 만들게 되면 해당 클래스의 인스턴스 값들이 언제 어디서 변할지 모른다.
- 대신, 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가한다.

### builder 클래스를 이용
- 아래와 같은 생성자에서 a와 b의 위치를 변경해도 코드를 실행하기 전까지는 문제를 찾을 수 없다
```java
public Example(String a, String b) {
    this.a = a;
    this.b = b;
}
//a와 b의 위치를 변경하여 생성자를 호출
Example example = new Example("b", "a");

//builder 클래스를 이용하여 명확히 인자의 의미를 나타낼 수 있다.
Example example = Example.builder()
    .a("a")
    .b("b")
    .build();
```
