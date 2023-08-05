### OOP (Object Oriented Programming)

객체 지향 프로그래밍은 현실 세계의 사물들을 객체로 보고 이 객체들의 특성과 동작들을 `추상화`하여 클래스로 정의하고 `캡슐화`하여 객체의 내부 상태를 외부에서 직접 접근하지 못하도록 보호하며, `상속`과 `다형성`을 이용해 유연하게 조합하여 프로그램을 구성하는 것을 말한다.

자바 코드로 설명하자면 아래와 같다

```Java
// 추상화 (Abstraction) - 현실 세계의 개념을 나타내는 클래스를 정의
class Animal {
    String name;
    int age;

    public void makeSound() {
        // 소리를 내는 동작을 구현
    }
}

// 캡슐화 (Encapsulation) - 클래스의 내부 세부 사항을 숨김
class BankAccount {
    private int balance;

    public void deposit(int amount) {
        // 돈을 입금하는 동작을 구현
    }

    public int getBalance() {
        // 계좌 잔액을 얻는 동작을 구현
        return balance;
    }
}

// 상속 (Inheritance) - 기존 클래스를 기반으로 새로운 클래스를 생성
class Dog extends Animal {
    public void makeSound() {
        System.out.println("멍멍!");
    }
}

// 다형성 (Polymorphism) - 서로 다른 타입의 객체를 하나의 인터페이스로 사용
class Shape {
    public void draw() {
        // 도형을 그리는 동작을 구현
    }
}

class Circle extends Shape {
    public void draw() {
        // 원을 그리는 동작을 구현
    }
}

class Square extends Shape {
    public void draw() {
        // 정사각형을 그리는 동작을 구현
    }
}

```

### 객체 지향 설계 원칙 (SOLID)


**SRP (Single Responsibility Principle) 단일 책임 원칙**
하나의 클래스는 단 하나의 책임을 가져야 한다. 클래스를 변경하는 이유는 단 하나의 이유여야 한다.

**OCP (Open-Closed Principle) 개방-폐쇄 원칙**
기존의 코드를 변경하지 않으면서 기능을 확장할 수 있도록 설계해야 한다. 추상화와 다형성을 이용하여 확장에는 열려 있고 변경에는 닫혀 있어야 한다.

**LSP (Liskov Substitution Principle) 리스코프 치환 원칙**
자식 클래스는 언제나 부모 클래스를 대체할 수 있어야 한다. 상속 관계에서 서브 타입은 언제나 슈퍼 타입으로 교체할 수 있어야 한다.

**ISP (Interface Segregation Principle) 인터페이스 분리 원칙**
클라이언트가 자신이 사용하지 않는 인터페이스에 의존하지 않아야 한다. 큰 인터페이스를 작은 단위로 분리하여 의존성을 최소화해야 한다.

**DIP (Dependency Inversion Principle) 의존성 역전 원칙**
의존 관계를 맺을 때 변화하기 쉬운 것보다 변화하기 어려운 것에 의존해야 한다.

