## Java란?
객체지향적 프로그래밍 언어(OOP)입니다.

- JVM을 이용하기 때문에 운영체제에 독립적
- 캡슐화, 상속, 다형성, 추상화 특징을 가진다.
- 런타임시 데이터 타입이 결정되는 동적타입 언어
- GC를 통해 메모리를 자동관리한다.
- 멀티스레드를 지원하여 동시에 여러 작업 지원
  ...

> **OOP**
프로그래밍에 사용 될 데이터의 상태와 행위를 객체로 만들어, 객체간의 상호작용을 통해 비즈니스 로직을 구성하는 프로그래밍 기법 ([링크](https://velog.io/@industry1111/OOP-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))

> **JVM**
Java Virtual Machine으로 자바 프로그램 실행환경을 만들어주는 소프트웨어이다.([링크](https://velog.io/@industry1111/Java-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%EA%B3%BC%EC%A0%95))


> **GC(Garbage Collection)**
자바의 메모리 관리 기법으로 어플리케이션이 동적으로 할당했던 메모리 영역 중 더이상 사용하지 않는 영역을 정리하는 기능 ([링크](https://velog.io/@industry1111/Java-Garbage-Collection))

### Java 접근 제어자
- **Public** : 모든 패키지, 클래스에서 접근 허용
- **Protected** : 같은 패키지내의 모든 클래스에서 접근 허용(단, 다른 패키지의 자식클래스에서 접근 허용)
- **Default** : 같은 패키지내 클래스만 접근 허용
- **Private** : 같은 클래스 내 접근만 허용

|접근 제어자|같은 클래스|같은 패키지|자식 클래스|그 외|
|---|---|---|---|---|
|Public|O|O|O|O|
|Protected|O|O|O|X|
|Default|O|O|X|X|
|Private|O|X|X|X|

### Java final
`final` 은 변수, 메서드 또는 클래스를 선언할 때 사용되는 한정자이며,
해당 요소에 대한 변경이나 재정의를 금지한다.

- `final 변수` : 상수로 취급하며, 일반적으로 대문자로 작성하여 상수임을 나타낸다.
- `final 메서드` : 해당 메서드는 하위 클래스에서 오버라이드할 수 없다.
- `final 클래스` : 해당 클래스는 상속할 수 없다.

### Java Interface vs Abstract
인터페이스와 추상 클래스 둘 다 다른 클래스에 공통된 메서드나 속성을 정의하기 위한 방법이지만, 목적과 특징에 차이가 있다.
`인터페이스`
- `추상 메서드의 집합`
- 선언부만을 가지면, 구현부가 존재하지 않는다
- 다중 상속 지원
- 인터페이스의 모든 멤버는 public 이다.

`추상 클래스`
- 일반 클래스와 달리 추상 메서드를 포함할 수 있다.
- 추상 메서드의 구현은 하위 클래스에서 이루어져야 한다.
- 단일 상속

### Java Class
자바의 클래스는 멤버(membe)로 속성을 표현하는 필드(field)와 기능을 표현하는 메소드(method)를 가진다.

>**member**
자바에서 멤버는 클래스나 인터페이스 내에서 선언되는 변수와 메서드를 가리키는 용어이다.

- `멤버 변수(Member Variables)` : 클래스나 인터페이스 내에서 선언된 변수로, 객체의 상태를 나타내는 데이터를 저장한다.

- `멤버 메서드(Member Method)` : 클래스나 인터페이스 내에서 정의된 함수로, 객체의 동작이나 행위를 구현

- `생성자(Contructors)` : 클래스 내에서 객체의 초기화를 담당하는 특수한 유형의 메서드이며

- `정적 멤버(Static Member)` : static 키워드로 선언된 멤버로, 클래스 수준에서 공유되는 변수와 메서드를 나타낸다.

- `인스턴스 멤버(Instance Member)` : 클래스의 인스턴스(객체)에 속하는 변수와 메서드를 나타낸다. 객체가 생성될 때 해당 멤버도 함께 생성한다.

- `내부 클래스(Inner Class)` : 클래스 내에 정의 되는 클래스로, 외부 클래스의 멤버에 더 밀접한 접근 권한을 가지거나 특정 상황에서 유용한 기능을 제공하기 위해 사용(ex LinkedList와 같은 데이터 구조에서 노드를 나타내는 inner class)

```java
public class ExampleClass {

    // 멤버 변수 (인스턴스 변수)
    private int instanceVar;

    // 정적 멤버 변수 (클래스 변수)
    static int staticVar;

    // 생성자
    public ExampleClass(int instanceVar) {
        this.instanceVar = instanceVar;
    }

    // 멤버 메서드 (인스턴스 메서드)
    public void instanceMethod() {
        System.out.println("Instance method is called. Instance variable: " + instanceVar);
    }

    // 정적 멤버 메서드 (클래스 메서드)
    public static void staticMethod() {
        System.out.println("Static method is called. Static variable: " + staticVar);
    }

    // 내부 클래스
    class InnerClass {
        // 내부 클래스 내부의 멤버들
    }
```

> **static**
변수와 메서를 정적 멤버로 만들 수 있는 키워드 이다.
정적 필드와 정적 메서드는 인스턴스가 아닌, 클래스에 고정되어, 클래스 로더가 클래스를 로딩에 메모리 영역에 적재할 때, 클래스 별로 관리되어 정적 메모리르 사용할 수 있다.