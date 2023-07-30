## Java Integer.toString() vs String.valueOf()

### 1. Integer.toString() 메서드
이 메서드는 기본 데이터 형식 int  의 `정수를 매개 변수로 받아들이고 지정된 정수를 나타내는 String 개체를 반환합니다.`

```java

@Test
public void whenValidIntIsPassed_thenShouldConvertToString() {
        assertEquals("11", Integer.toString(11));
        assertEquals("11", Integer.toString(+11));
        assertEquals("-11", Integer.toString(-11));
}
```
### 2. String.valueOf() 메서드
이 메서드는 또한 기본 데이터 형식 int  의 정수를 매개 변수로 받아들이고 String 개체를 반환합니다.

흥미롭게도 반환된 문자열 표현은 Integer.toString(int i) 메서드 에서 반환된 것과 정확히 동일합니다 . 

`내부적으로 Integer.toString() 메서드를 사용하기 때문입니다 .`

java.lang.String 클래스 에 제공된 내부 구현을 살펴보겠습니다 .

```java
    /**
 * Returns the string representation of the {@code int} argument.
 * <p>
 * The representation is exactly the one returned by the
 * {@code Integer.toString} method of one argument.
 *
 * @param   i   an {@code int}.
 * @return  a string representation of the {@code int} argument.
 * @see     java.lang.Integer#toString(int, int)
 */
public static String valueOf(int i) {
        return Integer.toString(i);
}
```
더 잘 이해하기 위해 정수에서 문자열로의 변환이 발생하는 것을 이해하기 위해 부호 있는/부호 없는 정수를 매개 변수로 전달하는 몇 가지 예를 볼 수 있습니다.

```java
@Test
public void whenValidIntIsPassed_thenShouldConvertToValidString() {
    assertEquals("11", String.valueOf(11)); 
    assertEquals("11", String.valueOf(+11));
    assertEquals("-11", String.valueOf(-11));
}
```

### 3. toString() , valueOf 의 차이점

요약하면 이 두 가지 방법 사이에 실제적인 차이점은 없지만 혼동을 피하기 위해 다음 사항을 이해해야 합니다.

내부적으로 동일한 Integer.toString () 메서드를 사용하기 때문에 String.valueOf( ) 메서드 를 사용할 때 스택 추적에 하나의 추가 호출이 있습니다 .

null 개체를 valueOf() 메서드  에 전달할 때 약간의 혼란이 있을 수 있습니다 . `기본 int를  valueOf() 메서드 에 전달할 때 동일하게 보이지만 실제 메서드 호출은 다른 오버로드된 메서드로 이동하기 때문입니다.`

`Integer.toString()은 주어진 Integer 객체가 null 인 경우 NullPointerException을 던질 수 있습니다 . `

String.valueOf()는 String.valueOf(Object obj) 메서드 로 이동하여 null을 반환하기 때문에 예외를 throw하지 않습니다. 

`String.valueOf(int i)  에 전달된 기본 int는 null 이 될 수 없지만 다른 메서드 String.valueOf(Object obj)가 있으므로 오버 로드된 두 메서드 사이에서 혼동될 수 있습니다.`

출처

[baeldung.com](https://www.baeldung.com/java-tostring-valueof)