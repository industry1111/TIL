# Java

**객체지향 (Object-Oriented) 프로그래밍:**
객체지향 프로그래밍은 프로그램을 작성할 때 현실 세계의 객체와 그들 간의 관계를 모델로 하여 프로그래밍하는 방법론입니다. 이를 통해 코드의 재사용성과 유지보수성을 향상시킬 수 있습니다.

**절차지향과의 차이점:**

- 절차지향 프로그래밍은 작업 단위를 함수로 나누고, 데이터와 함수를 분리하여 프로그램을 작성합니다.
- 객체지향 프로그래밍은 데이터와 관련 함수를 하나의 객체로 묶어서 사용하며, 객체 간의 상호작용을 강조합니다.

**객체지향 SOLID 원칙:**
SOLID는 객체지향 프로그래밍에서 좋은 설계와 유지보수성을 위한 다섯 가지 원칙의 머리글자입니다.

- S: 단일 책임 원칙 (Single Responsibility Principle)
- O: 개방/폐쇄 원칙 (Open/Closed Principle)
- L: 리스코프 치환 원칙 (Liskov Substitution Principle)
- I: 인터페이스 분리 원칙 (Interface Segregation Principle)
- D: 의존성 역전 원칙 (Dependency Inversion Principle)

**객체지향 4가지 특징:**

1. **추상화 (Abstraction):** 복잡한 현실 세계를 모델링하여 중요한 부분만 추출하여 표현하는 개념입니다.
2. **캡슐화 (Encapsulation):** 데이터와 그에 관련된 함수를 하나의 단위로 묶어 외부에서 직접 접근하지 못하도록 보호하는 개념입니다.
3. **상속 (Inheritance):** 부모 클래스의 특성을 자식 클래스가 물려받아 확장하거나 변경하여 사용하는 개념입니다.
4. **다형성 (Polymorphism):** 동일한 이름의 메서드를 서로 다른 객체에 대해 다양하게 구현하고 사용할 수 있는 개념입니다.

**대표적인 객체지향 언어:**
자바 (Java), C++, C#, Python, Ruby 등이 대표적인 객체지향 언어입니다.

**데이터 타입과 변수의 차이:**

- 데이터 타입은 값의 종류를 나타내며, 변수는 값을 저장하는 메모리 공간을 의미합니다.
- 변수는 특정한 데이터 타입의 값을 저장하며, 데이터 타입은 변수에 할당될 수 있는 값의 종류와 크기를 결정합니다.

**함수형 프로그래밍:**
함수형 프로그래밍은 프로그램을 수학적 함수의 연속적인 계산으로 보는 패러다임입니다. 함수들을 일급 시민으로 취급하며, 상태 변경보다는 입력과 출력에 초점을 두어 부작용을 최소화하려는 접근 방식입니다.

**AOP (Aspect-Oriented Programming):**
AOP는 프로그램을 여러 관심사로 분리하여 모듈화하고, 각 관심사를 따로 구현한 뒤 필요한 시점에 합치는 프로그래밍 패러다임입니다. 주로 로깅, 보안, 트랜잭션 등의 부가 기능을 분리하여 관리할 때 사용됩니다.

**컴파일러와 인터프리터의 차이:**

- 컴파일러는 소스 코드를 한 번에 기계어로 변환하여 실행 파일을 생성합니다.
- 인터프리터는 소스 코드를 한 줄씩 읽어들여 즉시 실행합니다.

**오버로딩과 오버라이딩의 차이:**

- 오버로딩 (Overloading): 하나의 클래스 내에서 메서드의 이름은 같지만 매개변수의 타입, 개수, 순서 등이 다른 여러 메서드를 정의하는 것을 말합니다.
- 오버라이딩 (Overriding): 상위 클래스가 가지고 있는 메서드를 하위 클래스에서 동일한 이름과 매개변수로 재정의하는 것을 말합니다.

**Java 접근 제어자 (Access Modifiers):**
접근 제어자는 클래스, 변수, 메서드 등의 멤버에 대한 접근 범위를 제어하는 역할을 합니다.

- `public`: 어떤 클래스에서나 접근 가능합니다.
- `protected`: 같은 패키지 내의 클래스와 상속 관계의 클래스에서 접근 가능합니다.
- `default` (package-private): 같은 패키지 내에서만 접근 가능합니다.
- `private`: 동일 클래스 내에서만 접근 가능합니다.
-

**Java 버전 별 특성:**
각 Java 버전마다 다양한 기능과 개선 사항이 추가됩니다. 몇 가지 예시:

