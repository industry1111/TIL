## 그래프 정의
- 일반적으로 그래프는 노드(Node)와 간선(Edge)으로 이루어진 자료구조이다.
- 노드는 정점(Vertex)라고도 불리며
- 간선은 노드를 연결하는 선이다.

****

## 그래프 표현

### 인접 행렬(Adjacency Matrix)
- 2차원 배열로 그래프의 연결 관계를 표현하는 방식
- 연결되어 있지 않은 노드끼리는 무한(INF)의 비용이라고 작성한다.

### 인접 리스트(Adjacency List)
- 리스트로 그래프의 연결 관계를 표현하는 방식
- 연결된 정보만을 저장하기 때문에 메모리를 효율적으로 사용한다.
#### 구현
```java
mport java.util.Iterator;
import java.util.LinkedList;

public class Graph {
   private int V;   // 노드의 개수
   private LinkedList<Integer>[] adj; // 인접 리스트

   /** 생성자 */
   public Graph(int v) {
      V = v + 1;
      adj = new LinkedList[V];
      for (int i = 0; i < V; i++) // 인접 리스트 초기화
         adj[i] = new LinkedList<>();
   }

   /** 노드를 연결 v->w */
   public void addEdge(int v, int w) {
      adj[v].add(w);
      adj[w].add(v);
   }
}
```
## 그래프 탐색

### DFS(Depth-First Search)
- 깊이 우선 탐색
- 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
- 스택 자료구조(혹은 재귀함수)를 이용한다.
- 자신과 연결된 정점을 선택해 그 정점에서 연결된 모든 정점을 파고들어가며 끝날 때 까지 탐색한다. 

#### 동작 과정
1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를한다.
   방문하지 않은 인접노드가 없으면 스택에서 최상단 노드를 꺼낸다.
3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.
4. 방문 처리를 하지 않은 노드가 없으면 탐색을 종료한다.

- 실제 구현은 재귀함수를 이용했을 때 매우 간결하게 구현할 수 있다.

- [문제](https://github.com/industry1111/algorithm/tree/main/src/main/java/programmers/leveltwo/dfs)

#### 구현
```java

/** DFS에 의해 사용되는 재귀 함수 */
private void dfshUtil(int v, boolean[] visited){
        // 현재 노드를 방문한 것으로 표시하고 값을 출력
        visited[v]=true;
        System.out.print(v+" ");
        
        // 방문한 노드와 인접한 모든 노드를 가져온다.
        Iterator<Integer> iterator=adj[v].listIterator();
        while(iterator.hasNext()){
           int n=iterator.next();
              // 방문하지 않은 노드면 해당 노드를 시작 노드로 다시 DFSUtil 호출
              if(!visited[n]){
               dfshUtil(n,visited); // 순환 호출
              }
        }
}

   /** 주어진 노드를 시작 노드로 DFS 탐색 */
   public void dfs(int v) {
      // 노드의 방문 여부 판단 (초깃값: false)
      boolean[] visited = new boolean[V];

      // v를 시작 노드로 DFSUtil 순환 호출
      dfshUtil(v, visited);
   }

   /** DFS 탐색 */
   public void dfs() {
      // 노드의 방문 여부 판단 (초깃값: false)
      boolean[] visited = new boolean[V];

      // 비연결형 그래프의 경우, 모든 정점을 하나씩 방문
      for (int i = 1; i < V; i++) {
         if (!visited[i])
            dfshUtil(i, visited);
      }
   }
}
```
### BFS(Breadth-First Search)
- 너비 우선 탐색
- 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘
- 큐 자료구조를 이용한다.

#### 동작 과정
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

- [문제](https://github.com/industry1111/algorithm/tree/main/src/main/java/programmers/leveltwo/bfs)
- 
#### 구현
```java
/** BFS 탐색 */
void bfs(int v) {
   // 노드의 방문 여부 판단 (초깃값: false)
   boolean[] visited = new boolean[V];

   // 큐(Queue) 생성
  Queue<Integer> queue = new LinkedList<>();

  // 현재 노드를 방문한 것으로 표시하고 큐에 삽입
  visited[v] = true;
  queue.offer(v);

  while (!queue.isEmpty()) {
     // 큐에서 노드를 꺼내서 출력
     int current = queue.poll();
     System.out.print(current + " ");

     // 인접한 노드들 중에서 방문하지 않은 노드를 큐에 삽입하고 방문 표시
     Iterator<Integer> iterator = adj[current].listIterator();
     while (iterator.hasNext()) {
         int n = iterator.next();
        if (!visited[n]) {
           visited[n] = true;
           queue.offer(n);
       }
     }
  }
}

  /** BFS 탐색 */
  void bfs() {
      // 노드의 방문 여부 판단 (초깃값: false)
     boolean[] visited = new boolean[V];

     // 비연결형 그래프의 경우, 모든 정점을 하나씩 방문
     for (int i = 1; i < V; i++) {
        if (!visited[i])
        bfs(i);
     }
 }

```



