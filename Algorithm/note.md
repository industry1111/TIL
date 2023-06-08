### 예상대진표 - 프로그래머스 레벨 2 
- [link](https://github.com/industry1111/algorithm/blob/main/src/main/java/programmers/leveltwo/ExpectedMatchups.java)

#### 내가 생각한 접근 방법
1. a,b가 포함된 각각의 지수를 찾는다.(a가 3이라면 a의 지수는 2, b가 7이라면 지수는 3)
2. 지수가 다를 경우 만나게되는 n번째 경기는 두 지수 중에 큰 지수의 값이다. (b가 7이고, a가 1~4의 값이면 7이 포함된 지수인 3번째 경기에서 a 와 b가 만나게 된다.)
3. 같은 경우 a,b에 2<sup>n-1</sup>의 나머지로 치환한다.(딱 떨어지는 경우 2<sup>n-1</sup>이다.)
    - a가 9. b가 16이라면 a는 1, b는 0(8)으로 치환한다.
4. 1번 부터 다시 반복한다.