- Java 8: 람다식, 스트림 API,  인터페이스에서 디폴트 메서드 사용가능
- Java 11:  var 키워드를 사용하여 지역변수를 선언할 수 있게 되었음
- Java 17 : GC알고리즘 추가, 패턴 매칭 기능추가,

**Java는 Call By Value일까요, Call By Reference 일까요?:**
Java는 메서드 호출 시 변수의 값을 복사하여 전달하는 Call By Value 방식을 사용합니다. 하지만 참조 타입의 경우, 변수가 참조하는 객체의 주소값이 복사되어 전달되므로 객체의 내용을 변경하는 것은 가능합니다. 이로 인해 'Call By Reference'처럼 동작할 수 있어 혼동을 일으킬 수 있습니다.

**리플렉션 (Reflection):**
리플렉션은 프로그램이 자신의 구조를 분석하고 변경할 수 있는 능력을 의미합니다. Java에서는 리플렉션을 사용하여 클래스, 메서드, 필드 등의 정보를 동적으로 조사하고, 인스턴스를 생성하거나 메서드를 호출할 수 있습니다. 주로 런타임 시에 클래스의 정보를 조사하거나 동적으로 객체를 다룰 때 활용됩니다.

**Stream API:**
스트림 API는 Java 8에서 도입된 기능으로, 컬렉션을 처리하거나 조작하는 작업을 더 효과적으로 수행할 수 있는 기능을 제공합니다. 스트림을 사용하면 데이터의 처리 파이프라인을 생성하고 병렬 처리를 통해 성능을 향상시킬 수 있습니다.

**Lambda:**
람다는 함수형 프로그래밍을 지원하기 위해 Java 8에서 도입된 개념으로, 익명 함수를 표현하는 방식입니다. 람다를 사용하면 코드의 간결성과 가독성을 향상시키며, 컬렉션의 데이터를 처리하거나 스레드를 다룰 때 유용하게 활용됩니다.

**함수형 인터페이스:**
함수형 인터페이스는 단 하나의 추상 메서드만을 가지는 인터페이스를 의미합니다. Java 8에서는 람다 표현식을 활용하기 위해 함수형 인터페이스를 사용합니다. 예를 들어, `Runnable`이나 `Callable` 등이 함수형 인터페이스의 예입니다.

**JVM 기동시 주로 사용되는 옵션들:**

- `Xms`: 초기 힙 크기 지정
- `Xmx`: 최대 힙 크기 지정
- `Xss`: 스레드 스택 크기 지정
- `XX:MaxPermSize`: 영구 영역의 최대 크기 지정 (Java 8 이전)
- `XX:MaxMetaspaceSize`: 메타스페이스의 최대 크기 지정 (Java 8 이후)
- `XX:+UseG1GC`: G1 GC 사용
- `XX:+UseParallelGC`: 병렬 GC 사용
- `XX:+UseConcMarkSweepGC`: CMS GC 사용

**foreach 사용 가능한 자료구조:**`Iterable` 인터페이스를 상속받은 컬렉션들 (예: List, Set)과 배열에서 `foreach` 루프를 사용할 수 있습니다.

**Iterator와 Iterable 차이:**

- `Iterable`: 이터레이션을 지원하는 컬렉션을 나타내는 인터페이스입니다. `Iterator`를 반환하는 `iterator()` 메서드를 포함하고 있습니다.
- `Iterator`: 컬렉션 내의 요소들을 순차적으로 접근하고 조작할 수 있는 방법을 제공하는 인터페이스입니다.

**synchronized 키워드:**`synchronized` 키워드는 멀티스레드 환경에서 공유 자원에 대한 동기화를 제공하는 방법 중 하나입니다. `synchronized` 메서드나 블록을 사용하여 특정 코드 영역이 한 번에 하나의 스레드만 실행되도록 보장합니다.

**volatile 키워드:**`volatile` 키워드는 변수의 값을 메인 메모리에서 직접 읽고 쓰도록 하여 스레드 간의 가시성과 순서를 보장합니다. 변수의 변경이 다른 스레드에게 즉시 알려지며, 스레드가 변수를 읽을 때 항상 최신 값을 읽을 수 있도록 합니다.

**final 키워드:**`final` 키워드는 변수, 메서드, 클래스를 선언할 때 사용됩니다.

