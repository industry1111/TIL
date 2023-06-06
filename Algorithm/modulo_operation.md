### [분배법칙 (Distributive Property)](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/dfsBfs/Fibonacci.java)
-  나머지 연산에서 적용될 수 있는 중요한 성질
-  덧셈과 곱셈 사이에서 모듈러 연산이 적용될 때 사용

분배 법칙은 다음과 같이 표현가능하다.

1. 덧셈의 분배 법칙:
    - (a + b) % n = ((a % n) + (b % n)) % n
2. 곱셈의 분배 법칙:
    - (a * b) % n = ((a % n) * (b % n)) % n

- 여기서, a와 b는 임의의 정수이며, n은 나누는 수. %는 모듈러 연산을 나타낸다. 

- 분배 법칙을 사용하면, 덧셈이나 곱셈을 수행하기 전에 모듈러 연산을 수행한 후 결과를 다시 모듈러 연산할 수 있으며. 
- 이를 통해 중간 계산 결과의 범위를 제한하고, 오버플로우나 값의 변형을 방지할 수 있다.


