## 프로그래머스 레벨 2

### 피보나치

- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/dfsBfs/Fibonacci.java)

분배 법칙 :
-  나머지 연산에서 적용될 수 있는 중요한 성질
-  덧셈과 곱셈 사이에서 모듈러 연산이 적용될 때 사용

1. 덧셈의 분배 법칙:
   - (a + b) % n = ((a % n) + (b % n)) % n
2. 곱셈의 분배 법칙:
   - (a * b) % n = ((a % n) * (b % n)) % n

   - 여기서, a와 b는 임의의 정수이며, n은 나누는 수. %는 모듈러 연산을 나타낸다.

- 분배 법칙을 사용하면, 덧셈이나 곱셈을 수행하기 전에 모듈러 연산을 수행한 후 결과를 다시 모듈러 연산할 수 있으며.
- 이를 통해 중간 계산 결과의 범위를 제한하고, 오버플로우나 값의 변형을 방지할 수 있다.

### 예상대진표 
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/ExpectedMatchups.java)

1. a,b가 포함된 각각의 지수를 찾는다.(a가 3이라면 a의 지수는 2, b가 7이라면 지수는 3)
2. 지수가 다를 경우 만나게되는 n번째 경기는 두 지수 중에 큰 지수의 값이다. (b가 7이고, a가 1~4의 값이면 7이 포함된 지수인 3번째 경기에서 a 와 b가 만나게 된다.)
3. 같은 경우 a,b에 2<sup>n-1</sup>의 나머지로 치환한다.(딱 떨어지는 경우 2<sup>n-1</sup>이다.)
    - a가 9. b가 16이라면 a는 1, b는 0(8)으로 치환한다.
4. 1번부터 반복한다.

### 점프와 순간이동
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/JumpAndTeleport.java)

1. 도착 지점을 d라고 할 때 d를 2로 나눈다.
   - 2로 나누는 이유는 가장 처음 점프를 무조건 1로 하고 중간에 점프를 한번 더하는것이 건전지 소모량을 줄일 수 있기 때문이다.
   - (d : 7 인 경우 빨간색 : 점프 , 파란색 : 순간이동)
     - <span style="color:red;">1</span> &rarr; <span style="color:blue;">2</span> &rarr; <span style="color:red;">3</span> &rarr; <span style="color:blue;">6</span> &rarr; <span style="color:red;">7</span> : 3번
     - <span style="color:red;">3</span> &rarr; <span style="color:blue;">6</span> &rarr; <span style="color:red;">7</span> : 4번
     - 이렇듯 처음에 많은 칸을 점프하는 것보단 중간에 점프를 하는 것이 더 효율적이다.
2. 나머지가 1인경우 점프를 한번 더 해야하므로 카운트를 1 증가시킨다.  
3. 1번부터 반복한다.


### N개의 최소공배수
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/LeastCommonMultiple.java)

1. 최소공배수를 구하는 방법은 두 수의 곱을 최대공약수로 나누는 것이다.
2. 유클리드 호제법이란?
    - 두 수의 최대공약수를 구하는 알고리즘
    - 두 수 a,b(a>b)가 있다고 할 때 a를 b로 나눈 나머지를 r이라고 한다면 a와 b의 최대공약수는 b와 r의 최대공약수와 같다.
    - 이를 반복하면 두 수의 최대공약수를 구할 수 있다.
    - 예를 들어 24와 16의 최대공약수를 구한다고 할 때
        - 24 % 16 = 8
        - 16 % 8 = 0
        - 8 % 0 = 8
        - 8이 최대공약수가 된다.

### 요격시스템
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/MissileDefenseSystem.java)

1. 미사일은 개구간(s,e)로 표현되며 s,e에서 발사되는 미사일로 요격 불가이기 떄문에 비교할 때 같다는 조건 제외
2. e를 기준으로 배열 정렬
3. 현재 미사일의 s보다 크면서 e보다 작거나 같을 경우 요격가능, 이 경우 e는 변경하지 않음
4. 3번 조건을 만족하지 못할 경우, 미사일 발사 횟수 1증가 및 e변경 


### 연속된 부분 수열의 합
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/dfs/calculateSum.java)

1. k를 만족 했을 경우 길이(시작인데스 - 종료인덱스)값 설정
    - 만족하는 경우의 수가 여러가지 일 경우를 가장 앞선 값들을 변경하지 않기 위해
    - 길이가 0인 경우 바로 탈출
2. 이중 for문을 이용하여 부분 수열의 합을 구함 
#### 문제점 
- 시간복잡도 O(n<sup>2</sup>)으로 인해 시간초과 발생
#### 해결 
- 부분 수열의 합을 구할 때 이전에 구한 부분 수열의 합을 이용하여 구함
- k보다 수열의 합이 클 경우 작아질 때까지 이전에 구한 부분 수열의 합을 빼고 다음 인덱스의 값을 더함 
- 시간복잡도 O(N)
   
   
### 멀리뛰기
1. 무식하게 1~6까지 뛰는 경우의 수를 구하다보니 피보나치인걸 확인 후 이번엔 DP로 품..
2. 해당 문제의 경우 점화식으로 판단할 수 있다는걸 알게됨
3. 점화식 : f(n) = f(n-1) + f(n-2) (n>=2)
      - [n - 1]번째 칸에서 1칸을 뛰어서 n번째 칸에 도착했다.
      - [n - 2]번째 칸에서 2칸을 뛰어서 n번째 칸에 도착했다.
![fibonacci.png](img%2Ffibonacci.png)
- 출처
  - [나무위키](https://namu.wiki/w/피보나치%20수열#s-7.1)