- 변수: 변수 값을 변경할 수 없음을 의미합니다.
- 메서드: 메서드 오버라이딩을 방지하거나 하위 클래스에서 재정의할 수 없음을 의미합니다.
- 클래스: 해당 클래스를 상속할 수 없음을 의미합니다.

**Wrapper Class:**
Wrapper Class는 기본 데이터 타입(primitive type)을 객체로 감싸주는 클래스를 의미합니다. Java에서는 int, char, boolean 등과 같은 기본 데이터 타입을 각각 Integer, Character, Boolean 등의 Wrapper Class로 감싸서 객체로 다룰 수 있도록 하며, 객체 지향 환경에서 기본 데이터 타입을 객체로 다루기 위해 사용됩니다.

**클래스, 객체, 인스턴스 차이:**

- **클래스(Class):** 클래스는 객체를 생성하기 위한 설계도 또는 템플릿으로, 객체의 속성과 행위(메서드)를 정의합니다.
- **객체(Object):** 클래스의 인스턴스를 의미하며, 클래스에 정의된 속성과 메서드를 실제로 가지고 있는 것입니다.
- **인스턴스(Instance):** 클래스의 객체를 생성한 실체를 의미합니다. 클래스를 기반으로 생성된 개별 객체를 인스턴스라고 합니다.

**직렬화(Serialization)와 역직렬화(Deserialization):**

- **직렬화:** 객체를 바이트 스트림으로 변환하는 과정을 말합니다. 객체를 저장하거나 네트워크를 통해 전송할 때 사용됩니다.
- **역직렬화:** 바이트 스트림을 객체로 변환하는 과정을 말합니다. 직렬화된 객체를 원래의 객체로 복원하는 작업을 의미합니다.

**Java Generic:**
Java Generic은 타입을 파라미터화하여 코드의 재사용성과 타입 안정성을 높이는 기능입니다. 제네릭을 사용하면 클래스나 메서드를 선언할 때 특정 타입을 지정하지 않고, 나중에 실제 사용할 때 타입을 지정할 수 있습니다.

**equals와 ==의 차이:**

- **equals:** `equals` 메서드는 객체의 내용(값)을 비교합니다. 주로 사용자 정의 클래스에서 오버라이딩하여 동등성 비교를 정의할 수 있습니다.
- **==:** `==` 연산자는 객체의 참조(메모리 주소)를 비교합니다. 기본 데이터 타입의 경우 값 비교를 하며, 객체의 경우 두 참조가 같은 객체를 가리키는지를 비교합니다.

**hashCode:**`hashCode`는 객체의 해시 코드를 반환하는 메서드입니다. 해시 코드는 객체의 식별값으로 사용되며, 해시 기반의 컬렉션에서 객체를 관리하는 데 사용됩니다.

**문자열 리터럴과 객체 할당의 차이:**

- 문자열 리터럴(`string = "abcd"`): 문자열 리터럴은 문자열 풀(String Pool)에 저장되며, 동일한 내용의 문자열이 여러 변수에서 사용될 때 메모리를 공유합니다.
- 객체 할당(`string = new String("abcd")`): 객체로 할당하면 매번 새로운 문자열 객체가 생성됩니다. 메모리 사용량이 증가할 수 있습니다.

**순수 추상 클래스와 인터페이스의 차이:**

- 순수 추상 클래스: 추상 클래스 중에서 추상 메서드만 가지며, 일반 메서드를 포함할 수 있습니다.
- 인터페이스: 추상 메서드만 가지며, 일반 메서드를 포함하지 않습니다. 다중 상속을 지원하며, 클래스가 여러 개의 인터페이스를 구현할 수 있습니다.

**인터페이스 사용 시점:**
인터페이스는 다중 상속을 지원하고, 클래스 간의 공통 기능을 정의할 때 주로 사용됩니다. 클래스가 여러 개의 관련 없는 클래스를 상속할 필요가 있을 때 인터페이스를 활용하여 기능을 구현할 수 있습니다.

**Java의 Collection:**
Java의 Collection은 데이터를 저장, 관리, 처리하기 위한 인터페이스와 클래스의 모음입니다. Collection은 데이터를 다루기 위한 다양한 자료구조와 알고리즘을 제공하며, 배열보다 유연하고 편리한 데이터 처리를 가능하게 합니다. 주요한 Collection 인터페이스로는 List, Set, Map 등이 있으며, 이를 구현한 클래스로는 ArrayList, HashSet, HashMap 등이 있습니다.

**Array와 ArrayList의 차이점:**

