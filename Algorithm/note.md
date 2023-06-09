## 프로그래머스 레벨 2
### 예상대진표 
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/ExpectedMatchups.java)

 접근 방법
1. a,b가 포함된 각각의 지수를 찾는다.(a가 3이라면 a의 지수는 2, b가 7이라면 지수는 3)
2. 지수가 다를 경우 만나게되는 n번째 경기는 두 지수 중에 큰 지수의 값이다. (b가 7이고, a가 1~4의 값이면 7이 포함된 지수인 3번째 경기에서 a 와 b가 만나게 된다.)
3. 같은 경우 a,b에 2<sup>n-1</sup>의 나머지로 치환한다.(딱 떨어지는 경우 2<sup>n-1</sup>이다.)
    - a가 9. b가 16이라면 a는 1, b는 0(8)으로 치환한다.
4. 1번부터 반복한다.

### 점프와 순간이동
- [source](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/JumpAndTeleport.java)

 접근 방법
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

    접근 방법
1. 최소공배수를 구하는 방법은 두 수의 곱을 최대공약수로 나누는 것이다.
2. 최대공약수를 구하는 방법은 유클리드 호제법을 사용한다.

