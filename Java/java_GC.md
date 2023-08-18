## 가비지 컬렉션(Garbage Collection)이란?

자바의 메모리 관리 기법으로 어플리케이션이 동적으로 할당했던 메모리 영역 중 더이상 사용하지 않는 영역을 정리하는 기능

GC는 Heap 메모리에서 활동하며, JVM에서 GC의 스케줄링을 담당하며 개발자가 직접 관여하지 않아도 더이상 사용하지 않는
점유된 메모리를 제거해주는 역할을 담당

### GC의 원리
GC가 가능했던건 약한 세대 가설(Weak Generational Hypothesis)) 덕분
아래 가정을 기반으로 메모리 구조를 크게 2개로 물리적 공간을 나눔 (Young Generation, Old Generation)

>**대부분 객체는 금방 접근 불가능(Unreachable)한 상태가 된다**</br>
대부분의 객체는 줄괄호 안에서 생성
이 객체들은 괄호가 끝나는 시점에서 더이상 사용되지 않음
특수한 경우에는 오래 사용할 수 있지만, 대부분의 경우 unreachable한 상태가 되어 GC의 대상이 됨

>**오래된 객체에서 젋은 객체로의 참조는 아주 적게 발생**</br>
일반적으로 순차적인 로직에 의해 객체를 생성하여 활용
이 과정에서 앞에 생성된 객체는 그 다음의 로직에서 사용된 이후 대부분 사용되지 않게 됨
이런 특성으로 인해 더이상 참조되지 않는 객체에 대해 GC를 할 수 있게됨


**Heap Area**
GC는 간단하게 말해서 Heap Area에서 더이상 사용하지 않는 메모리를 제거하는 것을 의미
전통적인 Heap Area는 아래와 같은 구조를 가지고 있으며, Eden, Survivor1, Survivor2, OldGeneration로 구분됨

<img width="40%" src="https://velog.velcdn.com/images/industry1111/post/83380715-6820-4593-b9c9-e4704d913757/image.png">

### GC Algorithm

#### Reference Counting Algorithm
- Garbage 탐색에 초점을 맞춘 알고리즘
- 각 객체마다 Reference Count를 관리하며, 이 카운트가 0이 되면 GC를 수행
- 카운트가 0이 되면 바로 메모리에서 제거된다는 장점이 있음
- 단, 순환 참조 구저에서 Reference Count가 0이 되지 않는 문제가 발생하여 Memory Leak이 발생할 수 있음

<img width="40%" src="https://velog.velcdn.com/images/industry1111/post/59d9e1ba-2cc5-42e0-b72b-90a0bab02284/image.png">

#### Mark-and-Sweep Algorithm
- Reference Counting Algorithm의 단점을 극복하기 위해 나온 알고리즘
- RSet(Root Set)에서 Reference를 추적하여 참조 상황을 파악
- Mark 단계에서 Garbage 대상이 아닌 객체를 마킹하는 작업을 수행
- 이후, Sweap 단계에서 망키되지 않은 객체를 지우는 작업을 수행
- 위 단계를 마친 후 마킹정보를 초기화
- 이 방식은 GC가 동작하고 있을 경우, Mark 작업과 어플리케이션 Thread의 충돌을 방지하기 위해 Heap 사용이 제한됨
 그리고 Compaction 작업이 없어 비어 있는 공간이 충분하지 않을 경우 Out of Memory가 발생할 수 있음

<img width="40%" src="https://velog.velcdn.com/images/industry1111/post/0d67a668-54d5-4380-af70-21781bb1b858/image.png">
마킹되지 않은 객체를 지우면서 생긴 메모리 공간

#### Mark-and-Compact Algorithm
- Mark-and-Sweep 알고리즘에서 발생하는 점유 메모리 분산을 해결하기 위해 나온 알고리즘
- Sweep 작업 이후에 Compact 작업이 추가되어 흩어져 있는 메모리를 모아주는 작업을 진행
- Compact 작업으로 메모리 효율을 높일 수 있는 장점이 있음
- 하지만, Compact 작업과 그 이후 Reference를 업데이트하는 작업으로 인해 오버헤드가 발생할 수 있음