- **Array:** 배열은 고정 크기의 같은 타입의 요소들로 이루어진 데이터 구조입니다. 크기가 한 번 정해지면 변경할 수 없으며, 연속된 메모리 공간에 요소들이 저장됩니다.
- **ArrayList:** ArrayList는 크기가 가변적으로 변할 수 있는 배열 기반의 리스트 구현체입니다. 내부적으로 배열을 사용하며, 요소가 추가될 때마다 배열의 크기가 동적으로 조정됩니다.

**char type과 string type으로 나뉘어진 이유:**
Java에서 char는 문자를 표현하는 데이터 타입이며, String은 문자열을 표현하는 데이터 타입입니다. 이 두 가지 타입이 별도로 나뉘어진 이유는 문자와 문자열을 다른 방식으로 다루기 위함입니다.

**Spring, Spring MVC, Spring Boot의 차이점:**

- **Spring:** Spring Framework는 자바 기반의 엔터프라이즈 애플리케이션을 개발하기 위한 프레임워크로서, 의존성 주입과 관점 지향 프로그래밍 등을 지원합니다.
- **Spring MVC:** Spring MVC는 Spring Framework의 하위 모듈로 웹 애플리케이션을 개발하기 위한 모듈입니다. Model-View-Controller 패턴을 기반으로 하며, 웹 애플리케이션의 요청과 응답을 처리합니다.
- **Spring Boot:** Spring Boot는 Spring 기반의 애플리케이션을 빠르고 간단하게 개발하기 위한 도구로, 설정을 자동화하고 개발 생산성을 높여줍니다.

**Spring Framework의 생명 주기:**

1. **Bean Definition:** Spring 컨테이너에게 Bean 정의를 제공하거나 XML 또는 어노테이션을 통해 Bean 설정을 정의합니다.
2. **Bean Initialization:** Bean이 생성되고 초기화되며, 생성자나 초기화 메서드 등이 호출됩니다.
3. **Bean Use:** 애플리케이션에서 Bean을 사용하고 의존성 주입(DI)을 통해 필요한 Bean들이 주입됩니다.
4. **Bean Destruction:** Bean이 더 이상 필요하지 않을 때, 종료 또는 소멸 메서드가 호출되어 리소스를 해제하거나 정리합니다.

**Bean이란 무엇인가요?**
Bean은 Spring Framework에서 관리되는 객체로, Spring 컨테이너에 의해 생성, 관리 및 제어됩니다. Bean은 Java 클래스의 인스턴스로서, Spring 컨테이너가 관리하는 객체로서의 역할을 수행합니다. Bean은 의존성 주입(DI)을 통해 다른 Bean들과 협력하며 애플리케이션의 비즈니스 로직을 구성합니다.

**Interceptor와 Filter의 차이점:**

- **Interceptor:** Spring MVC에서 사용되는 개념으로, 컨트롤러 실행 전후에 특정 작업을 수행하는 기능입니다. 예를 들어, 로그인 여부 확인, 권한 검사 등을 수행할 수 있습니다.
- **Filter:** Java 웹 애플리케이션에서 사용되는 개념으로, 클라이언트의 요청과 응답을 가로채서 처리하는 기능입니다. 서블릿 컨테이너의 요청 처리 전후에 실행됩니다.

**IOC와 DI에 대해서 설명해주세요:**

- **IOC (Inversion of Control):** 제어의 역전으로, 애플리케이션의 흐름을 개발자가 아닌 프레임워크가 제어하는 개념을 의미합니다. Spring에서는 Bean의 생성부터 생명 주기 관리까지 컨테이너가 담당합니다.
- **DI (Dependency Injection):** 의존성 주입으로, 객체 간의 의존 관계를 컨테이너가 관리하여 객체가 직접 의존하는 객체를 생성하지 않고 주입받아 사용하는 개념입니다. DI를 통해 유연하게 의존 관계를 변경하거나 테스트하기 쉬운 코드를 작성할 수 있습니다.

**Container란 무엇인가요?**
Container는 Spring Framework에서 Bean의 생명 주기를 관리하고 의존성 주입(DI)을 통해 객체를 관리하는 역할을 수행하는 런타임 환경입니다. Spring 컨테이너는 ApplicationContext와 BeanFactory라는 두 가지 주요 컨테이너를 제공합니다. 컨테이너는 Bean의 생성, 초기화, 의존성 주입, 소멸 등의 작업을 관리하여 개발자가 애플리케이션 로직에 집중할 수 있도록

**MVC에 대해서 설명해 주세요:**
MVC는 "Model-View-Controller"의 약자로, 소프트웨어 디자인 패턴 중 하나입니다. 이 패턴은 애플리케이션의 구성 요소를 세 가지 역할로 나누어 개발하는 방법을 제공하여 코드의 재사용성, 유지 보수성, 확장성을 높이는데 목적이 있습니다.

- **Model:** 애플리케이션의 데이터와 비즈니스 로직을 담당하는 부분입니다. 데이터를 관리하고 조작하는 역할을 수행합니다.
- **View:** 사용자 인터페이스(UI)를 담당하는 부분입니다. 모델의 데이터를 사용자에게 보여주는 역할을 수행하며, 데이터를 시각적으로 표현합니다.
- **Controller:** 모델과 뷰 사이의 중재자 역할을 하는 부분입니다. 사용자의 입력을 처리하고 해당하는 모델을 업데이트하며, 뷰에게 데이터를 전달하여 화면을 업데이트합니다.

MVC 패턴을 사용하면 코드의 모듈화가 용이해지며, 각 역할별로 변경이 필요한 경우 영향을 최소화할 수 있습니다.

**Servlet이 무엇인가요?:**
Servlet은 Java 웹 애플리케이션 개발을 위한 기술로, 서버 측에서 동적인 웹 컨텐츠를 생성하고 관리하는 역할을 수행합니다. Servlet은 Java 언어로 작성되며, HTTP 프로토콜을 기반으로 클라이언트의 요청을 처리하고 응답을 생성하는데 사용됩니다.

Servlet은 Java API를 구현한 클래스로, 주로 웹 서버에서 실행되어 클라이언트의 요청을 처리하고 그에 따른 동적인 웹 페이지나 데이터를 생성하여 응답합니다.

**Dispatcher-Servlet이란 무엇인가요?:**
Dispatcher-Servlet은 Spring Framework에서 웹 애플리케이션의 전체 요청을 받아들이고, 해당 요청을 처리할 컨트롤러로 분배하는 역할을 수행하는 서블릿입니다. 이를 통해 개발자는 여러 컨트롤러를 작성하고 각각의 컨트롤러가 특정 URL 요청을 처리하도록 구성할 수 있습니다.

Dispatcher-Servlet은 Spring MVC의 핵심 부분으로, 웹 애플리케이션의 다양한 컴포넌트(컨트롤러, 뷰 리졸버 등)와의 연결을 관리하며 요청과 응답을 조정합니다.

**Spring MVC에서 HTTP 요청이 들어왔을 때의 흐름을 설명해 주세요:**

1. **클라이언트 요청:**
   클라이언트가 HTTP 요청을 서버에 보냅니다. 이 요청은 URL 경로, HTTP 메서드, 헤더, 파라미터 등의 정보를 포함합니다.
2. **Dispatcher-Servlet 수신:**
   클라이언트 요청은 Spring의 Dispatcher-Servlet이 수신합니다. Dispatcher-Servlet은 웹 애플리케이션의 모든 요청을 중앙 집중적으로 처리합니다.
3. **핸들러 매핑 (Handler Mapping):**
   Dispatcher-Servlet은 요청을 처리할 적절한 핸들러(컨트롤러)를 찾기 위해 핸들러 매핑을 사용합니다. 핸들러 매핑은 요청의 URL 경로를 기반으로 어떤 컨트롤러가 해당 요청을 처리할지를 결정합니다.
4. **컨트롤러 호출:**
   찾아진 핸들러(컨트롤러)가 실행됩니다. 이때 컨트롤러는 비즈니스 로직을 수행하고 모델(Model)에 데이터를 추가합니다.
5. **모델 앤 뷰 생성:**
   컨트롤러는 처리된 데이터를 기반으로 모델(Model)을 생성합니다. 모델은 뷰(View)에 전달될 데이터를 담고 있습니다. 이때, 뷰의 이름도 함께 반환됩니다.
6. **뷰 리졸버 (View Resolver):**
   Dispatcher-Servlet은 반환된 뷰의 이름을 뷰 리졸버에게 전달합니다. 뷰 리졸버는 뷰의 이름을 실제 뷰 객체로 변환하는 역할을 수행합니다.
7. **뷰 렌더링:**
   뷰 리졸버에 의해 선택된 뷰가 실제로 렌더링됩니다. 뷰는 모델에 있는 데이터를 기반으로 HTML, XML, JSON 등의 형식으로 변환하여 클라이언트에게 전달됩니다.