<img width="40%" src="https://velog.velcdn.com/images/industry1111/post/bb696bd0-4ecb-4250-8b08-dd4646a363c9/image.png">

>**Compaction**
메모리에서 더 이상 사용되지 않는 객체를 정리하면서 동시에 메모리 블록들을 모으고 조직화하여 메모리 단편화 문제를 해결하는 과정

### 일반적인 GC의 과정(Generational Algorithm)

GC는 각 영역을 활용하여 최적의 메모리 운영을 하게 된다.

**Young Generation**

`Eden 영역`

- 새로 생성된 객체들이 할당되는 최초의 영역 대부분의 객체가 이곳에서 생성되며, Minor GC)이후 살아남은 객체들은 Survivor1 영역으로 이동

`Survivor1 영역`

- Eden 영역에서 살아남은 객체들이 이동하는 중간 영역입니다. Minor GC가 실행될 때마다 이동되며, 살아남은 객체들이 여기서 잠시 유지

`Survivor2 영역`

- 이전 Minor GC에서 살아남은 객체들 중 Survivor1 영역으로 이동하지 못한 객체들이 이동하는 임시 저장소이며, 다음 번 Minor GC 때는 Survivor1과 자리를 바꿔서 사용

**Old Generation**

`Old Generation` 
- Young Generation에서 일정 시간 동안 살아남은 객체들이 Old Generation 영역으로 이동
- Old Generation은 오래된 객체들을 보관하며, 객체들이 일정 수준 쌓이게 되면, 미사용으로 판단된 객체들을 제거해주는 Major GC발생
- 이 과정에서 `Stop The World`가 발생

간단히 말하자면 아래와 같다.
1. 객체가 생성되면 Eden영역에 할당
2. Minor GC에 살아남은 객체들은 Survivor1,2 영역으로 이동
3. Survivor1,2에서 오래된 객체들은 Old Generation 영역으로 이동
4. Major GC가 사용되지 않는 객체들을 제거

>**Stop The World**
GC를 수행하기 위해 JVM이 멈추는 현상을 의미
GC가 작동하는 동안 GC관련 Thread를 제외한 모든 Thread는 멈춤
일반적으로 튜닝이라는것은 이 시간을 최소화 하는것을 의미


### GC의 종류

#### Serial GC
- 하나의 CPU로 Young Generation과 Old Generation을 연속적으로 처리하는 방식
- 가장 오래된 GC이며, Mark-and-Compact 알고리즘 사용
- GC가 수행될 때 STW가 발생

#### Parallel GC
- 자바 7~8 버전에서 Default로 설정되어 있는 GC
- Parallel GC의 목표는 다른 CPU가 GC의 진행시간 동안 대기 상태로 남아 있는 것을 최소화 하는것
- GC 작업을 병렬로 처리하여 STW 시간이 비교적 짧음

#### Parallel Compacting GC
- Paraller GC에서 Old Generation의 처리 알고리즘을 변경

#### CMS(Concurrent mark-Sweep) GC
- Application의 Thread와 GC Threa가 동시에 실행되어 STW를 최소화 하는 GC
- Parallel GC와 가장 큰 차이점은 Compation작업 유무로 구분

#### G1(Garbage First) GC
- 자바 9 버전부터 Default 설정되어 있는 GC
- 큰 메모리에서 사용하기 적합한 GC(대규모 Heap 사이즈에서 짧은 GC 시간을 보장하는데 목적을 둠)
- 전체 Heap 영역을 Region이라는 영역으로 분할하여 상황에 따라 역할이 동적으로 부여됨

#### Z GC
- ZPage라는 영역을 사용하며, G1 GC의 Region은 크기가 고정인데 비해 ZPage는 2mb 배수로 동적으로 운영됨
- 정지 시간이 최대 10ms를 초과하지 않은 것을 목적으로 운영됨
- Heap 크기가 증가하더라도 정지 시간이 증가하지 않는 것이 특징



 

출처
[링크](https://www.youtube.com/watch?v=jXF4qbZQnBc)
